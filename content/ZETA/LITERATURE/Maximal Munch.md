---
connections:
  - "[[Scanner]]"
reference: https://craftinginterpreters.com/scanning.html
tags: 
type: literature_note
created: 2025-04-10 18:46
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> [!DEFINITION]
> When two lexical grammar rules can both match a chunk of code that the scanner is looking at, _whichever one matches the most characters wins_.

For example, if we have a word `orchid` which can be mapped as an identifier or as the keyword `or`, the former wins. The same applies for `<=`, it will map to less equal, not to less.