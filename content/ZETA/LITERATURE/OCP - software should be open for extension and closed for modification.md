---
up:
  - "[[Clean Architecture - Robert C Martin]]"
tags:
  - atomic
created: 2024-12-17 18:09
---
> [!note] 
> A software artifact should be open for extension but closed for modification.

Accomplished by partitioning the system into components, and arranging those components into a dependency hierarchy that protects higher-level components from changes in lower-level components

# See also
- [[Single Responsibility Principle (SRP)]] — SRP and OCP work together: a module with one reason to change is easier to extend without modifying; violation of SRP typically forces modification instead of extension
- [[Interface Segregation Principle (ISP)]] — segregated interfaces make OCP achievable: when interfaces are small and focused, new behaviour can be added by implementing a new interface rather than modifying an existing one
- [[Facade is a structural design pattern that provides a simplified interface to a library]] — Facade enables OCP at the architectural level: clients depend on the facade, not the subsystem; the subsystem can be extended or replaced without touching client code
- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]] — OCP is the design principle that operationalises evolvability: a system closed for modification but open for extension is one where future changes are additive, not destructive
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — Hyrum's Law is what happens when OCP is violated at scale: if you modify existing behaviour instead of extending, someone was depending on the old behaviour
- [[Functional Programming programs are trees of expressions, not sequences of steps]] — functional programming enforces OCP structurally: pure functions cannot be modified at a distance; new behaviour requires new functions, not changes to existing ones