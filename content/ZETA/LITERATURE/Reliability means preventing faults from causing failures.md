---
up:
  - "[[Designing Data-Intensive Applications - Martin Kleppmann]]"
tags:
  - atomic
created: 2024-12-17 18:12
---

> [!Definition]
> The system should continue to work correctly even in the face of adversity

The things can go wrong are called *faults*, which are different from *failures*. 
- fault = one component of the system deviating from its spec
- failure = system as a whole stops providing the service
It is best to design mechanisms that **prevent faults from causing failures**.

Sometimes you want to deliberately cause faults to test your system, with tools like Chaos Monkey.

# See also 
- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]] — reliability is one of the three pillars alongside maintainability and scalability in data-intensive systems 
- [[Scalability is a system's ability to cope with increased load]] — the companion property: a system can be reliable but unable to cope with increased load, or scalable but brittle; both are needed 
- [[The Actor Model Isolates State Behind Message Passing, No Shared Memory]] — the actor model is a structural mechanism for fault isolation: a crashing actor is a fault that doesn't propagate to a failure of the whole system 
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — Hyrum's Law is a reliability risk: undocumented behaviours that clients depend on become faults when changed 
# References
- [[Designing Data-Intensive Applications - Martin Kleppmann]]





























































