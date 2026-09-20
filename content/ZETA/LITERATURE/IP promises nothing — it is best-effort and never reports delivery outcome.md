---
up:
  - "[[An IP Address Identifies the Location of a Resource Within a Network]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
Hand IP a datagram and it makes a genuine *attempt* to deliver it. That is its entire commitment — "best-effort". Across delivery IP may **drop**, **delay** arbitrarily, **reorder**, **duplicate**, or **corrupt** the datagram, and in every case *you are never told*. Silence is indistinguishable from success.

Two caveat-free universal statements generate everything downstream:

> **Every IP datagram is routed independently, with no memory of any other.**
> **IP never reports the outcome of a delivery.**

The first is the source of reordering and duplication. The second is why "did it arrive?" must be answered somewhere else entirely.

IP also does **not** protect the payload from corruption. IPv4's checksum covers only the *header* (so a router doesn't misroute a datagram whose destination got mangled); IPv6 removed the header checksum entirely (RFC 8200 §8.1). End-to-end payload integrity is not an IP service — which is why TCP and UDP each carry their own checksum.

This is the single root of the whole transport subject: **IP promises nothing; every feature you've heard of is a specific fix, added elsewhere, with a specific price.**

# See also
- [[An IP Address Identifies the Location of a Resource Within a Network]] — IP addressing locates a *host*; this note is about what IP does (and refuses to do) once a datagram is on its way
- [[Every guarantee above IP is manufactured by state at the two endpoints]] — the direct consequence: because IP reports nothing, all guarantees must be built above it, and only the endpoints can do it
- [[OSI Model describes network communication in 7 layers from physical bits to application data]] — IP is the Network layer (3); this note explains why the layers above it exist at all
- [[Reliability means preventing faults from causing failures]] — IP's silent drop/reorder/corrupt are exactly the faults transport must prevent from becoming failures

# References
- https://datatracker.ietf.org/doc/html/rfc791
- https://datatracker.ietf.org/doc/html/rfc8200#section-8.1

# Questions
#flashcards/software-engineering/networking

What is IP's entire delivery commitment?::Best-effort — it attempts delivery but may silently drop, delay, reorder, duplicate, or corrupt a datagram, and never reports the outcome
<!--SR:!2026-10-14,24,250-->

Why must "did it arrive?" be answered above IP?::Because IP never reports the outcome of a delivery — silence is indistinguishable from success
<!--SR:!2026-10-02,12,270-->

The IPv4 checksum covers only the ==header==, not the payload; IPv6 removed even that (RFC 8200 §8.1), so payload integrity is left to ==TCP/UDP== checksums.
<!--SR:!2026-10-20,30,270!2026-09-01,3,250-->
