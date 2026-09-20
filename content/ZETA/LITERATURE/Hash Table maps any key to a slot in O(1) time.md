---
up:
  - "[[Hash Tables · Crafting Interpreters]]"
tags:
  - atomic
created: 2026-03-29 10:36
---

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


# See also
- [[An SSTable is a segment of key-value pairs sorted by keys]] - also a key-value structure, but sorted; trades $O(1)$ lookup for merge efficiency