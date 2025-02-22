---
connections: 
reference: 
tags:
  - theme/lsh
type: literature_note
created: 2025-02-03 10:28
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

Hashing function for [[Cosine Similarity]]
> [!DEFINITION]
> $$
> h_w^{sim}(x) = sign(w^Tx)
> $$

The probability of collision satisfy the following equation:
$$
P(h_w^{sim}(x)=h_w^{sim}(y)) = 1-\frac{\theta}{\pi}
$$
where $\theta=\arccos(sim_{cos})$.