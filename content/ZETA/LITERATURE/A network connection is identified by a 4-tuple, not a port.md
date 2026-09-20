---
up:
  - "[[Every guarantee above IP is manufactured by state at the two endpoints]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
IP reaches a *machine*, but nothing runs "on a machine" — your browser, an SSH session, and a game client share one IP. So a demultiplexing field was invented: the **port**, 16 bits (0–65535). TCP and UDP maintain independent port spaces, so TCP 53 and UDP 53 are unrelated identifiers that happen to share a number.

But a port does **not** identify a connection. Destination port 443 is identical for all clients of a web server; source IP isn't enough either (two browser tabs on one laptop share an IP). The identity is all four coordinates:

> **(local IP, local port, remote IP, remote port)** — the **4-tuple**.

RFC 9293 phrases a connection as *a pair of sockets*, where a socket is one (IP, port) pair — two sockets, four numbers, same thing. A **listening** socket has only a local half; it isn't a connection, it's a standing offer to form them. Real kernels key on the **5-tuple**, adding the protocol number since TCP and UDP have separate port spaces.

This retroactively explains two things: the client needs *some* source port and doesn't care which, so the kernel grabs one from the **ephemeral** range (making each browser tab a distinct 4-tuple); and **NAT** works by rewriting exactly these coordinates with a table to reverse it — NAT is a 4-tuple rewriter.

# See also
- [[Every guarantee above IP is manufactured by state at the two endpoints]] — the connection state the endpoints hold is keyed by this 4-tuple; it's the identity under which all guarantees are tracked
- [[The three-way handshake is agreement on sequence-space plus injection resistance]] — the handshake establishes the state indexed by this 4-tuple; the connection *is* that agreement
- [[Head-of-line blocking is the price of a single connection-wide byte order]] — a TCP connection *is* its 4-tuple, so an address change (WiFi→cellular) kills it, which QUIC's Connection ID fixes
- [[An IP Address Identifies the Location of a Resource Within a Network]] — the IP is only two of the four coordinates; the port pair is what disambiguates programs and flows on the same host

# References
- https://datatracker.ietf.org/doc/html/rfc9293

# Questions
#flashcards/software-engineering/networking

What actually identifies a network connection, if not a port?::The 4-tuple: (local IP, local port, remote IP, remote port). RFC 9293 phrases it as a pair of sockets
<!--SR:!2026-09-02,4,270-->

Why isn't a port enough to identify a connection?::A server's destination port is identical for all clients, and one host's tabs share a source IP — only all four coordinates disambiguate
<!--SR:!2026-09-01,3,250-->

A ==listening== socket has only a local half — it's not a connection but a standing offer to form them.
<!--SR:!2026-08-30,1,230-->

NAT works by rewriting the ==4-tuple== (with a table to reverse it), which is why it's called a 4-tuple rewriter.
<!--SR:!2026-09-03,2,230-->
