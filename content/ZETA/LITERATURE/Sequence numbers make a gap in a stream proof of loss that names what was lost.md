---
up:
  - "[[Every guarantee above IP is manufactured by state at the two endpoints]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
Retransmission-on-timeout answers *drop*. But a timeout can only fire on **silence**, and silence is ambiguous — the data may have arrived with the ACK lost, or everything arrived late and the timer was impatient. So retransmission *manufactures* duplicates on top of the ones IP already creates.

Acknowledgments must therefore name *what* is acknowledged, and the receiver must detect duplicates and place early arrivals. One mechanism solves all three: **label each byte with its position in the stream.**

Why positions and not timestamps — this is the crux. Timestamps are **sparse**: transmissions stamped $t=1,2,4$ are ambiguous (was there a $t=3$, or nothing to send?). Byte positions are **dense**: bytes $0$–$99$, $100$–$199$, $300$–$399$ prove $200$–$299$ are missing *and must exist*, because position 300 is unreachable without passing 299.

> **Because positions in a stream are dense, a gap in positions is proof of loss, and it names precisely what was lost.**

Three of IP's failure modes collapse into this one mechanism:
- **drop** — a gap reveals it; retransmit exactly those bytes
- **reorder** — an early arrival sits past the gap; buffer until it fills
- **duplicate** — positions already held are discarded

Ordering and deduplication were never separately designed — that's the compression.

# See also
- [[Every guarantee above IP is manufactured by state at the two endpoints]] — sequence numbers are the first concrete guarantee built from endpoint-held state (a buffer + a counter)
- [[IP promises nothing — it is best-effort and never reports delivery outcome]] — the drop/reorder/duplicate this mechanism repairs are exactly IP's silent failure modes
- [[A cumulative ACK N means "I have everything through N"]] — the acknowledgment scheme built directly on top of these byte positions
- [[The three-way handshake is agreement on sequence-space plus injection resistance]] — sequence numbers only work if both sides first agree where the stream's numbering starts
- [[An AEAD record nonce is the static IV XOR the record sequence number]] — TLS reuses a per-record sequence number the same way, exploiting that the reliable stream lets both sides count in lockstep

# References
- https://datatracker.ietf.org/doc/html/rfc9293

# Questions
#flashcards/software-engineering/networking

Why does labeling bytes by stream position (not timestamps) let a receiver prove and name loss?::Positions are dense — a gap in positions must exist and names exactly which bytes are missing; timestamps are sparse and ambiguous
<!--SR:!2026-09-01,3,250-->

Which three IP failure modes collapse into the single sequence-number mechanism?::Drop (a gap → retransmit those bytes), reorder (early arrival buffered past the gap), and duplicate (already-held positions discarded)
<!--SR:!2026-09-21,1,210-->

Retransmission itself ==manufactures duplicates==, because a timeout fires on ambiguous silence — the data may have arrived with only the ACK lost.
<!--SR:!2026-09-21,1,190-->
