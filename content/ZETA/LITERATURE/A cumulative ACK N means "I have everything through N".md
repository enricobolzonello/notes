---
up:
  - "[[Sequence numbers make a gap in a stream proof of loss that names what was lost]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
"ACK $N$" means **"I have everything through $N$"** — one number naming a contiguous prefix of the stream. So a receiver holding bytes $0$–$199$ and $300$–$399$ must acknowledge **199**, not 399, even though it physically holds the later bytes.

Acknowledging 399 would assert that $200$–$299$ arrived. The sender would then clear those bytes from its buffer, and they'd be lost permanently — both sides believing success. The cumulative ACK's contiguity is what makes it safe.

Two things fall out of this design:

- The receiver re-sends ACK 199 as more out-of-order data arrives. Those **duplicate ACKs** tell the sender data is still flowing but a specific gap isn't filling — three duplicate ACKs trigger **fast retransmit** without waiting for the timer (RFC 5681 §3.2). A limitation became a loss signal.
- The receiver can't *say* it already holds $300$–$399$, risking needless retransmission of those bytes. Hence **SACK** (RFC 2018), a later option that reports the islands past the gap.

Once the gap fills, the ACK jumps 199 → 399 in a single step.

# See also
- [[Sequence numbers make a gap in a stream proof of loss that names what was lost]] — cumulative ACKs are built directly on those dense byte positions; ACK N is a claim about the prefix up to position N
- [[Flow control protects the receiver, congestion control protects the network]] — the same ACKs that acknowledge data also carry the advertised receive window, so acknowledgment and flow control share one channel
- [[The three-way handshake is agreement on sequence-space plus injection resistance]] — cumulative ACKs are meaningless until both sides agree on the initial sequence numbers the counting starts from

# References
- https://datatracker.ietf.org/doc/html/rfc5681#section-3.2
- https://datatracker.ietf.org/doc/html/rfc2018

# Questions
#flashcards/software-engineering/networking

What does a cumulative "ACK N" assert?::That the receiver has everything through byte N — a contiguous prefix; it cannot ACK past a gap even if it holds later bytes
<!--SR:!2026-09-30,10,270-->

Why can't a receiver ACK bytes it holds past a gap?::Doing so would assert the gap arrived; the sender would clear those bytes from its buffer and they'd be lost permanently
<!--SR:!2026-10-08,18,250-->

Three ==duplicate ACKs== signal a specific unfilled gap and trigger ==fast retransmit== without waiting for the timeout.
<!--SR:!2026-09-21,1,210!2026-09-27,7,250-->

What does SACK add on top of cumulative ACKs?::A way to report the islands of data already held past the gap, avoiding needless retransmission
<!--SR:!2026-09-02,1,210-->
