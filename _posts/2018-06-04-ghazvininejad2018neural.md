---
layout: paper
title: Neural Poetry Translation
authors: Ghazvininejad, Choi, and Knight
year: 2018
venue: NAACL
link: "https://aclweb.org/anthology/N18-2011"
---

Douglas Hofstadter's *Le Ton Beau de Marot* points out that machine translation is mainly driven by military and industry. There's little room for nuance and beauty. Ghazvininejad et al. address that problem.

<!--more-->

There have been non-neural approaches—searching through translation lattices or decoding with constraints. Both of these, the authors claim, "report total failure". These phrase-based approaches have fewer options when constraints are introduced because they have learned a bilingual dictionary of phrases. There's no higher-level structure, and the source poem can't be freely altered. (One alteration that Hofstadter wrote about is changing metaphors from language to language.)

The network is a generic sequence-to-sequence network. They pre-train it on the WMT14 corpus—a standard, widespread dataset to give the model a sense for English–French relationships. (Pre-training implies that you'll fine-tune the training later.) To adapt the system to translate poetry, they continue training on 30,000 English or French songs with their corresponding (French or English) translations. 

**Model A:** Constraints:

- The **rhythm constraint** is expressed with a finite-state acceptor. During the beam search that happens in decoding, only translations that would be accepted by the FSA are allowed.
- The **rhyme constraint** is enforced by creating one FSA for each class of rhyming words. Every line is translated once for each class, then the classes with the highest combined scores are taken. (There are tons of rhyme classes in English, so they stick to just the 100 most frequent—which covers 67% of rhyming words.)

**Model B:** Another trick they attempt is using the unconstrained model to their advantage, boosting the probabilities of words in the unconstrained translation. (They multiply the log-probabilities by 5.)

**Model C:** They also need to handle rare words—the FSAs don't know how to pronounce them, so they use the translation table of a phrase-based system to get a list of all possible translations for words, which helps to guide the system. 

They surveyed online users of Amazon Mechanical Turk to get appraisals of the translations. Model C was preferred over Model B, which was preferred over Model A. (This does nothing to say whether it's a good translation of the original.) The authors also note that the MTurk respondents generally ranked the poems to be at least "okay". (I don't agree that this should be the middle of a Likert scale—Why not something more neutral? And do Internet randos really know how to rate poetry?) Still, that's notable validation for their model.

**The bottom line:** The authors present a model that produces new text in a given meter and rhyme pattern, based on poems in a different language. Whether the new text is poetry—or is a translation—is less clear.
