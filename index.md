---
title: welcome  
---

![alt text](https://tdalberg.github.io/files/small_FotografJN6.jpg)

This is the place where Tobias Dalberg shares information about his work.

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
