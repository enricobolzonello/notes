---
connections: 
reference: 
tags:
  - type/note
  - theme/engineering
type:
  - literature_note
created: 2024-12-17 18:16
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!Definition]
> Over time, many different people will work on the system (engineering and oper‐ations, both maintaining current behavior and adapting the system to new usecases), and they should all be able to work on it productively

Majority of the cost of software is not in its initial development, but in its ongoing maintenance. 
To reduce pain during maintenance, there are three design principles we should follow:
1) Operability --> easy to keep the system running
2) Simplicity --> easy to understand the system
4) Evolvability --> easy to make changes

### Operability
what to do:
- provide visibility into the runtime behaviour and internals with good monitoring
- provide good support for automation and integration with tools
- avoiding dependency on individual machines
- provide good documentation
- provide good default behaviour
- self healing where appropriate
- minimize surprises

### Simplicity
Making a system simpler does not mean reducing its functionality; it can also remove *accidental complexity*. One of the best tools to remove is *abstraction*. 

### Evolvability
Closely linked with simplicity and abstractions.