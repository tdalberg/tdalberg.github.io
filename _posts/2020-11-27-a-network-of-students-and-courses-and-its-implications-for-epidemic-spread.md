---
layout: post
title: A network of students and courses and its implications for epidemic spread
date: 2020-12-09 14:00:00 +0100
tags: [higher education, policy]
---

Since I began working on my project [*Mapping pathways in higher education*](https://tdalberg.github.io/mapping-pathways/) I've been particularly interested in what we might call the web of disciplines or, as in the case I'm about to describe, the web of courses. My particular interest in this topic has up until this point been largely based on a broader interest in the social and cognitive structure of higher education and research. In other words, the relations created between fields of study when, for instance, students enroll in multiple courses straddling different fields can often reveal structures of social hierarchies as some fields are commonly combined while others rarely are. These network representations of higher education also highlight a curricular complexity that goes beyond descriptions in the official catalog of course and program offerings. Recently, however, and informed by a paper by Kim Weeden and Benjamin Cornwell (2020), I discovered that this exercise in the sociology of education and science could be applied to a more immediate problem relating to the SARS-CoV-2 pandemic: The network of students and courses could be used as a model to simulate epidemic spread between students. In this post, I will compare some traditional network characteristics of the Weeden and Cornwell case, who use data on Cornell University in Ithaka, to a network based on a Swedish university.

The basic idea in this post -- as in the Weeden and Cornwell paper -- is that face-to-face instruction creates a situation of possible transmission. We all strive for transmission of knowledge, but in this case we fear that this can be also a situation when a virus is transmitted. Student enrollment in courses can be modeled as a bipartite, or two-mode, network where students are connected via courses and courses are connected via students. Students who enroll in the same course may come in contact with each other, and students who enroll in multiple courses create links between groups of students. 

It should be noted at this point that there are plenty of conditions not considered in this particular model, many of which are not even primarily epidemiological or virological in nature. For instance, the role of faculty involved is not considered, nor the frequency of face-to-face instruction or any division into sections or subsections. More importantly, students have lots of opportunities to meet on campus outside the classroom, and even more outside campus. Still, this kind of modeling, with all its limitations, might still inform university policy to shift parts or all of its instruction online. At the very least, this model could point out academic areas where the risk of transmission and spread throughout larger parts of the network might be higher.

Comparing US and Swedish universities is of particular interest in this case since they represent two different models of higher education curriculum: the elective system is more widely spread in the US while Swedish higher education tends to have more of a scripted curriculum. For instance, students in the US often apply to an institution before selecting any courses and majors whereas students in Sweden jointly apply to a course or program and an institution. Another important aspect is that US higher education tends to have more distribution requirements or core curriculum -- a set of courses all students are obliged to take. (Note that Cornell does not have a university wide curriculum.) There is no equivalent in the Swedish system, where students are instead obliged to follow the scripted curriculum of their programs or fill the requirements of majors. Although smaller course modules are becoming increasingly common in the Swedish system, they are often part of a sequence that adds up to 30 credits (30 credits = 20 weeks of studies on full time) over the course of a semester. An 30 credit introductory course in history might for instance consist of four 7.5 credit course modules that in theory could be taken separately and spread out over multiple semesters, but students often take all four modules in one semester. The elective system in the US allows more interdepartmental combinations within each semester (or quarter) than the Swedish system. Based on these characteristics alone, we might expect higher connectivity between students (via courses) at universities where the elective system is more pronounced than at universities in Sweden.

I use transcript data from Statistics Sweden on all students enrolled for campus instruction at one of the largest universities in fall 2019. These data include first- and second-cycle students, i.e., bachelor and master degrees. Unlike many US universities, there are no cross-listed courses. As mentioned above, the granularity of the data does not allow for courses to be divided into sections.

Following the methodology of Weeden & Cornwell (2020), I constructed an affiliation matrix $A$ for the two-mode student-to-course network, and a one-mode, student-student projection of this network ($AA^T=A_P$).

There are more students at Big Swedish university than at Cornell (25k vs 22k), but there are almost three times as many courses at Cornell, and almost twice as many edges (links between students and courses). These numbers highlight some of the curricular differences between the systems mentioned above, i.e., that courses or course modules are often larger in Sweden than in the US.

The share of students that are at least indirectly connected to each other by being part of the largest component of network $A$ is fairly similar in both cases (88.2% at Big Swedish, 99.1 at Cornell). The network at Big Swedish seems to be a bit weaker connected than the Cornell counterpart, since only 50.7% of students belong to the largest bi-component compared with 94.5% at Cornell. A bi-component is defined as the largest component where any randomly removed student or course wouldn't break the component apart. Another way to put it: by shifting just a couple of courses to online instruction one might break some potential paths for transmission of disease, and these paths might be easier to break at Big Swedish than at Cornell. 

The fact that the clustering coefficient is higher at Big Swedish than at Cornell is probably due to the fact that smaller course modules in the Swedish context are often part of a structured sequence for the whole semester. A 30 credit course might have been divided into four course modules, but the students signed up for the whole sequence.

Students seem to be farther apart in network terms at Big Swedish than at Cornell. The average student-to-student geodesic distance is 2.5 at Cornell, meaning that students are 1.5 courses removed from each other. This distance is 4.4 at Big Swedish (3.4 courses removed from each other). Another indicator of this difference in distance between the two universities is the proportion students reachable in 1, 2, 3 or 4 steps. The proportion reachable in 1 step is small at both universities, but while it increases fast by each step at Cornell -- 59% at 2 steps -- it continues to be fairly small at Big Swedish with only 48% of students reachable in 4 steps (97% at Cornell!).

Table 1. Characteristics of the university course enrollment network.

| Social network measures                        | Big Swedish university |   Cornell |
| ---------------------------------------------- | ---------------------: | --------: |
| *2-mode student-to-course network*             |                        |           |
| Number of students                             |                 25,415 |    22,051 |
| Number of courses                              |                  2,129 |     6,072 |
| Number of edges                                |                 64,866 |   118,314 |
| Network density                                |        (0.00017) 0.000 |     0.000 |
| Proportion of students in largest component    |                  0.882 |     0.991 |
| Proportion of courses in largest component     |                  0.823 |     0.976 |
| Proportion of students in largest bi-component |                  0.507 |     0.945 |
| Proportion of courses in largest bi-component  |                  0.659 |     0.730 |
| Average betweenness centrality (normalized)    |                 0.0002 |     0.098 |
| *Projected 1-mode student-to-student network*  |                        |           |
| Number of unique edges                         |              1,767,542 | 5,832,358 |
| Network density                                |                  0.006 |     0.024 |
| Clustering coefficient (transitivity/closure)  |                  0.725 |     0.480 |
| Average geodesic distance                      |                  4.361 |     2.466 |
| Network diameter (largest observed distance)   |                     16 |        10 |
| *Proportion reachable in $k$ steps*            |                        |           |
| $k = 1$                                        |                  0.006 |     0.024 |
| $k = 2$                                        |                  0.047 |     0.594 |
| $k = 3$                                        |                  0.220 |     0.921 |
| $k = 4$                                        |                  0.486 |     0.966 |

Note: Cornell numbers from Table 2 on p 229 in Weeden & Cornwell (2020).

Insofar as epidemic spread is due to contacts with peers in face-to-face instruction, shifting to online instruction might have a larger effect at an institution like Cornell than at Big Swedish, compared with the baseline of having all instruction being face-to-face.

For the original publication, see: Weeden, K. & Cornwell, B. (2020), "The Small-World Network of College Classes: Implications for Epidemic Spread on a University Campus", *Sociological Science* 7: 222--241.

{% for tag in page.tags %} <a href="/tags/{{ tag }}/">{{ tag }}</a> {% endfor %}