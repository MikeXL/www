---
layout: default
title:  "R packages, I used the most"
date:   2020-08-96 21:26:08 -0700
categories: stats, ml
---
Oh well, thinking to make a list of my fav packages when using R.   
Over the time, I've been happy with base R to do simple bayes analysis, 
simulations and quick check on A/B test results.   

tldr;  
Here are the list of packages, I used quite a bit
* DataExplorer
* rpart
* party
* ranger
* randomForest
* xgboost
* DALEX


More in details... 
### Data Munging
There is _dplyr_, though I do not use it much than getting the "pipe" %>%   
to make my code looks cleaner.  
Most of my data transformation and integration work are done using SQL at data source,   
then bring the well formatted (ahem, mostly well formatted) data into R.  

### Data Exploration 
Again, mostly I was relying on _summary_ and base plot to do basic checks in histogram, boxplot, trend lines etc.  
There is this _DataExplorer_ package, discovered recently, I'm quite fond of.   

And please don't ask me the fancy way of imputing data using _dplyr_, again, mostly just using base dataframe.  

### Model
Here, there are fancy wrappers, again, the packages like   
_rpart_, _party_, _ranger_, _randomForest_, _xgboost_ are quite intuitive to use, so I went with those packages.    

Quite happy with _DALEX_ for model checking.   

### Publishing 
Here, no need to say how much joy working with _rmarkdown_ either for document or presentation. 
