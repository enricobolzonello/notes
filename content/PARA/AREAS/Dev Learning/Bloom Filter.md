---
area: Dev Learning
tags:
  - area/dev_learning/untitled
type: area_note
created: 2025-04-04 10:49
---
# [[2. Dev Learning]] 
# Bloom Filter

From Big Data notes, [[Archive/University Notes/Big Data/Riassunto/Streaming/Filtering/Key Points|Bloom Filter]]:
- Keep an array $A$﻿ of $m$ bits
- With $k$﻿ hash functions, do $A[h_j(e)]=1, \forall 1\le j \le k$﻿ 
- For the membership test, $x_i\in S$﻿ if $A[h_1(x_1)]=...=A[h_k(x_i)]=1$
- probability that $x_i$﻿ is erroneously claimed to be in $S$﻿ is: $P(A[h_j(x_i)]=1,\:\forall 1\le j\le k)\simeq (1-e^{-km/n})^k$

-> typically $k$ is a small constant which depends on the desired false error rate $\epsilon$
-> $m$ is proportional to $k$ 

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

--> This is the simple Bloom Filter.



