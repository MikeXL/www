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
    hpneural ....... vanilla neural network 
    hpforest ....... random forest
                     varimp proves the same as hpgenselect
    hpbnet ......... bayesian network
    hpsplit ........ tree

*****************************************************************************************;

proc hpgenselect data=samples ;
    PARTITION FRACTION(TEST=0.3);
    class &vars;
    MODEL &target (EVENT=LAST) = 
        &vars
        &vars_int
        /dist=binomial;
    SELECTION
        /*METHOD=lasso*/
        METHOD=backward
        DETAILS=ALL;
run;

proc genmod data=samples ;
    class &vars;
    MODEL &target (EVENT=LAST) = 
            &vars_int
            &vars
    /dist=bin;
run;


proc hpneural data=samples;
    input &vars_int;
    input &vars / level=nom;
    target &target / level=nom;
    hidden 2;
    train outmodel=neural maxiter=1000;
    score out=scores_neural;
run;


proc hpforest data=samples;
    input &vars_int;
    input &vars / level=NOMINAL;
    target &target / level=NOMINAL;
run;

proc hpbnet data=samples
    nbin=5
    structure=Naive TAN PC MB 
    /*varselect=1*/
    bestmodel
;
    input 
        &vars_int
        &vars
    ;
    target &target;
    partition FRACTION (VALIDATE=0.3);
    output network=bnet fit=fit validinfo=vi varselect=vs varlevel=vl;
run;

%cat(bnet);
%cat(fit);
%cat(vi);
%cat(vs);
%cat(vl);

proc hpsplit data=samples ;
    input &vars
          &vars_int;
target &target;
   grow entropy;
   prune costcomplexity;
   code file='~/tmp/hpspexec.sas';
   rules file='~/tmp/hpsprules.txt';
run;


```


