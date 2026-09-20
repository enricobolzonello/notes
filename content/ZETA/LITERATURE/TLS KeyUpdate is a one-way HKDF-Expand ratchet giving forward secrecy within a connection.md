---
up:
  - "[[An AEAD nonce must be unique, not secret — reuse under one key is catastrophic]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
Two forces push TLS to rotate keys mid-connection: **nonce exhaustion** (the sequence counter is finite; you must get a fresh key before risking nonce reuse) and **limiting blast radius** (contain the damage if a key is compromised).

KeyUpdate does it with one Expand:

$$\text{app\_traffic\_secret}_{N+1} = \text{HKDF-Expand-Label}(\text{app\_traffic\_secret}_N,\; \texttt{"traffic upd"},\; \text{""},\; \text{Hash.len})$$

Take the current traffic secret, Expand it with the label `"traffic upd"`, get the next one; then derive fresh `key`/`iv` from it and reset the sequence counter to 0. No new Diffie-Hellman happens — that's what makes it cheap. The context is empty (`""`); it's a pure ratchet.

The elegant part is that **it's one-way**, because HKDF-Expand is built on HMAC:
- From secret$_N$ you can compute secret$_{N+1}$.
- From secret$_{N+1}$ you **cannot** run backward to secret$_N$.

Consequence: if an attacker compromises secret$_{N+1}$, all traffic encrypted under secret$_N$ and earlier stays safe. That's **forward secrecy within a single connection**, achieved with nothing but another Expand — the same one-way HMAC property seen in the Extract chain.

# See also
- [[An AEAD nonce must be unique, not secret — reuse under one key is catastrophic]] — nonce exhaustion is one of the two triggers: rotate the key before the counter climbs high enough to risk reuse
- [[An AEAD record nonce is the static IV XOR the record sequence number]] — after KeyUpdate the counter resets to 0, safe because the epoch now has a fresh key
- [[TLS 1.3 chains three HKDF-Extract calls to fold in secrets that arrive at different times]] — the same one-way HMAC ratchet idea, here applied to key rotation instead of combining secret sources
- [[HKDF has two operations, Extract whitens messy entropy and Expand clones one key into many]] — KeyUpdate is literally one HKDF-Expand-Label call with the label "traffic upd"

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-4.6.3

# Questions
#flashcards/software-engineering/tls

What does TLS KeyUpdate do, mechanically?::Expands the current traffic secret one-way (label "traffic upd") into the next secret, then derives fresh key/iv and resets the sequence counter — no new Diffie-Hellman
<!--SR:!2026-08-30,1,230-->

Why does KeyUpdate give forward secrecy within a connection?::HKDF-Expand is one-way (HMAC), so compromising a newer secret can't reveal older ones — past traffic stays safe
<!--SR:!2026-08-30,1,230-->

What two problems does KeyUpdate solve?::Nonce exhaustion (fresh key resets the counter) and limiting blast radius if a key is compromised
<!--SR:!2026-09-01,3,250-->
