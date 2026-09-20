---
up:
  - "[[Clustering is the task of grouping a set of objects]]"
tags:
  - atomic
created: 2024-12-14 19:55
---

> Given a dataset S ⊆ X and an integer k ≥ 1, the (k, δ) nearest neighbor problem ((k, δ)-NN) is to build a data structure, such that for every query q ∈ X, the query algorithm returns a set of k distinct points, each one being with probability at least 1 − δ among the k points in S closest to q
>  — Aumüller, Martin, Tobias Christiani, Rasmus Pagh, e Michael Vesterli. «PUFFINN: Parameterless and Universally Fast Finding of Nearest Neighbors». arXiv, 28 giugno 2019. https://doi.org/10.48550/arXiv.1906.12211.

# See also
- [[Clustering is the task of grouping a set of objects]] — (k,δ)-NN and clustering are dual problems: clustering assigns points to groups, (k,δ)-NN finds the group a query point belongs to
- [[An LSH Family maps closer points to the same bucket with higher probability]] — LSH is the primary data structure used to solve (k,δ)-NN efficiently: the hash family maps nearby points to the same bucket with high probability, giving the 1−δ guarantee
- [[SimHash - h(x) = sign(wᵀx)]] — SimHash is an LSH family for cosine similarity; collision probability P = 1 − θ/π directly gives the probability term in the (k,δ)-NN guarantee
- [[Angular Distance is the true metric version of cosine distance]] — (k,δ)-NN requires a distance function; angular distance is the metric-compliant choice for cosine-based similarity search
- [[@beyerWhenNearestNeighbor1999]] — the curse of dimensionality paper: in high dimensions nearest neighbour loses meaning entirely; (k,δ)-NN is partly a response to this, relaxing exactness to make the problem tractable
# References
- [[@aumullerPUFFINNParameterlessUniversally2019]]