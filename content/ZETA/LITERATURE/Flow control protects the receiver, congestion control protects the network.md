---
up:
  - "[[Every guarantee above IP is manufactured by state at the two endpoints]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
Nothing in reliability or ordering tells the sender **how fast** to send. Two separate things can be overwhelmed, and holding them apart is the whole lesson.

**Flow control protects the receiver.** Data lands in a buffer awaiting `read()`; a fast server streaming to a slow phone overflows it. But the receiver *knows* its free space and is already sending ACKs, so the fix is nearly free: advertise free buffer space in every ACK — the **receive window** (`rwnd`). A zero window stops the sender precisely, without loss.

**Congestion control protects the network.** A receiver advertising 10 MB says nothing about a slow link mid-path whose router queue overflows and drops silently. This is a genuinely separate bottleneck: a phone on a slow link has huge `rwnd` but tiny capacity; a slow app on fibre has the reverse. Neither number predicts the other, so no single mechanism can respect both:

$$\text{data in flight} \le \min(\text{rwnd},\, \text{cwnd})$$

The asymmetry that makes congestion control hard: **`rwnd` is *told* to the sender by the party who knows it; `cwnd` cannot be — nobody knows the path's capacity.** It's shared, changing, and (per IP) unreported, so it must be **inferred**, and the only evidence is loss:

> **Loss means congestion.**

Not obviously true (loss could be corruption), but queue overflow dominates on wired networks — which is also why TCP historically did badly over WiFi, where loss often means interference and backing off is wrong. Mechanisms: **AIMD** (grow `cwnd` linearly, halve on loss — retreat fast, creep back) and **slow start** (double each RTT from a couple of segments until first loss; it starts small, not slow). Their reason for existing: the 1986 NSFNET **congestion collapse**, where senders retransmitting into a saturated network collapsed throughput while the network stayed maximally busy.

# See also
- [[Every guarantee above IP is manufactured by state at the two endpoints]] — both windows are endpoint-held state; `cwnd` must be *inferred* precisely because IP (the network) reports nothing
- [[A cumulative ACK N means "I have everything through N"]] — the same ACK stream carries the advertised `rwnd`, so flow control rides free on acknowledgment
- [[IP promises nothing — it is best-effort and never reports delivery outcome]] — "loss means congestion" is inference forced by IP's silence: the network won't tell you it's overloaded
- [[Reliability means preventing faults from causing failures]] — congestion control is what stops retransmissions (a reliability mechanism) from cascading into network-wide failure

# References
- https://datatracker.ietf.org/doc/html/rfc5681#section-2

# Questions
#flashcards/software-engineering/networking

What does flow control protect, versus congestion control?::Flow control protects the receiver's buffer (limit rwnd); congestion control protects the network path (limit cwnd)
<!--SR:!2026-10-09,19,250-->

Why must cwnd be inferred while rwnd is simply told?::The receiver knows and advertises its free buffer (rwnd), but nobody knows the shared, changing path capacity — and IP reports nothing — so cwnd is inferred from loss
<!--SR:!2026-09-09,8,250-->

Data in flight is bounded by ==min(rwnd, cwnd)== — the tighter of the receiver's and the network's limits.
<!--SR:!2026-09-21,1,210-->

What does AIMD do on success versus loss, and why the asymmetry?::Grows cwnd linearly while nothing is lost, halves it on loss — overshoot hurts everyone at the bottleneck, so retreat fast and creep back
<!--SR:!2026-09-20,0,210-->
