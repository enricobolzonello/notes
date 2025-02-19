---
connections: 
reference:
tags: 
 - type/paper
type: literature_note
created: 2025-02-13 16:36
modified:
citekey: beyerWhenNearestNeighbor1999
status: unread
dateread:
---

> [!Cite]
> [1] K. Beyer, J. Goldstein, R. Ramakrishnan, e U. Shaft, «When Is “Nearest Neighbor” Meaningful?», in _Database Theory — ICDT’99_, C. Beeri e P. Buneman, A c. di, Berlin, Heidelberg: Springer, 1999, pp. 217–235. doi: [10.1007/3-540-49257-7_15](https://doi.org/10.1007/3-540-49257-7_15).


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
>> **FirstAuthor**:: Beyer, Kevin  
> **Author**:: Goldstein, Jonathan  
> **Author**:: Ramakrishnan, Raghu  
> **Author**:: Shaft, Uri  
~> **FirstEditor**:: Beeri, Catriel  
> **Editor**:: Buneman, Peter  
~    
> **Title**:: When Is “Nearest Neighbor” Meaningful?  
> **Year**:: 1999   
> **Citekey**:: beyerWhenNearestNeighbor1999  
> **itemType**:: conferencePaper  
> **Publisher**:: Springer  
> **Location**:: Berlin, Heidelberg   
> **Pages**:: 217-235  
> **DOI**:: 10.1007/3-540-49257-7_15  
> **ISBN**:: 978-3-540-49257-3    

> [!LINK] 
> > [Beyer et al. - 1999 - When Is “Nearest Neighbor” Meaningful.pdf](file:///Users/enricobolzonello/Zotero/storage/W2ABFD3N/Beyer%20et%20al.%20-%201999%20-%20When%20Is%20“Nearest%20Neighbor”%20Meaningful.pdf).


> [!Abstract]
>
> We explore the effect of dimensionality on the “nearest neighbor” problem. We show that under a broad set of conditions (much broader than independent and identically distributed dimensions), as dimensionality increases, the distance to the nearest data point approaches the distance to the farthest data point. To provide a practical perspective, we present empirical results on both real and synthetic data sets that demonstrate that this effect can occur for as few as 10–15 dimensions.
>.
> 

# Notes
If

$$\lim_{m\rightarrow \infty} var\bigg( \frac{(d_m(P_{m,1},Q_m))^p}{E[(d_m(P_{m,1}, Q_m))^p]}\bigg) = 0$$

then for every $\epsilon>0$:

$$\lim_{m\rightarrow \infty} P[Dmax_m \le (1+\epsilon)Dmin_m]=1$$

Basically, if the condition holds (and it holds quite frequently) all points converge to the same distance to the query point

The condition holds for:
- iid dimensions with query and data independence
- unique dimensions with correlation between all dimensions
- variance converging to 0
- marginal data and query distributions change with dimensionality

do not hold for:
- identical dimensions with no independence --> points fall on a line.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2025-02-13T16:36:21.545+01:00 %%
