---
up:
  - "[[Rust]]"
tags:
  - atomic
created: 2026-05-05 15:00
---
The `tracing` crate models program execution with two primitives:
- **spans**: represent a period of time in which a program executes in a particular context. 
- **events**: a single point in time (like a log line) but occurring within a span

`Subscriber`s consume this data (`tracing-subscriber` is the standard implementation).

# See also 
- [[Three types of faults - hardware is random, software is systematic, human is the most common]] — `tracing` spans are the observability mechanism for software faults: they make the causal chain visible so you can trace a fault back to its origin 
- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]] — `tracing` is the primary tool for operability in Rust: spans and events make the system's runtime behaviour visible and queryable 
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — span nesting mirrors the call stack: entering a span is like pushing a frame, exiting is like popping one; the active span is the tracing equivalent of the current execution context 
- [[Tree Recursion branches at each level]] — the span tree has the same structure as a recursive call tree: each span can contain child spans, and the depth is the nesting level of the execution context 
# References 
- https://docs.rs/tracing
