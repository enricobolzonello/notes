---
up:
  - "[[Software Engineering at Google - Titus Winters Tom Manshreck Hyrum Wright]]"
tags:
  - atomic
created: 2026-02-26 16:30
---

To develop a rule the following rules are enforced:
- **Pull their Weight**, not include rules expected to be self-evident
- **Optimize for the reader**
	- value more "simple to read" over "simple to write"
	- aim is to have understanding without needing to find and reference other code
- **Be consistent**
	- a local project can have its unique personality, but its tools, techniques, libraries are the same
	- good idea to be consistent with outside world
- **Avoid error-prone and surprising constructs**
	- avoid complex features, place higher value on simplified, straightforward code
- **Concede to practicalities when necessary**
	- performance matter, even sacrificing consistency or readability 

---

#flashcards/software-engineering

What is the "Pull their Weight" principle for style rules?::Only include rules that add real value — don't state the self-evident.
<!--SR:!2026-03-17,1,230-->

What does "Optimize for the reader" mean in a style guide?::Prioritize code that is easy to read over code that is easy to write; readers should understand code without needing to reference other files.
<!--SR:!2026-03-17,1,230-->

What does "Be consistent" mean in a style guide context?::Within a project, tools, techniques, and libraries should be uniform; it's also good practice to align with conventions used in the wider ecosystem.
<!--SR:!2026-03-19,3,250-->

What is the goal of "Avoid error-prone and surprising constructs"?::Prefer simple, straightforward code over complex features that can cause unexpected behavior.
<!--SR:!2026-03-19,3,250-->

When does "Concede to practicalities" apply in a style guide?::When performance requirements justify it — even if it means sacrificing consistency or readability.
<!--SR:!2026-03-17,1,230-->