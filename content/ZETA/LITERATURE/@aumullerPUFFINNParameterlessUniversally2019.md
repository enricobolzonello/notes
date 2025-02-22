---
connections:
  - "[[PARA/AREAS/CLANN/2. CLANN.md|2. CLANN]]"
reference: 
tags:
  - type/paper
  - theme/approximate-nearest-neighbor
type:
  - literature_note
created: 2024-12-18 10:14
modified: 
citekey: aumullerPUFFINNParameterlessUniversally2019
status: read
dateread: 2024-10-03
---

> [!Cite]
> [1] M. Aumüller, T. Christiani, R. Pagh, e M. Vesterli, «PUFFINN: Parameterless and Universally Fast FInding of Nearest Neighbors», 28 giugno 2019, _arXiv_: arXiv:1906.12211. doi: [10.48550/arXiv.1906.12211](https://doi.org/10.48550/arXiv.1906.12211)


>[!Synthesis]
>**Contribution**:: 
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**::  [[@aumullerRecentApproachesTrends2023]],   [[@charikarSimilarityEstimationTechniques2002]],   [[@andoniPracticalOptimalLSH2015a]] 
>

>[!Metadata]
>> **FirstAuthor**:: Aumüller, Martin  
> **Author**:: Christiani, Tobias  
> **Author**:: Pagh, Rasmus  
> **Author**:: Vesterli, Michael  
~    
> **Title**:: PUFFINN: Parameterless and Universally Fast FInding of Nearest Neighbors  
> **Year**:: 2019   
> **Citekey**:: aumullerPUFFINNParameterlessUniversally2019  
> **itemType**:: preprint  
> **DOI**:: 10.48550/arXiv.1906.12211    

> [!LINK] 
> > [arXiv Fulltext PDF](file:///Users/enricobolzonello/Zotero/storage/9I4MIQ97/Aumüller%20et%20al.%20-%202019%20-%20PUFFINN%20Parameterless%20and%20Universally%20Fast%20FIndin.pdf).


> [!Abstract]
>
> We present PUFFINN, a parameterless LSH-based index for solving the $k$-nearest neighbor problem with probabilistic guarantees. By parameterless we mean that the user is only required to specify the amount of memory the index is supposed to use and the result quality that should be achieved. The index combines several heuristic ideas known in the literature. By small adaptions to the query algorithm, we make heuristics rigorous. We perform experiments on real-world and synthetic inputs to evaluate implementation choices and show that the implementation satisfies the quality guarantees while being competitive with other state-of-the-art approaches to nearest neighbor search. We describe a novel synthetic data set that is difficult to solve for almost all existing nearest neighbor search approaches, and for which PUFFINN significantly outperform previous methods.
>.
> 

# Notes
# Faster distance computations with sketching

produce 1 bit sketches for efficient similarity _estimation_. (keyword is estimation, not actual computation)

IDEA (to find more concrete on other papers):

- use a random hash function to hash the output of an LSH function to a single bit
- pack $w=\Theta(\log n)$ bits into a w-bit machine word
- use word parallelism or table lookups to count the number of collisions between w sketches

### Why hash to a single bit?

indicates that two items are mapped to the same bucket, meaning it is probable that they are similar

Also it is really efficient

**What is a machine word?**

Hardware word, meaning 32 or 64 bit. This allows word parallelism with bitwise operations.

**Why is it fast?**

Allows to compute multiple similarities in one go, leveraging word parallelism and bitwise operations.

# Index Data Structure

-> trie built on the hash codes of the data points

variant of the LSH Forest

constructed by recursively splitting the set of points S on the next character until $|S|\le i$ or $i=K+1$. At that point, we have a leaf that stores references to points in $S$

# k-NN definition

> Given a dataset $S\subseteq X$ and an integer $k\ge 1$, the $(k,\delta)$ nearest neighbor problem is to build a data structure, such that for every query $q\in X$, the query algorithm returns a set of k distinct points, each one being with probability at least $1-\delta$ among the k points in S closest to q

-> guarantees an expected recall of $(1-\delta)\cdot k$

# Locality-sensitive hashing framework

> A LSH family $\mathcal{H}$ is a family of functions $h:X\rightarrow R$, such that for each pair $x,y\in X$ and a random $h\in \mathcal{H}$, for arbitrary $q\in X$, whenever $dist(q,x)\le dist(q,y)$ we have:
> 
> $$p(q,x)=P[h(q)=h(x)]\ge P[h(q)=h(y)]$$

-> an lsh function maps a datapoint to a hash code with the condition that closer points are more likely to collide.

concatenate $K\ge 1$ lsh functions to make it less probable that close points and far away points collide.

K is a function of the number of points of the dataset, the approximation factor c and the strength of the hash family.

-> from K and the hash family the guarantee of finding a close point with constant probability can be computed -> other methods does not have this theoretical guarantee!

# Query Algorithm

define:

$$S_{i,j}(q) = \{ x\in S | h_{1,j}(q) = h_{1,j}(x)\wedge ... \wedge h_{i,j}(q)=h_{i,j}(x)$$

as the subset of points in S that collide with q when we consider the first i hash values of the jth trie.

The algorithm is as follows:

Start with the bucket $S_{i,j}(q)$ at depth $i=K$ and explore all $L$ tries. Once done that, you can move to the next level. Track the top-k closest points with a data structure PQ.

Stop the search once we have explored enough tries where our candidate would have been found with probability $1-\delta$.

Lemma 3 states that the algorithm cannot terminate until j tries have been searched at level i where either:

- $j \ge \frac{\ln(1/\delta)}{p(q,x_k)^i}$, with this the probability of **not** finding a kNN is at most $(1-p(q,x_k)^i)^j \le \delta$
- or $i=0$.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-18T10:14:55.995+01:00 %%
