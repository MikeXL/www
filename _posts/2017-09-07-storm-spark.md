---
layout: default
title:  "storm v. spark streaming"
date:   2017-09-07 09:44:45 -0700
categories: www
---

*storm* has been coded with fault tolerance in heart, and in case of (worker) node failure, reroute to other workers to complete. That might be the main feature. and storm is the type of CEP (complex event processing) engine, if you are into buzz words.  

*spark* streaming, is actually _micro batching_ that spark does best, (in memory) batch processing. So in case of failure, if the data is not loaded into hdfs or into storage somehow, you are on your own.  

PS  
worth to mention that msft azure has implemented SQL interface for streaming analytics, that is much more convenient. So does spark structured streaming, not fully SQL yet, but getting there. 

