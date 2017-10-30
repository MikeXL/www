---
layout: default
title:  "data science - an art of balance"
date:  2017-10-19 11:51:45  -0700
categories: www
---

To _warm up_, here are some good quotes.

> Happiness is a place between too little and too much. ~ Finnish Proverb

> Enough is as good as a feast. ~ English Proverb

> Don't be sweet, lest you be eaten up; don't be bitter, lest you be spewed out.  ~ Jewish Proverb

> To go beyond is as wrong as to fall short. ~ Confucius

Now let's get into the topic of data science.

### Trade off of bias vs. variance
This would be the first thing to think of before an modelling.

Side note to myself:   
*Bias*, likely for underfitted model, and has similar high model errors for both training and testing set.   
*Variance*, likely for overfitted model, that fits really well on training set, but not testing. the variance refer to the variance between fits.

Regularization is there to help peeps to make the tradeoff by penalizing the model.

### Model selection
Another balance, trade off to be considered. We usually starts with _lm_ and may end up there too sometimes. Or else try out the complex models, or doing aggregates such as bagging, boosting.
