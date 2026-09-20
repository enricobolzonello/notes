---
up:
  - "[[An Edge Cut disconnects G, Min-Cut is the edge cut of minimum cardinality]]"
tags:
  - atomic
created: 2026-05-15 14:18
---

> **Objective**: Find the [[An Edge Cut disconnects G, Min-Cut is the edge cut of minimum cardinality|edge cut]] $C^*$ of minimum cardinality of a connected multigraph $G=(V, E)$, aka the *Min-cut problem*


The key operation is the **node contraction**, which for edge $e=(u,v)$ merges $u$ and $v$ into a single node. The operation never decreases the min-cut size.

> [!important] Crucial Property
> For each edge cut $C^\prime$ of $G/e$, it exists an edge cut C of G such that $|C^\prime|=|C|​$


IDEA: if I perform $|V|-2$﻿ contractions, I reduce $G$﻿ to a multigraph with only two nodes. If the contractions avoid the edges of a fixed min-cut, then $C^*$﻿ corresponds to $\{\{(z_1,z_2)\}\}$

```Python
def FULL_CONTRACTION(G=(V,E)):
	for i in range(|V|-2):
		e = random(E) # select a random edge (accounting for multiplicities)
		G <- G/e
	return |E|
```

```Python
def KARGER(G,s):
	min_cont = +infty
	for _ in range(s):
		t = FULL_CONTRACTION(G)
		min_cont = min(min_cont, t)
	return min_cont
```