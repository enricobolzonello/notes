---
connections: 
reference:
tags: 
 - type/paper
type: literature_note
created: 2025-02-13 16:00
modified:
citekey: aggarwalSurprisingBehaviorDistance2001
status: unread
dateread:
---

> [!Cite]
> [1] C. C. Aggarwal, A. Hinneburg, e D. A. Keim, «On the Surprising Behavior of Distance Metrics in High Dimensional Space», in _Database Theory — ICDT 2001_, J. Van den Bussche e V. Vianu, A c. di, Berlin, Heidelberg: Springer, 2001, pp. 420–434. doi: [10.1007/3-540-44503-X_27](https://doi.org/10.1007/3-540-44503-X_27).


>[!Synthesis]
>**Contribution**:: demonstrated that with high dimension low values of k for the $L_k$ distance metric are better, since for values of k higher than 2 the difference between the nearest and farthest point converge to 0
>
>**Strong Points**::
>
>**Weak Points**::
>
>**Related**:: [[@beyerWhenNearestNeighbor1999]]
>

>[!Metadata]
>> **FirstAuthor**:: Aggarwal, Charu C.  
> **Author**:: Hinneburg, Alexander  
> **Author**:: Keim, Daniel A.  
~> **FirstEditor**:: Van den Bussche, Jan  
> **Editor**:: Vianu, Victor  
~    
> **Title**:: On the Surprising Behavior of Distance Metrics in High Dimensional Space  
> **Year**:: 2001   
> **Citekey**:: aggarwalSurprisingBehaviorDistance2001  
> **itemType**:: conferencePaper  
> **Publisher**:: Springer  
> **Location**:: Berlin, Heidelberg   
> **Pages**:: 420-434  
> **DOI**:: 10.1007/3-540-44503-X_27  
> **ISBN**:: 978-3-540-44503-6    

> [!LINK] 
> > [Aggarwal et al. - 2001 - On the Surprising Behavior of Distance Metrics in .pdf](file:///Users/enricobolzonello/Zotero/storage/UK8CGEFU/Aggarwal%20et%20al.%20-%202001%20-%20On%20the%20Surprising%20Behavior%20of%20Distance%20Metrics%20in%20.pdf).


> [!Abstract]
>
> In recent years, the effect of the curse of high dimensionality has been studied in great detail on several problems such as clustering, nearest neighbor search, and indexing. In high dimensional space the data becomes sparse, and traditional indexing and algorithmic techniques fail from a effciency and/or effectiveness perspective. Recent research results show that in high dimensional space, the concept of proximity, distance or nearest neighbor may not even be qualitatively meaningful. In this paper, we view the dimensionality curse from the point of view of the distance metrics which are used to measure the similarity between objects. We specifically examine the behavior of the commonly used Lknorm and show that the problem of meaningfulness in high dimensionality is sensitive to the value of k. For example, this means that the Manhattan distance metric L(1norm) is consistently more preferable than the Euclidean distance metric L(2norm) for high dimensional data mining applications. Using the intuition derived from our analysis, we introduce and examine a natural extension of the Lknorm to fractional distance metrics. We show that the fractional distance metric provides more meaningful results both from the theoretical and empirical perspective. The results show that fractional distance metrics can significantly improve the effectiveness of standard clustering algorithms such as the k-means algorithm.
>.
> 

# Notes
For the $L_k$ norm in high dimensional space, it may be better to use lower values of $k$.
More specifically:

Let $\mathcal{F}$ be the arbitrary distribution of n points, then:

$$C_k\le\lim_{n\rightarrow \infty} E\bigg[ \frac{Dmax^k_d -Dmin_d^k}{d^{1/k-1/2}} \bigg]\le (n-1)\cdot C_k$$


Essentially, in high dimensional data $Dmax^k_d-Dmin_d^k$ (difference between the farthest and nearest distance of the N points to the origin) increases at the rate of $d^{1/k-1/2}$.
This means:
- for $L_1$ -> diverges to infinity
- for $L_2$ (Euclidean) -> bounded by constants
- for all other converges to 0.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2025-02-13T16:00:25.831+01:00 %%
