---
description: https://www.sciencedirect.com/science/article/pii/S1470160X22010949
---

# Sound Classification

Need to classify sound from protecting animals using soundscapes from tropical forests - there's a large training data sets. Author uses CNN - to investigate minimum viable training data set size, and the effect of data augmentation.

High sample sizes lead to mediocre accuracy, improved by data augmentation and transfer learning -> leading to high accuracy for relatively small sample sizes.

Challenges: small sample sizes for rare species, distances of sound source to sensor, inter-species/individual variations.

Approach: transfer learning + data augmentation.

### Methods

Data set is soundscape recordings collected at 15 sites in Indonesia. Selected 1 minute ar random with 1h period in morning and evening, and sampled once a month for 12 months, and se,ected same dawn minute from 15 sites, resulted in 63 minuts.

Annotated 3629 animal vocalizations $$V_1, V_2, \dots, V_{3629}$$ belonging to 448 sonotypes (note or series of note that constitute a unique acoustic signal). Each sonotype is assigned to one of four higher taxonomic groups: birds, invertebrates, mammals, amphibians.  E.g ($$V_1 \in$$(Sonotype 1, bird))

<figure><img src="../../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption><p>Worlflow</p></figcaption></figure>

Use scipy to get soundscape's spectrogram. Window size = 256, shape param = 0.25, number of points to overlap between window = 32. Samples were encoded in a 129 x 353389 image depicting the frequency components of soundscape in 0 - 22050 Hz range. (Height = window size, length = length of audio file/window size). Each $$V_i$$ is enclosed in a gray-scale image.

We determine from vocalization, its sonotype.

**Transfer Learning**

Author uses parameter from Keras VGG-19 model. Been trained on ImageNet dataset.&#x20;

Preprocessing: transfer data to Keras VGG-19 format - 8-bit per RGC channel, 224 x 224 colored images.

Author identified highest and lowest frequency intensities $$F_i$$ and $$f_i$$ for each vocalization image $$V_i$$ and performed following normalization:

$$
V_i^{\prime} = 255\frac{V_i-f_i}{F_i - f_i}
$$

Each pixel in $$V_i^{\prime}$$ take value between 0 and 255 - corresponding to 8-bit gray scale images. To transform into RGB images,simply replicate each $$V_i^{\prime}$$ into 3 channels.

<figure><img src="../../.gitbook/assets/image (7) (1) (1).png" alt=""><figcaption><p>VGG-19 without top layer on the left, after flatten - author's layers</p></figcaption></figure>

**Data Augmentation**

1. Cropping of spectogram's time range, frequency or both (x, y axis).
2. Adding sound of light, medium or heavy rain, thunder, aircraft, chainsaw, and car/truck into spectrogram
3. Translating whole spectrogram up or down in terms of frequency.
4. Widening the spectrogram in the time or frequency range.
5. Sharpening the spectrogram by squeezing it in time and frequency

Modified about 5 - 10% for changing the shape, and added 1/3 of the noise.

**Model**

VGG-19 model without four top layers. Then, flatten into a vector and concatenated with 4 values corresonding to start/end time, lowest and highest frequency of vocalization. Then, pass through two couples of dense dropout layers and a softmax dense output layer to obtain the final output.

**Training**

Initialize layers of VGG19 with weights trained on ImageNet and froze those layers during training.

Initialize weights randoms for each layers. Applied early stopping with a patience for 15 epochs to stop the training for overfitting.

Loss function: cross entryopy loss for each epoch.

Split: 80/10/10 (train/val/test)



