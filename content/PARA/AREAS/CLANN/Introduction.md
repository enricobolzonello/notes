---
area: CLANN
tags: area/clann/untitled_1
type: area_note_sub
created: 2025-01-24 21:30
---
# [[2. CLANN]] 
# Overview

Nearest Neighbor Search (NNS) is an important building block of many applications in the most diverse applications. While it is perhaps most commonly associated with information retrieval, where it has been extensively used and developed by tech giants like Google, Microsoft or Meta (formerly Facebook), its relevance extends beyond this domain. It has also been used in pattern recognition, data mining, machine learning, geographic information systems (GIS) and recommendation systems to name a few. More recently, vector databases are at the basis of augmenting the knowledge of LLMs beyond their training data with a technique Retrieval-Augmented Generation (RAG) which has amplified the importance of NNS, as efficient and accurate similarity searches are at the core of retrieving relevant information. 

At its core, NNS relies on vector similarity measures, which allow systems to identify data points that are closest to a given query in a $d$-dimensional vector space. The ability to perform it effectively depends on the ability to embed data into a vector space, a process in which raw data is transformed into numerical representations that preserve its features and semantics. Essentially, any type of data, no matter the representation, can be searched, providing a good embedder.

Many efficient solutions exist for the nearest neighbor problem when the points lie in a space of constant dimension. For instance, in a two-dimensional plane, the problem can be solved in $O(\log n)$ time per query using only $O(n)$ storage[^1]. This efficiency is achieved by leveraging specialized data structures, such as Voronoi diagrams or kd-trees, which exploit the geometric properties of low-dimensional spaces.

However, as the dimensionality of the space increases, these algorithms face significant challenges. This phenomenon, known as the curse of dimensionality, refers to the exponential growth of computational and storage requirements with respect to the dimension of the space. Theoretical analyses and practical experiments both demonstrate that the time complexity, storage demands, and query performance of these algorithms degrade rapidly as the dimension grows. The lack of success in removing the exponential dependence led many researchers to conjecture that there is no efficient solution when the dimension is large enough, thus the focus shifted to relax accuracy constraints to improve dramatically efficiency through the approximate NNS (ANNS) \cite{towards removing the curse of dimensionality}. The $\epsilon$-NNS problem is defined as follows: given a set of points $P$ in a metric space and a query point $q$, find a point $p \in P$ that is an $\epsilon$-approximate nearest neighbor of $q$. This means that for all points $p^\prime \in P$, the distance between $p$ and $q$ satisfies the inequality:
$$
d(p,q) \le (1+\epsilon)\cdot d(p^\prime,q)
$$
This formulation has enabled significant advancements in computational efficiency, making it feasible to scale nearest neighbor search algorithms to datasets containing billions of points or more \cite{BigANNBenchmarks}, which is critical in enterprise-grade applications.


[^1]: @INPROCEEDINGS{4567872,
  author={Shamos, Michael Ian and Hoey, Dan},
  booktitle={16th Annual Symposium on Foundations of Computer Science (sfcs 1975)}, 
  title={Closest-point problems}, 
  year={1975},
  volume={},
  number={},
  pages={151-162},
  keywords={Tree graphs;Computer science;Computational geometry;Upper bound;Clustering algorithms;Manufacturing;Wire;Algorithm design and analysis;Design optimization;Linear programming},
  doi={10.1109/SFCS.1975.8}}