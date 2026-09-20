---
up:
  - "[[Clustering is the task of grouping a set of objects]]"
tags:
  - atomic
created: 2025-04-04 10:49
---

A **Bloom Filter** keeps an array $A$ of $m$ bits. To insert an element $e$, set $A[h_j(e)]=1, \forall 1\le j \le k$﻿ with $k$ hash functions. To test membership of $x$:
- if any $A[h_j(x)]=0$ → $x$ is **definitely not** in the set 
- if all $A[h_j(x)]=1$ → $x$ is **probably** in the set (but false positives are possible)
There are no false negatives, so if an element was inserted all its bits are set. 

The probability that $x_i$﻿ is erroneously claimed to be in $S$﻿ is: 
$$
P(A[h_j(x_i)]=1,\:\forall 1\le j\le k)\simeq (1-e^{-km/n})^k
$$
where $n$ is the number of inserted elements, $m$ is the array size, $k$ is the number of hash functions. 
Typically:
- $k$ is a small constant which depends on the desired false error rate $\epsilon$
- $m$ is proportional to $k$ 

Insertion:
- feed the element to the $k$ hash functions to get $k$ array positions
- set positions bits to 1
Testing:
- feed the element to the $k$ hash functions to get $k$ array positions
- two cases
	- any of the position is at 0 = element def not in the set
	- otherwise = either:
		- the element is in the set
		- bits have by chance been set to 1 during insertion of other elements (no way to tell the difference)

# See also 
- [[A Hash Function Must Be Deterministic, Uniform, and Fast — FNV-1a Is One Example]] — each of the k hash functions must be uniform and independent; poor hash functions increase false positive rate by clustering bits 
- [[Collisions are unavoidable by Pigeonhole, Chaining and Open Addressing resolve them]] — false positives in Bloom Filters are the same phenomenon as hash collisions: different elements mapping to the same bit position 
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — the bit array is compact and cache-friendly for sequential scans; the k random bit positions accessed per query are not sequential, so membership tests cause cache misses

# References
- [[Archive/University Notes/Big Data/Riassunto/Streaming/Filtering/Key Points|big data notes]]