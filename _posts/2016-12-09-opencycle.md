---
layout: post
title: OpenCycle Fertility Planning
---

Children are a long way off for me, given that I don't know where I'll wind up in a year. For many U.S. families, they're too far off, though. The best fertility planning out there still isn't good enough, so we're applying machine learning to the problem.

We want a data-driven family planning technique that relies only on a simple, at-home measurement. The conventional guidance is called “three-over-six”: when a woman’s minimum basal body temperature (BBT) over the past three days has exceeded the maximum for the six days before, we can be reasonably sure that ovulation occurred three days ago. While BBT remains popular because results can be interpreted at home (rather than in a lab), the measurement is difficult. Movement raises BBT beyond the range of error, so a woman must be very still when measuring BBT, first thing in the morning. Naturally, there are a lot of missing data points, and there are likely also false data points from women who mis-measured or recorded only a guess.

Even if a woman does everything right, the three-over-six rule tells us that ovulation happened **three days ago**. Because fertility is at its peak during ovulation and declines afterward, couples seeking to hvae children lose three good days.

We're working to use machine learning with an existing dataset of recorded menstrual cycle data to forecast the rise in BBT that signals ovulation. This gives more time to families who seek to have children - and limits risk for those who do not. We will explore time series models, deep learning, and various cross-validation techniques to ensure statistical validity of our results. As the data are already collected, we will not need to involve human subjects. 

Because access to the data for this project is heavily restricted, I'm keeping the Github repo private for now. But anonymized graphs are definitely on the horizon. Expect **lots** of violin plots.

**Update 2017-03-15:** The repo is no longer private, so [check it out](https://github.com/aryamccarthy/OpenCycle). Incidentially, this work is conducted as part of the [SMU Ubiquitous Computing Lab](http://ubicomp.lyle.smu.edu).
