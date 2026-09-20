---
up:
  - "[[Designing Data-Intensive Applications - Martin Kleppmann]]"
tags:
  - atomic
created: 2024-12-17 18:16
---

> Over time, many different people will work on the system (engineering and oper‐ations, both maintaining current behavior and adapting the system to new usecases), and they should all be able to work on it productively

Majority of the cost of software is not in its initial development, but in its ongoing maintenance. Three design principles reduce that pain:
1) **Operability**: easy to keep the system running
2) **Simplicity**: easy to understand the system
3) **Evolvability**: easy to make changes

## Operability
Operability is about making it easy for operations teams to keep the system running:
- provide visibility into the runtime behaviour with good monitoring
- support automation and integration with tools
- avoiding dependency on individual machines
- provide good documentation and sensible default behaviour
- self healing where appropriate
- minimise surprises

## Simplicity
Making a system simpler does not mean reducing its functionality; it can also remove *accidental complexity*. One of the best tools to remove is *abstraction*. 

## Evolvability
Closely linked with simplicity and abstractions.


# References
- [[Designing Data-Intensive Applications - Martin Kleppmann]]

# See also
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — Hyrum's Law: surprises in observable behaviour become dependencies; operability requires making behaviour intentional and visible
- [[Interface Segregation Principle (ISP)]] — another form of accidental complexity: forcing irrelevant dependencies on clients 
- [[OCP - software should be open for extension and closed for modification]] — evolvability at the module level: open for extension, closed for modification