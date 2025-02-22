---
connections: 
reference: 
tags:
  - type/term
  - theme/big-data
type: literature_note
created: 2024-12-20 21:14
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!Definition]
> Partition $P$ into subsets $P_1,P_2,...,P_l$ and extract a small [[Coreset|coreset]] $T_i$ from each $P_i$. Run best known sequential algorithm for $\Pi_i$ on $T=\cup_{i=1}^lT_i$


Effective if:
- each $T_i$﻿ can be extracted efficiently from $P_i$﻿ in parallel
- final coreset $T$﻿ is still small and the solution on $T$﻿ is a good solution for $\Pi$﻿ with respect to the entire input $P$