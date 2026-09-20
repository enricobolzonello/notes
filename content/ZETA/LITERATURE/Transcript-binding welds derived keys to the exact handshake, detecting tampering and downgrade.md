---
up:
  - "[[TLS 1.3 chains three HKDF-Extract calls to fold in secrets that arrive at different times]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
When TLS derives the actual traffic secrets, it doesn't just Expand with a plain label — it folds in the **transcript hash**, a hash of *every handshake message seen so far*, as the derivation context:

$$\text{client\_hs\_traffic\_secret} = \text{Derive-Secret}(\text{Handshake Secret},\; \texttt{"c hs traffic"},\; \text{Hash}(\text{transcript}))$$

where `Derive-Secret(secret, label, msgs)` = `HKDF-Expand-Label(secret, label, Hash(msgs), …)` — so `Hash(msgs)` goes into HKDF's `info` context.

This is what catches **downgrade and tampering**. Both sides independently hash the exact sequence of handshake bytes they saw and mix that hash into every key. So:

- If a client saw one transcript and the server saw a tampered one, they compute **different transcript hashes → different keys**.
- Different keys means the first encrypted message — the **Finished** message, a MAC over the transcript under these keys — **fails to verify**, and the handshake aborts.

The keys are cryptographically welded to the exact conversation that produced them. It's this transcript-binding across the whole key schedule — not the certificate signature alone — that prevents downgrade and injection.

Precision point: transcript-binding applies to the *secret-derivation* steps (the traffic secrets). The **final `key`/`iv` expansion uses an empty context** — the binding already happened upstream.

# See also
- [[TLS 1.3 chains three HKDF-Extract calls to fold in secrets that arrive at different times]] — the secrets being bound here are exactly the Handshake and Master secrets produced by that chain
- [[HKDF has two operations, Extract whitens messy entropy and Expand clones one key into many]] — transcript-binding is just Expand with `Hash(transcript)` supplied as the `info` context
- [[A certificate authenticates a Diffie-Hellman exchange by signing the handshake transcript]] — a second, complementary defense of the same transcript: the cert signs it, the key schedule binds keys to it
- [[An AEAD record nonce is the static IV XOR the record sequence number]] — the *next* step down: the transcript-bound secret is then expanded (empty context) into the concrete key and iv

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-7.1

# Questions
#flashcards/software-engineering/tls

How does folding the transcript hash into key derivation catch a tampered or downgraded handshake?::A tampered handshake makes the two sides hash different transcripts → they derive different keys → the Finished MAC fails and the handshake aborts
<!--SR:!2026-09-01,3,250-->

What message actually fails when transcript-bound keys mismatch?::The Finished message — a MAC over the transcript computed under the derived keys
<!--SR:!2026-08-30,1,230-->

Transcript-binding is applied when deriving the ==traffic secrets==, but the final key/iv expansion uses an ==empty== context because the binding already happened upstream.
<!--SR:!2026-08-30,1,230!2026-09-01,3,250-->
