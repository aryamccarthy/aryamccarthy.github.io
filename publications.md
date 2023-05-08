---
layout: page
title: "Publications"
---


[last updated 2020-08-11] 

[Find up-to-date info on [my Google Scholar page](https://scholar.google.com/citations?hl=en&user=erysFsoAAAAJ&view_op=list_works&sortby=pubdate)] 

## Papers

<ol>
{% for paper in site.data.publications %}
  <li>
  <strong>{% if paper.url %}<a href="{{ paper.url }}">{% endif %}{{ paper.name }}{% if paper.url %}</a>{% endif %}</strong>
  <br>
  {{ paper.authors }}.
  <br>
  {{ paper.venue }} {{ paper.year }}.
  {% if paper.tldr %}<small><br><strong>TLDR:</strong> {{ paper.tldr }}</small>{% endif %}
    {% if paper.note %}<br><strong>{{ paper.note }}</strong>{% endif %}
  </li>
{% endfor %}
</ol>

1. **Arya D. McCarthy**, Xian Li, Jiatao Gu, and Ning Dong. [*Addressing Posterior Collapse with Mutual Information for Improved Variational Neural Machine Translation*](https://aclanthology.org/2020.acl-main.753/). ACL 2020.
1. Huiming Jin, Liwei Cai, Yihui Peng, Chen Xia, **Arya D. McCarthy**, and Katharina Kann. [Unsupervised Morphological Paradigm Completion](https://aclanthology.org/2020.acl-main.598/). ACL 2020.
1. Adina Williams, Tiago Pimentel, Hagen Blix, **Arya D. McCarthy**, Eleanor Chodroff, and Ryan Cotterell. [*Predicting Declension Class from Form and Meaning*](https://aclanthology.org/2020.acl-main.597/). ACL 2020.
1. Huda Khayrallah, Jacob Bremerman, **Arya D. McCarthy**, Kenton Murray, Winston Wu, and Matt Post. [*The JHU Submission to the 2020 Duolingo Shared Task on Simultaneous Translation and Paraphrase for Language Education*](https://aclanthology.org/2020.ngt-1.22/). WNGT 2020. <span style="color: rgb(165, 28, 48);">First place system.</span>
1. **Arya D. McCarthy**, Rachel Wicks, Dylan Lewis, Aaron Mueller, Winston Wu, Oliver Adams, Garrett Nicolai, Matt Post, and David Yarowsky. [*The Johns Hopkins University Bible Corpus: 1600+ Tongues for Typological Exploration*](https://aclanthology.org/2020.lrec-1.352/). LREC 2020.
1. **Arya D. McCarthy**, Christo Kirov, Matteo Grella, Amrit Nidhi, Patrick Xia, Kyle Gorman, Ekaterina Vylomova, Sabrina J. Mielke, Garrett Nicolai, Miikka Silfverberg, Timofey Arkhangelskiy, Nataly Krizhanovsky, Andrew Krizhanovsky, Elena Klyachko, Alexey Sorokin, John Mansfield, Valts Ernštreits, Yuval Pinter, Cassandra L. Jacobs, et al. [*UniMorph 3.0: Universal Morphology*](https://aclanthology.org/2020.lrec-1.483/). LREC 2020.
1. Garrett Nicolai, Dylan Lewis, **Arya D. McCarthy**, Aaron Mueller, Winston Wu, and David Yarowsky. [*Fine-grained Morphosyntactic Analysis and Generation Tools for More Than One Thousand Languages*](https://aclanthology.org/2020.lrec-1.488/). LREC 2020.
1. Aaron Mueller, Garrett Nicolai, **Arya D. McCarthy**, Dylan Lewis, Winston Wu, and David Yarowsky. [*An Analysis of Massively Multilingual Neural Machine Translation for Low-Resource Languages*](https://aclanthology.org/2020.lrec-1.458/). LREC 2020.
1. Jackson L. Lee, Lucas F.E. Ashby, M. Elizabeth Garza, Yeonju Lee-Sikka, Sean Miller, Alan Wong, **Arya D. McCarthy**, and Kyle Gorman. [*Massively Multilingual Pronunciation Modeling with WikiPron*](https://aclanthology.org/2020.lrec-1.521/). LREC 2020.
1. **Arya D. McCarthy**, Liezl Puzon, and Juan Pino. [*SkinAugment: Autoencoding speaker conversions for automatic speech translation*](https://ieeexplore.ieee.org/document/9053406). ICASSP 2020.
1. **Arya D. McCarthy**, Tongfei Chen, and Seth Ebner. [*An exact No Free Lunch Theorem for community detection*](https://arxiv.org/abs/1903.10092). Complex Networks 2019.
1. **Arya D. McCarthy**, Tongfei Chen, Rachel Rudinger, and David W. Matula. [*Metrics matter in community detection*](https://arxiv.org/abs/1901.01354). Complex Networks 2019.
1. **Arya D. McCarthy**, Winston Wu, Aaron Mueller, Bill Watson, and David Yarowsky. [*Modeling color terminology across thousands of languages*](https://arxiv.org/abs/1910.01531). EMNLP 2019.
1. Kyle Gorman, **Arya D. McCarthy**, Miikka Silfverberg, Ekaterina Vylomova, and Magdalena Markowska. [*Weird Inflects but OK: Making Sense of Morphological Generation Errors*](https://ling.auf.net/lingbuzz/004787). CoNLL 2019.
1. Juan Pino, Liezl Puzon, Jiatao Gu, Xutai Ma, **Arya D. McCarthy**, and Deepak Gopinath. [*Harnessing out-of-task data for automatic speech translation: Tricks of the trade*](https://arxiv.org/abs/1909.06515). IWSLT 2019.
1. Tiago Pimentel, **Arya D. McCarthy**, Damian Blasi, Brian Roark, and Ryan Cotterell. [*Meaning to form: Measuring systematicity as information*](https://www.aclweb.org/anthology/P19-1171). ACL 2019. <span style="color: rgb(165, 28, 48);">Best paper nominee.</span>
1. **Arya D. McCarthy**, Ekaterina Vylomova, Shijie Wu, Chaitanya Malaviya, Lawrence Wolf-Sonkin, Garrett Nicolai, Christo Kirov, Miikka Silfverberg, Sebastian Mielke, Jeffrey Heinz, Ryan Cotterell, and Mans Hulden. [*The SIGMORPHON 2019 shared task: Crosslinguality and context in morphology*](https://www.aclweb.org/anthology/W19-4226). SIGMORPHON 2019.
1. **Arya D. McCarthy**, Miikka Silfverberg,  Ryan Cotterell, Mans Hulden, and David Yarowsky. [*Marrying Universal Dependencies and Universal Morphology*](https://aclweb.org/anthology/W18-6011). Proceedings of [UDW 2018](http://universaldependencies.org/udw18/). 
1. Brian Thompson, Huda Khayrallah, Antonios Anastasopoulos, **Arya D. McCarthy**, Kevin Duh, Rebecca Marvin, Paul McNamee, Jeremy Gwinnup, Tim Anderson, and Philipp Koehn. [*Freezing subnetworks to analyze domain adaptation in neural machine translation*](https://www.aclweb.org/anthology/W18-6313). Proceedings of [WMT 2018](http://www.statmt.org/wmt18/). [[arxiv](https://arxiv.org/pdf/1809.05218.pdf)]
1. Ryan Cotterell, Christo Kirov, John Sylak-Glassman, Géraldine Walther, Ekaterina Vylomova, **Arya D. McCarthy**, Katharina Kann, Sebastian Mielke, Garrett Nicolai, Miikka Silfverberg, David Yarowsky, Jason Eisner, and Mans Hulden. [*The CoNLL–SIGMORPHON 2018 Shared Task: Universal Morphological Reinflection*](https://aclweb.org/anthology/K18-3001). CoNLL 2018.
1. Christo Kirov, Ryan Cotterell, John Sylak-Glassman, Géraldine Walther, Ekaterina Vylomova, Patrick Xia, Manaal Faruqui, **Arya D. McCarthy**, Sandra Kübler, David Yarowsky, Jason Eisner, and Mans Hulden. [*UniMorph 2.0: Universal morphology*](https://www.aclweb.org/anthology/L18-1293). Proceedings of [LREC 2018](http://lrec2018.lrec-conf.org/en/).


## Preprints

{:start="22"}
1. **Arya D. McCarthy**, Xian Li, Jiatao Gu, and Ning Dong. [*Improved variational neural machine translation by promoting mutual information*](https://arxiv.org/abs/1909.09237). arXiv.

## Refereed Abstracts

{:start="23"}
1. David Yarowsky, **Arya D. McCarthy**, Garrett Nicolai, Winston Wu, Aaron Mueller, Dylan Lewis, Yingqi Ding, Abhinav Nigam, Emre Ozgu, Debanik Purkayastha, James Scharf and Kenneth Zheng. *[A 1000-language Collaborative Universal Dictionary and Universal Translator](https://en.unesco.org/sites/default/files/lt4all_programme_day2and3.pdf)*. UNESCO Language Technologies for All (LT4All) 2019.

1. Xian Li, Jiatao Gu, Ning Dong, and **Arya D. McCarthy**. Improved variational neural machine translation via promoting mutual information. EMNLP Workshop on Neural Generation and Translation 2019.
1. Xian Li, Jiatao Gu, **Arya D. McCarthy**, and Ning Dong. Improving variational NMT by promoting mutual information. West Coast NLP Summit (WeCNLP) 2019.
1. **Arya D. McCarthy**. *Community Detection, The No Free Lunch Theorem, and Attack Games*. SIAM Workshop on Network Science 2019.
1. **Arya D. McCarthy**. [*An exact No Free Lunch theorem for community detection*](http://cs.jhu.edu/~arya/mccarthy.iccna18.pdf). [Complex Networks (ICCNA) 2018](https://www.complexnetworks.org).
1. **Arya D. McCarthy** and David W. Matula. [*Evaluating the leximin method for community detection*](http://cs.jhu.edu/~arya/mccarthy+matula.iccna18.pdf). [Complex Networks (ICCNA) 2018](https://www.complexnetworks.org).
1. **Arya D. McCarthy** and David W. Matula. [*Normalized mutual information exaggerates community detection performance*](http://cs.jhu.edu/~arya/mccarthy+matula.ns18.pdf). SIAM [Workshop on Network Science 2018](https://www.siam.org/conferences/CM/Main/ns18). 

## Master's thesis


{:start="20"}

1. **Arya D. McCarthy**. Gridlock in networks: [*The leximin method for hierarchical community detection*](https://search.proquest.com/docview/1907180434). Master's thesis, SMU. 2017.
