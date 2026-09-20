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
>- [[Sequence to Sequence Architectures#Basic Model|Basic Model]]
>- [[Sequence to Sequence Architectures#Picking the Most Likely Sentence|Picking the Most Likely Sentence]]
>- [[Sequence to Sequence Architectures#Beam Search|Beam Search]]
>	- [[Sequence to Sequence Architectures#Length Normalization|Length Normalization]]
>	- [[Sequence to Sequence Architectures#Discussion|Discussion]]
>- [[Sequence to Sequence Architectures#Error Analysis|Error Analysis]]
>- [[Sequence to Sequence Architectures#Bleu Score|Bleu Score]]
>- [[Sequence to Sequence Architectures#Attention Model|Attention Model]]
>	- [[Sequence to Sequence Architectures#Computing attention|Computing attention]]
>- [[Sequence to Sequence Architectures#Examples in Audio Data|Examples in Audio Data]]
>	- [[Sequence to Sequence Architectures#Speech Recognition|Speech Recognition]]

> Sequence Models have been motivated by the analysis of sequential data such text sentences, time-series and other discrete sequences data. These models are especially designed to handle sequential information while Convolutional Neural Network are more adapted for process spatial information.

## Basic Model
Suppose a translation from French to English example.
A first RNN could take care of encoding the input, this outputs a vector which will be fed to the decoder with a second RNN

Components:
- *Encoding network*
- *Decoding network*

This basic model could also work for Image captioning:
- learn an encoding with a convolutional network
- concatenate a RNN to generate an output which is a set of words

-> in the next section we will explore how to get not a random output (like in this basic model), but the most likely

## Picking the Most Likely Sentence
The basic model described above is very similar to a Language Model, with the only difference that the input is a vector processed by another network.
For this reason we will call the "machine translation" model ***Conditional Language Model***, which compute:
$$
P(y^{<1>},...,y^{<T_y>}| x^{<1>},...,x^{<T_x>})
$$

What we want now is $\arg \max_{y^{<1>},...,y^{<T_y>}} P(y^{<1>},...,y^{<T_y>}| x)$
To do it we will use an algorithm called ***Beam Search***. 

A greedy approach will not work, will return less optimal sentences.


## Beam Search
It has an hyperparameter $B$ (Beam Width), which regulates how many words we should keep. 
At the first step, the algorithm takes the $B$ most likely words, at the second step it takes the $B$ most likely words for each of the words taken at the last step, continues like this for every position.

For the decoder, at each position it will output: 
$$
P(y^{<2>}|x, y^{<1>})
$$

Some refinements:
### Length Normalization
instead of maximizing the product:
$$
\arg \max \prod_{t=1}^{T_y} P(y^{<t>}| x,y^{<1>},..,y^{<t-1>})
$$
which could give very small numbers and lead to errors due to numerical rounding of floating point numbers, in practice the log scale is used like this: 
$$
\arg \max \sum_{t=1}^{T_y} \log P(y^{<t>}| x,y^{<1>},..,y^{<t-1>})
$$

Also, to avoid that longer sequences get small probabilities, we multiply the factor $1/T_y^{\alpha}$, usually with $\alpha = 0.7$.

### Discussion

Beam width $B$:
- large : better result, slower
- small : worse result, faster
- usually around 10, 100 is considered very large

Beam search runs faster than other search algorithms, but does not guarantee to find the exact maximum.


## Error Analysis

human: $y^*$
algorithm: $\hat{y}$

**Cases**:
1) $P(y^*| x) > P(\hat{y} |)x)$, beam search is at fault
2) $P(y^*|x) \le P(\hat{y}|x)$, $y^*$ is a better translation than $\hat{y}$, so RNN model is at fault

for each dev set example, do this comparison and see who is at fault.
If you find Beam Search is at fault -> increase beam width
else -> deeper analysis to see if apply regularization and other ML techniques

## Bleu Score
>When you have multiple great answers, how do you measure accuracy?

BLEU (BiLingual Evaluation Understanding) could be a substitute to having humans evaluate each output.

As an example on Bigrams (pairs of words), consider the following references:
*Reference 1*: The cat is on the mat
*Reference 2*: There is a cat on the mat
and the algorithm output:
*Output*: The cat the cat on the mat

|         | count | count_{clip} |
|---------|-------|--------------|
| the cat | 2     | 1            |
| cat the | 1     | 0            |
| cat on  | 1     | 1            |
| on the  | 1     | 1            |
| the mat | 1     | 1            |
so the precision is $\sum count/\sum count_{clip}$,
- $count$, total number of bigrams in the output
- $count_{clip}$, maximum number of bigrams of all references 

on unigrams: 
$$
p_1 = \frac{\sum_{uni\in \hat{y}} Count_{clip}(uni)}{\sum_{uni\in \hat{y}} Count(uni)}
$$
more generally, on n-grams:
$$
p_n = \frac{\sum_{ngram\in \hat{y}} Count_{clip}(uni)}{\sum_{ngram\in \hat{y}} Count(uni)}
$$


We can also define the ***Combined Blue score*** on multiple ngrams:
$$
BP \cdot \exp\bigg(\frac{1}{n}\sum_{k=1}^n p_k\bigg)
$$
$BP$ is the *brevity penalty*, defined as: 

$$
BP=\begin{cases}
1 & \text{if output\_length > reference\_length} \\
\exp(1-\text{reference\_length}/\text{output\_length}) & \text{otherwise}
\end{cases}
$$


which penalizes shorter translations.


## Attention Model
Usually, with short sentences and sentences that are too long the model performs poorly.
The intuition is that a human translator translates a small part, than reads the next and translates and goes on until it is done.

Computes a set of attention weights $\alpha^{<t,t^\prime>}$, which says how much attention word $t^\prime$ needs with respect to word $t$. This repeats for each word $t$ of the input.

the context $c$ will be the weighted sum:
$$
c^{<1>} = \sum_{t^\prime} \alpha^{<1,t^\prime>}a^{<t^\prime>}
$$
with the constraint that $\sum_{t^\prime} \alpha^{<1,t^\prime>} = 1$.

![[attention_model.png]]

### Computing attention

$$
\alpha^{<t,t^\prime>} = \frac{\exp(e^{<t,t^\prime>})}{\sum_{t^\prime=1}^{T_x} \exp(e^{<t,t^\prime>})}
$$
parameters $e^{<t,t^\prime>}$ can be computed with a small Neural Network with inputs $s^{<t-1>}$ and $a^{<t^\prime>}$. 

One downside is the *quadratic time* of the algorithm.



## Examples in Audio Data

### Speech Recognition





















