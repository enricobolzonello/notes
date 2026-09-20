---
tags:
  - atomic
up:
  - "[[Coreset is a small subset from P which represent P well]]"
created: 2024-12-20 21:14
---


> [!Definition]
> Partition $P$ into subsets $P_1,P_2,...,P_l$ and extract a small [[Coreset is a small subset from P which represent P well|coreset]] $T_i$ from each $P_i$. Run best known sequential algorithm for $\Pi_i$ on $T=\cup_{i=1}^lT_i$


Effective if:
- each $T_i$﻿ can be extracted efficiently from $P_i$﻿ in parallel
- final coreset $T$﻿ is still small and the solution on $T$﻿ is a good solution for $\Pi$﻿ with respect to the entire input $P$

# See also
- [[Coreset is a small subset from P which represent P well]] — the parent concept: composability is the property that makes coresets parallelisable; without it each shard's coreset would be meaningless in isolation
- [[Natural Batching, start a batch as soon as requests arrive, complete it when full or queue is empty]] — the same greedy structure: each shard processes its partition independently and produces a result; the union step is the natural batching analogue at the data level
- [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] — the doubling dimension governs how small each per-shard coreset Tᵢ can be while still guaranteeing that their union T = ∪Tᵢ preserves the global solution
- [@ceccarelloSolving$k$centerClustering2021] — the paper that proves composability holds for k-center: the union of per-shard GMM outputs is a valid coreset for the global problem