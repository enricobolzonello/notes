---
connections: 
reference:
tags: 
 - type/paper
type: literature_note
created: 2025-02-13 18:08
modified:
citekey: mirkesFractionalNormsQuasinorms2020
status: unread
dateread:
---

> [!Cite]
> [1] E. M. Mirkes, J. Allohibi, e A. N. Gorban, «Fractional norms and quasinorms do not help to overcome the curse of dimensionality», _Entropy_, vol. 22, fasc. 10, p. 1105, set. 2020, doi: [10.3390/e22101105](https://doi.org/10.3390/e22101105).


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
>> **FirstAuthor**:: Mirkes, Evgeny M.  
> **Author**:: Allohibi, Jeza  
> **Author**:: Gorban, Alexander N.  
~    
> **Title**:: Fractional norms and quasinorms do not help to overcome the curse of dimensionality  
> **Year**:: 2020   
> **Citekey**:: mirkesFractionalNormsQuasinorms2020  
> **itemType**:: journalArticle  
> **Journal**:: *Entropy*  
> **Volume**:: 22  
> **Issue**:: 10   
> **Pages**:: 1105  
> **DOI**:: 10.3390/e22101105    

> [!LINK] 
> > [Preprint PDF](file:///Users/enricobolzonello/Zotero/storage/AFYUXECP/Mirkes%20et%20al.%20-%202020%20-%20Fractional%20norms%20and%20quasinorms%20do%20not%20help%20to%20ove.pdf).


> [!Abstract]
>
> The curse of dimensionality causes the well-known and widely discussed problems for machine learning methods. There is a hypothesis that using of the Manhattan distance and even fractional quasinorms lp (for p less than 1) can help to overcome the curse of dimensionality in classification problems. In this study, we systematically test this hypothesis. We confirm that fractional quasinorms have a greater relative contrast or coefficient of variation than the Euclidean norm l2, but we also demonstrate that the distance concentration shows qualitatively the same behaviour for all tested norms and quasinorms and the difference between them decays as dimension tends to infinity. Estimation of classification quality for kNN based on different norms and quasinorms shows that a greater relative contrast does not mean better classifier performance and the worst performance for different databases was shown by different norms (quasinorms). A systematic comparison shows that the difference of the performance of kNN based on lp for p=2, 1, and 0.5 is statistically insignificant.
>.
> 

# Notes
The $l_p$ functional $||x||_p$ in d dimensional vector space is defined as:

$$||x||_p = \bigg(\sum_{i=1}^d x_i^p\bigg)^{1/p}$$

- norm for $p\ge 1$
- quasinorm for $0<p<1$ (violates triangle inequality)

using quasinorms was proposed in ([Aggarwal et al., 2001](zotero://select/library/items/WAIY6QY6)), because using them can compensate the distance concentration.

Problem: time of calculation and algorithms which assume triangle inequality cannot use it.

This paper demonstrated:

1) small p does not prevent distance concentration

2) smaller distance concentration does not mean better accuracy.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2025-02-13T18:08:57.644+01:00 %%
