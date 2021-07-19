---
title: welcome  
---

---

<sup>:new:</sup> Published an article synthesizing the socio-political history of higher education in Sweden 1945–2020. See [writings](https://tdalberg.github.io/writings/) or download [fulltext](https://doi.org/10.1080/21568235.2021.1945473).

<sup>:new:</sup> Published a chapter on the extramural activities of scholars in humanities and social sciences in Sweden ca 1900&ndash;1950. See [writings](https://tdalberg.github.io/writings/) or [buy book](https://www.dialogosforlag.se/bocker/samhallsfragor/humanvetenskapernas-verkningar.html).

---

![alt text](https://tdalberg.github.io/files/small_FotografJN6.jpg)

This is the place where Tobias Dalberg shares information about his work. He currently spends his time:

- Exploring and evaluating the utility of techniques from graph theory, natural language processing and geometric data analysis for analyzing pathways in higher education.
- Developing a methodology for analyzing social change such as structural and relative social mobility and shifts in occupational status.
- Using the notion of curricular blind spots to analyze gender differences in consideration and choice of courses in college.
- Applying the sieve metaphor (à la Sorokin 1927 and Stevens et al 2008) to the higher education curriculum as a way to describe the social structure of the system of college majors.


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
