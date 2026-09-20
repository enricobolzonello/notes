---
up:
  - "[[Cosine Similarity is the cosine of the angle between two vectors]]"
tags:
  - theme/lsh
type: literature_note
created: 2025-02-03 10:28
---

Hashing function for [[Cosine Similarity is the cosine of the angle between two vectors]]
> [!DEFINITION]
> $$
> h_w^{sim}(x) = sign(w^Tx)
> $$

The probability of collision satisfy the following equation:
$$
P(h_w^{sim}(x)=h_w^{sim}(y)) = 1-\frac{\theta}{\pi}
$$
where $\theta=\arccos(sim_{cos})$.

# See also
- [[Cosine Similarity is the cosine of the angle between two vectors]] — SimHash's collision probability $P = 1 - \theta/\pi$ is a direct function of cosine similarity: $\theta = \arccos(\text{sim}_{cos})$
- [[Angular Distance is the true metric version of cosine distance]] — SimHash collision probability is $1 - \text{angular distance}$; the two are mathematically the same quantity expressed differently
- [[A Hash Function Must Be Deterministic, Uniform, and Fast — FNV-1a Is One Example]] — SimHash is a hash function with a different design goal: instead of uniform distribution, it preserves similarity structure; the two represent opposite ends of the hash function design space
- [[Swiss Table Breaks the Hash Array Into Groups of 8 — Each With a 64-bit Control Word for Metadata]] — Swiss Tables use hashing for O(1) lookup; SimHash uses hashing for approximate similarity search; both exploit the hash function's structure but for entirely different purposes
- [[@andoniPracticalOptimalLSH2015a]] — the Cross-Polytope LSH paper improves on SimHash (hyperplane LSH) for angular distance, achieving asymptotically optimal running time while remaining practical
- [[@datarLocalitysensitiveHashingScheme2004]] — the LSH framework that formalises what SimHash achieves: a $(r_1, r_2, p_1, p_2)$-sensitive family for a distance measure