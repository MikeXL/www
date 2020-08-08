---
layout: default
title:  "neural net or so called deep learning, revisit"
date:   2020-08-07 21:41:08 -0700
categories: ml, nnet, dl
---

Thought to write it down, before it gets buried in my tiny little brain.   

Neural network isn't new, most of the algorithms including BP were invented in last century.  
Yes, last century.   
It gets popularized by the increased computing power, and then it popularized the computing power.   

To train neural net, mostly come down to   
1. select the structure or topology, decide for shallow or deep, number of layers, type of layers, number perceptrons, type of activation functions, etc.
2. method for weight update, this one gets easier these days, as BP is the known easy working one, along with that, 
2.1 choosing error (loss) functions relatively easy, _mse_ for regression, and _cross entropy_ for classification or _mse_ for whatever
2.2 choosing optimizer, this could be a bit tricky, but not that bad, always could go with _sgd_ or _adam_ with default parameters 

Now, it adds whole bunch of hyperparameters to tune already, and those are not all.   
One could imagine the tedious work is more of tuning 10-30x more than other algorithms.    

The good news is, in business settings, I mean structured tabular data than vision, speech, text etc.  
Usually could get away with vanilla shallow neural net, most of time just single hidden layer.  

In my view, this field still requires tons of research work to be done on *auto structure search*, *auto hyperparameter search*,  
not only search the best settings or configurations, but do it in efficient fashion.  

And worth to mention, we still solving supervised learning problem, than unsupervised, i.e. 
an neural net today is not really comparable to an toddler yet.   
