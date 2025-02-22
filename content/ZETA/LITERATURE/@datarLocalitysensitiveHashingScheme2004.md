---
connections:
  - "[[PARA/AREAS/CLANN/2. CLANN.md|2. CLANN]]"
reference: 
tags:
  - type/paper
  - theme/lsh
type: literature_note
created: 2024-12-20 19:14
modified: 
citekey: datarLocalitysensitiveHashingScheme2004
status: unread
dateread:
---

> [!Cite]
> [1] M. Datar, N. Immorlica, P. Indyk, e V. S. Mirrokni, «Locality-sensitive hashing scheme based on p-stable distributions», in _Proceedings of the twentieth annual symposium on Computational geometry_, in SCG ’04. New York, NY, USA: Association for Computing Machinery, giu. 2004, pp. 253–262. doi: [10.1145/997817.997857](https://doi.org/10.1145/997817.997857).


>[!Synthesis]
>**Contribution**:: 
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**:: 
>

>[!Metadata]
>> **FirstAuthor**:: Datar, Mayur  
> **Author**:: Immorlica, Nicole  
> **Author**:: Indyk, Piotr  
> **Author**:: Mirrokni, Vahab S.  
~    
> **Title**:: Locality-sensitive hashing scheme based on p-stable distributions  
> **Year**:: 2004   
> **Citekey**:: datarLocalitysensitiveHashingScheme2004  
> **itemType**:: conferencePaper  
> **Publisher**:: Association for Computing Machinery  
> **Location**:: New York, NY, USA   
> **Pages**:: 253–262  
> **DOI**:: 10.1145/997817.997857  
> **ISBN**:: 978-1-58113-885-6    

> [!LINK] 
> > [Datar et al. - 2004 - Locality-sensitive hashing scheme based on p-stabl.pdf](file:///Users/enricobolzonello/Zotero/storage/H2JJZ9IN/Datar%20et%20al.%20-%202004%20-%20Locality-sensitive%20hashing%20scheme%20based%20on%20p-stabl.pdf).


> [!Abstract]
>
> We present a novel Locality-Sensitive Hashing scheme for the Approximate Nearest Neighbor Problem under lp norm, based on p-stable distributions.Our scheme improves the running time of the earlier algorithm for the case of the lp norm. It also yields the first known provably efficient approximate NN algorithm for the case p&lt;1. We also show that the algorithm finds the exact near neigbhor in O(log n) time for data satisfying certain "bounded growth" condition.Unlike earlier schemes, our LSH scheme works directly on points in the Euclidean space without embeddings. Consequently, the resulting query time bound is free of large factors and is simple and easy to implement. Our experiments (on synthetic data sets) show that the our data structure is up to 40 times faster than kd-tree.
>.
> 

# Notes
## LSH alternative definition

A family $\mathcal{H}=\{h:S\rightarrow U\}$ is called $(r_1,r_2,p_1,p_2)$-sensitive for D (distance measure) if for any $v,q\in S$:

- if $v\in B(q,r_1)$ then $P_H[h(q)=h(v)]\ge p_1$
- if $v\not\in B(q,r_2)$ then $P_H[h(q)=h(v)]\le p_2$

uses the p-stable distribution (in particular the dot product $a\cdot v$ where $a$ is a random vector of dimension $d$ where each entry is chosen independently from a p-stable distribution) to assign the has value to each vector $v$

The dot product projects each vector to the real line. Then chop the real line into equi-width segments and assign hash values to vectors based on which segment they project to.

The expression is the following:

$$h_{a,b}(v) =\bigg\lfloor \frac{a\cdot v+b}{r}\bigg\rfloor
$$

where $r$ is a parameter that regulates the width of the buckets..


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-20T19:14:38.302+01:00 %%
