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
closed: 2024-12-15T21:10
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

> $PQ.size <k$ or $p(q,x_k^\prime)\le p(q,x_k)$ at each stage of the algorithm

**definitions**
$PQ$ is the priority queue that holds the top-k closest points
$p(q,x)=P[h(q)=h(x)]$

**proof (by induction)**
*base*: PQ is empty, so the condition $PQ.size < k$ holds
*induction*: assume that the invariant holds before inserting a new point $x$ into PQ. We need to prove it still holds after the insertion. There are two cases:
1) $PQ.size<k$ --> after the insertions, either $PQ.size$ is still $<k$ or it becomes exactly $k$. In the latter case, we need to show that $p(q,x_k^\prime) \le p(q,x_k)$ 
2) $PQ.size = k$ --> if x is not inserted, the invariant still holds. Otherwise, it replaces the previous $x_k^\prime$, since the algorithm replaces the point with highest distance. We need to show that new $x_k^\prime$ satisfies $p(q,x_k^\prime) \le p(q,x_k)$
we still have to prove that $p(q,x_k^\prime) \le p(q,x_k)$ for any new $x_k^\prime$. By construction, it holds that for any point $x\in PQ$, $dist(q,x)\le dist(q,x_k^\prime)$. Since $x_k$ is the true [[(k, δ) Nearest Neighbor problem|k nearest neighbor]], we have that:
$$
dist(q,x_k^\prime) \ge dist(q,x_k)
$$
From the definition and the monotonicity of the [[LSH Family]], we can conclude that $dist(q,x_k^\prime) \ge dist(q,x_k)$ implies $p(q,x_k^\prime) \le p(q,x_k)$, thus concluding the proof.


