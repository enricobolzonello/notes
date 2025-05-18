---
Priority_Level: 
Status: 
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/kafka"
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
Brokers and clients communicate with each other using the TCP protocol.
The protocol uses a request-response model:
- **request** (sent by client) 
- **response** (sent by broker), has 3 parts:
	- message_size -> 32 bit signed integer which specifies the size of the head and body
	- header -> we will use only v0 which contains only the field  `correlation_id`, a 32 bit signed integer. How does it work?
		- client generates and id
		- client sends a request with the id
		- broker sends a response with the same id
		- client receives the response and matches the id with the original request
	- body



