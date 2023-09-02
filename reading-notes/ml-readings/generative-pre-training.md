---
description: >-
  https://s3-us-west-2.amazonaws.com/openai-assets/research-covers/language-unsupervised/language_understanding_paper.pdf
---

# Generative Pre-Training

Summary: Large gains on language tasks can be realized by generative pre-training of language model on a diverse corpus of unlabeled text, followed by discriminative fine-tuning on each task. Use task-aware input transformations during fine-tuning to achieve effective transfer while requiring minimal changes to model architecture.

This paper: combination of unsupervised pre-training and supervised fine-tuning. Learn a universal representation that transfers with little adaptation to wide range of tasks. Employ two-stage training procedure. 1 - language modeling objective on unlabeled data to learn initial parameters of a NN. Subsequently, adapt parameters to a task using corresponding supervised objective.

Model architrcture: transformer. Evaluate on 4 language understanding tasks - natural language inference, question answering, semantic similarity and text classification.&#x20;

Framework:

Unsupervised pre-training.

Given unsuprervised corpus of tokens $$U = \{u_1, \dots, u_n\}$$, use standard language modeling objective to max the following likelihood.

$$
L_1(U) = \sum_i \log P(u_i | u_{i-k} , \dots, u_{i-1}; \Theta)
$$

Here, k is the size of context window and condotional probability P is modeled using a NN with parameter Theta.

Transformer decoder for language model, variant of transformer. Applies a multi-headed self-attention on operation over input context tokens followed by position-wise feedforward layers to produce an output distribution over target tokens:

$$
h_0 = UW_e + W_p \\
h_l = transformer\_block(h_{l-1})\forall i \in [1,n] \\
P(u) = softmax(h_nW_e^T)
$$

Where U is context vector of tokens, n is number of layers, W\_e is token embedding matrix, W\_p is position embedding matrix.

Supervised fine-tuning:

After training, we adapt the parameter to supervised target task. Assume a labelled dataset C, each instance consist of sequence of input tokens x1, ... , xm , along with label y. The input are passed through sequence pre-trained model to obtain final activation $$h_l^m$$ which then fed into an added linear output layer parameters $$W_y$$ to predict $$y$$

$$
P(y|x^1, \dots, x^m) = softmax(h_l^mW_y)
$$

This gives the following objective to maximize:

$$
L_2(C) = \sum_{(x,y)}\log P(y|x^1, \dots,x^m)
$$

Including language modeling as an auxiliary obective to fine tuning helped learning by improving generalization of supervised model, and accelerating convergence, so we optimize the following objective:

$$
L_3(C) = L_2(C) + \lambda * L_1(C)
$$

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption><p>Model Architecture</p></figcaption></figure>

Need modification for certain tasks, significant amount of customization. Use a traversal-style approach, convert structured input into an ordered sequence that the pre-trained model can process.  - see paper for detail.&#x20;
