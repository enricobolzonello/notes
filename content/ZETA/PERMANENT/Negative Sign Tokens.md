---
connections:
tags:
  - permanent_note
  - theme/rust
  - theme/engineering
type: permanent_note
created: 2026-03-13 11:10
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

Consider as an example the floating point numbers, as can be seen in the [official reference](https://doc.rust-lang.org/reference/tokens.html#grammar-FLOAT_LITERAL):

```
FLOAT_LITERAL -> DEC_LITERAL (. DEC_LITERAL)?
```

which means that a float literal  is evaluated as a combination of a decimal and an optional fractional part.
But what about the negative sign?
Actually it is parsed as a distinct token.

## Why?

The main reason is simplicity. The lexer is designed to be as dumb and context-free as possible, which avoids ambiguity. 

> [...] going with the mathematical view would require context-sensitive parsing in order to make an exception for numeric literals. Context-sensitive parsing is a big no-no for modern programming languages (and yes, that means that I exclude C++ from that group of modern languages) for reasons of implementation complexity, theoretical limits of what you can do with the grammar of such a language (more expressive generally means more expensive to compute and manipulate) and probably reasons of simplicity in terms of usage, since it is much easier to remember a rule that applies everywhere than it is to remember "in situation A this goes, but in situation B that other thing goes, because of reasons".
> https://users.rust-lang.org/t/why-are-negative-value-literals-expressions/43333/6


## Practical impact

This means an expression like `-5.5f32.abs()` is evaluated as `-(5.5f32.abs())` rather than `(-5.5f32).abs()`, which actually matches mathematical notation.

# References
- https://users.rust-lang.org/t/why-are-negative-value-literals-expressions/43333
- https://doc.rust-lang.org/reference/tokens.html
- https://dtolnay.github.io/rust-quiz/22