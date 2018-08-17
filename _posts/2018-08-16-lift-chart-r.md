---
layout: default
title:  "Plot lift chart using R"
date:   2018-08-16 19:31:45 -0700
categories: www
---

Here is the code to draw cum lift chart
```
require(tidyverse)
n.groups=100

lift.tbl <- data.frame(label=label, pred=prediction) %>%
  drop_na()%>%
  mutate(cutoffs = ntile(-(pred), n.groups)) %>%
  group_by(cutoffs) %>%
  summarise_at(c("label"), funs(total=n(), totalresp=sum(., na.rm=T))) %>%
  mutate(cum.resp = cumsum(totalresp),
         gain = cum.resp / sum(totalresp),
         cum.lift = gain/(cutoffs/n.groups)) %>%
  with(plot(cutoffs, cum.lift, type="l"))
```

LLAP
