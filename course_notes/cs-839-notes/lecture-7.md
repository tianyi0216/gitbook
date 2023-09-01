# Lecture 7

## Generative Models

Supervised Learning: data and label, learn a function to map x -> y.

Unsupervised: just data, no labels. Learn some underlying hidden structure of data.

&#x20;**Discriminivative vs Generative Models**

DIscrimininative Modle: learn a probability distribution $$p(x|y)$$

Generative Model: learn a probability distribution $$p(x)$$

Conditional Generative Model, learn $$p(x|y)$$

**Density Function**

$$p(x)$$ assigns a positive number to each possible $$x$$; higher numbers mean $$x$$ is more likely.

Normalized:

$$\int_X p(x)dx = 1$$

Different values of $$x$$ comptete density.

Discriminative: Density function, $$p(x)$$ assigns a positive number to each possible $$x$$. Higher numbers mean $$x$$ is more likely. Possible labels for each input comptete for probability mass. But no competition between images.

No way for model to handle unreasonable inputs, it must give label distribution for all images.

Generative Model: all possible images compete with each other for probability mass.

Requires deep image understanding. Model can reject unreasonable input by assigning them small values.

Conditional Generative Model: each possible label induces a competition among all images.

Recall Bayes rule:

$$
P(x|y) = \frac{P(y|x)}{P(y)}P(x)
$$

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption><p>Bayes</p></figcaption></figure>

Discriminative -> Assign labels to data Feature Learning (with labels)

Generative -> Detect outliers. Feature learning (without labels). Sample to generate new data.

Conditional -> Assign labels, while rejecting outliers. Generate new data conditioned on input labels.
