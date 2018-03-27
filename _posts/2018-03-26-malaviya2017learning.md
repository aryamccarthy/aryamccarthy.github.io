---
layout: paper
title: "Learning Language Representations for Typology Prediction"
authors: "Malaviya et al."
year: 2017
venue: EMNLP
link: "https://www.aclweb.org/anthology/D17-1268"
---

Today we enter the wonderful world of linguistic typology: inventories of languages' features. Databases of these features have been compiled, such as the [World Atlas of Language Structures](https://en.wikipedia.org/wiki/World_Atlas_of_Language_Structures). The details of typology can be useful for downstream tasks.

The authors propose a model of learning these typological features from a translation system into English. They use it to fill in gaps in a database of features, then show that they outperform a baseline relying on geography and phylogeny.

<!--more-->

The work seems to operate on the Duolingo principle: that we can infer what a learning method knows about linguistic concepts by looking at their representations for a large number of sentences. This is like how Duolingo doesn't explicitly teach grammar, but hopes that you pick it up along the way.

The authors start off by considering the [URIEL database of typology](http://www.cs.cmu.edu/~dmortens/uriel.html), which is part of the DARPA LORELEI project. It compiles information from numerous prior databases. The features are syntactic (103), phonological (28), and phonetic (158). All features are binary. Because some features are one-hot encoded, certain vectors are impossible.

Building on this database, they produce baseline feature vectors for languages, averaging the 3 nearest neighbors. These neigbors come from normalizing the geodesic and genetic distances of the languages, which could be dicey because it would introduce numerous biases. Basque isn't close to Spanish or Catalan genetically, but their geodesic position would lead to each contributing to the other.

They trained a logistic regression classifier with either the above baseline vectors or their proposed features, then performed 10-fold cross-validation. A logistic regression classifier can perform either binary or multi-class prediction, and they use separate classifiers for each class of feature, like syntax. 

Next, the authors seek to determine vector representations of languages by neural methods. One that they attempt is by language modeling. The authors append a token representing the language to the sequence, then using the computed representation of that vector as its features. This builds on the RNNLM (recurrent neural network language model) of [Mikolov et al.](http://www.fit.vutbr.cz/research/groups/speech/publi/2010/mikolov_interspeech2010_IS100722.pdf) They call these "LMVec". 

The other model that they use is a translation-based language vector. These are called "MTVec". By translating from numerous languages into the same English sentence, they learn vectors with more grasp of the salient features.

Finally, they propose "MTCell", which is the average of the encoder *cell* states across all sentences in the language. These are different from the hidden states. Cell states are the longer-term values that are internal to each component. The hidden states, by contrast, are used for output. The cell state is what holds the long-term parts of the information.

Their data source is a scraping of 1017 languages of the Bible from bible.com. A lot of these are low-resource, which is why they used Google's many-to-one translation system. The authors used byte pair encoding to reduce the total vocabulary size. In translating all of these to English, the authors found that the hidden vectors representing languages were better than statically learned vectors. Additionally, vectors from similarly featured languages progress similarly over time. For instance, languages with or without the feature `S_OBJ_BEFORE_VERB` have similar trajectories.

**Future work idea:** There are 27 English versions of the Bible, so could this work be strengthened by averaging over these representations? Translate not into one English Bible, but into all 27. I think this could make a nice short paper, buttressing the work that colleague Patrick Xia has done. On top of that, the learned vectors could be used for phylogeny. Well, not the vectors themselves, but a transformation of them. Maybe the linguistic vectors you get out of them.
