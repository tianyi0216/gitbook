# Lecture 3

## Seam Carving

Content aware resizing.

Intuition: preserve the most interesting content (remove pixels with low gradient energy). To reduce or increase the size in one dimension, remove irregular shaped "seams". (Optimal solution via dp).

$$Energy(f) = \sqrt{(\frac{\partial f}{\partial x})^2 + (\frac{\partial f}{\partial y})^2}$$

Want to remove seam where they won't be very noticeable, measure energy as gradient magnitude.

Choose seam based on minimum total energy path across image, subject to 8-connectedness.

Algorithm:

* Let vertical seam $$s$$ consist of $$h$$ positions that form an 8-connected path.
* Let the cost of seam be $$Cost(s) = \sum_{i=1}^h Energy(f(s_i))$$
* Optimal seam minimize the cost: $$s^* = \min_{s} Cost(s)$$
* Compute efficiently with DP.

Identify min cost seam (height $$h$$, width $$w$$):

Greedy

For each entry $$(i, j)$$:

$$
M(i,j) = Energy(i,j) + \min (M(i-1,j-1), M(i-1,j), M(i-1,j+1))
$$

Min value in the last row of $$M$$ indicates the end of minimal connected vertical seam. Backtrack up, selecting min of 3 above in $$M$$.

Can also insert seams to increase size of imgae in either dimension. (duplicate optimal seam, average with neighbor)

M is min of gradient, high gradient part - energy - edge or important area (seam)

## 2D Transformations

Fit the parameters of transformation according to a set of matching feature pairs (alignment problem)

**Parametric Warping**

$$p = (x,y)$$ -> $$T$$ -> $$p^\prime = (x^\prime , y^\prime)$$

Transformation $$T$$ is a coordinate-changing machine.

$$p^\prime = T(p)$$

T is **global** means is the same for any point $$p$$ and can be described by just a few numbers.

Matrix representation of T:

$$p^\prime = Mp$$

$$
\begin{bmatrix} x^\prime \\ y^\prime  \end{bmatrix} =M \begin{bmatrix} x \\ y\end{bmatrix}
$$

### Scaling

Scaling a coordinate means multiplying each of its components by a scalar.&#x20;

Uniform scaling means this scalar is same for all components.

Non-uniform scaling: different scalars per component.

E.g:

$$x^\prime = ax$$ , $$y^\prime = by$$

Matrix:

$$
\begin{bmatrix} x^\prime \\ y^\prime  \end{bmatrix} =\begin{bmatrix} a&0\\ 0&b\end{bmatrix} \begin{bmatrix} x \\ y\end{bmatrix}
$$



<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption><p>Transformations represented by matrix</p></figcaption></figure>



<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption><p>continue</p></figcaption></figure>

Only linear 2D can be represented by 2x2 matrix.



**Homogenous Coordinates**

convenient.

$$(x, y) \implies \begin{bmatrix} x \\ y \\ 1\end{bmatrix}$$ convert to homogenous coordinates.

$$\begin{bmatrix}x\\ y\\ w \end{bmatrix} \implies (\frac{x}{w} , \frac{y}{w})$$ convert from homogenous coordinates.

How to represent 2d translation as 3x3 matrix using homogenous coordinates.

$$x^\prime = x + t_x \\ y^\prime = y + t_y$$

Using rightmost column:

$$Translation = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix}$$

$$\begin{bmatrix} x^\prime \\ y^\prime \\ 1 \end{bmatrix} = \begin{bmatrix} 1 & 0 & t_x \\ 0 & 1 & t_y \\ 0 & 0 & 1 \end{bmatrix} \begin{bmatrix} x \\ y \\ 1 \end{bmatrix} = \begin{bmatrix} x+t_x \\ y + t_y \\ 1 \end{bmatrix}$$



<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption><p>Basic 3x3 transformations</p></figcaption></figure>

