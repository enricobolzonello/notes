---
up:
  - "[[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]"
tags:
  - atomic
created: 2026-05-06 11:01
---
> The result of performing some operation should be obvious, consistent and predictable based upon the name of the operation and other clues

Interfaces should be intuitive enough that if the user has to guess, they usually guess correctly.

# See also
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — Hyrum's Law is what happens when the Principle of Least Astonishment is violated at scale: surprising behaviours become depended upon, making them impossible to fix without breaking callers
- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]] — operability is the Principle of Least Astonishment applied to running systems: the system should reveal its behaviour predictably so operators are never surprised by what it does
- [[Interface Segregation Principle (ISP)]] — violating ISP creates surprise: a client that depends on an interface discovers unexpected behaviour from methods it never asked for
- [[OCP - software should be open for extension and closed for modification]] — OCP violations are a form of astonishment: a caller expects extending behaviour to be additive, not to change existing behaviour they already depend on

# References
- https://wiki.c2.com/?PrincipleOfLeastAstonishment