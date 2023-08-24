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
