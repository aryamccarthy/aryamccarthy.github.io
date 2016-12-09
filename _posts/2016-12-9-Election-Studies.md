---
layout: post
title: Election Studies
---

What are the two hot topics of 2016? Celebrity deaths and elections. I'll admit that I caught the bug, too. I'm working with two professors on dynamical (think differential equations) models of the American electorate.

A hallmark of twenty-first century American politics is that American voters have become “sorted” such that political views are now strong predictors of one another. Nowadays, one’s stance on birth control is more informative about one’s stance on gun control than would have been the case a generation ago. A [Pew survey](http://www.people-press.org/2014/06/12/political-polarization-in-the-american-public/) conducted in 2014 shows that among the politically active, uniformity of views within one’s party has grown. Why has this happened?

### Political Considerations

One unique feature of American politics is our two-party system, and the significant obsta- cles faced by any putative third party in our winner-take-all election system. Nevertheless, this system is as old as our nation itself, so other factors must be at play. Candidate mecha- nisms frequently encountered in the popular media include the proliferation of cable news networks with specific ideological slants, and the rise of social media, both of which can encourage an “echo chamber” effect in which one’s views are never challenged, but only reinforced. Sure, now you hear about it on the news all the time. But you didn't when I wrote the fellowship application funding this work.

### Mathematical Considerations

These theories imply a dynamic relationship between voters, news organizations, and po- litical party leadership, which recalls the mathematical concept of a “dynamical system”— a collection of inter-dependent variables governed by differential equations. Moreover, the increasing levels of polarization in the past two decades recall the mathematical concept of an “instability”—a self-reinforcing shift away from an equilibrium (i.e. the prior hetero- geneous distribution of opinions). Finally, the transition away from heterogeneous, non- correlated opinions to a tightly-sorted set of opinions recalls the concept of a “bifurcation”—a fundamental structural change in the stability properties of a dynamical system induced by changes in an underlying system parameter.

### Methodology
As a starting place, one can picture each issue as an axis in a multidimensional vector space, and an individual's total political position as a point in this space. Over time, the “sorting” described above should manifest itself as a coalescence of these points into two distinct clusters: one for each political party. [Our first task](https://github.com/aryamccarthy/ANES/blob/master/ANES/clustering.ipynb) in understanding the process will be to quantify the sorting using Principal Component Analysis, which can quantify the extent of the sorting over time, as well as identifying the dominant correlations among different opinions. Then, after a literature review of dynamical systems applied to held beliefs (like political stances), we will create models attempting to capture the sorting effect, run them using computer simulations, and compare the output to collected polling data. This process can be repeated to “tune” the models to fit the data. The hope is that the tuned model will reveal a fundamental system dynamic that sheds light on the causes of increased polarization in recent years.

Some novel stuff we're doing:

- A new reordering criterion for correlation matrices, based on the singular value decomposition.
- Using Jupyter notebooks instead of just scripts. Github doesn't render the interactive Plotly plots, though.