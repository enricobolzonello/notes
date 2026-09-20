---
up:
  - "[[A process in operating systems is a program in execution]]"
tags:
created: 2026-04-13 10:45
---

In concurrent computation, the actor model uses the actor as the basic building block. An actor can:
 - make local decisions
 - create more actors
 - send more messages
 - determine how to respond to the next message received
They can modify their own private state, but they affect others only through messages. 

# References
- https://en.wikipedia.org/wiki/Actor_model

# See also
- [[A process in operating systems is a program in execution]] — an actor is conceptually a process: isolated state, no shared memory, communicates with the outside world through well-defined channels
- [[A Context Switch Saves the PCB of the Running Process and Restores Another]] — actor runtimes (like Erlang's BEAM) implement lightweight context switching between actors, analogous to OS context switching but at much lower cost
- [[The process scheduler chooses an available process]] — actor runtimes implement their own scheduler to dispatch messages to actors, mirroring the OS scheduler's role for processes
- [[Functional Programming programs are trees of expressions, not sequences of steps]] — actors share the functional programming principle of avoiding shared mutable state; the difference is that FP eliminates state mutation entirely, actors isolate it per actor
- [[Reliability means preventing faults from causing failures]] — the actor model's fault isolation is a direct mechanism for the reliability principle: a crashing actor (fault) doesn't bring down the system (failure); process isolation is listed there as a key reliability strategy