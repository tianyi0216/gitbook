# Lecture 4

## Deep Learning Fundamentals

#### Softmax Classifier

Multinomial Logistic Regression.

Want to interpret raw classifier as probabilities.

$$s = f(x_i; W)$$ , $$P(Y =k | X = x_i) = \frac{e^sk}{\sum_j e^sj}$$

$$L_i = - \log P(Y = y_i | X = x_i)$$

Cross Entropy: $$H(P, Q) = H(p) + D_{KL}(P||Q)$$, P = correcct probs, Q = normalized probabilities.

Put all together: $$L_i = -\log (\frac{e^sy_i}{\sum_j e^sj})$$

### Optimization

Random search, or follow the slope.

Gradient is the vector of partial derivatives along each dimension - steepest descent is negative gradient.

Loss gradient: denoted $$\frac{\partial E_n}{\partial w_{ji}^{(1)}}$$ or $$\Delta_w L$$

Gradient descent: update weights iteratively - move in opposite to gradient.

$$w^{\tau+1} = w^\tau - \eta \Delta E(w^\tau)$$

SGD: Full sum is expensive. Common minibatch: 32,64,128

$$\Delta_w L(W) = \frac{1}{N} \sum_{i=1}^N \delta_w L_i(x_i, y_i, W) + \lambda \Delta_w R(W)$$

**Problem with Linear Classifier**

If data is not linearly separable.

One Solution: feature transforms. E.g data in circle -> polar space.

$$f(x,y) = (r(x,y), \theta(x,y))$$



### Neutal Networks.



<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption><p>NN</p></figcaption></figure>

Activation function - ReLu (for non-linearity)

How to compute gradient?



<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption><p>back prop</p></figcaption></figure>

