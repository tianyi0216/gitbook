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
