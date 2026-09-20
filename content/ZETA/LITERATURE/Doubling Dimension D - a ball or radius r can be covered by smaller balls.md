---
up:
  - "[[Clustering is the task of grouping a set of objects]]"
tags:
  - literature
created: 2024-12-20 21:18
---
 > [!Definition]
> Smallest D such that for any radius r and point $u\in S$, all points in the ball of radius r centered at u are included in the union of at most $2^D$ balls of radius $r/2$ centered at suitable points
>  — [[@ceccarelloSolving$k$centerClustering2021]]


In computational geometry, doubling measures allow algorithms that were originally designed for Euclidean settings to be generalized and applied effectively in more abstract spaces.
For example, in the HNSW method for the [[(k, δ) Nearest Neighbor problem|k-NN problem]] the doubling property ensures that the graph does not become too dense, which helps in bounding the search time.

For clustering and k-NN this property ensures that the metric space behaves in a controlled way, specifically:
1) **bounding the number of neighbors**, since in a space with a doubling measure they are limited
2) **efficient partitioning**, doubling spaces can be often efficiently partitioned or embedded into lower-dimensional spaces with bounded distortion
3) **scalability**, ensures that computational resources grow in a controlled manner

# See also 
- [[Coreset is a small subset from P which represent P well]] — the doubling dimension determines how small a coreset can be: small D means very space-efficient coresets 
- [[Clustering is the task of grouping a set of objects]] — k-center clustering becomes very efficient when D is small; the doubling dimension is the parameter that captures "how hard" a clustering instance actually is 
- [[@beyerWhenNearestNeighbor1999]] — the curse of dimensionality is the high-D extreme: when D is large, nearest neighbour loses meaning because all distances converge 
# References 
- [[@ceccarelloSolving$k$centerClustering2021]]