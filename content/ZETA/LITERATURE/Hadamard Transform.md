---
connections:
  - "[[Fast Hadamard Transform (FHT)]]"
reference: 
tags:
  - type/note
  - theme/mathematics
type: literature_note
created: 2025-01-03 11:57
---
 

> [!DEFINITION]
> The Hadamard transform $H_m$ is a $2^m \times 2^m$ matrix (Hadamard Matrix) that transforms $2^m$ real numbers $x_n$ into $2^m$ real numbers $X_k$

Or simply: $y=H_m x$ 

It involves no multiplies, but only adding and subtracting the components of $x$ since the matrix has only $\pm 1$.

# Hadamard Matrix
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

