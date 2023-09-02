# Lecture 5

## Regularization

**Data Augmentation**

* Horizontal flips
* Random crops and scales.
* Color: contrast and brightness



## Attention and Transformer

&#x20;**RNNs**

Input and Output:

* one to one
* one to many
* many to one
* many to many
* many to many (aligned)

Sequence to Sequence

Input: Sequence $$x_1, \dots, x_T$$

Output: Sequence $$y_1, \dots, y_{T^\prime}$$

Encoder: $$h_t = f_w(x_t, h_{t-1})$$



<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

From initial hidden state predict: initial decoder state $$s_0$$, context vector $$c$$

Decoder: $$s_t = g_u(y_{t-1}, s_{t-1}, c)$$

### Attention

Compute alignment scores $$e_{t,i} = f_{att}(s_{t-1}, h_i)$$, $$f_{att}$$ is an MLP.

Normalize aligment scores to get attention weights $$0 < a_{t,i} < 1, \sum_i a_{t,i} = 1$$

context vector as $$c_t = \sum_i a_{t,i} h_i$$

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>With attention</p></figcaption></figure>

Repeat: use $$s_1$$ to compute new context vector $$c_2$$, use $$c_2$$ to compute $$s_2, y_2$$

Use a different context vector in each timestep of decorder. Input sequence not bottlenecked through single vector. At each timestep of decoder, context vector looks at different part of sequence.

Decoder doesn't use the fact that $$h_i$$ form an ordered sequence, treat them as unordered. Can use similar architecture given any set of vectors $$\{h_i\}$$

### Images with RNNs and Attention



<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Each timestep of decoder uses a different context vector that looks at different part of image.

Uses in image captioning.

&#x20;**Attention Layer**

Inputs:

Query vector: $$q$$ (shape: $$D_q$$)

Input vectors: $$X$$(shape: $$N_X \times D_X$$)

Similarity function: $$f_{att}$$



Computation:

similarities: $$e$$ (shape: $$N_X$$) $$e_i = f_att(q, X_i)$$

Attention weights: $$a = softmax(e)$$ (shape $$N_X$$)

Output vecotr: $$y = \sum_i a_xX_i$$ (shape $$D_X$$)



Change 1: could use dot product for similarity.

$$e_i = q \cdot X_i$$

Change 2: use scaled dot product

$$e_i = q \cdot \frac{X_i}{\sqrt{D_Q}}$$

Change 3: multiple query vectors

$$E = \frac{QX^T}{\sqrt{D_Q}}$$ (shape: $$N_Q \times N_X$$) $$E_{i,j} = \frac{(Q_i \cdot X_j)}{\sqrt{D_Q}}$$

Change 4: Separate key and value.

Key Matrix: $$W_K$$ (Shape: $$D_X \times D_Q$$)

Value Matrix: $$W_V$$ (Shape: $$D_X \times D_V$$)

Key Vectors: $$K = XW_K$$ (Shape: $$N_X \times D_Q$$)

Value Vectors: $$V = XW_V$$ (Shape: $$N_X \times D_V$$)



Final Attention Layer becomes:

Inputs:

Query vector: $$q$$ (shape: $$D_q$$)

Input vectors: $$X$$(shape: $$N_X \times D_X$$)

Key Matrix: $$W_K$$ (Shape: $$D_X \times D_Q$$)

Value Matrix: $$W_V$$ (Shape: $$D_X \times D_V$$)

Computation:

Key Vectors: $$K = XW_K$$ (Shape: $$N_X \times D_Q$$)

Value Vectors: $$V = XW_V$$ (Shape: $$N_X \times D_V$$)

$$E = \frac{QX^T}{\sqrt{D_Q}}$$ (shape: $$N_Q \times N_X$$) $$E_{i,j} = \frac{(Q_i \cdot X_j)}{\sqrt{D_Q}}$$ Similarities

Attention weights: $$a = softmax(e)$$ (shape $$N_X$$)

Output vecotr: $$Y = AV$$ (shape: $$N_Q \times D_V$$) $$Y_i = \sum_j A_{i,j}V_j$$



<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1).png" alt=""><figcaption><p>Attention Layer</p></figcaption></figure>

&#x20;**Self Attention Layer**

One query vector per input vector

<figure><img src="../../.gitbook/assets/image (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Self Attention</p></figcaption></figure>

Consider permutting the input vectors.

Queries and key will be the same, but permutted.Same for similarities, attention and output.

Self attention layer is Permutation Equivariant. $$f(s(x)) = s(f(x))$$

Self-attention layer works on sets of vectors.

Self-attention doesn't know the order of the vectors it is processing. So add positional encoding $$E$$ to the input. Can be learned lookup table, or fixed function



&#x20;**Masked Self-Attention Layer**&#x20;

Don't let vectors look ahead in sequence. Used for language modeling (predict next word).

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption><p>masked</p></figcaption></figure>



&#x20;**Multihead Self-Attention**

Use H independent Attention Heads in parallel.

Run self attention in parallel on each set of input vectors (different weights per head).



<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption><p>multihead</p></figcaption></figure>
