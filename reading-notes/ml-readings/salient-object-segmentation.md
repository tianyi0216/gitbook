# Salient Object Segmentation

Intro:

Fixation - compute probabilistic map of image to predict human eye gaze patterns.

Salient object segmentation - annotate an image by drawing pixel-accurate silhouettes of objects that are believed to be salient.

Model: Learning based framework. Given a proposed mask and map, function estimate the overlapping score of the region with ground-truth.

Two types of features: shape features and fixation distribution features within object. For fixation distribution features, we first align major axis of each object candidate and extract 4x3 histograms of fixations density over the aligne dobject mask. Finally, the 33 dimensional feature vector is extracted.

For each daaset, traina  random forest of 30 trees.
