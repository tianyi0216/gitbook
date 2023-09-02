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

