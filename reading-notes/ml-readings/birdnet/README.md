---
description: >-
  https://pdf.sciencedirectassets.com/273474/1-s2.0-S1574954120X00069/1-s2.0-S1574954121000273/main.pdf?X-Amz-Security-Token=IQoJb3JpZ2luX2VjENz%2F%2F%2F%2F%2F%2F%2F%2F%2F%2FwEaCXVzLWVhc3QtMSJGMEQCIEIAh
---

# BirdNet

Passively collected acoustic data for survey technique. Extraction of species richness data from large audio datasets. Birdnet is a DNN that is capable of identifying 984 North American and European bird species by sound. Based on ResNets. Data augmentarion is key -> against noise and cope with overlapping vocalizations.

### Importance

Birds are widely used as monitoring targets, they live in most environments and occupy almost every niche within the environments. They are also conspicuous relative to other taxa. So their trend is the de facto baseline for ecosystem health. They also have popular appeal. &#x20;

Before, they were monitored using point counts. Visually and aurally identify the count of birds in the field during 5-10min intervals. This can be negatively affected by variability in detectability among species and sites, and also weather conditions. Also hard when monitoring large areas with high temporal resolution. High bias might occur too.

PAM: autonomous recording units (ARUs) to monitor acoustic environment continuously over extended periods. Cost-effective. Better temporal resolution. Reducing bias and uncertainties.

Analysis: challenging. Automated analyses has limited success in the past. Use to be forced to choose between extracting avian diversity data from recordings.

Now, with DNN, outperform traditional techniques in the domain. MFCG was used for dimension reduction. SVM or KNN to classify. In 2016- CNN was trained and outperformed all spectrograms. 5-s chunks, extracting mel-scale spectrograms for each chunk, and filtering audio data. All were applied data augmentation with pitch and time shifts, and noise samples. Since 2017, all team used CNN, and even the shallow one works well.&#x20;

### Methods

Data: need to generate visual representation of sound, augmentation of visualizations, and training of this architecture.

Data: number of species = 1049. Data was collected from Xeno-canto, a community collection of recordings from the world for the species. Total of 500,000 recording over 10,000 bird species over 7000h. Macaulay Library of Natural Sounds. Could have incorrectly labeled data. Maximum of 500 recordings, a total of 226,078 audio files. Eliminate fewer than 10 recordings, a total of 984 bird species. Non-event classes included non-bird signals. Insects, anurans, mammals, wind rain humans, etc. (Google audio sets) 16 classes from AudioSet and enriched from Freefield1010 WarblR datasets. - 3 classes other animals, humans, and environmental noise.

Final dataset: 10000 bird, and non-bird, 3978hr recordings. Train/val/test for 80/10/10.

Issue- overlapping vocalization of multiple bird species, low signal-to-noise ratios. Expert to annotate a significant portion of data. Open data on focal voice, domain shift from focal to soundscape data. Datasets were solely focal, assembled in two long-term continuous sets for further evaluation of the model.  Expert analysts annotated all vocalizations. In addition 134,683 of 15 min duration were also used.

Preprocessing:&#x20;

input: spectrogram we treat as a monochrome image. A recent study says mel-spectrograms are good. They propose avian vocal and auditory capabilities should be considered when tuning spectrograms computations. Fast Fourier transform window size of 10.7ms and overlap of 25%, each frame representing a time step of 8ms. So restrict frequency to 150 HZ and 15 kHZ - converting most bird frequency ranges.  Time- 3s, which reflect bird sounds and also allow for temporal shifts during data augmentation.

Training on weakly labeled samples of length, the challenge is to extract segments of audio recordings that contain the target signal. - exact info on where species was not provided. So author developed a simple detector based on signal strength to extract segments containing vocalizations.&#x20;

Data augmentation:

1. the random shift in frequency and time.
2. random partial stretching in time and frequency.
3. Addition of noise from samples that were rejected in pre-processing.

Each was added with a probability of 0.5 and a maximum of 3 augmentations.

Model:

Based on ResNet. Improved residual blocks and scaling of the network in width ($$K$$) and depth ($$N$$) to identify the best possible layout. The author choosed $$K = 4$$ and $$N=3$$, resulted in a sequence 157 total layers of 36 was weighted. Three core components:&#x20;

1: preprocessing block transformed the original input spectrogram before it was passed through a series of residual stacks.

2: sequence of residual blocks - extracted features that were eventually passed through the third component.

3: classification block.&#x20;

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>



Training:

Trained using 1.5 million spectrograms with a maximum of 3500 samples per class. Cost-sensitive learning, but none of them improved the overall performance.&#x20;

Utilized mixed-up training by randomly combining 3 spectrograms into 1 sample. The author used Adam optimizer with a learning rate of 0.001 and batch size of 32. Reduce lr by 0.5 factor whenever validation loss stalled. There was also a step-wise reduction on drop-out probabilities by 0.1, with an initial at 0.5. Early stopping with a cooldown of 3 epochs was applied. Knowledge distillation was used to train a born-again network.&#x20;

Knowledge distillation: Knowledge distillation refers to the process of transferring the knowledge from a large unwieldy model or set of models to a single smaller model that can be practically deployed under real-world constraints. Born again- student model is same architecture as teacher model.

Inference:

Converting input data to spectrograms. Audio is converted to mel spectrogram and passed through the model.&#x20;

Focal recording analysis: Audio files were tested with 1-s overlap between spectrograms and averaged all predictions for every species, then derived a ranked list of species for entire recording.

Soundscape analysis: 3-s chunks. 3 setting adjusted: prediction sensitivity, overlap of segments, minimum confidence. Sensitivity: sigmoid to flatten activation function. LME pooling. Overlapping increased detection resolution, but small step for sliding predcition increased processing time.

### Results

Sample-wise and class-wise metrics. Training set: test samples were unevenly distributed across classes. F0.5 score, top-1 accuracy, area under ROC curve (AUC).&#x20;

Focal recording evaluation: data has 22960 focal recording for 984 species, mAP 0.79 and cmAP 0.693 in multi-label setting. Top-1 accuracy 0.77 with AUC 0.974 across all test files.&#x20;

Soundscape: decreased in soundscape domain. 0.414 But outperformed model for BirdClef 2019.

Continuous Stream: Test set: one of the largest fully annotated dataset for sound recognition. Changes in avian diversity. Dataset covered 12 days random selected from a 5-month period of single year. Recordings for this experiment were stored as flac-encoded files with durations of 15mins. Sigmoid activation at last layer and. Checklist: weekly occurrence of bird species across site. Min num of checklist was 7, max 83. Focused on species with at least 4 checklist entries > 0.5 between 2016 and 2019. Total number was 121. Inferred corruence pattern correlate with those observed by humans for many species.

### Discussion:

Replicating patterns generated by observer data despite focal vs soundscape data. High-end recording devices yielded more reliable results. Acoustic domain gaps is challenging. Species size alone is not predictor, there could be confusion for versatile species. Noisy data also.&#x20;

Note: High temporal resolution improved classification performance.

Multi-label classification increased performance.

Deeper layers does not necessarily performed than more filter. Did perform better when resource is limited.
