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
closed: 2025-03-21T11:28
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

> Let $\Gamma=r_{max}/ \rho$ where $r_{max}$ is the maximum radius for any cluster and $\rho=\text{dist}(q,x_k)$ is the $k$th true nearest neighbor distance. If the dataset $S$ belongs to a metric space of doubling dimension $D$ then, with probability $\delta$, we have that the query algorithm terminates with expected running time:$$
O(\Gamma^D \cdot (OPT(L, K, k, (1-\delta)/k) + L(K + k)))$$

## proof
The query algorithm defined in Algorithm \ref{} returns the true $k$ nearest neighbors with probability $\delta$, hence the time complexity result we derive holds with probability $\delta$. 
At iteration $t$ of the algorithm, denote by ${x_k^\prime}^{(t)}$ as the farthest point (in terms of distance to $q$) stored in the priority queue PQ and let
$$
R^{(t)}=\text{dist}(q,{x_k^\prime}^{(t)}) +r_{i}\le \text{dist}(q,{x_k^\prime}^{(t)}) +r_{max}
$$
where $r_i$ is the radius of the cluster $i$ and $r_{max}$ is the maximum radius of all clusters. 
Initially, at $t=0$, PQ is empty so ${x_k^\prime}^{(0)}=\infty$ and $R^{(0)} =\infty$. As the algorithm proceeds in the next iterations, ${x_k^\prime}^{(t)}$ decreases incrementally until it converges to the true $k$-nearest neighbor distance $\rho=\text{dist}(q,x_k)$.
To ensure all points within distance $\rho$ of $q$ are found, CLANN must examine all clusters that intersect the $\rho$-ball centered at $q$. For cluster $\mathcal{C}_i$ to intersect the $\rho$-ball it must hold that: $$\text{dist}(q,c_i) - r_i \le \rho$$
Rearranging, we obtain:
$$
\begin{align*}
\text{dist}(q,c_i) &\le \rho + r_i \\
&\le \rho + r_{max}
\end{align*}
$$
Therefore, every cluster contributing to the final $k$-nearest neighbors must lie within a ball of radius $R=\rho + r_{max}$ centered at $q$.

Given that the dataset $S$ belongs to a metric space of doubling dimension $D$, we can apply the doubling space property to bound the number of relevant clusters. This property allows us to recursively cover each ball of radius $R$ with $2^D$ balls of half the radius $R/2$, then each of those with $2^D$ balls of radius $R/4$ and so on. At each scale $R/2^i$ the number of clusters needed is $O(2^{iD})$. Summing over all scales until $R/2^{i}\ge \rho$ we get the total number of potentially relevant clusters:
$$
\begin{align*}
M &= 
\sum_{i=0}^{\lceil \log_2(R/\rho) \rceil} 2^{iD}\\
&= \frac{2^D(R/\rho)^D-1}{2^D-1} \\
&= O\bigg(\frac{2^D(R/\rho)^D}{2^D}\bigg)\\
&= O\bigg(\Big(\frac{R}{\rho}\Big)^D\bigg)
\end{align*}
$$
Define $\Gamma = \frac{r_{max}}{\rho}$, then:
$$
\begin{align*}
M &= O\bigg(\Big(\frac{R}{\rho}\Big)^D\bigg)\\
&= O\bigg(\Big(\frac{\rho + r_{max}}{\rho}\Big)^D\bigg)\\
&= O((1+\Gamma)^D)
\end{align*}
$$
when $\Gamma \gg 1$ (i.e., when the maximum cluster radius is significantly larger than the distance to the $k$-th nearest neighbor), this simplifies to $M=O(\Gamma^D)$. Bounded the number of relevant clusters, we can conclude the running time proof. 

For each of the $M$ clusters, the algorithm performs two main operations:
- A call to the PUFFINN search algorithm, which returns the candidate nearest neighbors in expected time $O(OPT(L, K, k, (1-\delta)/k) + L(K + k))$ with probability $\delta$. This time is linked to the optimal expected running time of an algorithm that knows optimal parameter choices for the number of tries and depth of each one.
- At most $k$ priority queue insertions, where each insertion requires time $O(\log k)$ for a total of $O(k \log k)$ per cluster.
Additionally, the initial sorting of the clusters is performed in time $O(|C|\log|C|)$. Thus, the overall expected running time is:
$$
O\Big(|C|\log|C| + \Gamma^D \cdot \big((OPT(L, K, k, (1-\delta)/k) + L(K + k)) +k\log k\big)\Big)
$$
Under typical assumptions where the sorting and $k\log k$ term are dominated by the PUFFINN search cost (which is typically true for large datasets), this expression simplifies asymptotically to:
$$
O(\Gamma^D \cdot (OPT(L, K, k, (1-\delta)/k) + L(K + k)))
$$
concluding the proof.