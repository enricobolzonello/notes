---
up:
  - "[[Clean Architecture - Robert C Martin]]"
tags:
  - type/term
  - theme/engineering
type:
  - literature_note
created: 2024-12-17 18:04
---

> [!note] 
> A module should be responsible to one, and only one, actor.

This means that we need to separate the code that different actors depend on.
You can instantiate several different classes, but it is tedious to track. The solution is to use the [[Facade is a structural design pattern that provides a simplified interface to a library]] design pattern.

# See also
- [[OCP - software should be open for extension and closed for modification]] — SRP and OCP work together: a module with one reason to change is easier to extend without modifying; a module with multiple actors forcing changes on it cannot be closed for modification
- [[Interface Segregation Principle (ISP)]] — ISP is SRP applied to interfaces: just as a module should serve one actor, an interface should serve one client type
- [[Facade is a structural design pattern that provides a simplified interface to a library]] — the recommended solution when SRP forces you to split a class: instantiate several focused classes but wrap them in a Facade so callers don't have to track them all
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — Hyrum's Law explains why violating SRP is dangerous at scale: when a module serves multiple actors, each actor depends on different observable behaviours; changing one breaks the other
- [[Single Writer Principle, one thread own all writes to a resource]] — the same principle at the concurrency level: one owner per resource; SRP is the design-time version, single writer is the runtime version of the same idea