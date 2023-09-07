---
description: https://arxiv.org/abs/1506.02640
---

# YOLO

For object detection.

Objection direction as a regression problem to spatially separated bounding boxes and associated class probabilities using a single neural network.&#x20;



<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

Advantages:

1. Extremely fast - since it is an regression problem.
2. Reasons globally about the image when making predictions.&#x20;
3. Learns generalizable representations of objects.&#x20;

Method/Process.

First, divide input image into an $$S \times S$$ grid. If center of an object falls into cell - cell is responsible for detecting the object. Each ggrid cell predicts $$B$$ bounding boxes and confident score for the boxes. - IOU between the predicted box and the truth (score)

Each box consist of 5 predictions. $$x, y, w, h$$ and confidence.

Each grid cell also predicts class probabilities $$Pr(Class_i | Object)$$.

At test time, we multiply conditional class probabilities with box confidnece prediction, the result is then&#x20;

$$
Pr(Class_i) * IOU_{pred}^{truth}
$$



<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (3) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

Training: details in paper. Final layer predict both class probabilities and bounding box. Final layer is linear activation, other is ReLu. Also dropout

Loss function:



<figure><img src="../../.gitbook/assets/image (4) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>
