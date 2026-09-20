---
up:
  - "[[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
HKDF is the single tool underneath the entire TLS 1.3 key schedule. It has exactly two operations, each solving a distinct problem, both built on HMAC (a keyed hash producing fixed-length, pseudorandom, unforgeable output).

Why two operations? A raw Diffie-Hellman secret `Z` can't be used directly as an AES key for two separate reasons:
- **It's not shaped like a key.** `Z` has mathematical structure (e.g. a curve point coordinate); its bits are biased and correlated, not uniformly random.
- **You need many keys, not one.** Each direction, each phase, and each rotation needs its own independent key.

The two operations map exactly onto these:

**Extract — the whitening step.**
$$\text{HKDF-Extract}(salt, IKM) = \text{HMAC}(salt, IKM) \rightarrow PRK$$
HMAC acts as a randomness extractor: feed it biased, structured input keying material (IKM), and the output PRK is statistically indistinguishable from uniform. Extract *compresses and cleans* — its input can be **longer** than its output. It never stretches.

**Expand — the cloning step.**
$$\text{HKDF-Expand}(PRK, info, L) \rightarrow L \text{ bytes}$$
Iterated HMAC keyed by PRK, so it can produce output of **any** length `L` (this is the stretch step). The `info` label makes outputs *cryptographically independent*: knowing the output for `info = "client key"` tells you nothing about `info = "server key"`.

So: **Extract** (messy secret → one clean key), then **Expand** (one clean key → many labeled keys). Everything in the TLS key schedule is one of these two calls.

# See also
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — HKDF is what turns the raw asymmetric-agreed secret into the actual symmetric keys used for bulk data
- [[TLS 1.3 chains three HKDF-Extract calls to fold in secrets that arrive at different times]] — the key schedule is just Extract applied repeatedly in a chain
- [[Transcript-binding welds derived keys to the exact handshake, detecting tampering and downgrade]] — transcript-binding is HKDF-Expand with the handshake hash placed in the `info` context
- [[An AEAD record nonce is the static IV XOR the record sequence number]] — the concrete key and IV each come from one more Expand call on the traffic secret
- [[A Hash Function Must Be Deterministic, Uniform, and Fast — FNV-1a Is One Example]] — HKDF's uniformity goal echoes what any hash wants; here HMAC is used specifically as a *randomness extractor*

# References
- https://datatracker.ietf.org/doc/html/rfc5869

# Questions
#flashcards/software-engineering/tls

What are HKDF's two operations and what does each do?::Extract whitens/compresses messy entropy into one clean fixed-length key (PRK); Expand stretches that key into many independent keys, one per label
<!--SR:!2026-08-30,1,230-->

Why can't a raw Diffie-Hellman secret be used directly as an AES key?::Its bits are biased/structured (not uniformly random), AND one secret must become many independent keys — two separate problems
<!--SR:!2026-08-30,1,230-->

HKDF-Extract can take input ==longer== than its output — it compresses and whitens, it does not stretch.
<!--SR:!2026-09-02,4,270-->

In HKDF-Expand, what makes two outputs cryptographically independent?::Using a different {{info label}} for each — same PRK, different label, independent output
<!--SR:!2026-08-30,1,230-->
