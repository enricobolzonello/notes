---
connections:
  - "[[PARA/AREAS/CLANN/2. CLANN.md|2. CLANN]]"
reference: 
tags:
  - type/paper
  - theme/approximate-nearest-neighbor
type: literature_note
created: 2024-12-20 19:17
modified: 
citekey: douzeFaissLibrary2024
status: read
dateread: 2024-10-03
---

> [!Cite]
> [1] M. Douze _et al._, «The Faiss library», 6 settembre 2024, _arXiv_: arXiv:2401.08281. doi: [10.48550/arXiv.2401.08281](https://doi.org/10.48550/arXiv.2401.08281).


>[!Synthesis]
>**Contribution**:: 
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**:: 
>

>[!Metadata]
>> **FirstAuthor**:: Douze, Matthijs  
> **Author**:: Guzhva, Alexandr  
> **Author**:: Deng, Chengqi  
> **Author**:: Johnson, Jeff  
> **Author**:: Szilvasy, Gergely  
> **Author**:: Mazaré, Pierre-Emmanuel  
> **Author**:: Lomeli, Maria  
> **Author**:: Hosseini, Lucas  
> **Author**:: Jégou, Hervé  
~    
> **Title**:: The Faiss library  
> **Year**:: 2024   
> **Citekey**:: douzeFaissLibrary2024  
> **itemType**:: preprint  
> **DOI**:: 10.48550/arXiv.2401.08281    

> [!LINK] 
> > [arXiv Fulltext PDF](file:///Users/enricobolzonello/Zotero/storage/JXH3XJR6/Douze%20et%20al.%20-%202024%20-%20The%20Faiss%20library.pdf).


> [!Abstract]
>
> Vector databases typically manage large collections of embedding vectors. Currently, AI applications are growing rapidly, and so is the number of embeddings that need to be stored and indexed. The Faiss library is dedicated to vector similarity search, a core functionality of vector databases. Faiss is a toolkit of indexing methods and related primitives used to search, cluster, compress and transform vectors. This paper describes the trade-off space of vector search and the design principles of Faiss in terms of structure, approach to optimization and interfacing. We benchmark key features of the library and discuss a few selected applications to highlight its broad applicability.
>.
> 

# Notes
## Indexing methods

- Locality Sensitive Hashing (LSH). Emphasis is on the **Cosine sketch:** produces binary vectors s.t. the Hamming distance is an estimation of the cosine similarity between the embeddings.  
    Two approaches:
    - binary codes -> such as cosine sketch
    - quantization
- Based on quantization, such as Product Quantization (PQ)
- Data-aware methods, for example multiple partitions based on kd-tree or hierarchical k-means
- Based on graphs, such as HNSW

## Metrics

### Accuracy metrics

discrepancy with the exact search results

_n-recall@k_: fraction of the n ground-truth nearest neighbors that are in the first k search results

if n=k=1, it is called _accuracy_.

_precision_: $P=|R\cap \hat{R}|/|\hat{R}|$

_recall_: $R=|R\cap \hat{R}|/|R|$

which are measures for range search (k-ANN). $\hat{R}$ is the result list from the algorithm.

Changing $\epsilon^\prime$ (the threshold for the search), we can produce a _precision-recall curve_. The area under this curve is called _mean average precision_.

_Mean Squared Error_ (MSE): error for the encoder and decoder pair.

$$MSE = E_x[||D(C(x))-x||^2_2]$$

### Resource metrics

during search:

- search time
- memory usage

index:

- constant memory overhead
- per-vector memory overhead
- index building time, can be decomposed into a training time and the addition time per vector
- number of I/O operations

-> not all metrics matter, _active constraints_ are the ones we care. These are:

- speed
- memory usage
- accuracy

### Pareto-optimal settings

defined as settings that are the fastest for a given accuracy or equivalently that have the highest accuracy for a given time budget

## Non-exhaustive search

different approaches:

- LSH -> has a fundamental drawback: it is not data-adaptive
- tree-based indexing -> dataset is stored in the leaves of a tree. Search starts from the root, at each node the search descends into one of the child based on a rule. The rule depends on the methods, some examples:
    
    - if it is based on KD-tree, the rule is the position with respect to the hyperplane
    - if it is based on hierarchical k-means, it is the proximity to a centroid
- Inverted files (IVF) -> clusters the database at indexing time. [[Clustering]] uses a vector quantizer that outputs $K_{IVF}$ distinct indices.  
    The vectors of each cluster are stored contiguously into inverted lists.
- Graph based -> building a directed graph whose nodes are the vectors. The search is done by following the edges towards the nodes that are closest to the query vector. FAISS implements HNSW and NSG.

LSH and tree-based indexing dont scale well for dimensions above 10.

# Vector Compressions

A quantizer converts a continuous multi-dimensional vector to an integer (bit string of size $\lceil \log_2 K \rceil$)

Then a decoder reconstructs an approximation of the vector.

-> this is done to **save space**

So also the search becomes approximate (assuming only the documents are quantized):

$$n = \argmin_{i=1..N}||q-D(C(x_i))||$$

-> called **Asymmetric Distance Computation** (ADC) [more accurate than symmetric]

types of quantizers:

1) k-means

2) scalar

3) multi-codebook

4) additive (residual quantizer and local search quantizer)

## Vector search definition

> given a set of database vectors $\{x_i, i=1..N\}\subset \mathbb{R}^d$ and a query vector $q\in \R^d$ it computes:
> 
> $$n = \argmin_{i=1..N}||q-x_i||$$

more generally, compute the k nearest neighbors:

$$(n_1,...,n_k,*,...,*) = \text{argsort}_{i=1..N} ||q-x_i||


$$.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-20T19:17:44.788+01:00 %%
