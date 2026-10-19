---
layout: page
title: "Publications"
---


[Find up-to-date info on [my Google Scholar page](https://scholar.google.com/citations?hl=en&user=erysFsoAAAAJ&view_op=list_works&sortby=pubdate)] 

Jump to... [[Papers](#papers)] [[Books](#books)] [[Preprints](#preprints)] [[Refereed Abstracts](#refereed-abstracts)] [[Theses](#doctoral-and-masters-theses)]

{% assign s_books = site.data.publications | size | plus: 1 %}
{% assign s_preprints = site.data.books | size | plus: s_books %}
{% assign s_abstracts = site.data.preprints | size | plus: s_preprints %}
{% assign s_theses = site.data.abstracts | size | plus: s_abstracts %}

## Papers
{% include pub-section.html items=site.data.publications start=1 %}

## Books
{% include pub-section.html items=site.data.books start=s_books %}

## Preprints
{% include pub-section.html items=site.data.preprints start=s_preprints %}

## Refereed Abstracts
{% include pub-section.html items=site.data.abstracts start=s_abstracts %}

## Doctoral and Master's Theses
{% include pub-section.html items=site.data.theses start=s_theses %}

  