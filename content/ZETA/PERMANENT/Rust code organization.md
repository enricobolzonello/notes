---
up:
tags:
  - permanent_note
created: 2026-05-12 19:02
---
- Between 10 thousand and one million lines, flat layout makes the most sense
```
rust-analyzer/
  Cargo.toml
  Cargo.lock
  crates/
    rust-analyzer/
    hir/
    hir_def/
    hir_ty/
    ...
```
- make the root of the workspace a virtual manifest
- write all automation in a dedicated crate (example: [cargo xtask](https://github.com/matklad/cargo-xtask))
- use `version = "0.0.0"` for internal crates you don't want to publish and extract crates you want to publish in a top-level folder `libs`

# See Also
- 
# References
- 