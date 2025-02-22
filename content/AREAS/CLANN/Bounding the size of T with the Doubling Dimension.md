---
area: CLANN
summary: 
tags: area/clann/bounding_the_size_of_t_with_the_doubling_dimension
type: area_note
created: 2025-01-07 10:11
---
# [[2. CLANN]] 
# Overview

On [[@ceccarelloSolving$k$centerClustering2021]] a technique to bound the size of the clusters using the [[Doubling Space|doubling dimension property]] is used. This is a rewrite and extension of the proof presented in the paper.

> [!THEOREM]
> If $S$ belongs to a metric space of doubling dimension $D$, then: 
> $$
> |T|\le l\cdot k\cdot \bigg(\frac{4}{\epsilon}\bigg)^D
> $$

## Basic Idea
- prove how many iterations are needed to reach the stopping condition of GMM
- since the algorithm adds one point at each iteration, we have therefore bounded the number of points
Formally, we have to find an upper bound on the number $\tau_i$ of iterations of GMM needed to obtain $r_{T_i^{\tau_i}}(S_i)\le (\epsilon/2)r_{T_i^k}(S_i)$

## Proof
For each subset $S_i$,the k-centers $T_k^i$ produce a clustering with radius $r_{T_i^k}(S_i)$. 
Using the [[Doubling Space#Iteratively Covering Smaller Balls|doubling dimension property]] , we have that each of the k clusters in $S_i$ can be covered with at most $(4/\epsilon)^D$ balls of radius $\le \epsilon/4 \cdot r_{T_k}^i(S_i)$. 
After running $h$ iterations of gmm, the algorithm guarantees that any two points in the set $T_i^h\cup \{x\}$ [^1] are at least $r_{T_i^h}(S_i)$ apart. This is because the greedy algorithm selects the farthest points each time.
Given there are only $h$ balls covering $S$, by the [[Pigeonhole Principle]] at least two points from $T_i^h\cup \{x\}$ must fall into the same ball.

The triangle inequality tells us that if two points are within the same ball, the distance between them is at most twice the radius of that ball. Since each ball has radius $\epsilon/4 \cdot r_{T_k^i}(S_i)$, the maximum distance between any two points within the same ball is:
$$
2\cdot \frac{\epsilon}{4}\cdot r_{T_k^i}(S_i)=\frac{\epsilon}{2}\cdot r_{T_k^i}(S_i)
$$
proving that with at most $h=k\cdot (4/\epsilon)^D$ we get to the termination criterion. So, since there are $l$ subsets and at each iteration the algorithm adds one point, we can say that:
$$
|T|\le l\cdot k\cdot \bigg(\frac{4}{\epsilon}\bigg)^D
$$
thus concluding the proof.

[^1]:: $x$ is the farthest point from any center in $T_i^h$