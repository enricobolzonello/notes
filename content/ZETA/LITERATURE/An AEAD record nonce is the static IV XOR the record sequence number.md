---
up:
  - "[[Transcript-binding welds derived keys to the exact handshake, detecting tampering and downgrade]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
A traffic secret (e.g. `client_application_traffic_secret_0`, a 32-byte pseudorandom value) isn't yet usable by AES-GCM. AEAD needs two concrete things: a **key** and an **IV**. One more Expand each:

$$\text{write\_key} = \text{HKDF-Expand-Label}(\text{traffic\_secret},\; \texttt{"key"},\; \text{""},\; \text{key\_len})$$
$$\text{write\_iv}  = \text{HKDF-Expand-Label}(\text{traffic\_secret},\; \texttt{"iv"},\;  \text{""},\; 12)$$

Two things to notice: the `"key"` and `"iv"` labels make the two outputs cryptographically independent (Expand clones by label), and the context is **empty** (`""`) — the transcript-binding already happened upstream when the secret was derived.

Now the per-record nonce. The IV is **not** the nonce; it's the ingredient the nonce is built from:

$$\text{nonce}_n = \text{write\_iv} \;\oplus\; n$$

where `n` is the **record sequence number** (0, 1, 2, …), a per-direction counter, left-padded to the IV length.

This is elegant for two reasons:
- **The sequence number is never sent.** It's *implicit*: both sides count records in order over the reliable TCP stream and independently compute the same nonce — zero bytes on the wire.
- **Every record gets a distinct nonce automatically**, because `n` increments each time.

The counter resets to 0 **each time the key changes** (handshake keys, application keys, each KeyUpdate epoch each start fresh at 0). That's safe because each epoch uses a *different key*, so (key, nonce) pairs still never collide.

# See also
- [[Transcript-binding welds derived keys to the exact handshake, detecting tampering and downgrade]] — the traffic secret consumed here was transcript-bound at derivation; this final key/iv Expand uses an empty context precisely because of that
- [[HKDF has two operations, Extract whitens messy entropy and Expand clones one key into many]] — key and iv are just two more Expand-by-label outputs of the same secret
- [[An AEAD nonce must be unique, not secret — reuse under one key is catastrophic]] — *why* the sequence counter matters: it guarantees uniqueness, which is the one property the nonce must have
- [[TLS KeyUpdate is a one-way HKDF-Expand ratchet giving forward secrecy within a connection]] — resetting the counter to 0 is safe only because KeyUpdate gives each epoch a fresh key
- [[Sequence numbers make a gap in a stream proof of loss that names what was lost]] — the record sequence number works for the same reason TCP's does: a reliable, ordered stream lets both sides count in lockstep without transmitting the counter

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-5.3

# Questions
#flashcards/software-engineering/tls

How is a TLS record's per-record nonce constructed?::write_iv XOR the record sequence number (an implicit per-direction counter 0,1,2,…)
<!--SR:!2026-09-01,3,250-->

Why is the record sequence number never sent on the wire?::Both sides count records in order over the reliable TCP stream, so each independently computes the same nonce
<!--SR:!2026-08-30,1,230-->

How are write_key and write_iv derived from a traffic secret?::Two HKDF-Expand-Label calls with labels "key"/"iv" and an empty context (the transcript was already bound upstream)
<!--SR:!2026-09-01,3,250-->

The record sequence counter resets to ==0== each time the key changes, which is safe because each epoch uses a ==different key==.
<!--SR:!2026-09-02,4,270!2026-09-01,3,250-->
