---
layout: paper
title: "Improving Low Resource Machine Translation using Morphological Glosses"
authors: "Shearing et al."
year: 2018
venue: AMTA
link: "https://www.aclweb.org/anthology/W18-1813"
---

Translation models demand oodles of training text. In low-resource languages, we need tricks to circumvent the data famine. Languages with many inflected forms for each base word make the famine even scarcer. This paper presents a trick for feeding the hungry by multiplying our few loaves and fish: glossing words and morphological annotations. (Also—my advisor is on this paper :D .)

<!--more-->

To help our models out, we want to make the source text more similar to the target.

Shearing et al.'s innovation is the inclusion of **morphological glosses**, which makes dictionaries more useful. Dictionaries often list only a principal form for a set of words: "run" but not "running" or "ran". The authors' glossing process creates in-place translations of "running" and "ran" from the one for "run" and knowledge about verb tense.

The morphological glosses work into a four-stage pipeline that creates an out-of-order English (English-prime; \\(E'\\)) from the foreign source text. For each foreign word, do the following:

1. Analyze the word to get a lemma and morphological tag: *comprábamos* → *comprar*, `V;1;PL;PST;IPFV`
2. Look up the lemma in a lemma-to-lemma dictionary: *comprar* → *buy*
3. Convert the morphological features into a morphological gloss: `V;1;PL;PST;IPFV` → ‘(we) were `VBG`.’
4. Replace the placeholder (VBG) with the corresponding form of the English lemma: ‘(we) were `VBG`’ + `buy` → ‘(we) were buying’

At the end, you get `comprábamos` → ‘(we) were buying’, which the authors stick into a phrase-based translation model, turning \\(E'\\) into \\(E\\).

**Little details:**

- Morph analysis using Kann and Schütze (2016).
- Translate lemmas with PanLex or Wiktionary. 
- Manually create glosses.
- Inflect English with Spedt and Daelemans (2012).
- The LORELEI data they use gives multiple definitions for some words. Split these into separate lines, expanding your Bitext.
- Append a gloss-to-gloss identity mapping to the bitext, biasing the aligner toward lining these two up.

