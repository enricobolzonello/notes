---
connections:
  - "[[PARA/AREAS/CLANN/2. CLANN.md|2. CLANN]]"
reference: 
tags:
  - type/paper
  - theme/lsh
type: literature_note
created: 2024-12-20 19:07
modified: 
citekey: aumullerSolvingKClosestPairs2023
status: read
dateread: 2024-10-07
---

> [!Cite]
> [1] M. Aumüller e M. Ceccarello, «Solving k-Closest Pairs in High-Dimensional Data», in _Similarity Search and Applications: 16th International Conference, SISAP 2023, A Coruña, Spain, October 9–11, 2023, Proceedings_, Berlin, Heidelberg: Springer-Verlag, ott. 2023, pp. 200–214. doi: [10.1007/978-3-031-46994-7_17](https://doi.org/10.1007/978-3-031-46994-7_17).


>[!Synthesis]
>**Contribution**:: 
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**:: [[@aumullerPUFFINNParameterlessUniversally2019]]


>[!Metadata]
>> **FirstAuthor**:: Aumüller, Martin  
> **Author**:: Ceccarello, Matteo  
~    
> **Title**:: Solving k-Closest Pairs in High-Dimensional Data  
> **Year**:: 2023   
> **Citekey**:: aumullerSolvingKClosestPairs2023  
> **itemType**:: conferencePaper  
> **Publisher**:: Springer-Verlag  
> **Location**:: Berlin, Heidelberg   
> **Pages**:: 200–214  
> **DOI**:: 10.1007/978-3-031-46994-7_17  
> **ISBN**:: 978-3-031-46993-0    

> [!LINK] 
> [Aumüller e Ceccarello - 2023 - Solving k-Closest Pairs in High-Dimensional Data.pdf](file:///Users/enricobolzonello/Zotero/storage/52M9QHRV/Aumüller%20e%20Ceccarello%20-%202023%20-%20Solving%20k-Closest%20Pairs%20in High-Dimensional%20Data.pdf).



> [!Abstract]
>
> We investigate the k-closest pair problem in high dimensions, that is finding the k≥1 closest pairs of points in a set S⊆X in a metric space (X,dist). This is a fundamental problem in computational geometry with a wide variety of applications, including network science, data mining, databases, and recommender systems. We propose an exact algorithm with a controllable failure probability, thus allowing the user to specify the desired recall. Our algorithm has expected subquadratic running time under mild assumption on the distance distribution, relying only on the existence of a Locality Sensitive Hash family for the metric at hand. We complement our theoretical analysis with an experimental evaluation, showing that our approach can provide solutions orders of magnitude faster than current state-of-the-art data structures designed for specific metrics.
>.
> 

# Notes
## k-closest pair problem

> Given a set $S\subseteq \mathcal{X}$ from a metric space $(\mathcal{X},\text{dist})$, the task is to identify k pairs of distinct points in $S\times S$ that are closest to each other

definition of k-closest pairs:

> the k-closest pairs in a set $S\subseteq \mathcal{X}$ are a sequence of distinct pairs $(r_1,s_1),…,(r_k,s_k)\in S^2$ such that for all other pairs $(r,s)\in S^2$ and for all $i\in \{1,…,k\}$:
> 
> $$\text{dist}(r_i,s_i)\le \text{dist}(r,s)$$

## PUFFIN query algorithm

1) check each trie j to find the leaf corresponding to the string

$$(h_{1,j}(q),...,h_{K,j}(q))$$

2) traverse the selected trie from bottom and keep track of the current kth closest point $x_k^\prime$

3) continue point 2 until the termination criterion

### Termination criterion

- current depth in the tries is $i$
- $\frac{\ln(1/\delta)}{p^i}$ is smaller than the index of the trie being expected

where $p$ is the probability of a collision under random choice of the LSH of the points at distance $dist(q,x_k^\prime)$.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-20T19:07:17.508+01:00 %%
