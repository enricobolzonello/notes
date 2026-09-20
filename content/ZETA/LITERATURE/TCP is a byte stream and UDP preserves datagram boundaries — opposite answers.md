---
up:
  - "[[Every guarantee above IP is manufactured by state at the two endpoints]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
Underneath, everything is packets. Whether the *application* sees those packet boundaries is a genuine design choice, and it hinges on one cost:

> **Preserving message boundaries forfeits the freedom to merge small writes and split large ones.**

A protocol that must preserve boundaries can't batch two small writes into one segment (that would fuse two messages) or split a large write without extra machinery. Efficiency comes precisely from that freedom — 1 byte of payload with 40 bytes of header is 2% efficient — so boundaries cost throughput.

TCP and UDP answer the same question **oppositely**:

- **TCP discards boundaries** and buys the freedom. It presents a **byte stream**: two 100-byte writes may arrive as one read of 200, or 3 then 197, or any split. Its sequence numbers count *bytes*, not messages — the decision is visible in the header. TCP is not losing information it promised to keep.
- **UDP preserves boundaries** by doing nothing. One `sendto()` = one datagram = one `recvfrom()`. Boundaries survive through the absence of interference.

So UDP is **not "TCP minus reliability"** — it's **"IP plus ports"** (RFC 768: four fields — source port, destination port, length, checksum). That makes it the natural substrate for a custom transport: no structure to fight, and unlike raw IP it traverses NATs. (Fragmentation is not an exception: if a datagram exceeds the path MTU, IP fragments it but reassembles at the *final destination* before handing up one whole datagram — never a piece.)

# See also
- [[Every guarantee above IP is manufactured by state at the two endpoints]] — the stream/datagram choice is one more endpoint-side decision about *which* guarantee to manufacture (a merged byte order, or preserved boundaries)
- [[TCP hands you a stream, so the application must frame its own messages]] — the direct consequence of TCP discarding boundaries: the application must re-impose them
- [[Head-of-line blocking is the price of a single connection-wide byte order]] — TCP's single byte stream (this decision) is exactly what forces one connection-wide order and makes per-stream ordering impossible
- [[A network connection is identified by a 4-tuple, not a port]] — UDP being "IP plus ports" means it adds only the port demux (the 4-tuple's port halves) on top of IP

# References
- https://datatracker.ietf.org/doc/html/rfc768
- https://datatracker.ietf.org/doc/html/rfc791

# Questions
#flashcards/software-engineering/networking

What is the cost of preserving message boundaries?::You forfeit the freedom to merge small writes and split large ones — the packaging freedom that gives throughput
<!--SR:!2026-09-01,3,250-->

How do TCP and UDP answer the "expose packet boundaries?" question?::Oppositely — TCP discards boundaries (a byte stream, counting bytes) to buy packaging freedom; UDP preserves them (one sendto = one recvfrom) by doing nothing
<!--SR:!2026-09-20,0,230-->

UDP is best described not as "TCP minus reliability" but as ==IP plus ports==.
<!--SR:!2026-09-21,1,190-->

If a UDP datagram exceeds the path MTU, IP fragments it but reassembles at the ==final destination==, so the app gets one whole datagram or nothing — never a piece.
<!--SR:!2026-09-09,8,250-->
