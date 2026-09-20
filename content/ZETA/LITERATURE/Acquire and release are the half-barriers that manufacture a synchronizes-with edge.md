---
up:
  - "[[Happens-before is the single relation guaranteeing visibility and ordering across threads]]"
tags:
  - atomic
created: 2026-08-31 10:16
---
A synchronizes-with edge needs a **release** on one side and an **acquire** on the other. These are directional half-barriers, and their asymmetry is the whole trick:

- **Release** (applies to a *write*): nothing before it in program order may be reordered *after* it. It **publishes** — everything the thread did before the release is finalised and made visible at the moment another thread observes this write.
- **Acquire** (applies to a *read*): nothing after it in program order may be reordered *before* it. It **subscribes** — once it observes a released value, everything after it sees everything the releaser published.

Picture it: release is a floor (things above can't fall through downward), acquire is a ceiling (things below can't rise through upward). When an acquire *observes the value written by* a release, they click into a **synchronizes-with edge**, and transitivity carries every write-before-the-release into visibility-after-the-acquire:

$$\underbrace{\text{writes} \dots}_{\text{T1}}\ ;\ \text{release}(L)\ \xrightarrow{\text{sync-with}}\ \text{acquire}(L)\ ;\ \underbrace{\dots \text{reads}}_{\text{T2}}$$

Beyond plain acquire/release there are weaker and stronger orderings: **relaxed** gives atomicity only, no ordering/visibility (fine for a pure counter); **seq_cst** adds a single global total order all threads agree on, stronger and costlier than acquire/release alone.

# See also
- [[Happens-before is the single relation guaranteeing visibility and ordering across threads]] — acquire/release is the concrete way to create the synchronizes-with edge that happens-before needs
- [[A lock provides two guarantees, mutual exclusion and a happens-before edge]] — a mutex is literally unlock=release and lock=acquire; this note is the mechanism that makes a lock provide guarantee two
- [[The store-buffer litmus test proves mutual exclusion is not enough]] — the test fails for lack of exactly this edge; inserting a release/acquire pair is what would fix it
- [[RCU allows one updater and many readers concurrently]] — RCU's "publish a new version" is a release store; readers' access is the acquire side, so the new version is safely visible without a lock

# References
- https://preshing.com/20120913/acquire-and-release-semantics/
- https://en.cppreference.com/w/cpp/atomic/memory_order

# Questions
#flashcards/stem/os

What is release semantics, and what is acquire semantics?::Release (on a write) forbids reordering earlier ops after it and publishes prior writes; acquire (on a read) forbids reordering later ops before it and observes what a matching release published

When do a release and an acquire form a synchronizes-with edge?::When the acquire read observes the value written by the release store — then everything before the release is visible after the acquire

Release is a ==floor== (nothing before it moves after it); acquire is a ==ceiling== (nothing after it moves before it).

memory_order_relaxed gives ==atomicity only== (no ordering); seq_cst adds a ==single global total order== all threads agree on.
