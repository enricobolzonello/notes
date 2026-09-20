---
up:
  - "[[OSI Model describes network communication in 7 layers from physical bits to application data]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
TLS gives you a secure channel over a reliable transport (TCP). That "secure channel" is exactly three guarantees:

- **Confidentiality** — encryption, so an eavesdropper on the wire sees gibberish.
- **Integrity** — a MAC/AEAD tag detects any tampering with the bytes.
- **Authentication** — you know *who* you're talking to (usually the server proves its identity via a [[A certificate authenticates a Diffie-Hellman exchange by signing the handshake transcript|certificate]]; optionally the client too).

Dropping authentication is the classic mistake: encryption alone is useless if you might be encrypting to an attacker (a man-in-the-middle). TLS does **not** provide delivery or ordering — that's TCP's job. TLS assumes a reliable, ordered byte stream already exists underneath it.

# See also
- [[OSI Model describes network communication in 7 layers from physical bits to application data]] — TLS sits between the Transport layer (4) and Application layer (7); it secures the application data that flows over the reliable stream TCP provides
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — how confidentiality is actually delivered: asymmetric crypto agrees on a key, symmetric crypto encrypts the data
- [[A certificate authenticates a Diffie-Hellman exchange by signing the handshake transcript]] — the authentication guarantee comes from here: without it, you have a private channel to *someone* but no idea who
- [[IP promises nothing — it is best-effort and never reports delivery outcome]] — the "reliable, ordered stream" TLS assumes underneath is itself manufactured above IP, which promises none of it

# References
- https://datatracker.ietf.org/doc/html/rfc8446

# Questions
#flashcards/software-engineering/tls

What three guarantees does a TLS secure channel provide?::Confidentiality (encryption), integrity (tampering detected via MAC/AEAD), and authentication (you know who you're talking to)
<!--SR:!2026-08-30,1,230-->

TLS relies on ==TCP== to provide delivery and ordering — it does not provide reliability itself.
<!--SR:!2026-09-01,3,250-->

Why is encryption without authentication useless in TLS?::Without authentication you might be encrypting to a man-in-the-middle instead of the real server
<!--SR:!2026-09-01,3,250-->
