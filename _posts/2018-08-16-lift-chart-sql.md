---
layout: default
title:  "Lift chart using SQL, indeed the lift table"
date:   2018-08-16 20:26:36 -0700
categories: www
---

It builds the lift table from scors {label, prediction}

```
select rnk, N, resp, cumresp, cumresp/totalresp gain, cumresp/totalresp/null_model lift
from (
        select  rnk, 
                N, 
                resp, 
                sum(resp) over(order by rnk rows between unbounded preceding and current row) cumresp, 
                sum(resp) over() totalresp, 
                rnk/100.0 null_model
        from (
                select rnk, sum(label) resp, sum(1) N
                from (
                        select label,  
                               ntile(100) over(order by prediction desc) rnk 
                        from workspace_mike.model_score_tbl
                     ) t 
                group by t.rnk
        ) tt 
) ttt
```

LLAP
