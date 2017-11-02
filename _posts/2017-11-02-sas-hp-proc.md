---
layout: default
title:  "HP Procedures in SAS"
date:   2017-11-02 11:03:02 -0700
categories: www
---

```
******************************************************************************************
  MJ LOG: 2317.011117
  fit all these models for HSIA surveys with mentally selected variables, likely underfit

    hpgenselect .... regression variable selection, 
                     this proves the mental selection doesnot work
    genmod ......... regression
    hpneural ....... neural network with 1 hidden layer, 2 neurons
    hpforest ....... random forest
                     varimp proves the same as hpgenselect
    hpbnet ......... bayesian network
    hpsplit ........ tree

*****************************************************************************************;

```


