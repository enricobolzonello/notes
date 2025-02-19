---
connections: 
reference: 
tags:
type: literature_note
created: 2024-12-20 21:27
---
 

> [!Note]
> What is wanted here is something like the following substitution property: If for each object o1 of type S there is an object o2 of type T such that for all programs P defined in terms of T, the behavior of P is unchanged when o1 is substituted for o2 then S is a subtype of T

The problem is highlighted in the figure below.
![[images/isp_example.png]]

User1 will depend on op2 and op3, even though it doesnt call them. This can be solved by segregating the operations into interfaces. 