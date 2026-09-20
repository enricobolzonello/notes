---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-04-30 17:11
---

> The *why* behind both crates is [[Coherence guarantees one impl per (trait, type) pair, enforced by the orphan rule and no-overlap]].

- use `thiserror` when you want a structured representation for your errors
- use `anyhow` when this representation is not needed

For example, in [bbstore](https://github.com/enricobolzonello/bbstore) my rationale is:
- anyhow in all internal errors which I do not expose to the outside world
- thiserror on errors I want to report ([commit](https://github.com/enricobolzonello/bbstore/commit/44e8aea82a28f089ec31634b5e2357f9b2ba8d0a))

# See also
- [[Reliability means preventing faults from causing failures]] — the `thiserror`/`anyhow` distinction maps onto the fault/failure model: `thiserror` names and structures faults so callers can handle them; anyhow propagates them as failures without requiring the caller to understand the cause
- [[Interface Segregation Principle (ISP)]] — `thiserror` is ISP applied to errors: expose only the error variants callers actually need to handle; anyhow is the escape hatch when no client needs to distinguish
- [[Single Responsibility Principle (SRP)]] — a library that exposes anyhow errors forces callers to depend on its internal error details; `thiserror` gives each error type one clear responsibility and one clear owner