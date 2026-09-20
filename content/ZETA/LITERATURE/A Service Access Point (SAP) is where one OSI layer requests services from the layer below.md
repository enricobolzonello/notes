---
up:
  - "[[OSI Model describes network communication in 7 layers from physical bits to application data]]"
tags:
  - atomic
created: 2025-12-21 16:07
---
The SAP is a conceptual location at which one [[OSI Model describes network communication in 7 layers from physical bits to application data|OSI layer]] can request the services of another layer of the stack.

example: PD-SAP or PLME-SAP. The Medium Access Control (MAC) layer requests certain services from the physical layer

SAPs are how the OSI model enforces layer independence: each layer only communicates with the layer directly above or below it through a SAP, never skipping layers.

---

# Questions
#flashcards/stem  

What is a Service Access Point (SAP) in networking?::location where one OSI layer can communicate with another layer
<!--SR:!2026-02-27,1,230-->