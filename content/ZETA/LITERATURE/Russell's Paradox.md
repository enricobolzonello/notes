---
connections:
  - "[[Foundational Crisis of Mathematics]]"
reference: https://en.wikipedia.org/wiki/Russell%27s_paradox
tags: 
type: literature_note
created: 2025-05-16 10:17
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!important] 
> Every set theory that contains an unrestricted comprehension principle leads to contradictions

--> unrestricted comprehension principle: there is a set of all and only the objects that have that property

# Counter example 
Let $R$ be the set of all sets that are not members of themselves. If $R$ is not a member of itself, then its definition entails that it is a member of itself.
Yet if it is a member of itself, then it is not a member of itself since it is the set of all sets that are not members of themselves.
In symbols:
$$
\text{Let } R=\{x|x\not\in x\}, \text{then } R\in R \Longleftrightarrow R\not\in R
$$
which is a paradox.