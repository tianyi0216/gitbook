# Lecture 6

## Attention and Transformers

Replace Convolution with "Local Attention"

Convolution: output at each position is inner product of conv kernel with receptive field in input.

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>



## RNN

Works on ordered sequences. Good at long sequences, not parallelizable.

Key idea: has an internal state.

We process sequence of vectors by applying recurrence formula:

$$
h_t = f_w(h_{t-1},x_t)
$$

Where $$h_t$$ is new state, $$f_w$$ is some function with parameters $$w$$, $$h_{t-1}$$is old state and x\_t is input at some time step.

RNN graph:

<figure><img src="../../.gitbook/assets/image (23).png" alt=""><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (24).png" alt=""><figcaption><p>Many to Many</p></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (26).png" alt=""><figcaption></figcaption></figure>

Sequence to Sequence (Many to one) + (One to many)

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption></figcaption></figure>

### Convolution on input.

Works on multidimensional grids. Bad at long sequences, need to stack many conv layers for input to see the whole sequence. Highly parallel: each output can be computed parallel.

### Self attention

Works on set of vectors, good at long sequences, after one attention layer, each output sees all inputs. Highly parallel. Very memory intensive.

### Transformer

All vectors interact with each other. + MLP independently on each vector, plus residual connection.

<figure><img src="../../.gitbook/assets/image (28).png" alt=""><figcaption></figcaption></figure>

A transformer is a sequence of transformer blocks.

Adding attention to RNN models let them look different parts of the input at each timestep.

Generalized self-attention is new, powerful neural network primitive.

Transformers are new nerual network model that only uses attention.

