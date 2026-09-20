---
up:
  - "[[Sequence numbers make a gap in a stream proof of loss that names what was lost]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
Sequence numbers only work if both sides agree where the stream starts. Each side must send its **initial sequence number** (ISN) *and confirm receipt of the peer's* — because the message carrying an ISN can be dropped like anything else, and numbering from an ISN the peer never learned makes every later ACK nonsense.

RFC 9293 §3.4.1 states this as four obligations. Naively four messages — but messages 2 and 3 both travel server→client at the same moment, so they combine into one **SYN-ACK**:

$$\text{SYN}(\text{ISN}_A) \rightarrow \text{SYN-ACK}(\text{ISN}_B,\ \text{ack } \text{ISN}_A) \rightarrow \text{ACK}(\text{ack } \text{ISN}_B)$$

Two messages fail: the last would be the server's SYN-ACK with nothing after it, so the server allocates buffers and numbers from an ISN the client may never have received. The third message closes exactly that loop, and also resolves the duplicate case — the server can't distinguish a fresh SYN from a delayed old duplicate, so it demands confirmation against its own freshly chosen ISN.

> The connection **is** this agreement. Nothing was reserved in the network.

Three consequences: **ISNs are random, not zero** (RFC 6528) — predictable ISNs let an off-path attacker who knows only the 4-tuple forge and inject segments; the handshake **costs a full RTT** before any data moves (why HTTP/2 reuses connections and QUIC fuses transport with TLS); and half-open state is attackable (**SYN flood**), mitigated by SYN cookies. Closing is per-direction (a FIN each way), and the first closer waits in **TIME_WAIT** for $2\times\text{MSL}$ so delayed duplicates expire and a lost final ACK can be re-sent.

# See also
- [[Sequence numbers make a gap in a stream proof of loss that names what was lost]] — the handshake exists solely to agree on the sequence-space these numbers live in
- [[A network connection is identified by a 4-tuple, not a port]] — the handshake establishes the state indexed by the 4-tuple; the connection is that agreement, held only at the endpoints
- [[A certificate authenticates a Diffie-Hellman exchange by signing the handshake transcript]] — TLS layers its own authenticated handshake on top of this one; QUIC fuses the two to reclaim the RTT
- [[TLS uses asymmetric crypto to bootstrap a shared key, then symmetric crypto for bulk data]] — the full-RTT cost here is why TLS+TCP handshakes are collapsed together in modern stacks
- [[A cumulative ACK N means "I have everything through N"]] — the ACKs that follow are meaningless without the ISN agreement this handshake produces

# References
- https://datatracker.ietf.org/doc/html/rfc9293#section-3.4.1
- https://datatracker.ietf.org/doc/html/rfc6528

# Questions
#flashcards/software-engineering/networking

What is the three-way handshake actually agreeing on?::Both sides' initial sequence numbers (each sent and confirmed) — sequence-space agreement, plus injection resistance from random ISNs
<!--SR:!2026-09-03,2,230-->

Why does a two-message handshake fail?::The server would allocate state and number from an ISN the client may never have received; the third message confirms the server's ISN and closes that loop
<!--SR:!2026-09-01,3,250-->

TCP ISNs are ==random==, not zero (RFC 6528), because predictable ISNs let an off-path attacker who knows the 4-tuple ==forge and inject== segments.
<!--SR:!2026-09-01,3,250!2026-09-02,1,210-->

Why does the first side to close wait in TIME_WAIT for 2×MSL?::So delayed duplicate segments expire before the 4-tuple is reused, and a lost final ACK can be re-sent
<!--SR:!2026-09-20,0,190-->
