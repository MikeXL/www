-
title: Classifier Evaluation 
date: 2018-11-12 11:11:11 -0700 
-


Classifier Evaluation

For binary classification, commonly we like to look into confusion matrix and its derivatives such as accuracy, misclassification rate, F1 scores. ROC curve also helps. And to business community especially on marketing lift, gain charts are the easiest to talk with. Recently I have learnt the calibration plot that is more for model calibration than anything else. But that is part of the model checking. Speaking of calibration ks test or ks plot also helps. 

For multi class classifiers, cross entropy would work, didn’t mention it above as it works for just any number of classes. And Kaggle popularize it. Confusion matrix is still good for quick glass. All others like ROC, PR curves, calibration plots etc. mostly would be done after the one hot encoding of the label and predicted class then do the one-vs-Rest. Or else utilize PCA or tsne to reduce classes into two and then run an scatter plot with colouring for each label, that way could tell how far apart the predictions are for all classes, close is bad and separation is good in this case. 

Online evaluation is even harder. 

The ones those are easier to explain to business stakeholders are gain, lift, responses as well as expected value (or so called cost based) 