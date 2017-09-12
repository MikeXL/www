---
title: "Stats for Hackers"
author: "M. Liu"
date: 2015-01-10 11:11:11 -0700
categories: www
output: html_document
---


## warm-up: coin toss
22 heads out of 30 coin tosses.
Is it a fair coin? 
How probable to get that?

Classic
```{r}
prop.test(22, 30, 0.05)
```

Simulation
```{r}
N <- 10000
x <- NULL

for(i in 1:N){
  x[i] <- ifelse(sum(sample(c(0,1), 30, replace=T))>=22, 1, 0)
}

sum(x)/N

```

## sneetches

Classic Student's T Test
```{r}
y1 <- c(84, 72, 57, 46, 63, 76, 99, 91)
y2 <- c(81, 69, 74, 61, 56, 87, 69, 65, 66, 44, 62, 69)
t.test(y1, y2)

```

Bayesian EStimates
```{r}
require(BEST)
best.sneetches <- BESTmcmc(y1, y2)
summary(best.sneetches)
plotAll(best.sneetches)
```

Bayesian Factor
posterior odd ... prior odd x likelihood odd (aka bayes factor)

0.578
https://en.wikipedia.org/wiki/Bayes_factor

```
require(BayesFactor)
bf.sneetches <- ttestBF(y1, y2, posterior = TRUE, iterations = 10000)
summary(bf.sneetches)
plot(bf.sneetches)
```

shuffling and resampling
?????
```{r}

ys <- c(y1, y2)
mean_diff <- NULL

for(i in 1:N){
  ys1[i] <- ys[sample(1:length(ys), 8, replace = T)]
  mean_diff [i] <- mean(ys1[i]) - (sum(ys) - sum(ys1[i]))/12
}

```

##yertle bootstraping

```{r}
yertle <- c(48, 24, 32, 61, 51, 12, 32, 18, 19, 24, 21, 41, 29, 21, 25, 23, 42, 18, 23, 13)

yertle.mean <- mean(yertle)
yertle.se <- sqrt(var(yertle)/(length(yertle)-1))
y.sample <- NULL
ymean <- NULL
yse <- NULL
for (i in 1:N) {
  y.sample[i] <-rnorm(20, yertle.mean, yertle.se)
}
mean(y.sample)
sd(y.sample)
```

## cross validation