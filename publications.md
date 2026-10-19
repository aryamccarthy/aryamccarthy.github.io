---
layout: page
title: "Publications"
---


[Find up-to-date info on [my Google Scholar page](https://scholar.google.com/citations?hl=en&user=erysFsoAAAAJ&view_op=list_works&sortby=pubdate)] 

[Papers](#papers) · [Books](#books) · [Preprints](#preprints) · [Abstracts](#refereed-abstracts) · [Theses](#doctoral-and-masters-theses)

{% assign n_papers = site.data.publications | size %}
{% assign n_books = site.data.books | size %}
{% assign n_preprints = site.data.preprints | size %}
{% assign n_abstracts = site.data.abstracts | size %}
{% assign n_theses = site.data.theses | size %}
{% assign s_papers = n_papers | plus: n_books | plus: n_preprints | plus: n_abstracts | plus: n_theses %}
{% assign s_books = s_papers | minus: n_papers %}
{% assign s_preprints = s_books | minus: n_books %}
{% assign s_abstracts = s_preprints | minus: n_preprints %}
{% assign s_theses = s_abstracts | minus: n_abstracts %}

## Papers

{% include pub-section.html items=site.data.publications start=s_papers %}

## Books

{% include pub-section.html items=site.data.books start=s_books %}

## Preprints

{% include pub-section.html items=site.data.preprints start=s_preprints %}

## Refereed Abstracts

{% include pub-section.html items=site.data.abstracts start=s_abstracts %}

## Doctoral and Master's Theses

{% include pub-section.html items=site.data.theses start=s_theses %}
