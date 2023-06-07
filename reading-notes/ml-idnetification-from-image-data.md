---
description: https://www.biorxiv.org/content/10.1101/2022.09.02.506375v1.abstract
---

# ML idnetification from Image Data

Identification of Pseudomonas aeruginosa strains.&#x20;

Uses data augmentation and transfer learning to overcome data starvation problem. Also uses DL and CNN.

Motivation: colonies, characterization in sizes, shapes, edges, textures and degrees of opacity and color. Categorization. From morphology -> genome sequencing technology.&#x20;

Paper: a collection of 69 clinical and environmental P.aeruginosa isolates which present a range of phenotypic features. From these 69 isolates, generate a library of 266 P.aeruginosa images.

D-CNN and data augmentation and transfer learning to classify strains of P.aeruginosa and achieved an accuracy of 94%.

**Morphological variation across strains and replicates**

Isolates -> LB agar plates with Congo red -> quadruplicate and generate images.&#x20;

<figure><img src="../.gitbook/assets/image (3).png" alt=""><figcaption><p>Data</p></figcaption></figure>

The above figure summarizes some of the metrics (B) we use for colony complexity, especially compression ratio and sobel operator. (both in form of vector)

Fig 4- extent of variation using coefficients of variation (CV = mean / standard deviation) across replicates and strains.&#x20;

**classifying from image data**

D-CNN. Use VGG19 DCNN on&#x20;

