---
up:
  - "[[An AEAD record nonce is the static IV XOR the record sequence number]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
An AEAD nonce's security requirement is **uniqueness, not secrecy**. It's right there in the name — *number used once*, not *number kept secret*.

The nonce is fully public: an eavesdropper can count records (0, 1, 2, …) and knows the structure `nonce = write_iv XOR n`. That buys them nothing, because AEAD security rests entirely on the secrecy of the **key**, not the nonce. Even knowing the nonce, without `write_key` an attacker can neither decrypt nor forge.

| Ingredient | Secret? | Must be unique? |
|---|---|---|
| `write_key` | **Yes** — security rests on this | no |
| nonce (`iv ⊕ n`) | **No** — attacker may know it fully | **Yes** — reuse under one key is fatal |

The catastrophe is **reuse**, and it's a *sender-side* fault: if the same (key, nonce) pair ever encrypts two different records, AEAD collapses:
- An attacker can XOR the two ciphertexts to cancel the keystream and recover the plaintext XOR.
- For AES-GCM, reuse also leaks the internal authentication key, letting the attacker **forge arbitrary messages** that pass the integrity check.

So confidentiality *and* integrity fall together. The whole sequence-counter scheme exists to make sender-side nonce reuse impossible — not to hide the nonce.

# See also
- [[An AEAD record nonce is the static IV XOR the record sequence number]] — the counter construction is exactly the mechanism that guarantees the uniqueness this note says is mandatory
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — security resting on the *key's* secrecy is the same principle: the symmetric key is the secret, derived from the handshake
- [[TLS KeyUpdate is a one-way HKDF-Expand ratchet giving forward secrecy within a connection]] — one reason to rotate keys is nonce exhaustion: rather than risk reuse when the counter climbs high, get a fresh key

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-5.3

# Questions
#flashcards/software-engineering/tls

What is the security requirement on an AEAD nonce — secret or unique?::Unique, not secret. It's a "number used once"; an attacker knowing it is harmless because security rests on the key's secrecy
<!--SR:!2026-09-01,3,250-->

What happens if a (key, nonce) pair is reused under AES-GCM?::Catastrophe — the attacker can XOR the ciphertexts to recover plaintext XOR and can leak the auth key to forge messages; confidentiality and integrity both collapse
<!--SR:!2026-09-01,3,250-->

Nonce reuse is a ==sender-side== fault: the danger is the same (key, nonce) encrypting two records, not an attacker learning the nonce.
<!--SR:!2026-09-01,3,250-->
