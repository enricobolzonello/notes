---
Priority_Level: 
Status: 4 Completed
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/clann_running_time"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
closed: 2025-03-18T10:08
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description
define:
- ${x_k^\prime}^{(t)}$ as the farthest point in PQ at iteration $t$
- $R^{(t)}=\text{dist}(q,{x_k^\prime}^{(t)}) +r_{i}\le \text{dist}(q,{x_k^\prime}^{(t)}) +r_{max}$  
At $t=0$, PQ is empty so ${x_k^\prime}^{(0)}=\infty$ and $R^{(0)} =\infty$. In the next iterations ${x_k^\prime}^{(t)}$ decreases incrementally until it converges to the true k nearest neighbor distance $\rho=\text{dist}(q,x_k)$.
To ensure all points within $\rho$ of $q$ are found, CLANN must search clusters that intersect the $\rho$-ball around $q$. A cluster $\mathcal{C}_i$ intersects the $\rho$-ball if:
$$
\text{dist}(q,c_i)-r_i\le \rho \rightarrow \text{dist}(q,c_i)\le \rho +r_i \le \rho +r_{max}
$$
So all clusters contributing to the $k$ nearest neighbors must lie within a ball of radius $R=\rho + r_{max}$ around $q$.

> # Doubling space: Iteratively Covering Smaller Balls
> Recursively cover each ball of radius $r$ with $2^D$ balls of half the radius $r/2$, then each of those with $2^D$ balls of radius $r/4$ and so on. After $k$ subdivisions, **the radius of each ball becomes $r/2^k$ and the number of balls needed is $(2^D)^k$.

given this, we decompose $R$ iteratively. At each scale $R/2^i$ the number of clusters is $O(2^{iD})$. Summing over until $R/2^i\ge \rho$:
$$
\begin{align*}
M &= 
\sum_{i=0}^{\log_2(R/\rho)} 2^{iD}\\
&= \frac{2^D(R/\rho)^D-1}{2^D-1} \\
&= O\bigg(\frac{2^D(R/\rho)^D}{2^D}\bigg)\\
&= O\bigg(\Big(\frac{R}{\rho}\Big)^D\bigg)
\end{align*}
$$
Define $\Gamma = \frac{r_{max}}{\rho}$, then:
$$
M = O\bigg(\Big(\frac{R}{\rho}\Big)^D\bigg) = O((1+\Gamma)^D)
$$
when $\Gamma >> 1$ it holds $M=O(\Gamma^D)$. 

> the worst case occurs when clusters are positioned on the edge of the ball of radius $\rho$ around $q$, meaning they minimally overlap it. 
> Covering the extended radius $R=\rho (1+\Gamma)$ requires exponentially more clusters as $\Gamma$ grows. 

--> $O(k\log k)$ for priority queue operations

--> final time: $O(\Gamma^D \cdot T_{puffinn})$ (dominated by puffinn)






