# Lec1

Optimization steps

Problem analysis: real world $$\iff$$ math relationship

$$\min f(x)$$ objective function (modeling)

s.t $$x \in S$$ , S = feasible set.

study the math properties of the model: (model analysis)

apply an algorithm to compute an optimal solution $$x^*$$ (solution method)

verification and simulation



## Linear Optimization

A function $$f: \mathbb{R}^n \rightarrow \mathbb{R}$$ is linear if:

1. $$f(x+y)=f(x)+f(y) \quad \forall x, y \in \mathbb{R}^n$$
2. $$f(\lambda x)=\lambda f(x) \quad \forall x \in \mathbb{R}^n, \forall \lambda \in \mathbb{R}$$ Equivalently, $$f$$ is linear if it can be written as:

$$
c^{\prime} x=\sum_{i=1}^n c_i x_i=c_1 x_1+c_2 x_2+\cdots+c_n x_n,
$$

where $$c_1, c_2, \ldots, c_n$$ are real numbers.



real-world relationships $$\Leftrightarrow$$ math relationships&#x20;

$$\min d^{\prime} x \quad$$ LINEAR objective function&#x20;

s.t. $$\quad a_i^{\prime} x \geq b_i \quad i \in M_1$$&#x20;

$$a_i^{\prime} x \leq b_i \quad i \in M_2 \quad$$ LINEAR inequalities&#x20;

$$a_i^{\prime} x=b_i \quad i \in M_3$$



Example

$$
\begin{aligned} \operatorname{minimize} & 2 x_1-x_2+4 x_3 \\ \text { subject to } & x_1+x_2+x_4 \leq 2 \\ & 3 x_2-x_3=5 \\ & x_3+x_4 \geq 3 \\ & x_1 \geq 0 \\ & x_3 \leq 0 \end{aligned}
$$

Strict inequalities like $$x_3+x_4>3$$ are not allowed!



We learn about model analysis and solution methods.

Optimal conditions, duality. - model analysis

Simplex algorithm - solution methods.



