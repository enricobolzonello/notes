---
connections: 
reference: 
tags:
  - type/note
  - theme/engineering
type:
  - literature_note
created: 2024-12-17 18:12
---
 
> [!Definition]
> The system should continue to work correctly even in the face of adversity

The things can go wrong are called *faults*, which are different from *failures*. 
- fault = one component of the system deviating from its spec
- failure = system as a whole stops providing the service
It is best to design mechanisms that **prevent faults from causing failures**.

Sometimes you want to deliberately cause faults to test your system, with tools like Chaos Monkey.

three kind of faults
- hardware faults
- software faults
- human faults

### Hardware Faults
Redundancy is one approach in which fault hardware gets replaced by a redundant component while the broken component is replaced. Cannot completely prevent hardware problems.

In addition or in preference to this technique there is also software fault-tolerance techniques.

### Software Faults
These are systematic errors within the system, which are harder to anticipate. 
There is no quick solution. What can help:
- thinking about assumptions and interactions in the system
- testing
- process isolation
- allow processes to crash and restart
- measure, monitor and analyse systems in production

### Human Errors
Humans are known to be unreliable. How to make systems reliable? 
- Design systems that minimizes opportunities for error.
- Decouple the places where people make the most mistakes from the places where they can cause failures --> provide non-production sandbox environments.
- Test at all levels
- Allow quick and easy recovery
- Set up detailed and clear monitoring
- Implement good management practices and training
































































