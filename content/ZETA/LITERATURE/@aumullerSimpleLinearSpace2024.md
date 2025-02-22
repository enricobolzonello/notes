---
connections: 
reference: 
tags:
  - type/paper
  - theme/approximate-nearest-neighbor
type: literature_note
created: 2024-12-20 19:04
modified: 
citekey: aumullerSimpleLinearSpace2024
status: unread
dateread:
---

> [!Cite]
> [1] M. Aumüller, F. Boninsegna, e F. Silvestri, «A Simple Linear Space Data Structure for ANN with Application in Differential Privacy», 11 settembre 2024, _arXiv_: arXiv:2409.07187. doi: [10.48550/arXiv.2409.07187](https://doi.org/10.48550/arXiv.2409.07187).


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
>> **FirstAuthor**:: Aumüller, Martin  
> **Author**:: Boninsegna, Fabrizio  
> **Author**:: Silvestri, Francesco  
~    
> **Title**:: A Simple Linear Space Data Structure for ANN with Application in Differential Privacy  
> **Year**:: 2024   
> **Citekey**:: aumullerSimpleLinearSpace2024  
> **itemType**:: preprint  
> **DOI**:: 10.48550/arXiv.2409.07187    

> [!LINK] 
> > [Preprint PDF](file:///Users/enricobolzonello/Zotero/storage/5W7UIMGF/Aumüller%20et%20al.%20-%202024%20-%20A%20Simple%20Linear%20Space%20Data%20Structure%20for%20ANN%20with%20.pdf).


> [!Abstract]
>
> Locality Sensitive Filters are known for offering a quasi-linear space data structure with rigorous guarantees for the Approximate Near Neighbor search problem. Building on Locality Sensitive Filters, we derive a simple data structure for the Approximate Near Neighbor Counting problem under differential privacy. Moreover, we provide a simple analysis leveraging a connection with concomitant statistics and extreme value theory. Our approach achieves the same performance as the recent findings of Andoni et al. (NeurIPS 2023) but with a more straightforward method. As a side result, the paper provides a more compact description and analysis of Locality Sensitive Filters for Approximate Near Neighbor Search under inner product similarity, improving a previous result in Aum\"{u}ller et al. (TODS 2022).
>.
> 

# Notes
La struttura dati è una hash table, con chiave l’indice i di $a_i$ che produce il massimo prodotto vettoriale tra $a_i$ e $x$ dove:

- $a_i$ è un vettore random estratto dalla Gaussiana (se ne estraggono m, che sono anche il numero di chiavi della hash table)
- $x$ è il vettore di input

I bucket sono definiti da:

$$\{i\in [m]:\langle a_i,q\rangle \ge \eta \}$$

dunque tutte le chiavi della hash table tale che il prodotto vettoriale tra il vettore random e la query sia maggiore di quel fattore.

Intuizione del perché funziona:

teorema 2, se associamo il vettore Gaussiano più vicino $a_x=\arg\max\langle a,x\rangle$ troveremo x associato ad un vettore Gaussiano con prodotto interno $\langle q,a_x\rangle \sim \delta \sqrt{2\log m}$

LSH suffers from large space requirements.

requires $O(nd+n^{1+p})$ memory words

## Tensoring

to reduce:

- pre-processing time
- space
- expected query time

create $t$ independent data structures $D_1,…,D_t$ each using $m^{1/t}$ Gaussian vectors $a_{i,j}$.

Search in all buckets.


# Annotations%% begin annotations %%


%% end annotations %%

%% Import Date: 2024-12-20T19:04:08.784+01:00 %%
