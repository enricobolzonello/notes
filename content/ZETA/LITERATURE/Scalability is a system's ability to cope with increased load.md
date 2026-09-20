---
up:
  - "[[Designing Data-Intensive Applications - Martin Kleppmann]]"
tags:
  - atomic
created: 2024-12-17 18:14
---
> Scalability is the term we use to describe a system's ability to cope with increased load

Load can be described with a few numbers called *load parameters*, which depend on the system's architecture. Some examples include requests per second, ration of reads to writes, number of simultaneous users, cache hit rate, etc.

Two ways to think about performance under increased load: 
1. Keep resources unchanged — how does performance degrade? 
2. Keep performance unchanged — how much do you need to increase resources?

# See also 
- [[Reliability means preventing faults from causing failures]] — reliability and scalability are companion properties: a system can be reliable but not scalable, or scalable but brittle 
- [[Most of the Cost of Software Is Maintenance — Operability, Simplicity, Evolvability Reduce It]] — the third pillar alongside reliability and maintainability in data-intensive systems 
- [[Scale and Efficiency applies to people, compute and codebase]] — the same concept at the codebase level: build systems and VCS that scale sublinearly, not superlinearly

# References
- [[Designing Data-Intensive Applications - Martin Kleppmann]]