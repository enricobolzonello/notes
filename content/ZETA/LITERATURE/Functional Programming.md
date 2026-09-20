---
connections: 
reference: 
tags:
  - theme/design-pattern
type: literature_note
created: 2025-04-13 17:55
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> paradigm where programs are constructed by applying and composing functions.

Rather than a sequence of [[Imperative paradigm|imperative]] statements, function definitions are trees of expressions that each return a value.

example:
```rust
println!("{}", (1..11).fold(0, |a, b| a + b));
```
We are describing what to do rather than how to do it.
`fold` is a function that composes functions [[Function composition|composes functions]]



