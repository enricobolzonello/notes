---
up:
tags:
  - atomic
created: 2025-01-03 11:57
---

> [!DEFINITION]
> The Hadamard transform $H_m$ is a $2^m \times 2^m$ matrix (Hadamard Matrix) that transforms $2^m$ real numbers $x_n$ into $2^m$ real numbers $X_k$

Or simply: $y=H_m x$ 

It involves no multiplies, but only adding and subtracting the components of $x$ since the matrix has only $\pm 1$.

# See also 
- [[Fast Hadamard Transform (FHT)]] — the efficient algorithm to compute this transform in $O(n \log n)$ rather than $O(n^2)$, analogous to FFT 
- [[SIMD - one operation applied to multiple data points simulaneously]] — the addition-only nature of the transform makes it ideal for SIMD: a single instruction can process multiple $\pm 1$ operations simultaneously 
- [[Swiss Table Breaks the Hash Array Into Groups of 8 — Each With a 64-bit Control Word for Metadata]] — same principle: exploit the structure of the operation (±1 / metadata bytes) to parallelise with SIMD 
# References 
- [[@andoniPracticalOptimalLSH2015a]]

