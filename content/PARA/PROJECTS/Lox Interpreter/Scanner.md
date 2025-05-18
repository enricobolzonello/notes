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
-> takes in raw source code and outputs tokens

## Reserved Words and Identifiers
We need to be careful, for example say we want to match the identifier `or`. If we are not careful, the word `orchid` might get matched with the identifier or which is not right.

This example gets us to an important property which is [[Maximal Munch]]. Maximal munch means we can’t easily detect a reserved word until we’ve reached the end of what might instead be an identifier. 
A reserved word is an identifier, but claimed by the language.


