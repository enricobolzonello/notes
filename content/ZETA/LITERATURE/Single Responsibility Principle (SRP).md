---
connections: 
reference: 
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
You can instantiate several different classes, but it is tedious to track. The solution is to use the [[Facade]] design pattern.