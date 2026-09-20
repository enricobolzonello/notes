---
up:
  - "[[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]"
tags:
  - atomic
created: 2025-10-08 23:16
---

Hyrum's law states:

> With a sufficient number of users of an API, it does not matter what you promise in the contract: all observable behaviours of your system will be depended on somebody

- We cannot assume perfect adherence to published contracts or best practices. 
- You can think of it as the concept of entropy in physics
- writing code that works vs writing code that works indefinitely 

# References
- [[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]

# See also
- [[Scale and Efficiency applies to people, compute and codebase]] — Hyrum's Law is why scale makes API contracts harder: more users means more accidental dependents
- [[Style Guides and Rules]] — one response to Hyrum's Law: enforce consistency so that observable behaviour is intentional, not accidental
- [[Documentation Is Not a Wiki — It Lives and Evolves With the Code]] — another response: document what the contract actually is, so users depend on the right things
