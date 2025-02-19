---
area: CLANN
tags:
  - area/clann
type: area_note_sub
created: 2025-01-23 16:23
---
# [[2. CLANN]] 
# Algorithm
As briefly discussed in Section {}, although LSH implementations like PUFFINN provide quality guarantees in expectation on the result of every single query, other approaches like HNSW outperform them, especially in industry scenarios where runtime performance is usually more critical than theoretical guaranteed accuracy. This performance gap can be attributed to two key behaviours of LSH:
1) Although the probability of collision for distant points is small, it is not zero. As a result, LSH implementations often produce many collisions for nearby points, but also a long tail of few far-away points colliding can be seen. An example of this behaviour can be found in Image \ref{}. This results in unnecessary computations in the final phase, as points that are clearly too far apart are still being processed.
2) The second issue arises with queries far away from the dataset. In such cases, the LSH functions tend to produce random collisions, as all points are equally distant and the sensitivity of the hash function diminishes. This behaviour undermines the purpose of LSH, which is to reduce the search space by focusing on likely candidates. Instead, it introduces additional overhead by requiring the processing of points that are irrelevant to the query. In some cases, this randomness can make the performance of LSH worse than a brute force approach.
The proposed algorithm addresses these problems by prioritizing a more expensive index-building phase, which involves explicitly clustering the dataset beforehand.


## Index Building
The first step is to cluster the dataset. Given a dataset $S\subseteq \mathbb{R}^d$ and a parameter $M$, run the GMM algorithm described in Section \ref{sec:clustering} to find $M$ centers and assign each point to its closest center. Then in each cluster $R_i, 1\le i\le M$ a PUFFINN index is built with memory:
$$
\text{mem}_{i} = k \cdot |R_i| 
$$
where $k$ is the parameter representing how many kilobytes we assign to each point. This proportional allocation ensures that larger clusters, which contain more points, are assigned more memory and the PUFFINN search algorithm can perform additional repetitions, increasing the likelihood of finding accurate results. The full pseucode can be found in Algorithm \ref{alg:index-building}.

## Query Algorithm
The main idea of the query algorithm is to independently find the best candidates in each cluster and combining them until we are sure there aren't any more possible candidates. The primary goal is to identify the best candidate neighbours by examining only a subset of clusters, minimizing unnecessary computations and early termination of the search when further exploration would not yield better results.

The query algorithm is described in Algorithm \ref{}. First we compute the distances from the query to all centers and sort the clusters in ascending order, preparing them for the scan. While searching we use a data structure PQ to keep track of the top-$k$ closest points seen so far. At each step of the algorithm, the PUFFINN query algorithm (described in **Section \ref{sec:puffinn_query}**) is invoked to identify potential nearest neighbor candidates within the currently considered cluster, and they are inserted into PQ if it is appropriate. To prevent redundant computations and unnecessary exploration, the algorithm evaluates a stopping condition: if the distance to the farthest point in PQ (denoted as $x_k^\prime$​) is smaller than the minimum possible distance to any point in the unexplored clusters, the search terminates early.

This stopping condition is based on the observation that clusters are sorted by proximity to $q$, and further clusters are less likely to contain points closer than those already identified. 