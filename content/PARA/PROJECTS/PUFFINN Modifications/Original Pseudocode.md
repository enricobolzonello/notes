---
Priority_Level: 
Status: 4 Completed
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/puffinn_modifications"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
closed: 2025-03-10T14:26
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

Let $S_{i,j}(q)$ denote the subset of points in $S$ that collide with $q$ when we consider the first $i$ hash values used in the construction of the $j$th trie. Define $\Pi_{i,j}(q) = S_{i,j}(q)\backslash S_{i+1,j}(q)$ where $S_{K+1,j}(q) = \emptyset$.  
```pseudo
    \begin{algorithm}
    \caption{PUFFINN query algorithm}
    \begin{algorithmic}
		\State $PQ \leftarrow \text{empty priority queue of (point, dist) of unique points}$
		\For{$i\leftarrow K,K-1,...,0$}
		\For{$j\leftarrow 1,2,...,L$}
		\For{$x\in \Pi_{i,j}(q)$}
			\If{$dist(q,x_k^\prime)\ge dist(q,x)$}
				\State $PQ\text{.insert}(x,dist(q,x))$
            \EndIf
        \EndFor
        \If{$i=0$ \Or $\Big(PQ\text{.size}()=k$ \And $j\ge \frac{\ln(1-\delta)}{p(q,x_k^\prime)^i}\Big)$} 
	        \Return $PQ$
        \EndIf
        \EndFor
        \EndFor
    \end{algorithmic}
    \end{algorithm}
```


