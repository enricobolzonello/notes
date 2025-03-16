---
Priority_Level: 3 Medium
Status: 4 Completed
Date_Created: 2025-03-03T15:12
Due_Date: 
connections:
  - "[[PARA/AREAS/CLANN/2. CLANN.md|2. CLANN]]"
tags:
  - "#project/clann_refactoring"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
_previous_status: 2 In Progress
closed: 2025-03-10T10:30
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# What is currently wrong?
There are many issues in the metrics storing.
- [x] if index is loaded from file, the build metrics are not stored (still todo) ✅ 2025-03-10
- [x] build metrics should be a separate table ✅ 2025-03-03
- [ ] the only way to see the metrics is through the sql database
- [x] k and delta now are defined before building the index -> no independent runs with different k and delta ✅ 2025-03-10

solution:
- rewrite the sql database, with build metrics separated from the search metrics
- index file should store inside the necessary metrics, so they can be added to the corresponding table if there is the need
- print for summary, csv for compatibility




- per lo storage delle build metric in teoria non serve salvarle in una struct separata -> aggiunge un overhead di performance ma sti cazzi (meglio che farlo alla fine). La funzione poi funzionerebbe sia se costruisco l'indice, sia se faccio il load da file

## build metric
- [x] funzione per salvare in modo indipendente che sia da file o buildato ✅ 2025-03-10
- [x] controllare nel processo di build ✅ 2025-03-03
- [x] fare il salvataggio delle metriche da file ✅ 2025-03-10
- [ ]  