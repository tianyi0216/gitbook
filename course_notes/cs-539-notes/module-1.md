# Module 1

Use vector, matrix, or tensor to represent data.

A $$M \times N$$ matrix is a 2D array with M rows and N columns.

1D array - row vector or column vector.

Some special matrix: diagonal - only diagonal is non 0. Identiy - diagonal with all 1. Sparse (lots of 0), and symmetric (square, a(i,j) = a(j,i) for all i and j).

### Tensor

Array of numbers, 0 dimension- scalar, 1 d - vector, 2d - matirx, 3 or higher is usually a tensor.

Matrix operation: element by element vector operations -  addition and subtractions. Size must be the same for all operands.

Matrix and scalar operation, multiply or divide.

Inner/outer product.

Let $$A = [a_{ij}]$$ be a $$M \times N$$ matrix and $$b = [b_n]$$ be a $$N \times 1$$ column vector.

Inner product: Let $$x$$ and $$y$$ be $$N \times 1$$ vectors:

$$x^Ty = \sum_{n=1}^Nx_ny_n$$

Result in a scalar, both x and y have the same dimension.

outer product:

$$x_{M\times 1}y_{1\times N}^T = [x_my_n]_{M \times N}$$ A $$M \times N$$ matrix.

Results in a matrix.

x and y do not need to be same dimension

Matrix vector product:

$$c = Ab = [c_i]_{i=1}^M$$  where $$c_i = \sum_{j=1}^Na_{ij}b_j = a_i^Tb , 1 \leq i \leq M$$

Matrix matrix product: dimension need to match (column of first and row of second)

$$C = A_{M \times N}B_{N \times P} \implies c_{m,p} = \sum_{n=1}^N a_{mn}b_{np}$$



### Vector Space

$$x$$ and $$y$$ are linearly independent if $$ax + by = 0$$ implies $$a=b=0$$. Otherwise, $$y = -(a/b)x$$ meaning $$y$$ is scaled version of x.

If $$\{v_k\}$$are $$K$$linearly independe t vectors, and each $$v_k$$ is a $$M(\geq K) \times 1$$ vector, then $$\{v_k\}$$span a K dim subspace in $$\R^M$$.

$$x$$ and $$y$$ are orthogonal if $$x^Ty=0$$.

if $$\{v_k\}$$ are mutually orthogonal, they can be a set of basis of the subspace.

### Rank

rank of a matrix is the number of linear independent column vectors, or linear independnet row vectors.

$$rank(A_{M \times N}) \leq \min \{M, N\}$$

A matrix is full rank if its rank equal to the smaller of its column numbers or row numbers. Otherwise, a matrix is rank-deficient.

### Vector Norms

L2: $$||x||2 = \sqrt{x^Tx} = (\sum_{i=1}^N x_i^2)^{1/2}$$   x is a unit vector if $$||x||_2 = 1$$

Angle: $$\cos \theta = (x^Ty)/(||x|| \cdot ||y||)$$

L1: $$||x||1 = \sum_{k=1}^m |x_k|$$

L infinity: $$||x|||_{\infty} = \max_{1\leq k \leq m} |x_k|$$



### Hyperplane

A hyperplane in an n-dimensional vector space is a (n-1) dim subspace. In the Euclidean space,a plane is a hyperplane in a 3D space, a line is a hyper plane in a 2D space.

Hyperplane function $$\{ x; x\in \R^n, w^Tx+b = \sum_{i=1}^n w_ix_i + b = 0\}$$

A hyperplane partition the space into two half spaces:

$$\{x; x\in \R^n, w^Tx = \sum_{i=1}^nw_ix_i < b\}$$ and $$\{x; x\in \R^n, w^Tx = \sum_{i=1}^nw_ix_i > b\}$$



Distance from a point to a hyperplane

$$r = -(w^Tx^*+b)/|w| = -g(x^*)/|w|$$

### SVD

$$A_{M \times N} = U_{M \times r} \Sigma_{r\times r}V_{r\times N}^T = \sum_{i=1}^r\sigma_iu_iv_i^T$$

Singular value: $$\sigma_1 \geq \sigma_2 \geq \dots, \geq \sigma_r \geq 0$$, $$r\leq \min(M,N)$$&#x20;

$$U^TU = I_r$$, $$V^TV=I_r$$, $$UU_{M \times M}^T \neq I$$, $$VV_{N\times N}^T \neq I$$

$$u_m^Tu_n = v_m^Tv_n = \begin{cases} 1 & m=n \\ 0 & m \neq n \end{cases}$$

Number of non-zero singular values = rank of matrix.

SVD is the procedure for PCA.

### Eigenvalue Decomposition

A symmetric matrix may be decomposed as:

$$A_{N\times N} = V\Lambda V^T = \sum_{n=1}^N \lambda_n v_n v_n^T$$

$$\Lambda_{N\times N} = diag\{\lambda_1, \dots, \lambda_N\}$$, $$\lambda_n$$ eigenvalue

$$v_n$$ eigenvector $$Av = \lambda v \implies (A - \lambda I)v = 0$$

$$VV^T = V^TV=I \implies v_m^Tv_n = \begin{cases}1 & m=n \\ 0 &m \neq n \end{cases}$$

A is positive definite iff all eigenvalues are posisitve

If A is Hermitian (A^H = complex conjugate transpose of A) then all eigenvalues are real numbers.
