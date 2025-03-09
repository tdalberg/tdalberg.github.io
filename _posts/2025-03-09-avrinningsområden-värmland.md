---
layout: post
title: "Avrinningsområden: Värmland"
date: 2025-03-09 22:30:00 +0100
tags: [R]
---

För den som är naturgeografiskt intresserad finns det en fantastisk resurs i form av [hydrosheds.org](https://www.hydrosheds.org/). Med hjälp av ett fåtal R-paket (`tidyverse, sf, giscoR`) kan man förvånansvärt smidigt skapa kartor över floder och avrinningsområden. Genom att följa instruktionerna från Milos Popovic ([Making pretty river basin maps with R](https://youtu.be/HugGwjogPv0?feature=shared)) lyckades jag skapa kartor över både Sverige och Värmland (se nedan).

![](https://tdalberg.github.io/files/avrinningsområden-värmland.png)

{% for tag in page.tags %} {{ tag }} {% endfor %}