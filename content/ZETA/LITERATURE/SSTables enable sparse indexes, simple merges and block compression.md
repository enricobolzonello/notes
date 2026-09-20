---
up:
  - "[[An SSTable is a segment of key-value pairs sorted by keys]]"
tags:
  - atomic
created: 2026-01-30 16:08
---
- advantages
	- merging is simple (mergesort)
	- no need to keep an index of all the keys in memory, just some (need to scan a few keys)
	- group records into a block and compress it before writing to disk (thanks to above)

# See also 
- [[An SSTable is a segment of key-value pairs sorted by keys]] — the structure that makes all three advantages possible 
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — the sparse index + sequential scan exploits spatial locality: once you find the right block, the keys you need are contiguous 
- [[Coreset is a small subset from P which represent P well]] — the sparse index is a coreset of the keyspace: a small representative subset that bounds the error of any lookup to a short sequential scan 
- [[Scalability is a system's ability to cope with increased load]] — the three advantages directly serve scalability: sparse indexes reduce memory load parameters, block compression reduces disk I/O load parameters

# References
- [[Designing Data-Intensive Applications - Martin Kleppmann]]