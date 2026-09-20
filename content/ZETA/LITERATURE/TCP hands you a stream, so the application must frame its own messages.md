---
up:
  - "[[TCP is a byte stream and UDP preserves datagram boundaries — opposite answers]]"
tags:
  - atomic
created: 2026-08-29 15:35
---
TCP hands you an unstructured byte stream, but your protocol needs *messages*. Boundaries must be encoded **inside the byte stream**, and only three ways exist: tell the reader the length, mark the end distinctively, or stop sending.

| | Length-prefix | Delimiter | Close-on-end |
|---|---|---|---|
| Must scan every byte | no | yes | no |
| Payload may contain any bytes | yes | needs escaping | yes |
| Sender must know size up front | yes | no | no |
| Connection reusable after | yes | yes | no |
| Truncation detectable | yes | yes | no |

HTTP/1.1 uses two in one message: headers are **delimiter**-framed (blank line) since their length isn't known until written and they're small text; the body is **length-prefixed** (`Content-Length`) since it can contain arbitrary bytes, including blank lines.

The streaming case (a response with no known total length) looks impossible for length-prefix — but **the length prefix was never the constraint; its *scope* was.** Prefix each *piece* as you produce it: that's **chunked transfer encoding** (RFC 9112). No scanning, no escaping, arbitrary binary, and truncation still detectable (a cut stream lacks its terminating zero chunk).

> **Framing composes.** Chunked encoding is a length-prefixed frame containing a stream of length-prefixed frames — the most reusable idea in protocol design, and HTTP/2 generalises exactly it.

Delimiters lose for binary because binary can contain any byte, including the terminator — forcing escaping (scan+rewrite both ways, unpredictable growth, silent corruption on rule mismatch). Hence **binary protocols are almost universally length-prefixed.**

# See also
- [[TCP is a byte stream and UDP preserves datagram boundaries — opposite answers]] — framing is the *direct consequence* of TCP discarding boundaries: the app must re-impose the messages TCP threw away
- [[Head-of-line blocking is the price of a single connection-wide byte order]] — HTTP/2 generalises this framing (typed, length-prefixed frames tagged with a stream ID) to interleave streams over one connection
- [[Maximal Munch; when two rules match, the scanner picks the one that consumes most characters]] — the delimiter-scanning problem is a parsing problem; framing is where network protocols meet lexing/parsing concerns
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — "framing composes" is the same compositional idea: a frame wrapping a stream of frames, like nesting functions

# References
- https://datatracker.ietf.org/doc/html/rfc9112

# Questions
#flashcards/software-engineering/networking

Why must the application frame its own messages over TCP?::TCP presents an unstructured byte stream (it discarded packet boundaries), so message boundaries must be re-encoded inside the stream
<!--SR:!2026-09-08,7,250-->

What are the only three ways to frame messages in a byte stream?::Length-prefix (tell the reader the size), delimiter (mark the end distinctively), and close-on-end (stop sending)
<!--SR:!2026-09-01,3,250-->

Chunked transfer encoding works because the length prefix's constraint was never length but its ==scope== — prefix each piece as you produce it.
<!--SR:!2026-09-20,0,190-->

Why are binary protocols almost universally length-prefixed?::A delimiter can appear inside binary payloads, forcing escaping (scan+rewrite, growth, silent corruption); length-prefix avoids scanning entirely
<!--SR:!2026-10-13,23,250-->
