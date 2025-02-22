---
connections: 
reference: 
tags:
  - type/paper
  - theme/lsh
type: literature_note
created: 2024-12-20 19:02
modified: 
citekey: andoniPracticalOptimalLSH2015a
status: read
dateread: 2024-10-20
---

> [!Cite]
> [1] A. Andoni, P. Indyk, T. Laarhoven, I. Razenshteyn, e L. Schmidt, «Practical and optimal LSH for angular distance», in _Proceedings of the 28th International Conference on Neural Information Processing Systems - Volume 1_, in NIPS’15. Cambridge, MA, USA: MIT Press, dic. 2015, pp. 1225–1233.


>[!Synthesis]
>**Contribution**:: 
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**::  [[@aumullerPUFFINNParameterlessUniversally2019]] 
>

>[!Metadata]
>> **FirstAuthor**:: Andoni, Alexandr  
> **Author**:: Indyk, Piotr  
> **Author**:: Laarhoven, Thijs  
> **Author**:: Razenshteyn, Ilya  
> **Author**:: Schmidt, Ludwig  
~    
> **Title**:: Practical and optimal LSH for angular distance  
> **Year**:: 2015   
> **Citekey**:: andoniPracticalOptimalLSH2015a  
> **itemType**:: conferencePaper  
> **Publisher**:: MIT Press  
> **Location**:: Cambridge, MA, USA   
> **Pages**:: 1225–1233    

> [!LINK] 
> > [Andoni et al. - 2015 - Practical and optimal LSH for angular distance.pdf](file:///Users/enricobolzonello/Zotero/storage/VYLCI82W/Andoni%20et%20al.%20-%202015%20-%20Practical%20and%20optimal%20LSH%20for%20angular%20distance.pdf).


> [!Abstract]
>
> We show the existence of a Locality-Sensitive Hashing (LSH) family for the [[Angular Distance|angular distance]] that yields an approximate Near Neighbor Search algorithm with the asymptotically optimal running time exponent. Unlike earlier algorithms with this property (e.g., Spherical LSH [1, 2]), our algorithm is also practical, improving upon the well-studied hyperplane LSH [3] in practice. We also introduce a multiprobe version of this algorithm and conduct an experimental evaluation on real and synthetic data sets.We complement the above positive results with a fine-grained lower bound for the quality of any LSH family for angular distance. Our lower bound implies that the above LSH family exhibits a trade-off between evaluation time and quality that is close to optimal for a natural class of LSH functions.
>.
> 

# Notes
# Bound for collision probability

Suppose that $p,q \in S^{d-1}$ are such that $||p-q||=\tau$, where $0<\tau<2$. Then

$$\ln \frac{1}{P_{h\sim \mathcal{H}}[h(p)=h(q)]} = \frac{\tau^2}{4-\tau^2}\cdot \ln d + O_\tau(\ln \ln d)$$

The implication is that the cross-polytope LSH achieves the same bounds as the theoretically optimal LSH for the sphere

# Cross-polytope LSH definition

the hash family is defined on a unit sphere $S^{d-1}\subset\mathbb{R}^d$

Let $A\in \mathbb{R}^{d\times d}$ be a random matrix with i.i.d Gaussian entries. The function to hash a point $x\in S^{d-1}$ is the following.

Compute:

$$y = \frac{Ax}{||Ax||}$$

and find the point closest to $y$ from $\{\pm e_i\}_1\le i\le d\}$_,_ where $e_i$ is the i-th standard basis vector of $\mathbb{R}^d$..


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-20T19:02:03.126+01:00 %%
