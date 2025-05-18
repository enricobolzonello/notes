---
Priority_Level: 
Status: 
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/lox_interpreter"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
---

# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

With the [[Scanner|scanner]] we transformed raw source code into a sequence of tokens, on the [[Chomsky hierarchy]] we were at the first level. 
Now we go up one level, to the [[Context-Free Grammars and Languages|context-free grammar]] (CFG). The parser role is to derive a syntactic structure of the program, fitting the words into a grammatical model of the source programming language.
We need CFGs mainly to express precedence, but also to see valid operations. Regular expressions are not capable of that, as for example $a + ( b × c$ is a valid expression for a regex. 


Remember the [[Context-Free Grammars and Languages#Context-Free Grammars|definition]], it has 3 different parts:
1) terminals --> word or sentence fragments used to put together the final output
2) variables --> used as abstract versions of decisions that will be made later
3) productions --> these describe how a variable can be converted into different sets of variables or terminal

We will use a variation of the [[Backus–Naur form]], modified like this:
> Each rule is a name, followed by an arrow (`→`), followed by a sequence of symbols, and finally ending with a semicolon (`;`). Terminals are quoted strings, and nonterminals are lowercase words.

As in the example grammar, for generating a breakfast:
```
breakfast → protein ( "with" breakfast "on the side" )?
          | bread ;

protein   → "really"+ "crispy" "bacon"
          | "sausage"
          | ( "scrambled" | "poached" | "fried" ) "eggs" ;

bread     → "toast" | "biscuits" | "English muffin" ;
```

# Final Grammar

The final grammar for Lox, without ambiguity is:
```
expression     → equality ;
equality       → comparison ( ( "!=" | "==" ) comparison )* ;
comparison     → term ( ( ">" | ">=" | "<" | "<=" ) term )* ;
term           → factor ( ( "-" | "+" ) factor )* ;
factor         → unary ( ( "/" | "*" ) unary )* ;
unary          → ( "!" | "-" ) unary
               | primary ;
primary        → NUMBER | STRING | "true" | "false" | "nil"
               | "(" expression ")" ;
```


# Recursive Descent
Structured as a set of mutually recursive procedures, one for each non-terminal symbols in the grammar. 

How to do it:
- for each nonterminal, construct a procedure to recognize its alternative right hand sides
	- they call one another to recognize nonterminals
	- they recognize terminals by direct matching

