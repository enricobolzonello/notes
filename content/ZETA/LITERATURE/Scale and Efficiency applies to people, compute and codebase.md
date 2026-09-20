---
up:
  - "[[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]"
tags:
  - atomic
created: 2025-10-08 23:29
---

- what needs to scale?
	- human resources
	- compute resources
	- codebase itself
		- if your build system or vcs scales superlinearly over time, it might come a point where you can't continue
		- something like the boiled frog

# See also
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — Hyrum's Law is the human-scale version of this problem: as the number of users grows, the surface area of implicit dependencies grows superlinearly
- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]] — maintainability is what keeps the codebase scaling sublinearly; a system that is hard to maintain accumulates complexity superlinearly over time
- [[Scalability is a system's ability to cope with increased load]] — the same concept applied to runtime systems rather than engineering organisations; both ask the same question: does the system grow linearly or superlinearly with load?
- [[Single-Loop Optimizes the Method, Double-Loop Questions the Goal Itself]] — a build system scaling superlinearly is the boiled frog problem: single-loop thinking keeps optimising the build, double-loop thinking questions whether the architecture itself needs changing
- [[Style Guides and Rules]] — one of the mechanisms that keeps human resources scaling: consistent style reduces the cognitive overhead of working across a large codebase, making each new engineer cheaper to onboard

# References
- [[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]