---
area: CLANN
summary: 
tags: area/clann/useful_queries
type: area_note
created: 2025-02-19 14:55
---
# [[2. CLANN]] 
# Overview


```sql

-- see the average distance computations done by clann
select num_clusters, avg(distance_computations) from clann_results_query where num_tables=84.0 and git_commit_hash='afb20f4b1ac5f9c85cf44499e810680e4d2e8915' and dataset='glove-50-angular' and k=1 group by num_clusters;

-- same but for puffinn
select avg(distance_computations) from puffinn_results_query where num_tables=84.0 and dataset='glove-50-angular' and k=1;

```

