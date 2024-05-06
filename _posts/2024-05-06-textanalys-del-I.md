---
layout: post
title: "Textanalys del I"
date: 2024-05-06 16:30:00 +0100
tags: [R]
---

Jag har länge varit nyfiken på att göra mer kvantitativt orienterade textanalyser. Min fascination för detta föddes troligen i juli 2011, på [International Classification Conference](https://thames.cs.rhul.ac.uk/bcs/bcs/ICC2011ProgrammeAbstracts.pdf) som det året hölls i St Andrews. [Fionn Murtagh](https://www.ria.ie/fionn-d-murtagh) presenterade sina geometriska dataanalyser av filmmanuskript på ett sätt som fick mig att bli intresserad av filmen som var föremål för själva analysen ([Casablanca](https://en.wikipedia.org/wiki/Casablanca_(film))). Jag återkommer till denne Murtagh i senare inlägg.

Hursomhelst har jag sedan dess på ett oerhört framgångsrikt sätt undvikit att själv göra textanalyser med hjälp av datorn. Jag kan säkert komma på ett dussin utmärkta bortförklaringar, men det för mig oöverstigliga hindret har i stort sett alltid varit detsamma: hur läser man in text på ett sätt som blir analyserbart i R?

Visst, det finns en uppsjö färdiginlästa korpusar att använda sig av, med tillhörande instruktioner för hur man kommer igång med någon av de för tillfället mest populära metoderna. Eftersom det finns så många färdiga paket med korpusar så saknas det ofta beskrivningar av hur man själv kan skapa en korpus. Det roligaste är ju ändå att kunna göra textanalyser av texter man själv är intresserad av att kvantifiera.

Så, vad är det egentligen som är så krångligt med att göra en textmassa analyserbar i R? Det beror såklart på vad syftet är, men om vi vill kunna analysera en textmassa på ett sådant sätt att vi förhållandevis enkelt kan pröva olika analysenheter (stycke, kapitel, bok) så behöver vi ha ett dataset (datatabell) som innehåller information om de olika analysenheterna. Ungefär såhär:

| Bok   | Kapitel | Stycke | Text                                                         |
| ----- | ------- | ------ | ------------------------------------------------------------ |
| Bok 1 | 1       | 1      | Jag har länge varit nyfiken på...                            |
| Bok 1 | 1       | 2      | Hursomhelst har jag...                                       |
| Bok 2 | 1       | 1      | Bok 2 har ett första stycke i första kapitlet som inleds såhär... |

I det här formatet är det förhållandevis enkelt att slå ihop textmassan på bok- eller kapitelnivå, och om råtexten innehåller skiljetecken kan jag till och med bryta ner texten på menings- eller satsnivå. Få böcker kommer emellertid i detta smidiga format, men de har ibland märkningar som gör att det med förhållandevis små medel går att sortera eller spjälka upp textmassorna i beståndsdelar som bok, kapitel och stycke.

En textmassa som inte bara har bra märkningar i utgångsläget utan också tillgängliggjorts i digital form på ett snillrikt sätt är [Bibeln i 1917 års svenska översättning](https://runeberg.org/bibeln/). Utöver att den är välorganiserad och välmärkt har den också genomgått en ordentlig korrekturläsning, vilket innebär en nära nog perfekt digital återgivning -- ner på teckennivå. För detta tackar vi [Projekt Runeberg](https://runeberg.org/)!

Bibeln är dessutom en utmärkt korpus för textanalys eftersom den genomgående består av numrerade verser, samlade i ett antal böcker med (i de flesta fall) ett antal kapitel. Därför tänkte jag i detta inlägg visa ett sätt att ladda hem, läsa in och bearbeta Bibeln i 1917 års översättning till en korpus som blir hyfsat lättarbetad för textanalyser i R.

Till att börja med laddar jag ned zip-filen som innehåller alla Bibel-filer. Ja, jag glömde nämna att hjältarna på Projekt Runeberg har organiserat hela Bibeln i enskilda html-filer för varje enskilt kapitel (bok för böcker utan kapitel) döpta till `boknummer_kapitelnummer.html`. Sådan service går inte att räkna med i andra sammanhang, men här står vi alltså redan inför en väldigt tacksam uppgift när vi vill skapa en korpus i R.

```R
# Get Bibeln 1917 from runeberg ####
## Download the zip-file ####

temp <- tempfile()

download.file("http://runeberg.org/download.pl?mode=txtzip&work=bibeln", temp)

## Unzip all the files into data folder ####
unzip("bibeln/zip/bibeln-txt.zip",exdir="bibeln/data")
```

Jag har som sagt ständigt fastnat i de steg som här följer, och jag har provat åtskilligt -- både för bibeltexter och andra texter -- utan att lyckas. Det betyder inte att det är särskilt svårt att bygga korpus för R. Det betyder bara att jag har varit lat när det gäller att lära mig hur man effektivt bygger funktioner och använder sig av reguljära uttryck i R.

Sen slog det mig plötsligt att det går kanske att beskriva för ChatGPT vad jag vill åstadkomma och vad jag har för data. Det gick faktiskt efter lite trevande dialog fram och tillbaka.

Det började ungefär med:

> And I want to create a corpus that makes it possible to create datasets either by testament, books, chapters or verses

Jag fick förslag på kod direkt, men jag hade inte riktigt hunnit beskriva vad det är för data.

> hold your horses. Let me tell you what I've done so far, step by step

Så jag beskrev vad jag hade gjort och kopierade koden ovan. Chatboten bekräftade att den förstått, och jag fortsatte:

> That is correct. Each chapter is in a separate html file. Genesis chapter 1 is in file 01_01.html and so on

Nu fick jag ännu en kodsnutt, innan jag hann skriva:

> and here is what the top 12 rows in file 01_01.html look like:

Jag visade alltså de första raderna i första bokens första kapitel. Då fick jag en kodsnutt som läste in just den filen, så jag frågade försynt:

> Could you loop this through all the html files, in the workflow from the previous example code?

Och fick ytterligare kod som inte riktigt gjorde vad jag ville:

> It works fairly well, but each verse contains 1 or several rows of text.

Chatboten återkom med lite bättre fungerande kod, där bara ett bekymmer återstod:

> We're getting there. Book 31 doesn't have any chapters, so the file is only named 31.html. Can your code accomodate that as well?

Svaret på den frågan ledde till koden nedan, där jag endast

```R
# List HTML files in the directory
html_files <- list.files("bibeln/data", pattern = "*.html", full.names = TRUE)

# (This code also works to get a list of relevant files)
html_files <- list.files(
  path = "bibeln/data/",
  pattern = "[[:digit:]]",
  full.names = TRUE,
  recursive = TRUE
)

# Because I do not want the first two files. 
# They are not part of the Bible.
html_files <- html_files[-c(1:2)] 


# Initialize a list to store the text data
bible_text <- list()

# Loop through each HTML file

for (file in html_files) {
  # Extract book and chapter information from the file name
  file_parts <- strsplit(basename(file), "_")[[1]]
  book_name <- file_parts[1]  # Assuming the file name format is "book_chapter.html"
  
  # Check if the file contains chapter information
  if (length(file_parts) > 1) {
    chapter_number <- file_parts[2]
  } else {
    chapter_number <- ""  # No chapter number specified
  }
  
  # Read HTML content from the file
  html_content <- readLines(file)
  
  # Initialize a list to store verse text for this chapter
  chapter_text <- list()
  
  # Initialize a variable to store current verse text
  current_verse_text <- ""
  
  # Loop through each line of HTML content
  for (line in html_content) {
    # Extract verse text using regex
    verse_match <- regmatches(line, regexpr("^[[:space:]]*\\d+\\.\\s+(.*)", line))
    
    # If a verse is found, store the previous verse text (if any) and start a new one
    if (!is.na(verse_match) && length(verse_match) > 0) {
      if (nchar(current_verse_text) > 0) {
        chapter_text[[length(chapter_text) + 1]] <- current_verse_text
      }
      current_verse_text <- verse_match[[1]]
    } else {
      # Append line to current verse text
      current_verse_text <- paste(current_verse_text, line)
    }
  }
  
  # Store the last verse text (if any)
  if (nchar(current_verse_text) > 0) {
    chapter_text[[length(chapter_text) + 1]] <- current_verse_text
  }
  
  # Store the chapter text in the list for this book
  if (chapter_number != "") {
    bible_text[[paste0(book_name, "_Chapter_", chapter_number)]] <- chapter_text
  } else {
    bible_text[[book_name]] <- chapter_text
  }
}


# Now you have the text data organized in a list
# You can further process and structure this data as needed
```

Huvudresultatet av denna kodsnutt är alltså listan `bible_text`, som egentligen är en lista över bokkapitel, vilka i sin tur är listor över verser, vilka i sin tur innehåller råtext. Den här kodsnutten gör att den första versen i varje kapitellista utgörs av kapitelrubriken (och epigrafen i förekommande fall). Jag försökte ett tag hantera detta i inläsningen, men valde till slut att låta detta bli ett senare problem att lösa.

En sak som jag kunde ha lagt större möda vid är namngivningen av böcker och kapitel och liknande, det vill säga information som finns tillgänglig i filerna på ett hyfsat strukturerat sätt. Det finns dock en fil med namnet `articles.lst` med anmärkningsvärt välstrukturerad information om varje fil. Jag valde helt enkelt att läsa in den filen istället:

```R
articles_content <- readLines("bibeln/data/Articles.lst")

## I know the lines of interest in this file.
lines_of_interest <- c(articles_content[21:986], articles_content[991:1272])

bible_books_chapters <- as_tibble(lines_of_interest) %>% 
  separate(
    col = "value",
    into = c("book_chapter_numerical", "book_name"),
    sep = "\\|"
  ) %>% 
  separate(
    col = "book_name",
    into = c("book_name", "chapter_number"),
    sep = "\\,"
  ) %>% 
  filter(book_chapter_numerical != "#") %>% 
  mutate(del = case_when(
    as.numeric(substr(book_chapter_numerical, 1, 2)) >= 40 ~ "Nya testamentet",
    TRUE ~ "Gamla testamentet")
  )
```

Just det, textmassan är ännu inte i ett smidigt format (för mig: datatabell eller *tibble*) för textanalys.

```R
bible_df <- stack(bible_text) %>% 
  as_tibble() %>% 
  rename(
    bible_text = values,
    book_chapter = ind
  ) %>%
  group_by(book_chapter) %>% 
  mutate(verse_number = row_number() - 1) %>% 
  ungroup() %>% 
  mutate(book_chapter_numerical = gsub("Chapter_|\\.html", "", book_chapter))
```

Vår bible_df ser alltså ut såhär:

```R
# A tibble: 32,357 × 4
   bible_text                       book_chapter verse_number book_chapter_numerical
   <chr>                            <fct>               <dbl> <chr>                 
 1 " <pre>                  Första… 01_Chapter_…            0 01_01                 
 2 "  1.  I begynnelsen skapade Gu… 01_Chapter_…            1 01_01                 
 3 "  2.  Och jorden var öde och t… 01_Chapter_…            2 01_01                 
 4 "  3.  Och Gud sade: »Varde lju… 01_Chapter_…            3 01_01                 
 5 "  4.  Och Gud såg att ljuset v… 01_Chapter_…            4 01_01                 
 6 "  5.  Och Gud kallade ljuset d… 01_Chapter_…            5 01_01                 
 7 "  6.  Och Gud sade: »Varde mit… 01_Chapter_…            6 01_01                 
 8 "  7.  Och Gud gjorde fästet, o… 01_Chapter_…            7 01_01                 
 9 "  8.  Och Gud kallade fästet h… 01_Chapter_…            8 01_01                 
10 "  9.  Och Gud sade: »Samle sig… 01_Chapter_…            9 01_01                 
# ℹ 32,347 more rows
# ℹ Use `print(n = ...)` to see more rows
```

Och vi kan lägga till lite metadata från `bible_books_chapters`, som ser ut såhär:

```R
# A tibble: 1,189 × 4
   book_chapter_numerical book_name                chapter_number del              
   <chr>                  <chr>                    <chr>          <chr>            
 1 01_01                  Första Mosebok (Genesis) " 1 Kapitlet"  Gamla testamentet
 2 01_02                  Första Mosebok (Genesis) " 2 Kapitlet"  Gamla testamentet
 3 01_03                  Första Mosebok (Genesis) " 3 Kapitlet"  Gamla testamentet
 4 01_04                  Första Mosebok (Genesis) " 4 Kapitlet"  Gamla testamentet
 5 01_05                  Första Mosebok (Genesis) " 5 Kapitlet"  Gamla testamentet
 6 01_06                  Första Mosebok (Genesis) " 6 Kapitlet"  Gamla testamentet
 7 01_07                  Första Mosebok (Genesis) " 7 Kapitlet"  Gamla testamentet
 8 01_08                  Första Mosebok (Genesis) " 8 Kapitlet"  Gamla testamentet
 9 01_09                  Första Mosebok (Genesis) " 9 Kapitlet"  Gamla testamentet
10 01_10                  Första Mosebok (Genesis) " 10 Kapitlet" Gamla testamentet
# ℹ 1,179 more rows
# ℹ Use `print(n = ...)` to see more rows
```

Det krävs med andra ord inte så många rader av kod (~70) för att göra över 32 000 verser användbara för textanalys. Mer om själva textanalyserna följer i senare inlägg.