---
up:
  - "[[Paradoxes Broke 19th-Century Math and Set Theory Rebuilt It — Until Gödel]]"
tags:
  - atomic
created: 2025-04-17 17:22
---

![[Chomsky hierarchy.png]]

Hierarchy of formal grammars. A formal grammar describes how to form strings from a language alphabet that are valid according to the language syntax. 

Each class in the hierarchy can completely generate the language of all inferior classes (set inclusive). 

Hierarchy:
- [[Regular Expressions]] -->  recognized by [[Finite State Automata (FA)]]
- [[Context-Free Grammars and Languages]] --> recognized by [[Pushdown Automata]]
- Context Sensitive
- Recursively Enumerable --> recognized by [[Turing Machines]]

# See also
- [[Backus–Naur form is the traditional notation for representing context-free grammars]] — BNF is the notation used to write the Context-Free level of the hierarchy; moving from Regular to Context-Free is the step from scanner to parser
- [[Maximal Munch; when two rules match, the scanner picks the one that consumes most characters]] — Maximal Munch operates at the Regular level of the hierarchy: lexical scanning is a finite state automaton problem
- [[Modus ponens, P è vero quindi Q è vero]] — modus ponens is a production rule in the Recursively Enumerable level: formal inference systems sit at the top of the hierarchy
- [[Gödel's incompleteness theorems]] — Turing's halting problem , which proved the limits of the Recursively Enumerable level, is one of the theorems at the top of the hierarchy; Gödel's theorems and the hierarchy share the same mathematical roots
- [[h(x) = g(f(x)) — Composing Functions With ∘ and Its Reverse]] — each level of the hierarchy is closed under composition of its grammars; the hierarchy is a hierarchy of what compositions are expressible