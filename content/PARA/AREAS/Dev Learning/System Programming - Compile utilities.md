---
area: Dev Learning
tags: area/dev_learning/untitled
type: area_note_sub
created: 2025-07-12 23:31
---
# [[2. Dev Learning]] 
# Overview

## thread safety
compile with:

```
gcc -fsanitize=thread -pie -fPIC -ltsan -g simple_race.c
```

it uses ThreadSanitizer, a tool from Google to detect race conditions in the code.

## undefined behavior sanitizer
https://clang.llvm.org/docs/UndefinedBehaviorSanitizer.html

It allows you to compile code with a runtime checker to make sure that you don’t do undefined behavior for various categories.