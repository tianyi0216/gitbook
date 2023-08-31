---
description: https://arxiv.org/pdf/2010.11929.pdf
---

# Transformer for Image

Transformer: computationally efficient, scalability, and can train over 100B  parameters.

This paper applies transformer directly to images. On large datasets, BiT attains excellent result.



<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption><p>Encoding</p></figcaption></figure>

Method:

ViT uses patch embedding, flatten the patches and map to D dimensions with trainable linear projection. MLP.&#x20;

The biggest difference is the encoding process, which is shown here.
