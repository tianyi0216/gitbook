# Script

Summary: Using the DL technique to identify birds from their sound. Traditionally, it is done by an observer, which is challenging and biased. But author developed BirdNet, which can classify bird species from their sound.&#x20;

6/1 - Why does this paper matter - intro:

Monitor status and trend of diversity, bird are often the target because they live in most environments, and niches, and are also the baseline for ecosystem health.

Many bird species also have cultural significance. In short, they are important.&#x20;

Traditionally, they are monitored by point count - domain experts visually and aurally identify birds in 5-10 intervals at sampling locations - which can be biased and difficult with lots of constraints.

In contrast, passive acoustic monitoring (PAM) uses autonomous recording units (ARUs) to monitor the acoustic environment continuously. Data collected this way is more cost-effective and more widely used in monitoring. Enables researchers to revisit the data to conduct additional analyses.&#x20;

It is still challenging to analyze. (Manually extract what the species is for researchers). Deep neural networks (DNN) solutions are needed.

Bird Detection Challenge. BirdCLEF. Uses mel-frequency cepstral coefficient (mfcc) - fed into SVM, or nearest neighbor. Computational constraint in a large amount of image data.

CNN was introduced in 2016 - spectrograms and CNN.&#x20;

The author presents BirdNet -built on previous success using CNNs and spectrogram data to classify 984 bird species.&#x20;

So, this paper present a way to correctly identify bird species - which improved a lot from others in its time.&#x20;

Its method - 2:

Sound Data -> Visualization (spectrogram) -> Augmentation -> Model -> Prediction.&#x20;

Data:&#x20;

1. List of 1049 species (most common species).&#x20;
2. Collected data Xeno-canto (community-curated collection of recordings for these species). (500,000 recordings for over 10,000 bird species over 7000h)
3. Extra recording from Macauly Library of Natural Sounds - (750,000 audio recording of more than 10,000 species.)



* Only select high-quality recordings - maximum of 500 recording for species - 226,078 audio files.
* $$<10$$ audio recording species eliminated -> $$n = 984$$
* Non-event classes to train to ignore non-bird signals - other animals, nature noise, human vocal etc, we use 16 classes from AudioSet data to enrich and combined to other animal, humna and environmental noise. Final dataset is about 1000 classes and 3978h recording, and split into 80/10/10.
* ARU data often overlapping vocalizations require annotation. (Low SNR) Need gemeralize. Use open source focal recordings - only signle clear audible bird species. So there's a domain shift from focal to soundscape spectrogram data. So there's also evaluation data of soundscape.

Pre-processing:

Input - specrogram as monochrome image. Avian vocal and auditory capabilities should be considered (not simply re-scaling arbitrary values to fit the size of model). Need high temporal resolution. (FFT - fast fourier transform window size of 10.7ms). Overlap of 25%, each frame is 8ms. Restrict between 150 Hz and 15kHz also leave room for pitch shifts during data augmentation.

Frequency - compression.&#x20;

Spectrogram - 3s chunk of audio - based on average duration of species and also allows for data augmentation.&#x20;

Extract segments containing vocalization - simple detrctor. (exact location)

Data augmentation:

1. the random shift in frequency and time.
2. random partial stretching in time and frequency.
3. Addition of noise from samples that were rejected in pre-processing.

Each was added with a probability of 0.5 and a maximum of 3 augmentations.



Model:

ResNet. Wide residual network provided similar performance compared to deep architectures, improved regularization in residual blocks and scaling of network in width. Followed this design of that paper and choose a network resulted in a sequence of 157 layers and 36 were weighted.&#x20;

Three core components:&#x20;

1: preprocessing block transformed the original input spectrogram before it was passed through a series of residual stacks.

2: sequence of residual blocks - extracted features that were eventually passed through the third component.

3: classification block.&#x20;



<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

Trained using 1.5 million spectrograms with a maximum of 3500 samples per class.&#x20;

tried Cost-sensitive learning, but none of them improved the overall performance.&#x20;

Utilized mixed-up training by randomly combining 3 spectrograms into 1 sample. The author used Adam optimizer with a learning rate of 0.001 and batch size of 32. Reduce lr by 0.5 factor whenever validation loss stalled. There was also a step-wise reduction on drop-out probabilities by 0.1, with an initial at 0.5. Early stopping with a cooldown of 3 epochs was applied. Knowledge distillation was used to train a born-again network.

Inference:

Skipped.

Results:Both sample-wise mAP and class-wise mean average precision. Top-1 accuracy, F0.5 and area under ROC curve.

Focal Recording: mAP and cmAP:0.791 and 0.694. TOP1 0.777 and AUC 0.974. Works great on focal data.

Sounscape: drastically decreased - 0.414 on 2019 CLEF - best 0.260 on 2019.&#x20;

3.3 - Continuous stream:&#x20;

