---
connections: 
reference: 
tags:
  - type/term
  - theme/big-data
type: literature_note
created: 2024-12-20 21:15
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

Suppose we want to solve a problem $\Pi$ on instances $P$ which are too large to be processed efficiently. The **coreset** aims at making it possible to solve the problem on a small subset of data, maintaining the accuracy within a small multiplicative factor. 

> [!Definition]
> Extract a small subset $T$﻿ (called **coreset**) from $P$﻿, which represents $P$﻿ well. Run best know sequential algorithm for $\Pi$ on the coreset $T$

Effective if:
- $T$﻿ can be extracted efficiently by processing $P$﻿
- The solution on $T$﻿ is a good solution with respect to the entire input $P$. A condition that might be satisfied is: $$(1-\epsilon) \cdot f(P_{sol}) \le f(T_{sol}) \le (1+\epsilon)\cdot f(P_{sol})$$
  for some small $\epsilon>0$