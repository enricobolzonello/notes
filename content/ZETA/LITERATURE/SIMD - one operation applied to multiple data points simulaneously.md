---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
  - atomic
created: 2026-01-30 10:49
---
> Describes computers with multiple processing elements that perform the same operation on multiple data points simultaneously

- data level parallelism, not concurrency

# See also
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] — SIMD and cache locality work together: SIMD is most effective when the data points it processes are contiguous in memory, already in the same cache line
- [[Swiss Table Breaks the Hash Array Into Groups of 8 — Each With a 64-bit Control Word for Metadata]] — Swiss Tables are the canonical real-world application: the 64-bit control word is processed with a single SIMD instruction to check all 8 slots simultaneously
- [[The Hadamard Transform y = Hₘx Transforms 2ᵐ Numbers Using Only Additions and Subtractions]] — the Hadamard transform's ±1 structure is ideal for SIMD: no multiplications means each operation fits in a single instruction across multiple elements
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]] — SIMD and false sharing are two sides of the same hardware coin: SIMD exploits data proximity for speed, false sharing suffers from it for correctness; both are consequences of the cache line as the fundamental unit of memory
- [[The process scheduler chooses an available process]] — SIMD is data-level parallelism within one process; the scheduler handles process-level parallelism across cores; they are orthogonal strategies for maximising CPU utilisation

# References
- https://en.wikipedia.org/wiki/Single_instruction,_multiple_data