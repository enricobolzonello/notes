---
up:
tags:
  - permanent_note
created:
---

-> takes in raw source code and outputs tokens

## Reserved Words and Identifiers
We need to be careful, for example say we want to match the identifier `or`. If we are not careful, the word `orchid` might get matched with the identifier or which is not right.

This example gets us to an important property which is [[Maximal Munch; when two rules match, the scanner picks the one that consumes most characters|maximal munch]]. Maximal munch means we can’t easily detect a reserved word until we’ve reached the end of what might instead be an identifier. 
A reserved word is an identifier, but claimed by the language.


