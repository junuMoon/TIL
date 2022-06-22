# Hidden Markov Model
HMM is a probabilistic sequence model: given a sequence of units (words, letters, morphemes, sentences, whatever), it **computes a probability distribution over possible sequences of labels** and chooses the best label sequence. 

## Markov Chains
- Represents the probabilities of sequences of random variables(states) 
- Markov Assumption: when predicting future, the past doesn’t matter, only the present
	- `P(qi=a|q1, q2, … , qi-1) = P(qi=1|qi-1)`
- Components
	- State: Node
	- Probability: Edge
		- `P(wi|wi-1)`
	- Q: a set of N states
	- A: a transition probability matrix A
		- aij: probability moving from state i to state j
	- `π`: an initial probability distribution over states
		- the probabilities that starts in state i
		- `∑πi = 1`

## Hidden Markov Model
- Hidden event: We don’t observe pos tags in a text. Rather, we see words and must infer the tags from the word sequence
- Components
	- `O = o1, o2, … , oT`: a sequence of T observations
	- `B = bi(ot)`: a sequence of observation likelihoods
		- emission probabilities 
- Assumption: the probability of an output observation `oi`  depends only on the state that produced the observation `qi` and not on any other states or any other observations
	- `P(oi|q1, … , qT, o1, … , oT) = P(oi|qi)`

## HMM tagger
- `A` matrix contains the tag transition probabilities 
	- Compute the maximum likelihood estimate of this transition probability by counting
	- `P(ti|ti-1) = C(ti-1, ti) / C(ti-1)`
- `B` matrix contains emission probabilities
	- the probability of a tag will be associated with a word
	- `P(wi|ti) = C(ti, wi) / C(ti)`
	- ITS NOT: “Which is the most likely tag for the word _will_?”
	- ITS: “If we were going to generate a MD, how likely is it that this modal would be _will_?”

### HMM tagging as decoding
Decoding: Given `HMM(ƛ) = (A, B), O = o1, o2, … , oT`, find the most probable sequence of states `Q = q1q2q3…qT`

- `t-hat_i:n = argmaxP(t1…tn|w1…wn)`
	- Bayes’ rule applied:  `argmax{P(w1…wn|t1…tn) * P(t1…tn) / P(w1…wn)}`
- Assumption
	- The probability of a word depends only on its own tag and is independent of neighboring words and tags
		- `P(w1…wn|t1…tn) := ∏P(wi|ti)`
	- Bigram assumption: the probability of a tag depends only on the previous tag
		- `P(t1…tn) := ∏P(ti|ti-1)`
- Assumption applied:  `t-hat_i:n = argmax∏P(wi|ti)P(ti|ti-1)`
	- `P(wi|ti)`: emission
	- `P(ti|ti-1)`: transition

### Viterbi Algorithm

![](https://s2.loli.net/2022/06/22/FEaCPYrtZxqkv8T.png)

- Lattice: a probability matrix[# of states, # of observations]
	- A column for each observation `ot`
	- A row for each states
- `vt(j) = max{vt-1(i) * aij * bj(ot)`
	- `vt-1(i)`: the previous Viterbi path probability
	- `aij`: transition probability from `qi` to `qj`
	- `bj(ot) = P(ot|qj)`: the state observation likelihood

