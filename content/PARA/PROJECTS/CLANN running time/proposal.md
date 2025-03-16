---
Priority_Level: 
Status: 
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/clann_running_time"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
---
define:
- ${x_k^\prime}^{(t)}$ as the farthest point in PQ at iteration $t$
- $R^{(t)}=\text{dist}(q,{x_k^\prime}^{(t)}) +r_{i}\le \text{dist}(q,{x_k^\prime}^{(t)}) +r_{max}$  
At $t=0$, PQ is empty so ${x_k^\prime}^{(0)}=\infty$ and $R^{(0)} =\infty$. In the next iterations ${x_k^\prime}^{(t)}$ decreases incrementally until it converges to the true k nearest neighbor distance $\rho$, so:
$$
R^{final} \le \rho + r_{max}
$$
> # Doubling space: Iteratively Covering Smaller Balls
> Recursively cover each ball of radius $r$ with $2^D$ balls of half the radius $r/2$, then each of those with $2^D$ balls of radius $r/4$ and so on. After $k$ subdivisions, **the radius of each ball becomes $r/2^k$ and the number of balls needed is $(2^D)^k$.

given this, we decompose $R$ [^1] iteratively. At each scale $R/2^i$ the number of clusters is $O(2^{iD})$. Summing over until $R/2^i\ge \rho$:
$$
\begin{align*}
M &= 
\sum_{i=0}^{\log_2(R/\rho)} 2^{iD}\\
&= \frac{2^D(R/\rho)^D-1}{2^D-1} \\
&= O\bigg(\frac{2^D(R/\rho)^D}{2^D}\bigg)\\
&= O\bigg(\Big(\frac{R}{\rho}\Big)^D\bigg)
\end{align*}
$$

Now consider the aspect ration $\Delta = \frac{\text{max distance}}{\text{min distance}}$. In the worst case scenario, if the $k$-th nearest neighbor $x_k^\prime$​ is located at the minimum distance $\rho = \text{min\_distance}$, and the dataset contains points at the maximum distance $\Delta \cdot \text{min\_distnace}$, then:
$$
R=\rho + \Delta\cdot \rho = \rho (1+\Delta) = O(\Delta \cdot \rho)
$$
So substituting in $M$:
$$
M = O\bigg(\Big(\frac{R}{\rho}\Big)^D\bigg) = O\bigg(\Big( \frac{\Delta \cdot \rho}{\rho}\Big)^D\bigg)=O(\Delta^D)
$$

Final running time:
- $O(\Delta^D \cdot (T_{puffinn}+k\log k))$ for the main loop, where $k\log k$ is the insertion time in the priority queue
- $+O(|C|\log|C|)$  for the sorting



[^1]:  I redefined $R=R^{final}$. I changed notation because i didnt want to write every time $R^{final}$




