---
up: "[[Backus–Naur form is the traditional notation for representing context-free grammars]]"
tags:
  - atomic
created: 2025-04-10 18:46
---
> When two lexical grammar rules can both match a chunk of code that the scanner is looking at, _whichever one matches the most characters wins_.

For example, if we have a word `orchid` which can be mapped as an identifier or as the keyword `or`, the former wins. The same applies for `<=`, it will map to less equal, not to less.

# References
- https://craftinginterpreters.com/scanning.html
- [[Lox Scanner]]
# See also
- [[Backus–Naur form is the traditional notation for representing context-free grammars]] — the formal grammar notation that defines the rules Maximal Munch arbitrates between 
- [[Chomsky hierarchy - Regular < Context-Free < Context-Sensitive < Recursively Enumerable]] — lexical scanning operates at the Regular language level of the hierarchy; Maximal Munch is a disambiguation rule at that level