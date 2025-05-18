---
connections:
  - "[[Hash Tables · Crafting Interpreters]]"
  - "[[Hash Table]]"
reference: https://craftinginterpreters.com/hash-tables.html#open-addressing
tags:
  - theme/low-level
  - theme/engineering
type: literature_note
created: 2025-03-20 11:10
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

A hash table is an effective data structure for implementing dictionaries. The average time to search is $O(1)$﻿

A hash table generalizs the simpler notion of an ordinary array.
# Direct-address Table
→ we can take advantage of it when we can afford to allocate an array that has one position for every possible key
  
Suppose that we need a dynamic set in which each element has a key drawn from the universe $U=\{0,1,...,m-1\}$﻿, where $m$﻿ is not too large.
To represent the dynamic set we use a direct-address table (i.e. array), in which each slot corresponds to a key in $U$﻿

> slot $k$﻿ points to an element in the set with key $k$﻿
  
In some applications rather than storing the key and the data in an external object, we can store the object in the slot itself.
  
# Hash Tables
→ direct-address tables can’t be used for large universes
  
Hash table requires much less storage when the set $K$﻿ of keys stored in a dictionary is much smaller than the universe $U$﻿.
Memory → $\Theta(|K|)$﻿
Searching requires $O(1)$﻿ time
  
We use a **hash function** $h:U\rightarrow \{0,1,...,m-1\}$﻿ to compute the slot number from the key $k$﻿. The hash function maps the universe of keys into the slot of a **hash table** $T[0:m-1]$﻿.
The hash function reduces the range of array indices, instead of a size of $|U|$﻿, the array can have size $m$﻿.

## Collisions
**Problem**:
Two keys may hash to the same slot → collision
Impossible to avoid due to the [[Pigeonhole Principle]], so we need a way to resolve collisions.

### Independent uniform hashing
→ what it means for a hash function to be “random”

> [!important]  Independent Uniform Hash Function
> For each possible input $k$﻿, the output $h(k)$﻿ is an element randomly and independently chosen uniformly from the range $\{0,1,...,m-1\}$
→ implementing hash tables with this function, we say we are using **independent uniform hashing** (not implementable)
  
### Separate chaining
The input set of $n$﻿ elements is divided randomly into $m$﻿ size. A hash function determines which subset an element belongs to and each subset is managed independently as a list.

![An array with eight buckets. Bucket 2 links to a chain of two nodes. Bucket 5 links to a single node.](https://craftinginterpreters.com/image/hash-tables/chaining.png)

**chaining** → each nonempty slot points to a linked list. Slot $j$﻿ contains a pointer to the head of the list of all stored elements with hash value $j$﻿
  
insertion: $O(1)$﻿ at worst assuming the element is not already present
searching: proportonial to the length of the list
deletion: $O(1)$﻿ if lists are doubly linked
#### Analysis
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

### Open Addressing
-> store all entries in a single array
The problem is that when inserting the bucket may be full, so we need to search another bucket. The process of finding an available bucket is called **probing**, while the bucket order is the **probe sequence** [^1]. 

Pros:
- easy
- cache-friendly
Cons:
- prone to clustering

## Hash Functions
-> takes a value (generic) and outputs a fixed-size integer hash code
requirements:
- deterministic
- uniform
- fast

They are different ones, one is [FNV-1a](http://www.isthe.com/chongo/tech/comp/fnv/).

```rust
pub trait Hashable {
    fn hash(&self) -> u32;
}

impl Hashable for String {
    fn hash(&self) -> u32 {
        let mut hash = 2166136261;
        for c in self.as_bytes() {
            hash = (hash ^ (*c as u32)).wrapping_mul(16777619);
        }
        hash
    }
}
```



[^1]: Same concept as Multi-Probing in LSH implementations