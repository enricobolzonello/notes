
<!--SR:!2026-08-30,1,230-->---
up:
  - "[[IP promises nothing — it is best-effort and never reports delivery outcome]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
A router receives a datagram, consults a table, forwards it, and forgets it. It therefore *cannot* repair loss: it never knew a datagram was expected, loss usually happens *at* a router (asking the failing component to notice its own failure), and the path can change mid-conversation so there's no fixed set of routers to hold state anyway.

The two **endpoints** are the only parties present for the whole conversation.

> **Every guarantee above IP is manufactured by state held at the two endpoints.**

This is the **end-to-end principle** (Saltzer, Reed & Clark, 1984). Two consequences:

- Every guarantee costs **endpoint memory and latency**. Reliability costs a buffer of unacknowledged data plus a timeout wait; ordering costs buffered early arrivals plus the wait for gaps to fill. Nothing is free, because the network isn't participating.
- Inventing a transport requires changing **only the two machines talking** — no router upgrade. This is what makes "write my own transport" physically sensible (though still constrained by deployment reality).

Where it leaks — three named asterisks, none of which change any derivation: **ECN** lets a router mark "congested" instead of dropping; **ICMP** carries some error reports; **NAT** holds per-flow state inside the network.

# See also
- [[IP promises nothing — it is best-effort and never reports delivery outcome]] — this is the direct consequence of IP's silence: guarantees can't live in the network, so they live at the ends
- [[A network connection is identified by a 4-tuple, not a port]] — the connection state that endpoints hold *is* keyed by the 4-tuple; NAT (an end-to-end leak) works by rewriting exactly those coordinates
- [[Sequence numbers make a gap in a stream proof of loss that names what was lost]] — the first concrete "fix at the endpoints": reliability built from endpoint-held state
- [[Single Writer Principle, one thread own all writes to a resource]] — same shape of idea: correctness comes from *who holds the authoritative state*, here the two endpoints rather than the network

# References
- https://en.wikipedia.org/wiki/End-to-end_principle

# Questions
#flashcards/software-engineering/networking

Why can't routers repair packet loss?::A router forwards and forgets — it never knew a datagram was expected, loss often happens at the router itself, and the path can change, so no fixed router holds the state
<!--SR:!2026-10-10,20,250-->

What is the end-to-end principle's core claim about guarantees above IP?::Every guarantee above IP is manufactured by state held at the two endpoints, since only they are present for the whole conversation
<!--SR:!2026-09-02,1,208-->

Every guarantee above IP costs endpoint ==memory and latency== — nothing is free because the network isn't participating.
<!--SR:!2026-08-30,1,230-->


