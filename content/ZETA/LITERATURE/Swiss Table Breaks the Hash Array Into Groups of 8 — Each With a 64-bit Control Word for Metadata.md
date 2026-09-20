---
tags:
  - atomic
up:
  - "[[Collisions are unavoidable by Pigeonhole, Chaining and Open Addressing resolve them]]"
created: 2026-04-17 18:57
---
A Swiss Table is a form of [[Collisions are unavoidable by Pigeonhole, Chaining and Open Addressing resolve them|open-addressed hash table]] optimized around cache-line-sized groups. The key to having an efficient hash table is the probe sequence, i.e. how to choose in which slot to put keys or how to retrieve them.

Swiss tables break the array into logical groups of 8 slots each. Each group has an associated 64-bit control word where each byte stores the state of one slot:
- empty 
- deleted 
- in use, in which case it stores $h_2$, the lower 7 bits of the hash

The complete hash is 64 bit, split as:
- $h_1$(upper 57 bits): used to select the group
- $h_2$ (lower 7 bits): stored in the control word as a fingerprint

In insertion or lookup, after selecting the group with $h_1$ instead of linear scanning to find the slot, we check the control word first. Since the control word is 64 bits, all 8 slots can be check simultaneously with [[SIMD - one operation applied to multiple data points simulaneously|SIMD]]. Only if a byte matches then the full key comparison is done.

# See Also
- [[Collisions are unavoidable by Pigeonhole, Chaining and Open Addressing resolve them]] — Swiss Table is open addressing with a structured probe sequence; the group is the unit of probing 
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — grouping 8 slots together is a deliberate cache line alignment: the control word and its 8 slots fit in one or two cache lines, making probing cache-friendly 
- [[SIMD - one operation applied to multiple data points simulaneously|SIMD - one operation applied to multiple data points simulaneously]] — the control word check is exactly SIMD's use case: one instruction, multiple data points checked simultaneously
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — the control word is the metadata that must be read atomically; concurrent writes to slots in the same group would cause false sharing, which is why Swiss Tables are typically used in single-writer contexts 
- [[A Hash Function Must Be Deterministic, Uniform, and Fast — FNV-1a Is One Example]] — the split of the hash into $h_1$ and $h_2$ requires a hash function whose bits are independently uniform; a poor hash function would cluster $h_2$ values and defeat the SIMD comparison
# References
- https://go.dev/blog/swisstable