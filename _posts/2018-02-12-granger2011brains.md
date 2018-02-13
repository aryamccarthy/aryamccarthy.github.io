---
title: "How Brains are Built: Principles of Computational Neuroscience"
layout: post
excert_separator: <!--more-->
---

([Granger 2011](https://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.352.2852&rep=rep1&type=pdf)) in *Cerebrum*

This paper treats the word "computational" not as something pertaining to computers, but rather as David Marr would use it. Marr identifies [three levels of phenomena](https://www.albany.edu/~ron/papers/marrlevl.html): the computational, the algorithmic, and the implementational. (Pylyshyn refers to these as the semantic, syntactic, and physical.) It's outside of NLP, but I've meant to read it for a long time—a glimpse into the state of computational neuroscience as it attempts to adapt models from the brain to other purposes.

<!--more-->

> Despite huge efforts and large budgets, we have no artificial systems that rival humans at recognizing faces, nor understanding natural languages, nor learning from experience.

## Do we know enough about brains to build them?

The thing is that we don't know much about brains. We know that most brain structures are similar, and bigger brains yield better computation. We know (and Jeff Hawkins has written [an entire book](https://en.wikipedia.org/wiki/On_Intelligence), [plus](https://doi.org/10.3389/fncir.2016.00023), on) the fact that the brain's structure is largely repeated.

We know that brains are slow and sloppy. They must be more precise than we realize, or they can do math that survives imprecision. We're also massively parallel. Amdahl's law in mind, there must be some tricks we're not exploiting in our simulations.

## From circuits to algorithms to prosthetics

We have a decent understanding of the basal ganglia—they take sensory information and an external reward or punishment signal. This is [reinforcement leraning](https://en.wikipedia.org/wiki/Reinforcement_learning), implemented in the brain. (ML people, get excited.) But brains are also great at structuring knowledge, and this happens in the neocortex—the region which has grown over the course of mammalian evolution.

> There is a growing consensus that circuits in the neocortex, by far the largest set of brain structures in humans, carry out another, quite different kind of learning: the ability to rapidly learn new facts and to organize newly acquired knowledge into vast hierarchical structures that encode complex relationships, such as categories and subcategories, episodes, and relations.

Between the two of these, we have ways of learning skills and organizing a database of facts.

## From percept to concept

The database starts off empty, though. Just how we manage to operate on our memories—"association, recall, retrieval, organization"—is totally opaque.

> Seeing a phone, we perceive not only its visual form but also its affordances (calling, texting, photographing, playing music), our memories of it (when we got it, where we have recently used it), and a wealth of potential associations (our ringtone, whom we might call, whether it is charged, etc.). The questions of how cross-modal information is learned and integrated, and in what form the knowledge is stored􏱭how percepts become concepts􏱭now constitute the primary frontier of work in computational neuroscience. In this borderland between perception and cognition, the peripheral language of the senses is transmuted to the internal lingua franca of the brain, freed from literal sensation and formulated into internal representations that can include a wealth of associations.

Granger also goes on to discuss some of the policy implications of the development of computational prosthetics, though it's largely speculative. The writeup is at an introductory level. I enjoyed Jeff Hawkins's [On Intelligence](https://en.wikipedia.org/wiki/On_Intelligence), and I strongly recommend it for someone who wants to dive deeper into this content.
