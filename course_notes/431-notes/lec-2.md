# Lec 2

### Math 431 - Introduction to Probability

#### September 8, 2023

Last time.

Probability Space. A probability space is a triple $$(\Omega, \mathcal{F}, P)$$.

* $$\Omega$$ is the sample space.(set of all possible outcomes)
* $$\mathcal{F}$$ set of events. (Subset of $$\Omega$$). ($$\emptyset, \Omega \in \mathcal{F}$$)
* $$P$$ is a probability measure. $$P: \mathcal{F} \rightarrow [0,1]$$

$$A_1, \dots, A_n$$ disjoint -> $$P(A_1 \cup \dots \cup A_n) = P(A_1) + \dots + P(A_n)$$

$$P(\bigcup_iA_i) = \sum_iP(A_i)$$

#### Uniformly chose element froma finite set.

$$\Omega$$ is a finite set.

Each outcome is equally likely.

$$\Omega = {\omega_1, \dots, \omega_n}$$

$$P({\omega_i}) = P({\omega_2}) = \dots = P({\omega_n}) = \frac{1}{n}$$

$$\sum_iP({\omega_i}) = P(\bigcup_i^n{\omega_i} =1$$

$$A\subset \Omega$$. $$P(A) = P({a_1, \dots, a_n}) = \sum_i=1^nP({\omega_i}) = \frac{|A|}{|\Omega|}$$.

Worksheet.

1- Possible outcomes: $${(a,b,c), 1 \leq a \leq 6, b , c \in {H,T}}$$

2- b. $${(a,b), 1\leq a, b \leq 6}$$

d. $$\Omega = {(a,b), 1\leq a \leq b \leq 6}$$ - different. (1,1) is 1/36 and (1,2) is 1/18 (because (2,1) (1,2) is same.)

### Sampling

We have a finite set $$X$$. Non empty set.

We take a sample of size $k$ from the set unfiromly at random.

Can take without replacement or with replacement.

Can also consider with order or without order.

With order: $$(a_1, a_2, \dots, a_k)$$.- ordered sequence. without order: pick 3 dice and get a set with 3 dice (without order information). - $${{a_1, a_2, \dots, a_k}}$$

**Sample from X with replacement k times.**

$$\Omega = {(a_1, a_2, \dots, a_k), a_i \in X} = X^k$$

$$|\Omega| = n^k$$ , $$n = |X|$$

**Sample from X without replacement k times with order**

$$1 \leq k \leq n$$

$$\Omega = {(a_1, a_2, \dots, a_k), a_i \in X, a_i \neq a_j \text{ if } i \neq j}$$

$$|\Omega| = \frac{n!}{(n-k)!}$$

**without replacement and without order**

size = $$k$$

$$\Omega = {{a_1, a_2, \dots, a_k}, a_i \in X, a_i \neq a_j \text{ if } i \neq j}$$

$$|\Omega| = \binom{n}{k} = \frac{n!}{k!(n-k)!}$$
