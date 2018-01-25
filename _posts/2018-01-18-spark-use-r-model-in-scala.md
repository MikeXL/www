---
layout: default
title:  "spark, reuse R model from scala"
date:   2018-01-25 10:32:45 -0700
categories: www
---

Often the scenario comes in as we develop and train the spark model in R, and then
we need productionize that either don't have R or no skill of R.. fortunately,
spark makes it easier to ship the model around and make it language agnostic

_train the model in R_
```
df.train <- sample(df, withReplacement=FALSE, fraction=0.7)
df.test  <- except(df, df.train)
m4 <- spark.mlp(df.train, f, layers=c(34, 5 ,2))
write.ml(m4, 'churn.ann.ml', overwrite=T)
```

_load the model in scala and predict_
```
import org.apache.spark.ml.PipelineModel
import org.apache.spark.ml.classification.MultilayerPerceptronClassifier

val model = PipelineModel.load("churn.ann.ml/pipeline")

val newData = ... /// retrieve new data
val result = model.transform(newData)

/// do something after the prediction

```
