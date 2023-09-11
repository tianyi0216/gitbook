# Lecture 8

## VAE

PixelRNN explicity parameterizes density function with nn, so we train maximize likelihood of training data

$$
p_W(x) = \prod_{t=1}^Tp_W(x_t|x_1, \dots,x_{t-1})
$$

VAE define an intractable density that we cannot explicitly compute or optimize, we can optimize a lower bound for the density.

### Autoencoders (Non variational)

Unsupervised method for learning feature vectors from raw data x, without labels.

Features should extract useful information that we can use for downstream taks.

Originally: Linear + nonlinearilty (sigmoid)

Later: Deep, fully-connected

Later: ReLU CNN

input data x -> Encoder -> features Z

We use features to reconstruct the input data with a decoder.

features Z -> Decoder -> Reconstructed data X^.

Loss: l2 distance between input and reconstructed data

$$
||\hat{X} - X||_2^2
$$

Features need to be lower dimensional than data.

After training, throw away decoder and use encoder for a downstream task.

Autoencoders learn latent features for data without any labels.&#x20;

Can use features to initialize a supervised model.

Not probabilistic: No way to sample new data from learned model.



### Variational Autoencoders

AE: learn latent z from rwa data and sample from model to generate new data.

&#x20;Assume training data $$\{x^(i)\}_{i=1}^N$$ is generated from unobserved representation z.&#x20;

intuition: x is image, z is latent factors used to generate x.

After training: sample new data like this:

Sample $$z$$ from prior $$p_{\theta^*}(z)$$. Assume simple prior p(z)

Sample $$x$$ from conditional $$p_{\theta^*}(x|z^{(i)})$$ Represent p(x|z) with a neural network

Decoder must be probabilistic: decoder inputs $$z$$, output mean $$\mu_{x|z}$$ and covariance $$\Sigma_{x|z}$$.

Sample X from Gaussian with mean and covariance.

How to train this model?

Maximize likelihood of data.

If we could observe z from each x, the could train a generative model p(x|z)

We don't observe z, so need to marginalize:

$$
p_\theta(x) = \int p_\theta(x,z)dz = \int p_\theta(x|z)p_\theta(z)dz
$$

We can compute $$p_\theta(x|z)$$ with decoder network.We assumed gaussian prior $$p_\theta(z)$$. But impossible to integrate over all z.

Could also try Bayes rule, but we cannot compute $$p_\theta(z|x)$$.

Solution: train another network to learn $$q_\Phi(z|x) \approx p_\theta(z|x)$$ . (Encoder)

Then

$$
p_\theta(x) = \frac{p_\theta(x|z)p_\theta(z)}{p_\theta(z|x)} \approx \frac{p_\theta(x|z)p_\theta(z)}{q_\Phi(z|x)}
$$

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption><p>VAE</p></figcaption></figure>

VAE

$$\log p_\theta(x) = \log \frac{p_\theta(x|z)p(z)}{p_\theta(z|x)}$$ Bayes Rule

$$= \log \frac{p(x|z)p(z)q\Phi(z|x)}{p_\theta(z|x)q_\Phi(z|x)}$$ Multiply top and bot by $$q_\Phi(z|x)$$

\= $$\log p_\theta(x|z) - \log \frac{q_\Phi(z|x)}{p(z)} +  \log \frac{q_\Phi(z|x)}{p_\theta(z|x)}$$ Split using rules for logarithms.

$$\log p_\theta(x) = E_{z \sim q_\Phi(z|x)} [\log p_\theta(x)]$$ We can wrap in expecations since it doesn't depend on z

$$= E_z[\log p_\theta(x|z)] - E_z[\log \frac{q_\Phi(z|x)}{p(z)}] + E_z[\log \frac{q_\Phi (z|x)}{p_\theta(z|x)}]$$

$$= E_{z \sim q_\Phi(z|x)}[\log p_\theta(x|z)] - D_{KL}(q_\Phi(z|x), p(z)) + D_{KL}(q_\Phi(z|x), p_\theta(z|x))$$

Part1: data reconstruction

Part2: KL divergence between prior, and samples from encoder network

Part3: KL divergence between encoder and posterior of decoder. KL>=0, so this term gives a lower bound on the data likelihood.

$$\log p_\theta(x) \geq E_{z \sim q_\Phi(z|x)} [\log p_\theta(x|z)] - D_{KL}(q_\Phi(z|x), p(z))$$

Jointly train the encoder q and decoder p to maximize the variationla lower bound on the data likelihood. Alsso called Evidence Lower Bound (ELBo)

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption><p>VAE</p></figcaption></figure>

3. sample code z from encoder output.
4. Run sample code through decoder to get a distribution over data samples.
5. Original input data should be likely under distribution output from (4).
6. Can sample a reconstruction from (4)



### VAE: Generating Data

1. Sample z from prior p(z)
2. Run sample z through decoder to get distribution over data x.
3. Sample from distribution in (2) to generate data.

Diagonal prior on p(z) causes dimensions of z to be independent.

### VAE: Edit images

1. run input through encoder to get a distribution over latent codes.
2. Sample code z from encoder output.
3. Modify some dimension of sampled code.
4. Run modified z through decoder to get a distribution over data sample.
5. Sample new data from (4).

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Summary</p></figcaption></figure>
