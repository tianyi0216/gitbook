# Attention is all you need

Proposed Transformer, solely based on attention mechanisms, dispensing recurrence and convolutions entirely.&#x20;

Self-attention: attention mechanism relating different positions of a single sequence in order to compute a representation of the sequence.&#x20;



### Model architecture

Encoder: maps input sequence $$(x_1, \dots, x_n)$$ to a sequence of representations $$(z_1, \dots, z_n)$$. Consuming previously generated symbols as additional input when generating next.

**Encoder and Decoder Stacks**

The encoder is composed of stack of $$N = 6$$ identical layers. Each layer has 2 sublayers. First is a multi-head self-attention mechanism, second is  a position-wise FFN. Employ a residual connection around each of 2 sub-layers, followed by layer normalization. Output of each sub-layer is LayerNorm($$x + Sublayer(x))$$ $$Sublayer(x)$$ is a function by sublayer itself.

Decoder is also 6 layers, also insert a third layer in addition, which performs multi-head attention over output of the encoder  stack. Similar to encoder, we employ residual connection around each sublayers. Also prevent positions from attending to subsequence position - masking. Enusures predictions from position $$i$$ can depend only on known output position less than $$i$$



**Attention**

Function mapping a query and set of key-value pairs to an output, where query, keys, values and output are all vectors.

$$
Attention(Q,K,V) = softmax(\frac{QK^T}{\sqrt{d_k}})V
$$

Here, dk is dimension of keys. d\_v is dimension of values. (Divide to avoid softmax issue with extremely small gradients)

Multihead attention.

Allows model to jointly attend to information from different representation subspaces at different positions.&#x20;

$$MultiHead(Q, K, V) = Concat(head_1, \dots, head_h)W^O$$

Where $$head_i = Attention(QW_i^Q, KW_i^K, VW_i^V)$$. Where projections are parameter matrixs W.

In this we deploy h = 8 parallel attention layers or head.



### FFN

$$
FFN(x) = \max (0, xW_1 +b_1)W_2 + b_2
$$

Positional encoding: use positional encodings to input embeddings at the bottoms of the encoder and decoder stacks.  (In order to make use of order of sequence).



