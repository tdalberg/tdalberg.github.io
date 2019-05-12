---
title: welcome  
---

![alt text](https://tdalberg.github.io/files/small_FotografJN6.jpg)

This is the place where Tobias Dalberg shares information about his work. He currently spends his time:

- Exploring and evaluating the utility of techniques from graph theory, natural language processing and geometric data analysis for analysing pathways in higher education.
- Finishing a report on rater agreement in the assessments of student texts written within the framework of the national test in Swedish.
- Analysing the usage of freestanding courses in Swedish higher education.

<p>
    {% for tag in site.tags %}
    <!-- Here's a hack to generate a "tag cloud" where the size of
    the word is directly proportional to the number of posts with
    that tag. Thank you Ryan Palo at https://github.com/rpalo -->
    <a href="/tags/{{ tag[0] }}/" 
    style="font-size: {{ tag[1] | size | times: 2 | plus: 10 }}px">
        {{ tag[0] }} | 
    </a>
    {% endfor %}
</p>
