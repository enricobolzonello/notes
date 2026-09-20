---
up:
  - "[[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]"
tags:
  - atomic
created: 2026-03-07 13:45
---
benefits to the writer:
- formulate the API
- provides a road map for maintenance and a historical record
- makes code look more professional and drive traffic
- will prompt fewer questions from other users

aims:
- enforce consistency
- improve clarity
- avoid comprehension errors

- NOT A WIKI, IT SHOULD BE ALONGSIDE SOURCE CODE AND TREATED AS SOURCE CODE (bugs, issue tracking, version control, etc.)

## Reference documentation

> anything that documents the usage of code within the codebase

types:
- **file comments**, 
	- begin with an outline of what's contained
	- should identify the code's main use cases and intended audience
- **class comments**
	- describe the class/struct, important methods and the purpose
- **function comments**
	- stress the active nature; begin with an indicative verb describing what the function does and what is returned

## Design docs

like in amazon

## Conceptual documentation

> way to augment the reference documentation to have more insight and context

- if comments are the unit tests of documentation, conceptual documents are the integration tests
- emphasize clarity and sacrifice completeness and strict accuracy
