---
layout: post
title: "Sociology of education defined I"
date: 2024-09-13 10:30:00 +0100
tags: [disciplines]
---

Some people say there is more to life than to search for definitions of disciplines. I find it hard to understand why anyone would say such a thing; defining what a discipline is all about, or looking up what others think it is all about, is an activity whose entertainment value is equalled only by the fun you can have building a database. After years of looking for definitions of all possible humanities and social sciences, I realized I've never really done any serious collection of how to define the discipline I belong to: the sociology of education. When someone asks me to describe what it is, I often respond with something like: If you're doing social science, including historical studies, and education is an important part of either your answer or your question, then you are probably doing sociology of education.

There are, however, others who have carved out more well thought out definitions of the discipline and I thought I'd use this space to collect a few of them. One of my favorites, and the one I most often use in the classroom, is one I found i Mohamed Cherkaoui's *Sociologie de l'éduation* (2012). Roughly translated, it reads: 

> Although the sociology of education is centered on academic phenomena, it does not exclude from its field of interest the study of the relations between the school and other institutions, notably the family, politics, economy. (Cherkaoui 2012: 3-4)

Cherkaoui then goes on to elaborate on different elements of sociology of education using the metaphor of inputs and outputs from system theory. I took the liberty of drawing a chart of his metaphorical elaboration.

<pre class="mermaid">
graph TD

subgraph Attributes
a1(gender) --> v1(physical)
a2(age) --> v1
a3(IQ) --> v2(psychological)
a4(social origin) --> v3(social)
a5(culture) --> v3
a6(level of education) --> v4(professional)
a7(mode of recruitment) --> v4
a8(position in social structure) --> v4
a9(political and trade-
union orientations) --> v5(political)
end


v1 --> p1
v2 --> p1
v3 --> p1
v4 --> p2
v4 --> p3
v5 --> p2
v5 --> p3

subgraph Populations
p1(students)
p2(faculty)
p3(administration)
end

subgraph inputs
Attributes 
Populations
end

subgraph scholastic-mechanisms
sm1(Transmission of moral
order and knowledge)
sm2(type of pedagogy)
sm3(rules of evaluation)
sm4(the hierarchy of knowledge
its horizontal division --sciences 
or letters, pure or applied 
sciences--, the explicit and 
implicit rules presiding over it, 
the consequences of these 
stratifications on the elaboration 
of students' academic identity)
sm5(the way in which content is transmitted, 
to technologies --manuals, 
laboratories, maps, films--, to 
the timetable, which is partly 
a function of the social importance 
of the disciplines, to the 
nature of relationships between 
teacher and students, to the 
power structure in the classroom)
sm6(the set of manifest and latent 
rules that are at work in the 
selection processes of individuals)
sm1 --> sm4
sm2 --> sm5
sm3 --> sm6
end

subgraph mechanisms
selection
socialization
end


inputs --> scholastic-mechanisms



subgraph outputs
o1(assimilation of knowledge
and know-how)
o2(academic success)
o3(effects of learning on)
o3-->o3a(lifestyles)
o3-->o3b(political behavior)
o3-->o3c(social status)
end

scholastic-mechanisms --> mechanisms

mechanisms --> outputs
</pre>
<script src="https://cdn.jsdelivr.net/npm/mermaid@10.9.1/dist/mermaid.min.js"></script>

Why is this a useful definition? It has the education-as-part-of-the-rest-of-society element of which I am quite fond. Furthermore, the systems metaphor is great because (almost) no matter which theory is your favorite, you can always communicate this theory to others by refering to the schematic model of the system.


{% for tag in page.tags %} {{ tag }} {% endfor %}