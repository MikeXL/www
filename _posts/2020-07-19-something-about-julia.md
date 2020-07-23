---
layout: default
title:  "Something about Julia"
date:   2020-07-19 21:59:08 -0700
categories: www
---

Simple statistics using Julia

```
# mainly I need the language to perform
# 1. experiment analysis
#   1.1 hypothesis tests in frequentist eyes
#         t.test, chisq.test, poisson.test, prop.test, bino.test
#   1.2 in bayesians' eyes naive simulation of gamma, beta distribution
#        for possion and binomial proportion tset
# 2. modelling and interpretation
#        glm, random forest, xgboost, mcmc, neural net
# 3. nice to have
#        call fortran when needed
#        matmul when having spare time for fun
#        GPU directly or indirectly
#        comfy IDE

using Statistics
using HypothesisTests           # t.test ordinary or welch

using Distributions             # Gamma, Beta
using StatsPlots


#1. experiment

a = rand(Beta(400, 600), 10000)
b = rand(Beta(450, 550), 10000)

var(a)
var(b)
EqualVarianceTTest(a, b)


violin([a b])
histogram([a b])
density([a b], label=["A" "B"])     
density([a b], layout=(2,1))           # split density view

marginalhist(a, b)
plot(a, b)
scatter(a, b)


#2. modelling
~
```
