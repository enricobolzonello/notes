---
connections:
  - "[[Clustering is the task of grouping a set of objects]]"
tags:
  - atomic
created: 2024-12-20 21:15
---
 
Suppose we want to solve a problem $\Pi$ on instances $P$ which are too large to be processed efficiently. The **coreset** aims at making it possible to solve the problem on a small subset of data, maintaining the accuracy within a small multiplicative factor. 

> [!Definition]
> Extract a small subset $T$﻿ (called **coreset**) from $P$﻿, which represents $P$﻿ well. Run best know sequential algorithm for $\Pi$ on the coreset $T$

Effective if:
- $T$﻿ can be extracted efficiently by processing $P$﻿
- The solution on $T$﻿ is a good solution with respect to the entire input $P$. A condition that might be satisfied is: $$(1-\epsilon) \cdot f(P_{sol}) \le f(T_{sol}) \le (1+\epsilon)\cdot f(P_{sol})$$
  for some small $\epsilon>0$

# See also
- [[Clustering is the task of grouping a set of objects]] — coresets exist specifically to make clustering tractable on large inputs; the coreset is only meaningful relative to the clustering objective f
- [[Composable Coreset partitions P, the union of the coresets of P is still a coreset]] — the parallel extension: partition P into shards, extract a coreset per shard, union them; composability is what makes coresets usable in MapReduce
- [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] — the doubling dimension D of the metric space determines how small the coreset can be; small D means very space-efficient coresets
- [[Angular Distance is the true metric version of cosine distance]] — coresets require a true metric for their approximation guarantees; angular distance qualifies, cosine distance does not
- [@ceccarelloSolving$k$centerClustering2021] — the paper that introduced the composable coreset construction for k-center clustering with and without outliers