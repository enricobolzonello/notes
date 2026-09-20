---
up:
  - "[[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]]"
tags:
  - atomic
created: 2026-08-29 14:57
---
Diffie-Hellman gives two parties a shared secret over a visible wire (each sends a public value, each combines its own private value with the other's public value to compute the same secret, which is never transmitted). But DH alone is **unauthenticated**: an active man-in-the-middle can run a separate DH exchange with each side and sit in the middle.

The certificate plugs the gap without ever touching the secret:

- The server **signs the handshake transcript** — which includes its ephemeral DH public value — with the private key corresponding to the public key in its certificate.
- The client **verifies that signature** against the certificate (and verifies the certificate against a trusted CA).

So the certificate does not encrypt anything and does not carry the shared secret. It **authenticates the DH exchange**, binding "the party I just did DH with" to "the identity the CA vouched for." Without it, you'd have a private channel — but to *someone unknown*.

# See also
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — this is the authentication half of that split: the cert's private key signs, proving identity, while DH agrees the key
- [[TLS provides confidentiality, integrity and authentication over a reliable stream]] — this mechanism is what actually delivers the *authentication* guarantee of the three
- [[Transcript-binding welds derived keys to the exact handshake, detecting tampering and downgrade]] — the transcript being signed here is the same transcript that gets folded into key derivation; both defend the handshake against tampering
- [[The three-way handshake is agreement on sequence-space plus injection resistance]] — TLS's authenticated handshake layers on top of TCP's; QUIC fuses the two into one exchange to reclaim the round trip

# References
- https://datatracker.ietf.org/doc/html/rfc8446#section-4.4.3

# Questions
#flashcards/software-engineering/tls

How does a certificate authenticate a Diffie-Hellman exchange?::The server signs the handshake transcript (including its DH public value) with its certificate's private key; the client verifies that signature against the cert
<!--SR:!2026-08-30,1,230-->

Why is Diffie-Hellman alone insufficient for TLS?::It is unauthenticated — a man-in-the-middle can run a separate DH exchange with each side
<!--SR:!2026-08-30,1,230-->

Does the certificate encrypt or carry the DH shared secret?::No — it only authenticates the exchange by signing the transcript; the secret is never encrypted with or carried by the cert
<!--SR:!2026-08-30,1,230-->
