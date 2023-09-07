# Lecture 10

## Diffusion Models

Learning to generate by denoising.

2 processes, forward diffusion process that gradually add noise to input and reverse denoising process that learn to generate data by denoising.&#x20;

**Forward**

$$q(x_t | x_{t-1}) = N (x_t; \sqrt{1- \beta_t}x_{t-1}, \beta_tI)$$ -> $$q(x_{1:T}|x_0) = \prod_{t=1}^T q(x_t|x_{t-1})$$

**Diffusion Kernel**

define $$\hat{\alpha}_t = \prod{s=1}^t (1-\beta_s)$$ -> $$q(x_t|x_0) = N(x_t; \sqrt{\hat{\alpha}_t}x_0, (1-\hat{\alpha}_t)I))$$

For sampling: $$x_t = \sqrt{\hat{\alpha}_t}x_0 + \sqrt{(1-\hat{\alpha}_t}\epsilon$$ where $$\epsilon \sim N(0, I)$$

$$\beta_t$$ values schedule is designed such that $$\hat{\alpha}_t \rightarrow 0$$ and $$q(x_T|x_0) \approx N(x_T; 0, I)$$

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption><p>Forward distribution</p></figcaption></figure>

### Denoising

Generation:

Sample $$x_T \sim N(x_T ; 0,I)$$

Iteratively sample $$x_{t-1} \sim q(x_{t-1}|x_t)$$

In general, $$q(x_{t-1}|x_t) \propto q(x_{t-1})q(x_t|x_{t-1})$$ is intractable

We can approximate $$q(x_{t-1}|x_t)$$ use normal distribution if $$\beta_t$$ is small each forward diffusion step.

<figure><img src="../../.gitbook/assets/image (1) (1).png" alt=""><figcaption><p>Reverse</p></figcaption></figure>

Learning

<figure><img src="../../.gitbook/assets/image (2) (1).png" alt=""><figcaption><p>Learning</p></figcaption></figure>

Parameterization

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>
