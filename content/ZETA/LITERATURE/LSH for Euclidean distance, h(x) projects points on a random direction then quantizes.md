---
up:
  - "[[An LSH Family maps closer points to the same bucket with higher probability]]"
tags:
  - atomic
created: 2026-05-14 19:27
---

> [!DEFINITION]
> The LSH function for a point $\vec{x}\in \mathbb{R}^d$ is defined as:
> $$
h(x) = \Bigg\lfloor \frac{\vec{a}\cdot \vec{x}+b}{r}\Bigg\rfloor
> $$
> where $\vec{a}\in \mathbb{R}^d$ is a random vector with coordinates sampled from the normal distribution, $b$ is a random scalar distributed uniformly in $[0,r]$ and $r$ is a parameter

This function projects input points on a random direction, shifts them and then quantizes the shifted projections according to the parameter $r$.

# See also 
- [[An LSH Family maps closer points to the same bucket with higher probability]] — this is the concrete instantiation of the abstract definition for Euclidean distance 
- [[SimHash - h(x) = sign(wᵀx)]] — SimHash is the angular distance analogue: instead of projecting and quantising, it takes the sign of the projection; both are random projection methods 
- [[The Hadamard Transform y = Hₘx Transforms 2ᵐ Numbers Using Only Additions and Subtractions]] — the random projection $\vec{a}\cdot\vec{x}$ can be approximated with the Hadamard transform for efficiency, same technique used in Cross-Polytope LSH 
# References 
- [[@datarLocalitysensitiveHashingScheme2004]]