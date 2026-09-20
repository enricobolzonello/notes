---
up:
tags:
  - atomic
created: 2024-12-20 19:29
---

> [!DEFINITION]
> Clustering is the task of grouping a set of objects such that similar objects end up in the same group and dissimilar objects are separated into different groups.

# See also
- [[Coreset is a small subset from P which represent P well]] — coresets make clustering tractable on large inputs: instead of clustering all of P, extract a small T that preserves the clustering structure within (1±ε)
- [[Composable Coreset partitions P, the union of the coresets of P is still a coreset]] — the parallel version: partition P into shards, extract a coreset per shard, union them and cluster the union
- [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] — the geometric property that makes clustering algorithms efficient in abstract metric spaces: bounds the number of neighbours and enables efficient partitioning
- [[Cosine Similarity is the cosine of the angle between two vectors]] — one of the core similarity measures used in clustering; the choice of sim(A,B) defines which objects are "similar" and therefore which cluster they belong to
- [[Angular Distance is the true metric version of cosine distance]] — clustering algorithms that require a true metric (e.g. k-center) need angular distance rather than cosine distance for correctness guarantees