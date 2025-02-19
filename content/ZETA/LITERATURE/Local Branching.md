---
connections: 
reference: 
tags:
  - theme/operation-research
type: literature_note
created: 2025-02-19 11:52
---
 

>[!SUMMARY] Table of Contents
>- [[Local Branching#Local Branching|Local Branching]]
>    - [[Local Branching#Discussione|Discussione]]
>    - [[Local Branching#Struttura|Struttura]]
>    - [[Local Branching#Motivi perché non funziona|Motivi perché non funziona]]
>    - [[Local Branching#Estensione|Estensione]]

# Local Branching

> Il Local Branching è una tecnica metaeuristica alternativa all'Hard Fixing, in cui non impostiamo direttamente le variabili, ma, tramite un vincolo, scegliamo solo quante.

Nell'hard fixing, data la soluzione euristica $x^H$, dobbiamo decidere: 
- quante variabili $x^e$ fissare a 1
- quali
L'intuizione nel **local branching** è quello di scegliere *solo quante*. 

Aggiungiamo al modello il seguente vincolo:
$$\underbrace{\sum_{e:x_e^H=1} x_e}_{\text{n lati preservati}} \ge n-k$$
che da $k$ gradi di libertà al modello. 

Il nome del vincolo è *Local Branching*, perché, per esempio, con $k=2$ do uno spazio di ricerca come nel 2-OPT. La differenza è che già dal 3-OPT abbiamo un algoritmo $O(n^3)$, mentre nel Local Branching possiamo esplorare una neighborhood anche di 20.

L'approccio non è specifico per il TSP, ma vale in generale.


## Discussione
Potrebbe essere che il modello con un vincolo in più venisse risolto in più tempo, ma si è notato che: 
- *k piccolo* (ordine di 20): il mip solver è più veloce 

Sono tutte prove da implementazioni. 
Quando è stato scritto il paper funzionava bene con $k=5,10$, oggi, con CPLEX molto più veloce, ci possiamo spingere a $k=20,30,50$.

Sto dando al modello di CPLEX un taglio molto deep, che possibilmente potrebbe tagliare il convex hull ottimo (che per il tsp non conosciamo).
Nonostante ciò, il gap che otteniamo è molto più basso. Il gap senza il vincolo sarebbe gigantesco da colmare con il solo Branch&Cut.

Se metto k troppo grande, il gap risulterà troppo grande. Invece se k è troppo piccolo, CPLEX risolverà subito il modello e sarà inutile.

> Da notare che il vincolo proposto vale in questo caso SOLO per il TSP

- Per evitare di riesplorare parti già visitate:
	aggiungere vincolo $\sum_{e:x_e^{H_1}} x_e\le n-k-1$
	in realtà aggiungere questi vincoli non danno migliorie.
- Suggerisce ad ogni iterazione di aumentare il $k$ e ***ricordarsi di cancellare il vincolo precedente***. Come?
  Con `CPXgetnumrows` prima di mettere il vincolo saprò la posizione dove metterà il vincolo, una volta che voglio rimuoverlo esiste una funzione che rimuove il vincolo in quella posizione.


Originariamente, per rendere il vincolo generale e per essere indipendenti dal significato di 0 e 1, era stato scritto cosi: 
$$\underbrace{\underbrace{\sum_{e:x_e^H=0} x_e}_{\text{n flip 0-1}} + \underbrace{\sum_{e:x_e^H=1} (1-x_e)}_{\text{n flip 1-0}}}_{\text{distanza di Hamming } H(x,x^H)} \le k$$
Nel TSP, dato che il numero di 1 è sempre n, il numero di flip è sempre lo stesso, quindi sto calcolando due volte la stessa cosa. Quindi o si rende il vincolo a $2k$ oppure si elimina uno dei due calcoli dei flip -> versione *asimmetrica* 
## Struttura

Parto da un k, se non riesco a trovare nulla entro il timelimit, fisso $k = k+\Delta k$ e ripeto la ricerca.

## Motivi perché non funziona
1) troppi gradi di libertà, per esempio in un paper si è fissato $k=\frac{n^2/2}{2}$, che è decisamente troppo grande
2) si parte da una $x^H$ molto scarsa

## Estensione
Paper "Learning to Search", rete neurale per determinare il $k$. 
Un'idea che è uscita: se non si vuole proprio inserire una NN, posso fissare $k$ al valore minimo per far si che la soluzione $x^*$ rimanga inalterata. 
Per calcolare questo $k$ minimo, chiamato $k^*$: 
$$k^* = \sum_{e:x_e^H=1} (1-x_e^*)$$
Una volta calcolato, possiamo fissare $k$ come la media tra $k^*$ e 0.

Passaggi:
1) build_model
2) rilasso MIP -> LP
3) CPXlpopt
4) CPXgetsol, otteniamo $x^*$
5) calcoliamo $k^*$
6) rimetto le condizioni di interezza, da LP a MIP
7) Local Branching

per convertire da MIP a LP
- settare le variabili (colonne) a intere [^1] (non più binarie), quindi per ogni variabile devo chiamare `CPXsetctype(env,lp, j, 'C')`   
- CPXchproblem(..., CPX_RELAX_LP)
- CPXchprep(..., CPX_MIP)
- alla fine reimpostare tutte le variabili a 'B'

[^1] : cytpe = 'C'






-> stima lagrangiana per uccidere il 90% delle soluzioni



