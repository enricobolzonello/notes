---
up:
  - "[[Reliability means preventing faults from causing failures]]"
tags:
  - atomic
created: 2024-12-17 18:12
---
### Hardware Faults
Redundancy is one approach in which fault hardware gets replaced by a redundant component while the broken component is replaced. Cannot completely prevent hardware problems.

In addition or in preference to this technique there is also software fault-tolerance techniques.

### Software Faults
These are systematic errors within the system, which are harder to anticipate. 
There is no quick solution. What can help:
- thinking about assumptions and interactions in the system
- testing
- process isolation
- allow processes to crash and restart
- measure, monitor and analyse systems in production

### Human Errors
Humans are known to be unreliable. How to make systems reliable? 
- Design systems that minimizes opportunities for error.
- Decouple the places where people make the most mistakes from the places where they can cause failures --> provide non-production sandbox environments.
- Test at all levels
- Allow quick and easy recovery
- Set up detailed and clear monitoring
- Implement good management practices and training

# See also 
- [[Reliability means preventing faults from causing failures]] — the framing: these three types are the concrete instances of the fault/failure distinction 
- [[Single Writer Principle, one thread own all writes to a resource]] — process isolation (listed as a software fault mitigation) is the single writer principle applied to fault containment: confine writes to one owner so a fault in one thread can't corrupt another's state 
- [[Non possiamo eliminare i bias, possiamo solo riconoscere le situazioni a rischio]] — human faults are cognitive biases in action; the mitigation strategy mirrors Kahneman's advice: you can't eliminate human error, only design systems that reduce its impact 
# References




























































