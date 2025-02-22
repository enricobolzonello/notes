---
Priority_Level: 
Status: 
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/clann_metrics"
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

git_commit_hash = afb20f4b1ac5f9c85cf44499e810680e4d2e8915
num_tables =84.0

## glove-100
CLANN
num_clusters|avg(distance_computations)
0.05|31979.1648
0.10|48250.9143
0.15|61735.8471
0.20|73074.7946
0.25|84092.819
0.30|93649.7506
0.35|102328.7981
0.40|110818.9776
0.45|118681.8729
0.5|127378.3316
0.55|133745.6655
0.60|142133.5649
0.65|148942.7167
0.7|155677.6314

PUFFINN: 6486.5337

## glove-50
CLANN
0.05|9778.1729
0.10|13947.4176
0.15|16971.4757
0.20|19380.5755
0.25|21101.1654
0.30|22729.3242
0.35|24655.313
0.40|26363.2283
0.45|27847.9649
0.5|28752.6448
0.55|29949.6742
0.60|31275.5148
0.65|32280.9354
0.7|33447.9972

PUFFINN: 1387.7174