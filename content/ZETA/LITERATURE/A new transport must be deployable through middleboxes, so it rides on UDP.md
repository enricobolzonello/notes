---
up:
  - "[[Head-of-line blocking is the price of a single connection-wide byte order]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
The end-to-end principle predicts you can invent a transport, give it a fresh IP protocol number, and ship it by changing only the two endpoints. **That prediction is false** — it's the end-to-end principle's leak (per-flow state inside the network) becoming the binding constraint.

NATs must read and rewrite port numbers, and they only know where ports live in **TCP and UDP** headers. An unknown protocol number has no parseable ports, so a NAT drops it; firewalls permit only known protocols. Your protocol fails on a large fraction of real paths regardless of both endpoints supporting it perfectly.

**SCTP** (protocol 132) is the evidence: it offered per-stream ordering — the exact fix [[@QUICTransportProtocol|QUIC]] later shipped — *years* earlier, and never deployed. But "it died of middlebox blocking" is too tidy: middlebox opacity was one cause among several of comparable weight — Windows never shipped native support, browsers exposed no API, and once HTTP/2 and QUIC-over-UDP solved the same problems without a new protocol number, demand evaporated. DCCP (protocol 33) tells the same story.

> A new transport must be **deployable through existing middleboxes**, **shippable without OS-vendor cooperation**, and **reachable from application code**. A new IP protocol number fails all three. **UDP passes all three.**

[[@QUICTransportProtocol|QUIC]]'s 8 bytes of UDP header aren't waste — they're the admission fee. And **ossification** closes the loop: middleboxes inspect and "helpfully" rewrite TCP headers, freezing TCP; QUIC's answer was to encrypt almost everything.

> **Anything you leave visible on the wire, the network will eventually depend on, and then you can never change it.**

# See also
- [[Head-of-line blocking is the price of a single connection-wide byte order]] — QUIC solves HOL blocking, but *this* note is why it had to be built on UDP rather than as a new IP-level transport
- [[Every guarantee above IP is manufactured by state at the two endpoints]] — this is that principle's leak (NAT's in-network per-flow state) becoming the binding constraint on new protocols
- [[A network connection is identified by a 4-tuple, not a port]] — NATs block unknown protocols precisely because they can't find the ports (4-tuple coordinates) they need to rewrite
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — the ossification lesson ("encrypt what you can't afford to have frozen") is why QUIC and TLS 1.3 encrypt nearly the whole header

# References
- https://datatracker.ietf.org/doc/html/rfc9260
- https://datatracker.ietf.org/doc/html/rfc9000

# Questions
#flashcards/software-engineering/networking

Why must a new transport ride on UDP rather than get its own IP protocol number?::It must be deployable through middleboxes, shippable without OS-vendor cooperation, and reachable from app code — a new IP protocol number fails all three (NATs/firewalls drop it); UDP passes all three
<!--SR:!2026-09-08,7,250-->

What does SCTP's failure to deploy illustrate?::A technically superior transport (per-stream ordering, years early) can still fail — middlebox opacity plus no OS/browser support, and later UDP-based solutions removed the demand
<!--SR:!2026-10-12,22,250-->

Ossification: anything you leave ==visible on the wire== the network eventually depends on, and then you can never change it — which is why QUIC encrypts almost the whole header.
<!--SR:!2026-09-03,2,230-->
