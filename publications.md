---
layout: page
title: "Publications"
---


[Find up-to-date info on [my Google Scholar page](https://scholar.google.com/citations?hl=en&user=erysFsoAAAAJ&view_op=list_works&sortby=pubdate)] 

Jump to... [[Papers](#papers)] [[Books](#books)] [[Preprints](#preprints)] [[Refereed Abstracts](#refereed-abstracts)] [[Master's Thesis](#masters-thesis)]

## Papers

<ol>
{% for paper in site.data.publications | sort: 'year' | sort: 'month' | reverse %}
  <li style="padding-bottom: 0.5em;">
  <strong>{% if paper.url %}<a href="{{ paper.url }}">{% endif %}{{ paper.name }}{% if paper.url %}</a>{% endif %}</strong>
  <br>
    <small><i>{{ paper.authors  | markdownify  | remove: '<p>' | remove: '</p>' | strip }}. {{ paper.venue }} {{ paper.year }}.</i></small>
  {% if paper.tldr %}<br><small><strong>TLDR:</strong> {{ paper.tldr }}</small>{% endif %}
    {% if paper.note %} <small><span style="color: rgb(165, 28, 48);">{{ paper.note }}</span></small>{% endif %}
  </li>
{% endfor %}
</ol>

## Books

{:start="{{ site.data.publications | size | plus: 1 }}"}
1. Giovanna Maria Dora Dore, **Arya D. McCarthy**, and James A. Scharf. [*A Free Press, If You Can Keep It: What Natural Language Processing Reveals About Freedom of the Press in Hong Kong*](https://link.springer.com/book/9783031275852). Springer 2022.
   <br><small><strong>TLDR:</strong> Interdisciplinary analyses of protest coverate in print media that will "appeal to a wide range of readers with interests in computational social science, public policy, political sciences as well as policy-makers, think tanks, and practitioners who focus on the China-Hong Kong nexus".</small>

## Preprints

{:start="43"}
1. Joel Niklaus, Lucia Zheng, **Arya D. McCarthy**, Christopher Hahn, Brian M. Rosen, Peter Henderson, Daniel E. Ho, Garrett Honke, Percy Liang, Christopher D. Manning. [*FLawN-T5: An Empirical Examination of Effective Instruction-Tuning Data Mixtures for Legal Reasoning*](https://arxiv.org/abs/2404.02127). arXiv.
1. **Arya D. McCarthy**, Hao Zhang, Shankar Kumar, Felix Stahlberg, Axel H. Ng. [*Improved Long-Form Spoken Language Translation with Large Language Models*](https://arxiv.org/abs/2212.09895). arXiv.
1. Nibhrat Lohia, Raunak Mundada, **Arya D. McCarthy**, Eric C. Larson. [*AirWare: Utilizing Embedded Audio and Infrared Signals for In-Air Hand-Gesture Recognition*](https://arxiv.org/abs/2101.10245). arXiv.
1. **Arya D. McCarthy**, Xian Li, Jiatao Gu, and Ning Dong. [*Improved variational neural machine translation by promoting mutual information*](https://arxiv.org/abs/1909.09237). arXiv.

## Refereed Abstracts

{:start="47"}
1. David Yarowsky, **Arya D. McCarthy**, Garrett Nicolai, Winston Wu, Aaron Mueller, Dylan Lewis, Yingqi Ding, Abhinav Nigam, Emre Ozgu, Debanik Purkayastha, James Scharf and Kenneth Zheng. *[A 1000-language Collaborative Universal Dictionary and Universal Translator](https://en.unesco.org/sites/default/files/lt4all_programme_day2and3.pdf)*. UNESCO Language Technologies for All (LT4All) 2019.
1. Xian Li, Jiatao Gu, Ning Dong, and **Arya D. McCarthy**. Improved variational neural machine translation via promoting mutual information. EMNLP Workshop on Neural Generation and Translation 2019.
1. Xian Li, Jiatao Gu, **Arya D. McCarthy**, and Ning Dong. Improving variational NMT by promoting mutual information. West Coast NLP Summit (WeCNLP) 2019.
1. **Arya D. McCarthy**. *Community Detection, The No Free Lunch Theorem, and Attack Games*. SIAM Workshop on Network Science 2019.
1. **Arya D. McCarthy**. [*An exact No Free Lunch theorem for community detection*](http://cs.jhu.edu/~arya/mccarthy.iccna18.pdf). [Complex Networks (ICCNA) 2018](https://www.complexnetworks.org).
1. **Arya D. McCarthy** and David W. Matula. [*Evaluating the leximin method for community detection*](http://cs.jhu.edu/~arya/mccarthy+matula.iccna18.pdf). [Complex Networks (ICCNA) 2018](https://www.complexnetworks.org).
1. **Arya D. McCarthy** and David W. Matula. [*Normalized mutual information exaggerates community detection performance*](http://cs.jhu.edu/~arya/mccarthy+matula.ns18.pdf). SIAM [Workshop on Network Science 2018](https://www.siam.org/conferences/CM/Main/ns18). 

## Master's thesis


{:start="54"}

1. **Arya D. McCarthy**. Gridlock in networks: [*The leximin method for hierarchical community detection*](https://search.proquest.com/docview/1907180434). Master's thesis, SMU. 2017.
