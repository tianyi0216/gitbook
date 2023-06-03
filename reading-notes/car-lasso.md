---
description: https://arxiv.org/abs/2012.08397
---

# CAR-LASSO

### Abstract

Need statistical models to denote interactions among microbes. The author proposed a chain graph model with two sets of nodes (predictors and responses) whose solution yields a graph with edges representing conditional dependence. The model uses Bayesian LASSO - the solution is sparse.&#x20;

\[R package]\([https://github.com/YunyiShen/CAR-LASSO](https://github.com/YunyiShen/CAR-LASSO))



### Introduction

What was lacking in microbiome analysis: lack of statistical tools to simultaneously infer connections among microbes and their direct reactions to different environmental factors in a unified framework.&#x20;

For the graphical model:

1. Nodes represent variable
2. Edges represent conditional dependence between nodes, the absence of such edges represents conditional independence.

Intuitively, a multiresponse linear regression with LASSO prior on regression coefficients combined with graphical LASSO prior on the precision matrix can provide sparse regression coefficients among responses and predictors. In addition, sparse graphical models can be used to estimate sparse graphical structure among responses. - However, predictors represent marginal effects rather than conditional effects.

Goals:

* Estimate the graphical structure between predictors (environment) and responses (microbes).
* The graphical structure among responses while keeping the conditional interpretation of both parameters.

CAR-LASSO simulatenoelously estimates the conditional effect of a set of predictors that influence the responses and connections among responses. The model is represented by a chain graph with two sets of nodes - $$\{predictors\}$$ and $$\{responses\}$$. And direct edges between predictor and response represent conditional links, and undirected edges among responses represent correlations.

* Guarantees sparse solution - Bayesian LASSO.
* Fixed penalty - posterior is log-concave.
* Adaptive extension allows different shrinkage to different edges to incorporate edge-specific knowledge to model, and use Normal model to build hierarchical structures.
* Handles small and big data through Gibbs sampling algorithm.&#x20;

### Methods

Let $$Y_i \in \mathbb{R}^k$$ be multivariate reponse with $$k$$ entries for $$i = 1, \dots , n$$ observations.&#x20;

Let $$X_i \in \mathbb{R}^{1 \times p}$$ be the row vector of predictors for $$i = 1, \dots , n$$, assume design matrix is standardized so each column has mean of 0 and same standard deviation.

Let $$Y_i$$ follow a normal distribution with mean vector $$\Omega^-1(B^TX_i^T + \mu)$$ and precision matrix $$\Omega \in \mathbb{R}^{k \times k}$$ (positive definite) where $$B \in \mathbb{R}^{p \times k}$$ correspond to regression coefficients connecting the responses to predictors and $$\mu \in \mathbb{R}^k$$ correspond to the intercept.  Author use transpose $$B^TX_i^T \in \mathbb{R}^{k \times 1}$$ because samples are encoded as row vectors in the design matrix while by convention multivariate Normal samples are column vectors.

The likelihood function of the model is:

$$
p(Y_i|X_i, \mu, B, \Omega) \propto \exp[(B^TX_i^T+\mu)^TY_i - \frac{1}{2}Y_i^T\Omega Y_i]
$$

$$B$$ encodes the conditional dependence between $$Y$$ and $$X$$. If $$B_{jq} = 0$$, then $$X_j$$ and $$Y_q$$ are conditionally independent. $$\Omega$$ off diagonal entried encode the conditional dependence between $$Y_q$$ and $$Y_{q^\prime}$$.  The regression coefficients in multiresponse linear regression, $$\tilde{B} = B\Omega$$ are marginal effects.

**Prior Specification:**

Assume Laplace prior on $$B$$ and GLASSO prior on $$\Omega$$

<figure><img src="../.gitbook/assets/image (1).png" alt=""><figcaption><p>Full Model Specification</p></figcaption></figure>

Note $$I_{\Omega \in M^+}$$ means $$\Omega$$ must be positive definite.

**Algorithm**

<figure><img src="../.gitbook/assets/image (2).png" alt=""><figcaption><p>Algorithm for Gibbs Sampling</p></figcaption></figure>

hyperparameters: we determine $$\lambda_\Beta$$ and $$\lambda_\Omega$$.

**Learning:**

Continuous prior $$\implies$$zero probability for parameter to be zero.

Amount of shrinkage, $$1 - \pi$$ where $$\pi = \frac{\tilde{\theta}}{E_g(\theta|Y)}$$ , $$\tilde{\theta}$$ is the estimate of parameter under LASSO prior and denominator is the posterior mean of parameter under non-shrinkage prior. Use $$\pi > 0.5$$ to decide that $$\theta \neq 0$$.

**Extensions**

Adaptive lasso - prior knowledge of independence among certain nodes.

