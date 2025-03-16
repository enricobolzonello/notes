---
Priority_Level: 
Status: 4 Completed
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/puffinn_analysis"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
closed: 2025-03-07T14:38
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

> $\text{PuffinnSearch}(q,k,\delta)$ returns a set of $k$ points, each one being with probability at least $\delta$ among the k nearest neighbors to q

**definitions**
$PQ$ is the priority queue that holds the top-k closest points
$x_k^\prime\in PQ$ farthest point in the priority queue from $q$
$p(q,x)=P[h(q)=h(x)]$

Let $x_1,...,x_k$ be the $k$ nearest neighbors of $q$, with k$\ge 1$. 
At each stage of the algorithm, the invariant "$PQ.size<k$ or $p(q,x_k^\prime)\le p(q,x_k)$" is  satisfied, and can be proven by induction. 
*base*: $PQ$ is empty, so the condition $PQ.size<k$ holds
*induction*: assume that the invariant holds before inserting a new point $x$ into PQ. We need to prove it still holds after the insertion. There are two cases:
1) $PQ.size<k$. After the insertions, either $PQ.size$ is still $<k$ or it becomes exactly $k$. In the latter case, we need to show that $p(q,x_k^\prime) \le p(q,x_k)$ 
2) $PQ.size = k$. If x is not inserted because $\text{dist}(q,x)\ge \text{dist}(q,x_k^\prime)$, the invariant still holds. Otherwise, it replaces the previous $x_k^\prime$, since the algorithm replaces the point with highest distance. We need to show that new $x_k^\prime$ satisfies $p(q,x_k^\prime) \le p(q,x_k)$
We still have to prove that $p(q,x_k^\prime) \le p(q,x_k)$ for any new $x_k^\prime$. By construction, it holds that for any point $x\in PQ$, $dist(q,x)\le dist(q,x_k^\prime)$. Since $x_k$ is the true [[(k, δ) Nearest Neighbor problem|k nearest neighbor]], we have that:
$$
dist(q,x_k^\prime) \ge dist(q,x_k)
$$
From the definition and the monotonicity of the [[LSH Family]], we can conclude that $dist(q,x_k^\prime) \ge dist(q,x_k)$ implies $p(q,x_k^\prime) \le p(q,x_k)$, thus concluding the proof of the invariant. 

Now we want to find the minimum number of tries to visit before returning a set of $k$ points each one with probability at least $\delta$ to be among the true k nearest neighbors. 
Suppose we are at level $i$ of the search and the probability of collision at this level is $p(q,x_k)^i$. If we perform $j$ independent searches at level $i$, the probability that none of these candidates collide with $x_k$ is $(1-p(q,x_k)^i)^j$. Our aim is to find $j$ that satisfies:
$$
(1-p(q,x_k)^i)^j \le 1-\delta
$$
$$
\begin{align*}
&(1-p(q,x_k)^i)^j \le 1-\delta && \text{take the logarithm of both sides }\\
&\ln((1-p(q,x_k)^i)^j) \le \ln(1-\delta) && \text{use} \ln a^b = b\ln a\\
&j\cdot \ln(1-p(q,x_k)^i)\le \ln(1-\delta) && \text{isolate }j\\
&j\le \frac{\ln (1-\delta)}{\ln(1-p(q,x_k)^i)}
\end{align*}
$$
At this point we can use the Taylor expansion $\ln(1-x) = -x -x^2/2 -x^3/3 + O(x^4)$, on the dividend, to obtain:
$$
\begin{align*}
j&\le \frac{\ln(1-\delta)}{\ln(1-p(q,x_k)^i)}\\
j&\le \frac{\ln(1-\delta)}{-p(q,x_k)^i +O(c)}\\
j&\le \frac{\ln(1-\delta)}{-p(q,x_k)^i}\\
j&\ge \frac{ln(1/(1-\delta))}{p(q,x_k)^i}
\end{align*}
$$
since we proved that $dist(q,x_k^\prime) \ge dist(q,x_k)$ implies $p(q,x_k^\prime) \le p(q,x_k)$, we can conclude the proof:
$$
j\ge \frac{ln(1/(1-\delta))}{p(q,x_k)^i}\ge \frac{ln(1/(1-\delta))}{p(q,x_k^\prime)^i}
$$
