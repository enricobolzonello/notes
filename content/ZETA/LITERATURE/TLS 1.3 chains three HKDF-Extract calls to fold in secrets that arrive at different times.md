---
up:
  - "[[HKDF has two operations, Extract whitens messy entropy and Expand clones one key into many]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
TLS 1.3 does not run a single HKDF-Extract on the DH secret. It runs **three Extracts in a chain**:

$$\text{Early Secret} = \text{Extract}(0,\; PSK)$$
$$\text{Handshake Secret} = \text{Extract}(\text{derived}_{\text{Early}},\; Z_{\text{DHE}})$$
$$\text{Master Secret} = \text{Extract}(\text{derived}_{\text{Handshake}},\; 0)$$

The reason: TLS has **more than one source of secret**, and they arrive at **different times** — an optional **PSK** (from a resumption ticket or configured out-of-band) and the fresh **(EC)DHE** secret `Z`. A single Extract can only ingest one input keying material (IKM).

So TLS uses a **ratchet**: each stage feeds the *previous stage's output as the salt* for the next Extract, and mixes in *the next secret* as the IKM:
- **Early Secret** — mixes in the PSK (or zeros if none).
- **Handshake Secret** — mixes in the DH secret `Z`; now there's enough to derive handshake keys.
- **Master Secret** — mixes in nothing new (IKM = 0), just advances the ratchet to a final secret for application keys.

The final Master Secret therefore depends on **every** input mixed in along the way, and because each stage is a one-way HMAC, the ratchet cannot be run backward. (The `derived` step between stages is just an Expand turning one stage's output into a proper salt for the next — ratchet plumbing.)

# See also
- [[HKDF has two operations, Extract whitens messy entropy and Expand clones one key into many]] — the chain is nothing but Extract applied three times; each link is one HKDF-Extract call
- [[Transcript-binding welds derived keys to the exact handshake, detecting tampering and downgrade]] — the traffic secrets pulled out of the Handshake/Master secrets are transcript-bound as they're derived
- [[TLS 1.3 0-RTT trades forward secrecy and replay protection for a saved round trip]] — 0-RTT keys come from the *Early* Secret, i.e. before `Z` is mixed in at the Handshake stage — the reason 0-RTT lacks forward secrecy
- [[TLS KeyUpdate is a one-way HKDF-Expand ratchet giving forward secrecy within a connection]] — the same one-way HMAC ratchet idea, reused later for mid-connection key rotation

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-7.1

# Questions
#flashcards/software-engineering/tls

Why does TLS 1.3 chain three HKDF-Extract calls instead of one?::It has multiple secret inputs (optional PSK + the DH secret) that arrive at different times, and each Extract can absorb only one IKM — the ratchet folds them in stage by stage
<!--SR:!2026-08-30,1,230-->

In the TLS 1.3 key schedule, which secret is mixed in at the Handshake Secret stage?::The (EC)DHE shared secret Z
<!--SR:!2026-08-30,1,230-->

The Early → Handshake → Master chain uses each stage's output as the ==salt== of the next Extract, mixing in the next secret as the IKM.
<!--SR:!2026-08-30,1,230-->
