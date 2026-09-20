---
tags:
  - permanent_note
up:
  - "[[ZETA/PERMANENT/Rust]]"
created: 2026-05-12 18:29
---
- Large projects should have only one integration test crates with several modules. On Cargo itself this refactor decreased the compile time by 3x and reduce on-disk artifacts by 5x ([source](https://github.com/rust-lang/cargo/pull/5022#issuecomment-364691154)).
```
tests/
	it/
		main.rs
		foo.rs
		bar.rs
```
- Another improvement is to consolidate several tests into one, since Cargo runs tests binaries sequentially.
- For internal library, avoid integration tests all together.
- Avoid doc tests 
```rust
[lib]
doctest = false
```
- prefer a separate test file
```rust
#[cfg(test)]
mod tests; // tests in `tests.rs` file
```
- another trick is to have a single test crate for the whole workspace, since the library is recompiled twice instead
```rust
[lib]
test = false
```

# See also
- [[Scale and Efficiency applies to people, compute and codebase]] — the 3x compile time and 5x artifact reduction from Cargo's own refactor is a concrete data point for the superlinear scaling problem: test binaries were the hidden culprit
- [[Most of the cost of software is maintenance (operability, simplicity, evolvability)]] — slow test suites erode evolvability: if tests take too long to run, engineers stop running them; consolidation keeps the feedback loop fast
# References
- https://matklad.github.io/2021/02/27/delete-cargo-integration-tests.html