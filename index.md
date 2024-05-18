---
title: welcome  
---

---

<sup>:new:</sup> Published an article on major selection as iteration and how gender differentiation is mediated by elective curriculums. See [writings](https://tdalberg.github.io/writings/) or download [fulltext](https://doi.org/10.1177/23328584241249600).

---

![alt text](https://tdalberg.github.io/files/small_FotografJN6.jpg)

This is the place where Tobias Dalberg shares information about his work. He currently spends his time:

- Exploring and evaluating the utility of techniques from graph theory, natural language processing and geometric data analysis for analyzing pathways in higher education.
- Developing a methodology for analyzing social change such as structural and relative social mobility and shifts in occupational status.
- Using the notion of curricular blind spots to analyze gender differences in consideration and choice of courses in college.


<div style="width: 100%; display: table;">
    <div style="display: table-row">
        <div style="width: 30%; display: table-cell;"> <p>
    {% for tag in site.tags %}
    <!-- Here's a hack to generate a "tag cloud" where the size of
    the word is directly proportional to the number of posts with
    that tag. Thank you Ryan Palo at https://github.com/rpalo -->
    <a href="/tags/{{ tag[0] }}/" 
    style="font-size: {{ tag[1] | size | times: 2 | plus: 10 }}px">
        {{ tag[0] }} | 
    </a>
    {% endfor %}
</p> </div>
        <div style="display: table-cell;"> <script async src="https://cse.google.com/cse.js?cx=018083339573084129855:aqzq48shiey"></script>
<div class="gcse-search"></div> </div>
    </div>
</div>
