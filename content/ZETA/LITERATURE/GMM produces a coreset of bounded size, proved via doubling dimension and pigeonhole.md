---
up:
  - "[[Composable Coreset partitions P, the union of the coresets of P is still a coreset]]"
tags:
  - atomic
created: 2025-01-07 10:11
---

On [[@ceccarelloSolving$k$centerClustering2021]] a technique to bound the size of the clusters using the [[Doubling Dimension D - a ball or radius r can be covered by smaller balls|doubling dimension property]] is used. This is a rewrite and extension of the proof presented in the paper.

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
Using the [[Doubling Dimension D - a ball or radius r can be covered by smaller balls#Iteratively Covering Smaller Balls|doubling dimension property]] , we have that each of the k clusters in $S_i$ can be covered with at most $(4/\epsilon)^D$ balls of radius $\le \epsilon/4 \cdot r_{T_k}^i(S_i)$. 
After running $h$ iterations of gmm, the algorithm guarantees that any two points in the set $T_i^h\cup \{x\}$ [^1] are at least $r_{T_i^h}(S_i)$ apart. This is because the greedy algorithm selects the farthest points each time.
Given there are only $h$ balls covering $S$, by the [[Pigeonhole Principle - if n items fill m containers and n>m, some container has more than one]] at least two points from $T_i^h\cup \{x\}$ must fall into the same ball.

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

# See also
- [[Composable Coreset partitions P, the union of the coresets of P is still a coreset]] — this theorem bounds the size of the coreset that GMM produces per shard; composability guarantees the union is still valid
- [[A ball can be covered by N balls of radius epsilon*r]] — the iterative covering is the key step in the proof: each of the k clusters is covered by (4/ε)^D balls, giving the total bound
- [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] — the doubling dimension D is the parameter that controls how tight the bound is; small D means small coreset
- [[Pigeonhole Principle - if n items fill m containers and n>m, some container has more than one]] — the argument that terminates the proof: with more GMM iterations than balls covering S, two selected points must fall in the same ball, bounding the distance between them
- [[Coreset is a small subset from P which represent P well]] — the theorem is what gives the coreset its size guarantee: not just that a coreset exists, but that GMM finds one of bounded size

# References
- [[@ceccarelloSolving$k$centerClustering2021]]