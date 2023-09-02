# Lecutre 9

## GANs

Give up modeling p(x), but allows to draw samples from p(x)

Assume we have data xi drawn from distribution $$p_{data}(x)$$, we want to sample from $$p_{data}$$

Idea: Introduce a latent variable z with simple prior p(z). Sample $$z \sim p(z)$$ and pass to Generator Network $$x = G(z)$$. Then x is sample from the generator distribution $$p_G$$. Want $$p_G = p_{data}$$

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption><p>GANs</p></figcaption></figure>

Training Objective

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>Objective</p></figcaption></figure>

Train using alternating gradient updates.

$$= \min_G \max_D V(G,D)$$

For t in 1, ..., T:

1. update D. $$D = D + \alpha_D \frac{\partial V}{\partial D}$$
2. update G. $$G = G - \alpha_G \frac{\partial V}{\partial G}$$

At start of training, generator is very bad and discriminator can easily tell real/fake so D(G(z)) close to 0.

Problem: vanishing gradient for G.

Solution: G is trained to minimize log(1-D(G(z)). Instead, train G to minimize -log(D(G(z)). Then G gets strong gradient at start of training.

It achieves global minimum when $$p_G = p_{data}$$

$$\min_G \max_D (E_{x \sim p_{data}}[\log D(x)] + E_{z \sim p(z)} [\log (1-D(G(z)))])$$

$$=\min_G \max_D (E_{x\sim p_{data}}[\log D(x)] + E_{x \sim p_G} [\log (1-D(x))])$$ Change of variable on second term.

$$= \min_G \max_D \int_x (p_{data}(x) \log D(x) + p_G (x) \log (1-D(x))) dx$$ Definition of Expectation.

$$= \min_G \int_x max_D(p_{data}(x) \log D(x) + p_G (x) \log (1-D(x))) dx$$ push max\_D inside integral.

$$f(y) = a\log y - b \log (1-y)$$ . a = p\_data (x) y = D(x), b = p\_G(x). (Side computation to compute max)

$$f^\prime (y) = \frac{a}{y} - \frac{b}{1-y}$$, $$f^\prime (y) = 0 \iff y = \frac{a}{a+b}$$ (local max)

Optimal Discriminator: $$D_G^* (x) = \frac{p_{data}(x)}{p_{data}(x) + p_G(x)}$$

$$= \min_G \int_x (p_data(x) \log D_G^* (x) + p_G(x) \log (1-D_G^*(x)))dx$$

$$= \min_G \int_x (p_data(x) \log \frac{p_{data}(x)}{p_{data}(x) + p_G(x)} + p_G(x) \log \frac{p_G(x)}{p_{data}(x) + p_G(x)} dx$$

$$= \min_G (E_{x \sim p_{data}} [\log \frac{p_{data}(x)}{p_{data}(x) + p_G(x)}] + E_{x\sim p_G} [\log \frac{p_G(x)}{p_{data}(x) + p_G(x)}])$$ (definition of expectation)

$$= \min_G (E_{x \sim p_{data}} [\log \frac{2}{2} \frac{p_{data}(x)}{p_{data}(x) + p_G(x)}] + E_{x\sim p_G} [\log \frac{2}{2} \frac{p_G(x)}{p_{data}(x) + p_G(x)}])$$ (Multiply by a constant)

$$= \min_G (E_{x \sim p_{data}} [\log \frac{2 \cdot p_{data}(x)}{p_{data}(x) + p_G(x)}] + E_{x\sim p_G} [\log  \frac{2 \cdot p_G(x)}{p_{data}(x) + p_G(x)}] - \log 4)$$

KL Divergence: $$KL(p,q) = E_{x \sim p} [\log \frac{p(x)}{q(x)}]$$

