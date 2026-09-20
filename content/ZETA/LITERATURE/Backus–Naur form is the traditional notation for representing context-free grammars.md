---
tags:
  - atomic
up:
  - "[[Lox Scanner]]"
  - "[[Context-Free Grammars and Languages]]"
created: 2025-04-22 16:36
---
 Backus–Naur form is the traditional notation for representing [[Context-Free Grammars and Languages|context-free grammars]]. 
- Non-Terminal symbols are represented by wrapping symbols in angle brackets, like `<SheepNoise>`, 
- Terminal symbols are underlined. 
- Symbol `:==` means "derives", while `|` means "also derives"

As an example, the sheep noise grammar is:
```
<SheepNoise> :== <u>baa</u> <SheepNoise> | <u>baa</u>
```

# Reference
- Linda Torczon and Keith Cooper. 2007. Engineering A Compiler (2nd. ed.). Morgan Kaufmann Publishers Inc., San Francisco, CA, USA.