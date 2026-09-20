---
Priority_Level: 3 Medium
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
closed: 2025-03-07T11:54
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

> [!info] the algorithm cannot terminate until j′ tries have been searched at level i′ where either $j^\prime \ge \ln(1/\delta)/p(q,x_k)^{i^\prime}$ or $i^\prime = 0$.

**definitions**
$p(q,x)=P[h(q)=h(x)]$

**proof**
suppose we are at level $i$ of the search and the probability of collision at this level is $p(q,x_k)^i$. If we perform $j$ independent searches at level $i$, the probability that none of these candidates collide with $x_k$ is $(1-p(q,x_k)^i)^j$.
we want to find $j$ that satisfies:
$$
(1-p(q,x_k)^i)^j \le \delta
$$
for some error tolerance $\delta$.

$$
\begin{align*}
&(1-p(q,x_k)^i)^j \le \delta && \text{take the logarithm of both sides }\\
&\ln((1-p(q,x_k)^i)^j) \le \ln\delta && \text{use} \ln a^b = b\ln a\\
&j\cdot \ln(1-p(q,x_k)^i)\le \ln \delta && \text{isolate }j\\
&j\le \frac{\ln \delta}{\ln(1-p(q,x_k)^i)}
\end{align*}
$$
at this point we can use the [[Taylor Expansion]] $\ln(1-x) = -x -x^2/2 -x^3/3 + O(x^4)$, on the dividend:
$$
\begin{align*}
j&\le \frac{\ln\delta}{\ln(1-p(q,x_k)^i)}\\
j&\le \frac{\ln\delta}{-p(q,x_k)^i +O(c)}\\
j&\le \frac{\ln\delta}{-p(q,x_k)^i}\\
j&\ge \frac{ln(1/\delta)}{p(q,x_k)^i}
\end{align*}
$$
thus concluding the proof.

