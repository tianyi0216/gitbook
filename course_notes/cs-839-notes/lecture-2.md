# Lecture 2

### Image Formation

#### Digital Image

Basic: Scene element + Illumination (source) as input to imaging system -> Image plane

Digital camera: replaces film with a sensor array, each cell in the array is light-sensitive diode that converts photons to electrons.

**Sample** the 2D space on a regular grid and **Quantize** each sample. Image thus represented as a matrix of integer values.



<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption><p>Digital Image representations</p></figcaption></figure>

Each sensor records amount of light coming in.

#### Color Images

Each sensor has a filter (R, G, B) layer that filters red, blue or green and result in a pattern. Estimating RGB at each cell from neighboring values.

RGB space.

Digital color image:



<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### Image Filtering

Compute a function of the local neighborhood at each pixel in the image.

&#x20;\- Function specified by a "filter" or mask saying how to combine values from neighbors.

Uses:

* Enhance an image (denoise, resize, increase contrast etc)
* Extract information (texture, edges, interest points, etc)
* Detect patterns (template matching)

**Noise reduction**

Multiple images of same static scene will not be identical.

Common types of noise:

* Salt and pepper noise: random occurrences of black and white pixels.
* Impulse noise: random occurrences of white pixels.
* Gaussian noise: variations in intensity drawn from a Gaussian normal distribution.

&#x20;**Gaussian Noise**&#x20;

$$f(x, y) = \hat{f} (x,y) + \eta (x,y)$$ where $$\hat{f}(x,y)$$ is the ideal image and $$\eta (x,y)$$ is the noise process.

Gaussia noise: $$\eta (x,y) \sim \mathcal{N} (\mu, \sigma)$$ .

Here, $$\sigma$$ controls how strong the noice is. $$\mu$$ is often 0, noise has zero mean. $$x, y$$ is just the coordinate.

How to reduce noise?

Attempt 1: Replace each pixel with an average of all value in its neighborhood.

Assumptions:

* Expect pixels to be like thier neighbors.
* Noise processes to be independent from pixel to pixel.

&#x20;**Correlation filtering**

Say averaging window size is $$2k+1 \times 2k+1$$ :

$$
g(i, j) = \frac{1}{(2k+1)^2} \sum_{u=-k}^k \sum_{v=-k}^kf(i+u, j+v)
$$

Here, first part is attribute uniform weight to each pixel, the second part is loop over all pixels in neighborhood around image pixel f\[i, j].&#x20;

Now we generalize to allow **different wieghts** depending on neighboring pixel's relative position:

$$
g(i, j) = \sum_{u=-k}^k \sum_{v=-k}^k h(u,v)f(i+u, j+v)
$$

Where $$h(u,v)$$ is non-uniform weights. This is **cross-correlation**, denoted $$g = h \bigotimes f$$

Filtering: replace each pixel with a linear combination of its neighbors, the filter "**kernel**" or "**mask**" h\[u, v] is the prescription for the weights.

&#x20;**Averaging Filter**



<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption><p>box filter</p></figcaption></figure>

Smoothing by averaging.

Near boudary issue- methods:

* clip filter (black)
* wrap around
* copy edge
* reflect across edge

&#x20;**Gaussian Filter**

If we want nearest neighboring pixels to have most influence on output.

Kernel approximation is a 2d gaussian function: $$h(u,v) = \frac{1}{2\pi \sigma^2}e^{-\frac{u^2 + v^2}{\sigma^2}}$$

This removes high-frequency component from image (low pass filter)

Parameter: **size** of kernel. **Variance** determine extent of smoothing.

Smoothing filter properties:

* Values positive
* Sum to 1 -> constant regions same as input
* Amount of smoothing proportional to mask size
* Remove "high-frequency" components, "low-pass" filter.

### Convolution

Filp the filter in both dimensions (bottom to top, right to left), then apply cross-correlation.

$$
g(i, j) = \sum_{u = -k}^k \sum_{v = -k}^k h(u,v)f(i-u, j-v)
$$

$$g = h * f$$ - notation for convolution operator

Properties:

* Shift invariant - operator behaves the same everywhere
* Superposition: $$h* (f1 + f2) = (h*f1) + (h*f2)$$
* Commutative: $$f*g = g*f$$
* Associative: $$(f*g)*h = f*(g*h)$$
* Distributes over addition: $$f*(g+h) = (f*g) + (f*h)$$
* Scalars factor out: $$kf*g = f*kg = k(f*g)$$
* Identity: unit impulse $$e = [ \dots , 0,0,1,0,0,\dots]. f*e=f$$

&#x20;**Median Filter**

No new pixel values introduced, removes spikes - good for impulse, salt & pepper noise and non-linear filter. Also edge preserving.

### Edge Detection

Map image from 2d array of pixels to a set of curves or line segments or contours. Look for strong gradients, post-process.

A edge is a place of rapid change in the image intensity function.

For 2D, $$f(x,y)$$, the partial derivative is:

$$
\frac{\partial f(x,y)}{\partial x} = \lim_{\epsilon \rightarrow 0} \frac{f(x+\epsilon, y) - f(x,y)}{\epsilon}
$$

For discrete data, we approximate using finite differences:

$$
\frac{\partial f(x,y)}{\partial x} \approx \frac{f(x+1, y) - f(x,y)}{1}
$$

Filters:



<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>filters for edge detection</p></figcaption></figure>

&#x20;**Image Gradient**

$$\Delta f = [\frac{\partial f}{\partial x}, \frac{\partial f}{\partial y}]$$

In the direction of most rapid change in intensity.

Gradient detection (orientation of edge normal) is given by $$\theta = tan^-1(\frac{\partial f}{\partial y}/\frac{\partial f}{\partial x})$$

Edge strength is given by magnitude of gradient: $$|| \Delta f || = \sqrt{(\frac{\partial f}{\partial x})^2 + (\frac{\partial f}{\partial y})^2}$$

**Effect of noise**

Different filters respond strongly to noise. Image noise results in pixels look very different from their neighbors, generally, larger noise -> stronger response.

Solution: smooth first.

Edge: look for peaks in $$\frac{\partial}{\partial x} ( h *f)$$.

Derivative theorem of convolution:

$$
\frac{\partial }{\partial x} (h * f) = (\frac{\partial}{\partial x} h) * f
$$

Smoothing gaussian, effect of $$\sigma$$ - larger value result in larger scale edges detected. Smaller values-> fine features detected.
