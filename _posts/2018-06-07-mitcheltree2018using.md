---
layout: paper
title: "Using Aspect Extraction Approaches to Generate Review Summaries and User Profiles"
authors: "Mitcheltree, Wharton, and Saluja"
year: 2018
venue: NAACL
link: "https://www.aclweb.org/anthology/N18-3009"
---

I'm incredibly proud of a friend that I met in elementary school, [Veronica Wharton](http://veronicawharton.com), for her publication at NAACL this year. She and her colleagues at Airbnb have exploited [maximum entropy classifiers](https://en.wikipedia.org/wiki/Multinomial_logistic_regression) to pick apart users' reviews.

<!--more-->

There are two tasks in question here:

1. Information retrieval: picking out the sentence that exemplifies some aspect of the reviewed accommodation—cleanliness, communication with the host, location, and 'other'.
2. Learning to rank: producing embeddings for each guest from their reviews. Using these embeddings to determine how users appraise accommodations relative to one another.

The authors rely on the distributional hypothesis to include co-occurrence information: words are represented by vectors that are trained to incorporate their context. Words with similar contexts get similar vectors. A sentence is a matrix of one vector for each word. Since these are variable-size, all sentences are squeezed into a common size by a self-attention mechanism ([Lin et al., 2017](https://openreview.net/pdf?id=BJC_jUqxe)). 

Their method of extracting aspects presupposes the number of aspects, so they test different values and evaluate them using a 'coherence score'. These aspects are then condensed into the four categories mentioned above by hand. (Why not community detection on these?) It also sits on top of k-means as initialization (so no wonder it outperforms k-means?). I hope they ran multiple rounds of k-means, since k-means itself is sensitive to initialization.

When the authors produce guest embeddings, they evaluate them by comparing the distance between them to the difference in ratings given by the users. 
