---
up: "[[Designing Data-Intensive Applications - Martin Kleppmann]]"
tags:
  - atomic
created: 2026-01-30 16:08
---

An SSTable is a log-structured storage segment where:
- key-value pairs are **sorted by key**
- each key appears only once (enforced by the **compaction process**)

# See also 
- [[LSM-Trees]] — SSTables are the on-disk component of an LSM-Tree: the memtable (in-memory) is flushed to an SSTable when it gets too large; compaction merges multiple SSTables 
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — compaction is merge-sort on multiple SSTables; merge-sort is efficient precisely because the inputs are sorted, which is why the sorted-by-key invariant is worth maintaining # References

# References
- [[Designing Data-Intensive Applications - Martin Kleppmann]]