---
type: new_note
tags:
  - new_note
created: 2025-01-04 09:50
---
Efficient approximate nearest neighbour (ANN) search is a cornerstone of modern machine learning, data retrieval, and high-dimensional data analysis. Among the many methods to solve the problem, approaches based on locality-sensitive hashing (LSH) functions are among the most studied and widely used in academic contexts, owing to their inherent nature of providing formal probabilistic guarantees for the quality of the solution. But traditional LSH methods, while effective, often suffer from suboptimal performance due to hash collisions between distant points and struggles with query points that lie far from the dataset points. This thesis addresses these limitations by proposing a novel algorithm, which we call CLANN, that integrates k-center clustering with PUFFINN, an optimized LSH implementation. 

By first partitioning data into clusters using k-center clustering and then applying PUFFINN indexing within each cluster, CLANN aims to achieve improved query performance while preserving LSH's probabilistic guarantees. The central theoretical contribution is a framework for adaptively partitioning the data space to reduce unnecessary hash computations while maintaining formal guarantees of accuracy and efficiency. This work will analyze the theoretical bounds of the proposed method and evaluate its performance against existing approaches across various high-dimensional datasets.