---
Priority_Level: 3 Medium
Status: 4 Completed
Date_Created: 2025-01-13T16:54
Due_Date: 2025-01-13T16:54
connections:
  - "[[PARA/AREAS/Verità/2. Verità.md|2. Verità]]"
tags:
  - "#project/metrics_for_patent_similarity"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
closed: 2025-01-13T16:54
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Metrics for the whole pipeline

### AUC
Computing the similarity will result in two distributions of similarity scores: one for the positive samples (similar documents) and one for the negative samples (non relevant documents). We want them separated by a good threshold.

To measure how good they are separated, the [ROC curve](https://it.wikipedia.org/wiki/Receiver_operating_characteristic) can be used, or more specifically, the AUC, which is the area under the curve. 

Definitions:
- FP (False positives) -> unrelated patents considered relevant
- FN (False negatives) -> related patents considered irrelevant
- TN (True negatives) -> random parents correctly considered as irrelevant
- TP (True positives) -> correctly detected patents
Compute:
- TPR (True Positive Rate or **recall**):
  $$
  TPR = \frac{TP}{TP+FN}
  $$
- FPR (False Positive Rate):
  $$
  FPR=\frac{FP}{FP+TN}
  $$
- FNR (False Negative Rate):
  $$
  FNR=\frac{FN}{TP+FN}
  $$
By plotting the TPR against the FPR, we can obtain the graph of the ROC curve. Finally the area under the ROC curve (AUC) is a range between 0.5 (no separation between distributions) and 1 (clear distinction).

# Metrics before the threshold

### Precision@k
number of relevant documents in the top-k search results

$$
P@k = \frac{|R_k|}{|S_k|}
$$
where $R_k$ are the relevant items in $S_k$. 

### Mean reciprocal rank (MRR)
measures how quickly a ranking system can show the first relevant item.
$$
π
$$

### AP
Average Precision (AP) for the final result. Precision (P=TP+FP) and recall can be plotted against each other for n different threshold, the area is the AP:
$$
AP=\sum_n (R_n - R_{n-1})P_n
$$
### nDCG (Normalized Discounted Cumulative Gain)
Graded relevance scale of documents to evaluate the gain of a document based on its position in the result list.

DCG = sum the gain of the results discounted by their position in the result list
$$
DCG_p = \sum_{i=1}^p \frac{rel_i}{\log_2 (i+1)}
$$
where $rel_i$ is the graded relevance of the result at position $i$. 

-> should be normalized across queries, since the result list length may vary depending on the query:
$$
nDCG_p = \frac{DCG_p}{IDCG_p}
$$
where IDCG is the ideal discounted cumulative gain:
$$
IDCG_p = \sum_{i=1}^{|REL|_p} \frac{2^{rel_i} - 1}{\log_2(i+1)}
$$
($REL_p$ is the list of ordered relevant documents up to position $p$)


# Comments
For this to work, we need a ground truth dataset, in my knowledge with human labeled data. 