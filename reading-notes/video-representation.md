---
description: >-
  https://openaccess.thecvf.com/content/CVPR2023/papers/Yu_Learning_Procedure-Aware_Video_Representation_From_Instructional_Videos_and_Their_Narrations_CVPR_2023_paper.pdf
---

# Video Representation

Proposes a method that jointly learns a video representation to encode step concepts and a deep probabilistic model to capture temporal dependencies and immense individual variations in step ordering. Representation: matching a video clip to its corresponding narration. Model: predict distribution of video representation for a missing step, given steps in its vicinity.



<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption><p>Model outcome</p></figcaption></figure>

Method

Input: $$N$$ clips $$\{v_1, v_2, \dots, v_N\}$$. Each $$v_i$$ captues a potential action step and time. We assume sentences $$\{s_1, s_2, \dots, s_N\}$$ is associated with videos, $$s_i$$ describes action.

Learn video representation that encodes both action step and temporal dependencies. Representation: video encoder $$f$$ that extracts representation $$x_i$$ from $$v_i$$ ($$x_i = f(v_i)$$). Probabilistic model: conditional probability $$p(x_j = f(v_j) | \{ x_i = f(v_i) \} _{i \neq j} ) \forall j$$. $$p(x_j | \{ x_i \} _{i \neq j} )$$ models the temporal dependencies among steps.

Overview: leverage pretrained text encoder $$g$$ that is fixed during learning, extend the idea of masked token modeling, populated in NLP. For randomly sample clip, train the model and predict the distribution of $$x_j = f(v_j)$$ from the probabilistic model. Align with expecation $$\mathbb{E} (x_j)$$ with corresponding text emvedding $$y_j = g(s_j)$$ and match $$\{ x_i = f(v_i) \}_{i \neq j}$$ to their text embedding $$\{ y_i = g(s_i) \}_{i\neq j}$$. The method seeks to characterize the distribution of $$x_j$$ instead of predict.&#x20;



<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption><p>method</p></figcaption></figure>

It is important to know that the model uses a diffusion process to model p(x\_j | {x\_i}_{i \neq j). Which gradually add noise to input x_j over T steps.&#x20;
