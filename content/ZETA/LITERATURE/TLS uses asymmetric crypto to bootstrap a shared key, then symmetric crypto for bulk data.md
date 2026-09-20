---
up:
  - "[[TLS provides confidentiality, integrity and authentication over a reliable stream]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
TLS uses both kinds of crypto, with a clean division of labor:

- **Asymmetric (public-key) crypto** — used *only during the handshake* to authenticate the peer and to agree on a shared secret (e.g. RSA, or ephemeral Diffie-Hellman).
- **Symmetric crypto** — used afterward to encrypt *all* the application data (e.g. AES-GCM).

Why split it this way? Two facts force it:
- Asymmetric operations are orders of magnitude **slower per byte**, so you'd never use them for bulk data.
- Symmetric ciphers are fast but need both sides to **already share a key** — and you can't just send a key over an open wire.

So asymmetric crypto solves the *bootstrapping* problem (agree on a key safely, over a visible channel), and symmetric crypto does the heavy lifting once the key exists.

# See also
- [[TLS provides confidentiality, integrity and authentication over a reliable stream]] — this split is *how* TLS delivers confidentiality: the handshake sets up the key, symmetric crypto encrypts the stream
- [[HKDF has two operations, Extract whitens messy entropy and Expand clones one key into many]] — the shared secret from the handshake is raw and messy; HKDF turns it into the actual symmetric keys
- [[A certificate authenticates a Diffie-Hellman exchange by signing the handshake transcript]] — the asymmetric half is where authentication happens, binding the key agreement to a verified identity
- [[Head-of-line blocking is the price of a single connection-wide byte order]] — QUIC fuses this key agreement into its transport handshake (handshake collapse) to get 1-RTT, or 0-RTT on resumption

# References
- https://datatracker.ietf.org/doc/html/rfc8446

# Questions
#flashcards/software-engineering/tls

What is the division of labor between asymmetric and symmetric crypto in TLS?::Asymmetric crypto handles the handshake (authentication + agreeing on a shared key); symmetric crypto encrypts all the application data
<!--SR:!2026-09-02,4,270-->

Why isn't asymmetric crypto used to encrypt the bulk application data?::It is orders of magnitude slower per byte than symmetric crypto
<!--SR:!2026-09-01,3,250-->

Symmetric crypto is fast but requires both sides to ==already share a key==, which is the bootstrapping problem asymmetric crypto solves.
<!--SR:!2026-09-01,3,250-->
