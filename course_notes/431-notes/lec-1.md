# Lec 1

Experiment with uncertain outcomes.

We would like to measure the likelihood of an outcome or a group of outcomes.

* How to make this rigorous.
* Random numbers.

Repeated experiments (patterns)

Modeling real life examples

Flip a fair coin: probability of head? $$\frac{1}{2}$$

Roll a fair die:  {3,6} = p = $$\frac{2}{6}$$

1. flip a coin 10 times, probability of getting 10 tails.
2. Flip a  coin until get a tail. What is the probability we need to flip coin more than 5 times.
3. Suppose you have a dart board. Radius of 9 inches. What is the probability of landing less than 1 inch

Answer

1: $$\frac{1}{2}^{10}$$

$$(a_1, a_2, \dots, a_{10})$$, $$a_i \in \{H, T\}$$. There are 2^10 outcomes. One would be all tails. So $$\frac{1}{2^{10}}$$.

2: first 5 flips are all heads. $$\frac{1}{2^5}$$.&#x20;

3: $$\frac{\pi}{81\pi}$$= $$\frac{1}{81}$$.&#x20;

Experiment:

Probability of something.&#x20;



Kolmogorov's axioms of probability.

$$\Omega$$ sample space. Set of all possible outcomes. (Non-empty, at least 1 possible outcomes)

$$F$$: set of event. Event is a subset of $$\Omega$$.  $$\emptyset \in F, \Omega \in F$$

$$P$$: function $$f \rightarrow [0,1]$$ . (Probability of the event)

$$(\Omega, F, P)$$ - probability space.

$$F \subset \{\text{all subset of} \Omega\} = 2^{\Omega} = P(H)$$





E.g

Flip a coin.  $$\Omega = \{ H, T\}$$ $$F = \{ \{H\}, \{T\}, \emptyset, \{H, T\}\}$$

Roll a die $$\Omega = \{1,2,3,4,5,6\}$$&#x20;

Flip a coin 10 times.$$\Omega = \{(a_1,\dots,a_{10}); a_i \in \{H,T\}\}$$$$= \{H,T\}^{10}$$

$$A, B$$ sets. $$A \times B = \{(a,b), a\in A, b\in B\}$$



$$A \in F$$ $$0\leq P(A) \leq 1$$.&#x20;

$$P(\emptyset) = 0$$

$$P(\Omega) = 1$$

$$A_1, A_2, \dots,$$ disjoint event. $$P(\bigcup_i Ai) = \sum_i P(A_i)$$. (Additivity)





