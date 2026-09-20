---
Priority_Level: 3 Medium
Status: 4 Completed
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/deep_learning"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
closed: 2025-01-07T11:03
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description

>[!SUMMARY] Table of Contents
>- [[Transformer#Transformer|Transformer]]
>	- [[Transformer#Self-Attention|Self-Attention]]
>	- [[Transformer#Multi-Head Attention|Multi-Head Attention]]
>	- [[Transformer#Transformer Architecture|Transformer Architecture]]
>		- [[Transformer#Further improvements|Further improvements]]

# Transformer

> A transformer is a deep learning architecture developed by researchers at Google and based on the multi-head attention mechanism, proposed in a 2017 paper "Attention Is All You Need". Text is converted to numerical representations called tokens, and each token is converted into a vector via looking up from a word embedding table. At each layer, each token is then contextualized within the scope of the context window with other (unmasked) tokens via a parallel multi-head attention mechanism allowing the signal for key tokens to be amplified and less important tokens to be diminished.

LSTM and GRU improved RNN's performance on long sequences, but at some costs:
- increased complexity
- sequential model (creates bottlenecks)
The transformer architecture allows to be *parallel*. 

Transformer is basically combining [[Sequence to Sequence Architectures#Attention Model |Attention]] with *CNN*. 

## Self-Attention
> attention-based representations for each of the words in the input sequence

$A(q,K,V)$ = attention-based vector representation of a word, which is calculated for each word $A^{<1>},..., A^{<T_x>}$. 
The representation will look at surrounding words to choose the appropriate embedding. 

$$
A(q,K,V) = \sum_i \frac{\exp(q\cdot k^{<i>})}{\sum_j \exp(q\cdot k^{<j>})}v^{<i>}
$$
where:
- $q$ is called *Query* and $q^{<k>} = W^Qx^{<k>}$
- $k$ is called *Key* and $k^{<k>} = W^kx^{<k>}$
- $v$ is called *Value* and $v^{<k>} = W^vx^{<k>}$
Names are due to Databases analogy, for example if we have the phrase:
> Jane visite l'Afrique en septembre

For word 3 (l'Afrique), the query might be "What's happening there?" and the key for word 2 might be "action", which is the most similar, so we get the value corresponding to the key.


## Multi-Head Attention
Repeat the self-attention step for all words and we get:
$$
Attention(W_1^Q Q,W_1^K K,W_1^V V)
$$

Do the previous step multiple times with different matrices $W_i$ with $i\in [0,h)$, you can see it like asking different questions or having different features. 
Then:
$$
MultiHead(Q,K,V) = concat(head_1, head_2,...)W_0
$$

## Transformer Architecture
In the encoder, the NN identifies most important sections.
In the decoder, the NN tries to predict the next word in the translation.

The decoder inputs a partial phrase and predicts the next word.

![[transformer_architecture.png]]


### Further improvements

**Positional Encoding**:
![[transformer_posencoding.png]]

$2i$ gives a sinusoid while $2i+1$ gives the correspondent cosinusoid.
Each word will have a different $p$ vector with fixed length $d$, and each position will correspond to a point in the sinusoid or cosinusoid.


**Add & Norm**: 
At each layer there is an add and normalize block

**Decoder output**:
Linear and softmax layers

**Masker Multi-Head**:
assumes that the first words are perfect translations and masks the rest. In this way we can verify if the next word translated corresponds




















































