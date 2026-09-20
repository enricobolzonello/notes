---
up:
  - "[[TCP is a byte stream and UDP preserves datagram boundaries — opposite answers]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
A receiver holding bytes $300$–$399$ with $200$–$299$ missing delivers **nothing** — that's ordering working correctly. But if those bytes belong to two unrelated things (a stylesheet and an image multiplexed over one connection), the image sits complete and unusable, waiting on a stylesheet packet it has nothing to do with.

> **Head-of-line blocking** is not a bug. It's the unavoidable price of a single connection-wide byte order.

HTTP's three attempts to escape it:
- **HTTP/1.1** — one request at a time; pipelining required in-order responses, so a slow response blocked the rest. Browsers opened ~6 parallel connections instead.
- **HTTP/2** — generalises framing into typed, length-prefixed **frames** tagged with a **stream ID**, so streams interleave over one connection (HPACK compresses headers). Fixes *application-level* blocking — but all streams still ride one TCP byte stream, so one TCP-level loss stalls everything. The blocking moved down a layer.
- **HTTP/3** — the only remaining move: leave TCP.

The real question is *"how do I avoid a shared order while keeping one connection?"*, and it has exactly one answer: **give each stream its own sequence space** — which is **impossible in TCP**, because TCP's sequence space *is* a single flat byte stream (the decision that bought packaging freedom). No option can subdivide it.

That impossibility is the whole story of **QUIC** (RFC 9000): a full transport in user space over UDP, giving per-stream ordering. Three further wins: **handshake collapse** (transport + TLS 1.3 in one exchange, 1 RTT or 0 on resumption), **connection migration** (an explicit Connection ID survives WiFi→cellular, where a TCP 4-tuple would not), and **escaping ossification** (encrypting nearly the whole header so middleboxes can't inspect or "fix" it).

# See also
- [[TCP is a byte stream and UDP preserves datagram boundaries — opposite answers]] — TCP's single flat byte stream is *why* per-stream ordering is impossible; HOL blocking is that decision's cost surfacing
- [[TCP hands you a stream, so the application must frame its own messages]] — HTTP/2 generalises exactly this framing (typed, length-prefixed, stream-ID-tagged) to interleave streams
- [[A network connection is identified by a 4-tuple, not a port]] — a TCP connection *is* its 4-tuple, so it dies on address change; QUIC's Connection ID decouples identity from the 4-tuple
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — QUIC's handshake collapse fuses this TLS 1.3 key agreement into the transport handshake for 1-RTT (or 0-RTT)
- [[TLS 1.3 0-RTT trades forward secrecy and replay protection for a saved round trip]] — QUIC's 0-RTT resumption inherits exactly this TLS 1.3 trade-off

# References
- https://datatracker.ietf.org/doc/html/rfc9000

# Questions
#flashcards/software-engineering/networking

What is head-of-line blocking and why isn't it a bug?::A complete message stalls waiting on an unrelated missing packet — it's the unavoidable price of a single connection-wide byte order, working as designed
<!--SR:!2026-09-01,3,250-->

Why can't TCP give each stream its own sequence space to avoid HOL blocking?::TCP's sequence space *is* a single flat byte stream (the decision that bought packaging freedom); no option can subdivide it
<!--SR:!2026-09-21,1,210-->

HTTP/2 fixes ==application-level== HOL blocking with stream-ID-tagged frames, but one ==TCP-level== loss still stalls all streams — so the blocking moved down a layer.
<!--SR:!2026-09-22,2,190!2026-09-20,0,210-->

Beyond per-stream ordering, name QUIC's three further wins.::Handshake collapse (1-RTT/0-RTT with TLS 1.3), connection migration (Connection ID survives address change), and escaping ossification (encrypted header)
<!--SR:!2026-08-30,1,230-->
