---
connections:
  - "[[PARA/AREAS/CLANN/2. CLANN.md|2. CLANN]]"
reference: 
tags:
  - type/paper
  - theme/clustering
type: literature_note
created: 2024-12-20 19:09
modified: 
citekey: ceccarelloSolving$k$centerClustering2021
status: read
dateread: 2024-10-08
---

> [!Cite]
> [1] M. Ceccarello, A. Pietracaprina, e G. Pucci, «Solving $k$-center Clustering (with Outliers) in MapReduce and Streaming, almost as Accurately as Sequentially», 1 giugno 2021, _arXiv_: arXiv:1802.09205. doi: [10.48550/arXiv.1802.09205](https://doi.org/10.48550/arXiv.1802.09205).


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
>> **FirstAuthor**:: Ceccarello, Matteo  
> **Author**:: Pietracaprina, Andrea  
> **Author**:: Pucci, Geppino  
~    
> **Title**:: Solving $k$-center Clustering (with Outliers) in MapReduce and Streaming, almost as Accurately as Sequentially  
> **Year**:: 2021   
> **Citekey**:: ceccarelloSolving$k$centerClustering2021  
> **itemType**:: preprint  
> **DOI**:: 10.48550/arXiv.1802.09205    

> [!LINK] 
> > [arXiv Fulltext PDF](file:///Users/enricobolzonello/Zotero/storage/TVWH237F/Ceccarello%20et%20al.%20-%202021%20-%20Solving%20$k$-center%20Clustering%20(with%20Outliers)%20in%20M.pdf).


> [!Abstract]
>
> Center-based [[Clustering|clustering]] is a fundamental primitive for data analysis and becomes very challenging for large datasets. In this paper, we focus on the popular $k$-center variant which, given a set $S$ of points from some metric space and a parameter $k<|S|$, requires to identify a subset of $k$ centers in $S$ minimizing the maximum distance of any point of $S$ from its closest center. A more general formulation, introduced to deal with noisy datasets, features a further parameter $z$ and allows up to $z$ points of $S$ (outliers) to be disregarded when computing the maximum distance from the centers. We present coreset-based 2-round MapReduce algorithms for the above two formulations of the problem, and a 1-pass Streaming algorithm for the case with outliers. For any fixed $\epsilon>0$, the algorithms yield solutions whose approximation ratios are a mere additive term $\epsilon$ away from those achievable by the best known polynomial-time sequential algorithms, a result that substantially improves upon the state of the art. Our algorithms are rather simple and adapt to the intrinsic complexity of the dataset, captured by the doubling dimension $D$ of the metric space. Specifically, our analysis shows that the algorithms become very space-efficient for the important case of small (constant) $D$. These theoretical results are complemented with a set of experiments on real-world and synthetic datasets of up to over a billion points, which show that our algorithms yield better quality solutions over the state of the art while featuring excellent scalability, and that they also lend themselves to sequential implementations much faster than existing ones.
>.
> 

# Notes
# (Composable) Coreset

a coreset is a small subset extracted from the input which has a solution with cost close to the optimal solution of the whole set

_composable_ -> if coresets are from distinct subsets their union has a close-to-optimal solution

# Core Idea

based on the GMM sequential approx. alg. for k-center

> **GMM**  
> first phase: find k centers in each subset  
> second phase: compute the solution on the coreset formed by the union of the centers

-> contribution: select more centers from each subset in the first phase

## Doubling dimension

> The doubling dimension of $\mathcal{S}$ is the smallest D such that for any radius $r$ and point $u\in S$, all points in the ball of radius $r$ centered at $u$ are included in the union of at most $2^D$ balls of radius $r/2$ centered at suitable points

-> it follows that a ball of radius $r$ can be covered by at most $(1/\epsilon)^D$ balls of radius $\epsilon r$

# GMM algorithm

sequential 2-appoximation

How it works:

> select an arbitrary point as the center and add it to T. Iteratively, select the next center and add it to T, until T contains k centers

## Property

Let $X\subseteq S$. For a given k, let $T_X$ be the outputof GMM when run on X. We have that:

$$r_{T_X}(X)\le 2\cdot r_k^*(S)$$

(GMM is a 2-approximation algorithm)

# k-center problem

Given a set S of points in the metric space and a positive integer $k<|S|$, find a subset $T\subseteq S$ of k points (centers) so that the maximum distance between any point of S to its closest center in T is minimized.

-> outliers can influence a lot the final solution, but there exists a formulation to account for outliers.

# MapReduce algorithm for k-center

First round:

- partition S in $l$ subsets of equal size
- on each subset, run GMM incrementally until $r_{T_i^{\tau_i}}(S_i) \le \epsilon/2 \cdot r_{T_i^{k}}(S_i)$ where:
    
    - $T_i^j$ is the set of i centers selected in the first j iterations
    - $r_{T_i^k}(S_i)$ is the radius of the set $S_i$ with respect to the first k centers

-> the coreset will be $T_i=T_i^{\tau_i}$

Second round:

- make the union of the coresets and run GMM to compute the final set of k centers

# Variant with z outliers

in the first round, we define for each point s its proxy as before, but we add to each $t\in T_i$ a weight $w_t\ge 1$ (number of points of $S_i$ with proxy t)

in the second round, instead of using GMM we use an algorithm called OutliersCluster to solve a weighted variant of k-center with outliers..


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-20T19:09:34.434+01:00 %%
