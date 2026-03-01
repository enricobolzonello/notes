---
connections:
reference: "[[Designing Data-Intensive Applications - Martin Kleppmann]]"
tags:
type: literature_note
created: 2026-01-30 16:08
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

- each log-structured storage segment is a sequence of key-value pairs (**hash index**)
- SSTables
	- require that the sequence of key-value pairs is **sorted by keys**
	- each key appears only once (*compaction process*)
	- advantages
		- merging is simple (mergesort)
		- no need to keep an index of all the keys in memory, just some (need to scan a few keys)
		- group records into a block and compress it before writing to disk (thanks to above)