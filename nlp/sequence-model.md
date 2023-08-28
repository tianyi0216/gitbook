# Sequence Model

Used when input/output data is a sequence. Used on tasks such as speech recongition, music generation, sentiment classification, DNA sequence analysis, Machine translation, Video acivity recongition etc.&#x20;

Notation:

* $$x$$ : input. We use $$x^{<t>}$$ to denote the $$t$$'s sequence of the input.
* $$y$$: output. We use $$y^{<t>}$$ to denote the $$t$$'s sequence of the output.&#x20;
* $$T$$ can be used to denote length. $$T_x$$, $$T_y$$ denote length of input, output.
* $$X_i, y_i$$ can be used to denote $$i^{th}$$ training/testing data. $$T_x^i, T_y^i$$ denote its length.

Word representation: we can use a vocabulary vector, and then use one-hot encoding for all the words.

### RNN

Problem with standard NN: input, output can have different length. Doesn't share features learned across different positions of text.

RNN:&#x20;

![](<../.gitbook/assets/image (1) (1) (1) (1) (1).png>)

Activation of previous input (word) can be used in the next one. So allow output of one node to affect subsequence nodes. (Unidirection RNN)

Forward prop: Initialize $$a^{<0>} = 0$$. $$a^{<t>} = g(w_{aa}a^{<t-1>} + w_{ax}x^{<t>} + b_a)$$, $$\hat{y}^{<t>} = g(w_{ya}a^{<t>} + b_y)$$ where $$g$$ is an activation function, $$w_{aa}$$ is the weight for learning calculating activating layer from activation. $$w_{ax}$$ is weight to learn calculate a from x, and so on...

Common activation - tanh, sometimes relu for $$a$$ . For $$y$$ , can be sigmoid, or anything.(depend on problem)



