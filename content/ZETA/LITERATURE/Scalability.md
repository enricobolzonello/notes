---
connections: 
reference: 
tags:
  - type/note
  - theme/engineering
type:
  - literature_note
created: 2024-12-17 18:14
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

> Scalability is the term we use to describe a system's ability to cope with increased load

How to determine scalability?
1. **Describe Load**. Load can be described with a few numbers called *load parameters*, which depend on the system's architecture. 
2. **Describe Performance**. two ways to see it:
	- increase a load parameter and keep the system resources unchanged, how is performance
	- increase a load parameter, how much do you need to increase resources if you want to keep performance unchanged
	Use **percentiles**, not mean. For the dashboard, keep a rolling window of response times in the last 10 minutes. Every minute, calculate the median and various percentiles. *Averaging percentiles is mathematically meaningless*