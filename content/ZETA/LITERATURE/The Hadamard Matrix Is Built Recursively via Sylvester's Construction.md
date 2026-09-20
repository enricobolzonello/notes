---
up:
  - "[[The Hadamard Transform y = Hₘx Transforms 2ᵐ Numbers Using Only Additions and Subtractions]]"
tags:
  - atomic
created: 2025-01-03 11:57
---
> Square matrix whose entries are either +1 or -1 and whose rows are mutually orthogonal.

This means that each pair of rows represents two perpendicular vectors. The easier construction comes from the square Sylvester construction. Starting from the fundamental matrix $H_1$:
$$
H_1 = [1]
$$
The partitioned matrix is, if $H$ is a Hadamard matrix of order $n$ is:
$$
\begin{bmatrix}
H & H \\
H & -H\\
\end{bmatrix}
$$
So, for $H_2$:
$$
H_2 = \begin{bmatrix}
1 & 1\\
1 & -1
\end{bmatrix}
$$
To generate each successively higher-order matrix, repeat the substitution with the previous order matrix. The general rule boils down to this formula:
$$
H_{2^k} = \begin{bmatrix}
H_{2^{k-1}} & H_{2^{k-1}}\\
H_{2^{k-1}} & -H_{2^{k-1}}
\end{bmatrix} = H_2\otimes H_{2^{k-1}}
$$
where $\otimes$ is the Kronecker product.

# See also 
- [[The Hadamard Transform y = Hₘx Transforms 2ᵐ Numbers Using Only Additions and Subtractions]] — the matrix is what defines the transform; the recursive structure is why the Fast Hadamard Transform achieves O(n log n) 
- [[Linear Recursion is a chain of deferred operations]] — Sylvester's construction is a recursive process: $H_{2^k}$ is defined entirely in terms of $H_{2^{k-1}}$, with base case $H_1 = [1]$ 
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — the Kronecker product $H_2 \otimes H_{2^{k-1}}$ is function composition at the matrix level: the transform of order $k$ is the composition of the order-2 transform with the order $k-1$ transform 
- [[Cosine Similarity is the cosine of the angle between two vectors]] — mutual orthogonality of rows means each pair has cosine similarity 0; the Hadamard matrix is a basis of maximally uncorrelated directions 
# References 
- [[@andoniPracticalOptimalLSH2015a]]