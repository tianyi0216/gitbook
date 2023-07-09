---
description: https://www.sciencedirect.com/science/article/pii/S0307904X21005291
---

# Multivariate Distribution and Inference Applications

Summary: The paper introduce a multivariate family of distributions for multivariate count data with excess zeros,which is a multivariate extension of univariate zero-inflated bell distribution. Model parameters are estimated using traditional maximum likelihood estimation. They also develop a EM algorithm to compute the MLE of parameters with closed-form expressions.&#x20;

Univariate bell family's Probability Mass Function:

$$
f_{Bell}(x; \alpha) := Pr(X = x) = \exp(1-e^{W(\alpha)})\frac{W(\alpha)^{x}B_x}{x!}, x = 0,1,\dots
$$

where $$\alpha > 0$$, $$W(.)$$ denote the principal branch of Lambert function, $$B_x$$ are the bell numbers. We use $$X \sim Bell(\alpha)$$to denote this univariate distribution. Its properties:

* Belongs to one-parameter exponential family of distributions
* It is infinitely divisible
* Variance larger than mean. $$E(X) = \alpha$$ and $$Var(X) = \alpha[1+W(\alpha)]$$ and $$E(X) > Var(X)$$

Bell distribution might be suitable for data with overdispersion, unlike poisson.&#x20;

Univariate Zero-inflated bell distribution. Let $$D$$ denote a degenerate distribution at constant $$c$$ i.e $$Pr(D = c) = 1$$, $$D \sim Degenerate(c)$$.&#x20;

Let $$D \sim Degenerate(0)$$ and $$X \sim Bell(\alpha)$$. Assume $$D$$ and $$X$$ are independent. Thus, PMF of ZIB can be expressed in the form of&#x20;

$$
f_{ZIB}(y; \alpha, \omega) = \begin{cases}
\omega + (1-\omega)e^{1-e^{W(\alpha)}} & y=0, \\
(1-\omega)e^{1-e^{W(\alpha)}}\frac{W(\alpha)^yB_y}{y!} & y=1,2\dots \\
\end{cases} \\
= [\omega+(1-\omega)e^{1-e^{W(\alpha)}}]\mathbb{I}(y=0)+[(1-\omega)e^{1-e^{W(\alpha)}}\frac{W(\alpha)^yB_y}{y!}]\mathbb{I}(y\neq0)
$$

$$
f_{ZIB}(y; \alpha; \omega)= \begin{cases}
$$

Where $$\alpha > 0 , \omega \in (0, 1)$$ and $$\mathbb{I}(.)$$ denote indicator function. ZIB is a mix a distribution degenerate at zero with Bell distriution.&#x20;

$$Y \sim ZIB(\alpha, \omega)$$ admit following stochastic representation:

$$
Y  \overset{D}= ZX = \begin{cases}
0 & \text{with probability }\omega\\
X & \text{with probability} (1-\omega)\\
\end{cases}
$$

Where $$Z \sim Bernoulli(1-\omega)$$, $$X \sim Bell(\alpha)$$ and $$Z\perp X$$. Random variables on both sides of the squality have the same distribution(Y, ZX). From above, it is immediate that $$E(Y) = E(Z)E(X)= (1-\omega)\alpha, E(Y^2)=E(Z)E(X^2)=(1-\omega)\alpha[1+\alpha+W(\alpha)]$$

and $$VAR(Y) = (1-\omega)\alpha[1+\alpha \omega + W(\alpha)]$$.&#x20;

Poisson can be effected by overdisperson due to zero-inflated dataset, thus bell distribution might be more suitable.

### Multivariate ZIB distribution.

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption><p>Model (to lazy to type all again since it was typed before)</p></figcaption></figure>

**Remark 2** PMF of $$Y \sim MZIB(\alpha, \omega)$$ can be expressed as $$f(y;\alpha , \omega ) = \omega Pr(D = y) + (1-\omega )Pr(X = y)$$, where $$D = (D_1, \dots, D_m)^T$$ and $$\{D_r\}_{r=1}^m \overset{iid}\sim Degenerate(0)$$.

**Distributional Properties**

From stochastic representation, we immediately obtain&#x20;

$$
E(Y) = (1-\omega)\alpha , E(YY^T) = (1- \omega)[\text{diag} \{ \alpha \} + \text{diag} \{ M \} + \alpha \alpha^T] \\
VAR(Y) = (1-\omega)[\text{diag} \{\alpha\} + \text{diag}\{M\} + \omega \alpha \alpha^T]
$$

Where $$M = (\alpha_1W(\alpha_1), \dots , \alpha_mW(\alpha_m))^T$$ and $$\text{diag}\{\alpha \}, \alpha = (\alpha_1, \dots, \alpha_m)^T$$ denotes an $$m \times m$$ diagonal matrix with element $$\alpha_r (r= 1, \dots, m)$$. We have that&#x20;

$$
CORR(Y_j, Y_k) = \omega (\alpha_j \alpha_k)^{\frac{1}{2}} \frac{[1 + W(\alpha_j) + \omega \alpha_j]^\frac{-1}{2}}{[1 + W(\alpha_k) + \omega \alpha_k]^]\frac{1}{2}} , j\neq k
$$

