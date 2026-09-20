---
up:
  - "[[Other Metaheuristics]]"
tags:
  - atomic
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

Nell'hard fixing, data la soluzione euristica $x^H$, dobbiamo decidere *quante* variabili $x^e$ fissare a 1 e *quali*. L'intuizione del **local branching** è quello di scegliere *solo quante*:
$$\underbrace{\sum_{e:x_e^H=1} x_e}_{\text{n lati preservati}} \ge n-k$$
Il vincolo dà $k$ gradi di libertà al modello. Con $k=2$ do uno spazio di ricerca come nel 2-OPT, ma già dal 3-OPT abbiamo un algoritmo $O(n^3)$, mentre nel Local Branching possiamo esplorare una neighborhood anche di $k=20$ efficientemente.

L'approccio non è specifico per il TSP, ma vale in generale.

Quando $k$ è piccolo (ordine di 20), il MIP solver è più veloce nonostante il vincolo aggiuntivo. Con CPLEX moderno ci si spinge a $k=20,30,50$.


## Discussione
Sto dando al modello di CPLEX un taglio molto deep, che possibilmente potrebbe tagliare il convex hull ottimo (che per il tsp non conosciamo).
Nonostante ciò, il gap che otteniamo è molto più basso. Il gap senza il vincolo sarebbe gigantesco da colmare con il solo Branch&Cut.

Se metto k troppo grande, il gap risulterà troppo grande. Invece se k è troppo piccolo, CPLEX risolverà subito il modello e sarà inutile.

> Da notare che il vincolo proposto vale in questo caso SOLO per il TSP

- Per evitare di riesplorare parti già visitate:
	aggiungere vincolo $\sum_{e:x_e^{H_1}} x_e\le n-k-1$
	in realtà aggiungere questi vincoli non danno migliorie.
- Suggerisce ad ogni iterazione di aumentare il $k$ e ***ricordarsi di cancellare il vincolo precedente***. Come?
  Con `CPXgetnumrows` prima di mettere il vincolo saprò la posizione dove metterà il vincolo, una volta che voglio rimuoverlo esiste una funzione che rimuove il vincolo in quella posizione.


La formulazione generale del vincolo di Local branching è indipendente dal significato di 0 e 1:
$$\underbrace{\underbrace{\sum_{e:x_e^H=0} x_e}_{\text{n flip 0-1}} + \underbrace{\sum_{e:x_e^H=1} (1-x_e)}_{\text{n flip 1-0}}}_{\text{distanza di Hamming } H(x,x^H)} \le k$$
Nel TSP il numero di 1 nella soluzione è sempre $n$ (ogni nodo ha grado 2), quindi i flip da $0\rightarrow1$ e da $1\rightarrow0$  sono sempre in numero uguale. Si sta calcolando la stessa cosa due volte: si può quindi usare la versione *asimmetrica*, eliminando uno dei due termini oppure portando il bound a $2k$.

## Struttura
La struttura iterativa: si parte da un $k$ iniziale; se non si trova una soluzione migliorante entro il timelimit, si aggiorna $k=k+\Delta k$ e si ripete.

Due motivi per cui non funziona:
1. $k$ troppo grande -> troppi gradi di libertà, gap enorme
2. si parte da una $x^H$ molto scarsa

In CPLEX, prima di aggiungere il vincolo, salvare la posizione corrente con `CPXgetnumrows`. Quando si vuole rimuovere il vincolo precedente, usare quella posizione. **Sempre cancellare il vincolo precedente** prima di aggiungere uno nuovo con $k$ aggiornato.

## Estensione
Dal Paper "Learning to Search", rete neurale per determinare il $k$. 
Invece di usare una NN, si calcola il $k^*$ minimo tale che la soluzione ottima $x^*$ rimanga raggiungibile:
$$k^* = \sum_{e:x_e^H=1} (1-x_e^*)$$
Si usa poi $k=k^*/2$ come punto di partenza. Procedura:
1) `build_model`
2) Rilassare MIP -> LP
3) `CPXlpopt` -> `CPXgetsol` per $x^*$
4) Calcolare $k^*$
5) Reimpostare le variabili a binarie `'B'` e tornare a MIP con `CPXchprobtype(..., CPX_MIP)`
6) Applicare Local branching con il $k$ calcolato

per convertire da MIP a LP
- settare le variabili (colonne) a intere [^1] (non più binarie), quindi per ogni variabile devo chiamare `CPXsetctype(env,lp, j, 'C')`   
- CPXchproblem(..., CPX_RELAX_LP)
- CPXchprep(..., CPX_MIP)
- alla fine reimpostare tutte le variabili a 'B'

[^1] : cytpe = 'C'

# See also
- [[Other Metaheuristics]] — Simulated Annealing e Genetico affrontano lo stesso problema di diversificazione/intensificazione con approcci diversi
