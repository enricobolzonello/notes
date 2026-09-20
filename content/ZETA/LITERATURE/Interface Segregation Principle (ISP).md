---
up:
  - "[[Clean Architecture - Robert C Martin]]"
tags:
  - atomic
created: 2024-12-20 21:27
---
What is wanted here is something like the following substitution property: 
> If for each object $o1$ of type $S$ there is an object $o2$ of type $T$ such that for all programs $P$ defined in terms of $T$, the behavior of $P$ is unchanged when $o1$ is substituted for $o2$ then $S$ is a subtype of $T$

The problem is highlighted in the figure below.
![[isp_example.png]]

User1 will depend on op2 and op3, even though it doesn't call them.

The fix is to segregate the interface into smaller, focused interfaces so each client only depends on what it actually uses.

# See also 
- [[Single Responsibility Principle (SRP)]] — same spirit at the module level: one reason to change; ISP applies this to interfaces 
- [[OCP - software should be open for extension and closed for modification]] — segregated interfaces make it easier to extend behaviour without modifying existing code 
- [[Facade is a structural design pattern that provides a simplified interface to a library]] — Facade is a structural solution to the same problem: hide what clients don't need behind a simpler surface