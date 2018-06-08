---
layout: default
title:  "Andrew's advice on PCA"
date:   2018-06-07 17:44:00 -0700
categories: www
---

>I would recommend, instead of putting PCA into the algorithm, just try doing whatever it is you're doing with the X first. And only if you have a reason to believe that doesn't work, so that only if your learning algorithm ends up running too slowly, or only if the memory requirement or the disk space requirement is too large, so you want to compress your representation, but if only using the X doesn't work, only if you have evidence or strong reason to believe that using the X won't work, then implement PCA and consider using the compressed representation. 

At last, he mentioned PCA is quite useful technique for dimension reduction.   
He did also mentioned to check the proportion of variance explained to be over 99% or 90% to get a better K.

Wish he covered autoencoder too, but that might be for his deep learning course.

LLAP