If $$\alpha_j = \alpha_k = \alpha$$, we have $$CORR(Y_j, Y+k) = \frac{\omega \alpha}{[1 + W(\alpha) + \omega \alpha]} \text{ for } j \neq k$$. Also $$\omega \rightarrow 0 \implies CORR(Y_j, Y_k) \rightarrow 0 \text{ for } j\neq k.$$&#x20;

Let $$T_n(\theta)$$ be the n-th Touchard polynomial (see vocabulary) - correspond to n-th moment of Poisson distribution with parameter $$= \theta > 0$$. Let $$B_n(Z_1, \dots, Z_n)$$ denote the n-th compelte Bell polynomial. k-th moment of $$X \sim Bell(\alpha)$$ is given by $$E(X^k) = B_k(k_1, \dots, k_k)$$ where $$k_k = e^{W(\alpha)}T_k(W(\alpha))$$. Thus, mixed moments of $$Y \sim MZIB(\alpha, \omega) \text{ for } k_1, \dots, k_m \in \mathbb{N}$$ are given by&#x20;

$$
E(\prod_{r=1}^m Y_r^{k_r}) = (1-\omega) \prod_{r=1}^mB_{k_r}(k_{k_1}, \dots, k_{k_r})
$$

where $$k_{k_r} = e^{W(\alpha_r)}T_{k_r}(W(\alpha_r))$$. We then got the following propositions.

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Proposition 2, 3</p></figcaption></figure>

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption><p>Corr3, Prop 4</p></figcaption></figure>

I'm going to skip few propositions (there are just too many, see paper for all and their proof)

### Parameter Estimation

Let $$Y_1 = (Y_{11}, \dots , Y_{1m})^T, \dots , Y_n = (Y_{n1} , \dots, Y_{nm})^T$$ be $$n$$ indenpendent identically distribute random vectors such that each $$Y_i = (Y_{i1}, \dots , Y_{im})^T \sim MZIB(\alpha, \omega) \text{ for } i = 1, \dots, n.$$Let $$y_i = (y_{i1}, \dots , y_{im})^T$$ be the realization of random vector $$Y_i \text { for } i = 1, \dots, n$$. $$Y_{data} = [y_1, \dots, y_n]^T$$ be the $$n \times m$$ matrix that contains the observed multivariate data. Define $$I = \{i : y_1 = 0_m, i= 1, \dots, n \}$$ and let $$n_0 = \sum_{i=1}^n (y_i=0_m)$$ be the number of elements in $$I$$, number of lines in matrix $$Y_{data}$$ where all elements are equal to zero. Likelihood function eliminationg constants can be expressed as:&#x20;

$$
L(\alpha, \omega) = [\omega + (1-\omega)e^{\xi_+}]^{n_0}(1-\omega)^{n-n_0}e^{n-n_0\xi_+}\prod_{r=1}^mW(\alpha_r)^{N_r}
$$

where $$N_r = \sum_{i \notin I}y_{ir} = \sum_{i=1}^n y_{ir}$$ and $$\xi_{+}:=\xi_+(\alpha)$$ and corresponding log-likelihood functions:

$$
l(\alpha, \omega) = n_0\ln (\omega + (1-\omega)e^{\xi_+}) + (n-n_0)\ln (1-\omega) + (n-n_0)\xi_+ + \sum_{r=1}^m N_r \ln (W(\alpha_r))
$$

Some assumptions on behavior of $$l(\alpha, \omega)$$ as $$n \rightarrow \infty$$, regularity of first two derivatives with respect to model parameters and existence and uniqueness of ML estimate of $$\alpha$$.

**Direct Maximization**

Can be from direct maximization of log-likelihood function.

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>First two  derivatives</p></figcaption></figure>

No-closed form of ML estimate, non-linear optimization algorithm.

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption><p>Optimization Process</p></figcaption></figure>

It is simpler to otpimize $$l_{profile}(\alpha)$$. - earlier is m dimensional later is (m+1) dimensional.

Fisher matrix - variance and covatiance matrix given by the inverse of it. See paper for details.

**EM Algorithm**

We partition $$I$$ defined earlier into $$I = I_e \cup I_s$$ , $$I_e$$ denote the number of extra zeros corresponding to degenerate distribution at point zero, $$I_s$$ denote the number of structural zero vectors corresponding to baseline Bell distribution.

Let $$V$$ be the latent variable that denotes number of elements in set $$I_e$$ to split $$n_0$$ into $$V$$ and $$n_0 - V$$, $$V\in \{0, 1, \dots, n\}$$.&#x20;

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Distribution</p></figcaption></figure>

2 steps of EM - E-step: compute the conditional expectation of complete log-likelihood function given $$Y_{data}$$.

M-step: Maximization of the Q-function. (from step 1)

<figure><img src="../.gitbook/assets/image (5) (1).png" alt=""><figcaption><p>EM</p></figcaption></figure>
