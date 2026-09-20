---
up:
  - "[[Hash Tables · Crafting Interpreters]]"
tags:
  - atomic
created: 2026-03-29 10:36
---
Collisions — two keys hashing to the same slot — are unavoidable by the [[Pigeonhole Principle - if n items fill m containers and n>m, some container has more than one]]. Two strategies resolve them.

## Separate Chaining

The input set of $n$﻿ elements is divided randomly into $m$﻿ size. A hash function determines which subset an element belongs to and each subset is managed independently as a list.

![An array with eight buckets. Bucket 2 links to a chain of two nodes. Bucket 5 links to a single node.](https://craftinginterpreters.com/image/hash-tables/chaining.png)

**chaining** → each nonempty slot points to a linked list. Slot $j$﻿ contains a pointer to the head of the list of all stored elements with hash value $j$﻿
  
insertion: $O(1)$﻿ at worst assuming the element is not already present
searching: proportonial to the length of the list
deletion: $O(1)$﻿ if lists are doubly linked
### Analysis
Define the **load factor** $\alpha$﻿ for hash table $T$﻿ as $n/m$﻿, with $m$﻿ number of slots and $n$﻿ number of elements.
  
The worst case is in which all keys hash the same slot, creating a list of length $n$﻿. Searching is $\Theta(n)$﻿
  
The average case depends on how well the hash function distributes the set of keys. We assume that we are using independent uniform hashing.
Because hashes of distinct keys are assumed to be independent, independent uniform hashing is **universal** → chance of collide is $1/m$﻿.
For $j=0,1,...,m-1$﻿ denote the length of the list $T[j]$﻿ by $n_j$﻿ so that $n=n_0+n_1+...+n_{m-1}$﻿. Then $E[n_j]=\alpha=n/m$﻿.

> [!theorem] Theorem 1 (Unsuccessful Search) 
> In hash table with chaining, an unsuccessful search takes $\Theta(1+\alpha)$﻿ time on average, with the assumption of independent uniform hashing  
  
> [!theorem]  Theorem 2 (Successful Search)
> In hash table with chaining, a successful search takes $\Theta(1+\alpha)$﻿ on average  
  
So, concluding:
- searching → $O(1)$﻿ on average
- deletion → $O(1)$﻿ at worst
→ we can support all dictionary operations in $O(1)$﻿ time on average

## Open Addressing
-> store all entries in a single array
The problem is that when inserting the bucket may be full, so we need to search another bucket. The process of finding an available bucket is called **probing**, while the bucket order is the **probe sequence** [^1]. 

Pros:
- easy
- cache-friendly
Cons:
- prone to clustering

[^1]: Same concept as Multi-Probing in LSH implementations

# References
- https://craftinginterpreters.com/hash-tables.html#open-addressing

# See also
- [[Pigeonhole Principle - if n items fill m containers and n>m, some container has more than one]] — the reason collisions are mathematically unavoidable