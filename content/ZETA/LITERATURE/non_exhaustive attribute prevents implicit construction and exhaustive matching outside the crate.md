---
up:
  - "[[ZETA/PERMANENT/Rust]]"
tags:
  - atomic
created: 2026-05-18 16:49
---
`#[non_exhaustive]` attribute constraints how outside code behaves in that struct or enum variant, specifically it disallows:
- implicit constructors
```rust
#[non_exhaustive]
struct Point {
	x: f32,
	y: f32
}

// outside the crate, this is not allowed
Point {x: 10.0, y: 20.0};
```
- non-exhaustive pattern matches
```rust
enum Point {
	2D,
	3D
}

// outside the crate, this is not allowed
match point {
	2D => print!("two-dimensional"),
	3D => print!("three-dimensional"),
	// would compile with `_ => {},`
}
```

Useful when you suspect you will modify a particular type in the future.

# See also
- [[OCP - software should be open for extension and closed for modification]] — `#[non_exhaustive]` is OCP applied to Rust types: the type is open for extension (you can add fields/variants in future versions) because callers are closed against assuming exhaustiveness
- [[All Observable Behaviours of an API Will Be Depended On by Someone]] — without `#[non_exhaustive]`, adding a field or variant is a breaking change because callers depend on the exhaustive list; the attribute is a direct defence against Hyrum's Law
- [[Principle of Least Astonishment]] — `#[non_exhaustive]` makes future additions unsurprising: callers who pattern match are forced to handle the `_` case, so new variants never break their code silently

# References
- J. Gjengset, _Rust for Rustaceans: Idiomatic Programming for Experienced Developers_. No Starch Press, 2021.