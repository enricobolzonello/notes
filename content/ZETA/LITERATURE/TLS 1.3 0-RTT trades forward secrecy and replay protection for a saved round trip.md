---
up:
  - "[[TLS 1.3 chains three HKDF-Extract calls to fold in secrets that arrive at different times]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
A normal TLS 1.3 handshake costs one round trip before the client can send data. If the client has a **PSK** from a previous session (a resumption ticket), it already shares a secret with the server — so it can send application data (**"early data"**) immediately, in its very first flight, encrypted right away. Zero round trips before useful data: **0-RTT**.

The early-data key is derived from the **Early Secret**:

$$\text{client\_early\_traffic\_secret} = \text{Derive-Secret}(\text{Early Secret},\; \texttt{"c e traffic"},\; \text{ClientHello})$$

And crucially, **Early Secret = Extract(0, PSK)** — derived from the **PSK alone**, *before* the ephemeral DH secret `Z` is mixed in (that happens at the Handshake Secret stage). Both weaknesses of 0-RTT fall directly out of this one fact:

1. **No forward secrecy.** Normal TLS gets forward secrecy from the *ephemeral* DH keys being discarded. But the PSK is long-lived. If an attacker records the 0-RTT traffic and later compromises the PSK, they can decrypt that early data — no ephemeral secret ever protected it.

2. **Replayable.** Normal TLS binds the client's data to a *fresh, server-chosen* value before the server acts. But 0-RTT data is a function of PSK + ClientHello only — sent before the server contributes any freshness. A network attacker can capture and resend the whole early-data flight, and the server can't cryptographically distinguish a replay from the original.

Hence the spec is blunt: 0-RTT replay **cannot be cryptographically prevented**, only *mitigated* — restrict early data to **idempotent** operations, use single-use tickets, or a bounded-window replay cache.

# See also
- [[TLS 1.3 chains three HKDF-Extract calls to fold in secrets that arrive at different times]] — 0-RTT's weakness is literally *which stage of the chain* it derives from: the Early Secret, before `Z` is mixed in
- [[TLS KeyUpdate is a one-way HKDF-Expand ratchet giving forward secrecy within a connection]] — the forward secrecy KeyUpdate provides is exactly what 0-RTT early data lacks
- [[A certificate authenticates a Diffie-Hellman exchange by signing the handshake transcript]] — 0-RTT skips the fresh ephemeral DH contribution, which is why it loses the freshness that normally binds data to the session
- [[Reliability means preventing faults from causing failures]] — the idempotency requirement for 0-RTT is the same at-least-once concern that appears with retransmission: the app layer must tolerate repeats

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-2.3

# Questions
#flashcards/software-engineering/tls

What single design choice causes 0-RTT to lack both forward secrecy and replay protection?::Its early key comes from the Early Secret (PSK alone) before the ephemeral DH secret is mixed in — so no forward secrecy, and no server freshness yet, so it can be replayed
<!--SR:!2026-08-30,1,230-->

Why can 0-RTT early data be replayed?::It's a function of PSK + ClientHello only, sent before the server contributes any fresh value, so a captured flight can be resent and looks identical to the original
<!--SR:!2026-08-30,1,230-->

0-RTT replay cannot be cryptographically prevented, only ==mitigated== — e.g. restricting early data to ==idempotent== operations, single-use tickets, or a replay window.
<!--SR:!2026-09-02,4,270!2026-09-01,3,250-->
