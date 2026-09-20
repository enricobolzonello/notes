---
tags:
  - permanent_note
up:
created: 2026-04-22 17:57
---

While implementing my simple key-store I wanted to benchmark the cache miss rate. In the M-series Macs there is no `perf`, rather you need to use Instruments, which is a GUI (ugh) built on top of the DTrace framework. 

Since I was doing it in Rust I used `cargo-instruments` to profile directly, and to test it I instructed claude code to do two simple benchmarks with `criterion`: access to an hash map sequentially (in order of pair addition) and random.

What I found out was interesting: on the metric **L1 cache miss rate** (which in Instruments on my machine is `L1D_CACHE_MISS_LD / INST_RETIRED`) these are the results:
- sequential: $\approx15\%$
- random: $\approx40\%$

This led me to an investigation of how Rust implements the Hash table, which is called [[Swiss Table Breaks the Hash Array Into Groups of 8 — Each With a 64-bit Control Word for Metadata|SwissTable]][^1]. Like open-addressing hash tables, it stores entries and metadata contiguously in memory, which is why sequential access benefits from [[Prefer sequential memory access, CPUs predict and prefetch based on locality|spatial locality]]. 
The floor is $15\%$ because the values are `String`, which are heap-allocated, so each lookup involves three pointer dereferences: metadata -> entry -> string data.

In the random access case, spatial locality is destroyed since each lookup jumps to an arbitrary spot.

# See also 
- [[Prefer sequential memory access, CPUs predict and prefetch based on locality]] 
- [[Swiss Table Breaks the Hash Array Into Groups of 8 — Each With a 64-bit Control Word for Metadata]] 
- [[False Sharing Forces CPUs to Serialise Access When Two Threads Write to the Same Cache Line]]


[^1]: https://abseil.io/docs/cpp/guides/container