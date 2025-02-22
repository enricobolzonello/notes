---
connections: 
reference: 
tags:
  - theme/operation-research
type: literature_note
created: 2025-02-19 11:53
---
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#permanent_note), optionQuery(#literature_note), optionQuery(#fleeting_note)):connections]` 

>[!SUMMARY] Table of Contents
>- [[Altri Metaeuristici#Simulated Annealing|Simulated Annealing]]
>	- [[Altri Metaeuristici#Alternativa (inventata da Fischetti)|Alternativa (inventata da Fischetti)]]
>- [[Altri Metaeuristici#Genetico|Genetico]]
>	- [[Altri Metaeuristici#Inizializzazione|Inizializzazione]]
>	- [[Altri Metaeuristici#Genetico|Genetico]]
>		- [[#Crossover|Crossover]]
>		- [[#Repair|Repair]]

# Simulated Annealing
Da ispirazione fisica.

In metallurgia, riscaldando e successivamente raffreddando il metallo si presenta una configurazione atomica ottimale di minima energia e massima forza.
Il punto chiave è che a temperatura alta le molecole vibrano molto e abbassando la temperatura vibrano meno. Se raffreddo *lentamente*, riesco ad uscire dai minimi locali e riesco molto spesso ad arrivare al minimo globale

Simulato: 
- genero uno scambio 2opt random con un $\Delta \text{costo}$
- se $\Delta \text{costo}<0$, cambio la soluzione migliore 
- altrimenti, ho peggiorato la soluzione. 
	- se è piccolo, con una certa probabilità aggiorno la soluzione migliore
	- se è grande, non viene eseguita la mossa

Il motivo per cui implementiamo una soluzione peggiorativa è la ***DIVERSIFICAZIONE***.

Forma "*Metropolis*":

$$
Prob = \begin{cases}
1 & \text{se }\Delta\text{costo} < 0\\
e^{-\frac{\Delta \text{costo} / \text{costo medio sol.}}{T}} & \text{altrimenti}
\end{cases}
$$
$T$ = temperatura.
All'inizio T è grande, quindi c'è una grande probabilità di accettare mosse anche molto peggiorative. T viene aggiornato ad ogni iterazione con un *fattore di cooling down*, di solito con la regola $T = T \cdot 0.99$. 

Iperparametri da scegliere: 
- $T_0$, temperatura iniziale
- cooling factor (es, 0.99)

Un'altra possibilità è dopo un certo numero di iterazioni (terzo iperparametro) si riporta la temperatura al massimo e si ripete il raffreddamento. 

## Alternativa (inventata da Fischetti)
-> visione economica
Applico uno sconto (per esempio tra 20 e 50%) se $\Delta {costo}>0$, se la soluzione scontata è minore della soluzione migliore corrente, aggiorno. 
Come prima, abbasso lo sconto.


# Genetico

Il campione mondiale è un algoritmo genetico.
Gli euristici hanno due componenti principali:
- diversificazione
- intensificazione

Si lavora con una *popolazione*, che sono soluzioni del TSP. 
Come iperparametro di popolazione si sta in un range tra 100 e 1000. 

Si parte dalla popolazione 0 nell'epoca 0 e si simula la realtà:
- prendere due elementi della popolazione, si combinano per ottenerne uno nuovo -> si ottiene una popolazione più grande di 1
	come scelgo i genitori? 
	 - una possibilità è accoppiare il campione con tutti -> non funziona bene, serve accoppiare anche individui pessimi
	 - random 
- un'altra operazione è la *mutazione*, si duplica un elemento e si randomizza per cambiarlo
- alla fine dell'iterazione, abbiamo ottenuto una popolazione molto superiore al nostro iperparametro. Dobbiamo ammazzare le soluzioni con minor *fitness* (nel nostro caso $-costo$)

Quello che ci aspettiamo è che gradualmente aumenti il costo medio (nel nostro caso, meglio vedere come migliora il campione). 

Una cosa che si fa è non uccidere mai il campione, e conservalo per l'iterazione successiva. 

Un'altra estensione è quella di tenere le soluzioni che non sono valide per il TSP, definendo una nuova funzione di fitness:
$$
costo\_eq = c(sol) + M_1 \cdot (\#\text{ vert. di grado 2}) + M_2\cdot (\#\text{ componenti connesse}-1)
$$

> La proposta di Fischetti è di avere *solo* soluzioni del tsp

## Inizializzazione
- soluzioni completamente random (PIU USATA)
- partire dagli euristici e fare kick

## Accoppiamento
Dobbiamo decidere come rappresentare un individuo. Nella natura è rappresentato dal suo *genoma*, stessa cosa da applicare nel tsp.

Il più semplice è di rappresentarlo come lista di nodi.

### Crossover
Prendere dal padre un pezzo e dalla madre il secondo pezzo. 
Il punto di crossover è casuale tra 1/4 e 3/4

Il problema di questo metodo è che probabilmente la soluzione non sarà più una soluzione del tsp. Queste soluzioni vanno penalizzate (se vogliamo anche soluzioni non del tsp), altrimenti dobbiamo applicare una procedura chiamata *Repair*.

### Repair
- scorro la lista e salto i vertici che ho già visitato (*Short Cut*)
- rimarranno fuori i vertici isolati. Per connetterli si usa l'*Extra Mileage*. 
Alla fine otteniamo una soluzione del tsp, chiaramente non ottimale, quindi possiamo applicare il 2opt. 


---

Una visione dell'algoritmo genetico è quella di aggiungere un buon metodo di diversificazione su cui poi applicare il 2opt. 



