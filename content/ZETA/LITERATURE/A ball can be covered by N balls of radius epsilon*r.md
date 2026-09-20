---
up:
  - "[[Clustering is the task of grouping a set of objects]]"
tags:
  - literature
created: 2024-12-20 21:18
---
> Given the [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] definition, we can apply it iteratively to break down ball of radius $r$ into smaller and smaller balls

Recursively cover each ball of radius $r$ with $2^D$ balls of half the radius $r/2$, then each of those with $2^D$ balls of radius $r/4$ and so on. After $k$ subdivisions, **the radius of each ball becomes $r/2^k$ and the number of balls needed is $(2^D)^k$.**

In terms of $\epsilon$, we want to cover a ball of radius $r$ with smaller balls of radius $\epsilon r$, with $\epsilon\le 1$. Set $\epsilon=1/2^k$ so that $\epsilon r = r/2^k$. Solving for $k$, we get $k=\log_2(1/\epsilon)$.

Substituting $k=\log_2(1/\epsilon)$ on the number of balls we get:
$$
2^{kD} = 2^{D\log_2(1/\epsilon)} = \bigg(\frac{1}{\epsilon}\bigg)^D
$$

**Takeaway**: a ball of radius $r$ can always be covered by at most $(1/\epsilon)^D$ balls of radius $\epsilon r$.

# See also 
- [[Doubling Dimension D - a ball or radius r can be covered by smaller balls]] — the definition this construction is built on; iterative covering is the proof technique that extracts the $(1/\epsilon)^D$ bound 
- [[Coreset is a small subset from P which represent P well]] — the $(1/\epsilon)^D$ bound directly controls coreset size: the number of centers selected per shard in the MapReduce algorithm is bounded by this quantity 
- [[Linear Recursion is a chain of deferred operations]] — iterative halving is a recursive process: the covering of radius $r$ is defined in terms of the covering of radius $r/2$, with depth $\log_2(1/\epsilon)$ 
# References 
- [[@ceccarelloSolving$k$centerClustering2021]]
























