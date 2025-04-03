## I. Definitions
### 1. Vector space
A **vector** $v$ is an element of a vector space.

A **vector space** $V$ is a family of vectors that obey some basic rules.
A vector in $V$ that is multiplied by a scalar is also in $V$ -- a vector space must always containing a zero vector (the scalar can be 0).

A **subspace** of a vector space is a subset that obeys the rules of a vector space.

### 2. Matrices
A matrix is linear operator that perform a linear transformation from one vector to another.

**Index notation** for matrix multiplication:
$$C_{i j}=\sum_k A_{i k} B_{k j}$$
**Transpose of a matrix:**
$$\left(\mathbf{A}^T\right)_{ij} = A_{ji}$$

**Hermitian transpose (or conjugate transpose):**
$$
\left(\mathbf{A}^H\right)_{ij} = \bar{A}_{ij}
$$
Note that $\mathbf{A}^H=\overline{\mathbf{A}^T}=\bar{\mathbf{A}}^T$.

**Hermitian matrix:**
A matrix $\mathbf{M}$ is Hermitian if
$$
\mathbf{M}^H = \mathbf{M}
$$
(If the matrix is real-valued, this is the same as the matrix being **symmetric**)
Note that $(\mathbf{A B})^H=\mathbf{B}^H \mathbf{A}^H$.

**Dot product:**
The dot product that yields a scalar is defined as:
$$\mathbf{x}^H \mathbf{y}=\sum_{i=1}^n \bar{x}_i y_i$$

**Eigenpair:**
For a matrix $\mathbf{A}$, $(\lambda, \mathbf{x})$ is an eigenpair of $\mathbf{A}$ if:
$$
\mathbf{Ax} = \lambda \mathbf{x}
$$
where $\lambda$ is the eigenvalue and $\mathbf{x}$ is the corresponding eigenvector.

**Note:**
- Eigenvalues of a Hermitian matrix are real
- Eigenvectors of a Hermitian matrix are orthogonal

**Unitary matrix:**
A matrix $\mathbf{Q} \in \mathbb{C}^{n \times n}$ is a unitary matrix if $\mathbf{Q}^H=\mathbf{Q}^{-1}$, i.e.
$$\mathbf{Q}^H \mathbf{Q}=\mathbf{Q} \mathbf{Q}^H=\mathbf{I}$$
(equivalent to **orthogonal matrix** of real numbers)

**Positive definite** and **positive semi-definite:**
A Hermitian matrix $\mathbf{M} \in \mathbb{C}^{n \times n}$ is **positive definite** if
$$
\mathbf{x}^H \mathbf{M} \mathbf{x}>0 \quad \forall \mathbf{x} \in \mathbb{C}^n \backslash \mathbf{0}
$$
(the eigenvalues are strictly positive)

A Hermitian matrix $\mathbf{M} \in \mathbb{C}^{n \times n}$ is **semi-positive definite** if
$$
\mathbf{x}^H \mathbf{M} \mathbf{x} \geq 0 \quad \forall \mathbf{x} \in \mathbb{C}^n
$$
(the eigenvalues are positive)

The matrix $\mathbf{A}^H \mathbf{A}$ is positive semi-definite.

**Rank of a matrix:**
The rank of a matrix $\mathbf{A} \in \mathbb{C}^{m \times n}$ is the number of linearly independent rows or columns (the number is equal). It satisfies: $$ \operatorname{rank} \mathbf{A} \leq \min (m, n) $$ A matrix is full rank if $$ \operatorname{rank} \mathbf{A}=\min (m, n) $$ and rank deficient if $$ \operatorname{rank} \mathbf{A}<\min (m, n) $$
**Sparse matrix:**
A matrix in which most entries are zero is a **sparse matrix**.

### 3. Norms
**Motivation:** A norm of an object is a non-negative real-valued number that measures 'how big' it is.

A norm of a vector $\mathbf{x}$ is denoted $\|\mathbf{x}\|$. It is a scalar that satisfies:
$$\begin{aligned} & \|\mathbf{x}\|>0 \quad \text { when } \mathbf{x} \neq \mathbf{0} \\ & \|\mathbf{x}\|=0 \quad \text { when } \mathbf{x}=\mathbf{0} \\ & \|k \mathbf{x}\|=|k|\|\mathbf{x}\| \\ & \|\mathbf{x}+\mathbf{y}\| \leq\|\mathbf{x}\|+\|\mathbf{y}\| \quad \text { (triangle inequality)}\end{aligned}$$
#### Vector norms
$l_p$-norms:
$$\|\mathbf{x}\|_p=\left(\sum_{i=1}^n\left|x_i\right|^p\right)^{1 / p}$$
Note that the $l_\infty$ norm is defined as:
$$\|\mathbf{x}\|_{\infty}=\max _i\left|x_i\right|$$
**Unit sphere and unit shell:**
Unit ball (open)
$$
\{x \in V:\|x\|<1\}
$$

Unit ball (closed)
$$
\{x \in V:\|x\| \leq 1\}
$$

Unit sphere
$$
\{x \in V:\|x\|=1\}
$$

**Energy norm** -- norm induced by a matrix:
$$\|\mathbf{x}\|_A^2=\mathbf{x}^H \mathbf{A} \mathbf{x}$$
To obey the definition of a norm, $\mathbf{A}$ must be positive definite.

#### Matrix norms
**Operator norms**:
A norm of a matrix $\mathbf{A}$ is defined as:
$$
\|\mathbf{A}\|=\max _{\mathbf{x} \in \mathbb{C}^n \backslash \mathbf{0}} \frac{\|\mathbf{A} \mathbf{x}\|}{\|\mathbf{x}\|}
$$
**Interpretation:** measure the 'maximum amount' by which the matrix $\mathbf{A}$ can re-scale a vector $\mathbf{x}$.

Starting with $\|\mathbf{A}\|_1$ (1-norm): $$ \begin{aligned} \|\mathbf{A}\|_1 & =\max _{\mathbf{x} \in \mathbb{C}^n \backslash \mathbf{0}} \frac{\|\mathbf{A} \mathbf{x}\|_1}{\|\mathbf{x}\|_1} \\ & =\max _j \sum_{i=1}^n\left|a_{i j}\right|, \end{aligned} $$which is **the $l_1$-norm of the column of $\mathbf{A}$** with the maximum $l_1$-norm.

For $\|\mathbf{A}\|_{\infty}$ ($\infty$-norm): $$ \begin{aligned} \|\mathbf{A}\|_{\infty} & =\max _{\mathbf{x} \in \mathbb{C}^n \backslash \mathbf{0}} \frac{\|\mathbf{A} \mathbf{x}\|_{\infty}}{\|\mathbf{x}\|_{\infty}} \\ & =\max _i \sum_j^n\left|a_{i j}\right|, \end{aligned} $$which is **the $l_1$-norm of the row of $\mathbf{A}$** with the maximum $l_1$-norm.

For $\|A\|_2$ (2-norm):
$$\begin{aligned}\|\mathbf{A}\|_2^2 & =\max _{\mathbf{x} \in \mathbb{C}^n \backslash \mathbf{0}} \frac{\|\mathbf{A} \mathbf{x}\|_2^2}{\|\mathbf{x}\|_2^2} \\
&=\max \frac{\mathbf{x}^H \mathbf{A}^H \mathbf{A} \mathbf{x}}{\mathbf{x}^H \mathbf{x}}=\frac{\mathbf{x}^H \lambda_{\max }\left(\mathbf{A}^H \mathbf{A}\right) \mathbf{x}}{\mathbf{x}^H \mathbf{x}} \\ & =\lambda_{\max }\left(\mathbf{A}^H \mathbf{A}\right)\end{aligned}$$
where $\lambda_{\max }\left(\mathbf{A}^H \mathbf{A}\right)$ is the largest eigenvalue of $\mathbf{A}^H \mathbf{A}$ (recall that $\mathbf{A}^H \mathbf{A}$ is positive semi-definite, so all eigenvalues are positive). 

The norm $\|\mathbf{A}\|_2$ is therefore the **square root of the largest eigenvalue of $\mathbf{A}^H \mathbf{A}$**, or the largest **singular value** of $\mathbf{A}$.

If $\mathbf{A}$ is Hermitian $\|\mathbf{A}\|_2=|\lambda|_{\max }(\mathbf{A})$.

**Note:** The vector and matrix 2-norms are **invariant** under rotation.
For vector $\mathbf{x}$:
$$ \|\mathbf{Q} \mathbf{x}\|_2=\|\mathbf{x}\|_2 $$

For matrix $\mathbf{A}$: 
$$ \|\mathbf{Q} \mathbf{A}\|_2=\|\mathbf{A}\|_2 $$

**Frobenius norm:**
$$
\|\mathbf{A}\|_F=\sqrt{\sum_i \sum_j\left|a_{i j}\right|^2}
$$
The Frobenius norm is also **invariant** under rotation.

## II.Stability and condition number

### 1. Condition number
**Motivation:** Round-off errors may have a significant impact on the accuracy of the computed solution. The error can be bounded in terms of the condition number.

The condition number of an invertible matrix $\mathbf{A}$ is:
$$
\kappa(\mathbf{A})=\|\mathbf{A}\|\left\|\mathbf{A}^{-1}\right\|
$$

For the 2-norm
$$\kappa_2(\mathbf{A})=\frac{\sqrt{\lambda_{\max }\left(\mathbf{A}^H \mathbf{A}\right)}}{\sqrt{\lambda_{\min }\left(\mathbf{A}^H \mathbf{A}\right)}}$$

If $\mathbf{A}$ is Hermitian
$$\kappa_2(\mathbf{A})=\frac{|\lambda(\mathbf{A})|_{\max }}{|\lambda(\mathbf{A})|_{\min }}$$

### 2. Error bounds
Consider the problem
$$
\mathbf{A}(\mathbf{x}+\delta \mathbf{x})=\mathbf{b}+\delta \mathbf{b}
$$
Since $\mathbf{b} = \mathbf{Ax}$ and $\delta \mathbf{x} = \mathbf{A}^{-1} \delta \mathbf{b}$:
$$\begin{aligned} \frac{\|\delta \mathbf{x}\|}{\|\mathbf{x}\|} & \leq\|\mathbf{A}\|\left\|\mathbf{A}^{-1}\right\| \frac{\|\delta \mathbf{b}\|}{\|\mathbf{b}\|} \\ & =\kappa(\mathbf{A}) \frac{\|\mathbf{b}\|}{\|\mathbf{b}\|}\end{aligned}$$

Consider another problem
$$(\mathbf{A}+\delta \mathbf{A})(\mathbf{x}+\delta \mathbf{x})=\mathbf{b}$$
In this case:
$$\frac{\|\delta \mathbf{x}\|}{\|\mathbf{x}+\delta \mathbf{x}\|} \leq\left\|\mathbf{A}^{-1}\right\|\|\delta \mathbf{A}\|=\kappa(\mathbf{A}) \frac{\|\delta \mathbf{A}\|}{\|\mathbf{A}\|}$$
**Note:** A matrix with a **large condition number** is said to be **ill-conditioned.** Conditioning $\neq$ determinant!

## III. Interpolation and least-squares methods
### 1. Interpolation
**Goal:** fit a function to a data set that passes through the data points.
#### Polynomial interpolation
**Goal:** interpolate $n$ data points with a polynomial with $n$ coefficients.
**Issues:**
- The matrix consisting of the polynomial variables terms is ill-conditioned Vandermonde matrix (and the condition number of the Vandermonde matrix increases with polynomial degree)
- Polynomial interpolation can be very sensitive to the choice of interpolation points

#### Runge effect
The amplitude of oscillations of the interpolations near the ends of the domain are more severe at **higher order**. This is particularly severe for high order interpolating polynomials with **equispaced** points. ($\rightarrow$ can be addressed by using non-equispaced sampling points).

#### Legendre polynomials
There are various expressions computing the Legendre polynomials. One of them is:
$$
(n+1) P_{n+1}(x)=(2 n+1) x P_n(x)-n P_{n-1}(x)
$$
where $P_0=1$ and $P_1=x$. The special feature of Legendre polynomial is that:
$$
\int_{-1}^1 P_m(x) P_n(x) d x=0 \quad \text { if } m \neq n
$$
i.e. Legendre polynomials of different degree are **orthogonal** to each other.

**Interpolation using Legendre polynomial:**
$$f=\alpha_n P_n(x)+\alpha_{n-1} P_{n-1}(x)+\ldots+\alpha_0 P_0(x)$$
### 2. Chebyshev polynomials
#### Definition
$$ T_n(\cos \theta)=\cos (n \theta), \quad \theta \in[0, \pi] $$ or $$ T_n(x)=\cos \left(n \cos ^{-1} x\right), \quad x \in[-1,1] $$ The Chebyshev polynomial $T_n$ has $n+1$ extreme values, and the values have alternating sign: $$ \left\|T_n\right\|_{\infty}=1, \quad T_n\left(x_k\right)=(-1)^k \text { where } x_k=\cos (\pi k / n), k=0, \ldots, n . $$ and $n$ distinct roots in $[-1,1]$ : $$ T_n\left(t_k\right)=0 \text { where } t_k=\cos ((2-k) \pi / 2 n), k=1, \ldots, n$$
By trigonometric identity, for $n\geq 2$:
$$
T_n = 2xT_{n-1} - T_{n-2}
$$

#### Orthogonality
$$\int_{-1}^1 T_n(x) T_m(x) \frac{\mathrm{d} x}{\sqrt{1-x^2}}= \begin{cases}0 & n \neq m \\ \pi & n=m=0 \\ \pi / 2 & n=m \neq 0\end{cases}$$


#### Minimax property
For $y \notin(-1,1)$, the solution to
$$
\underbrace{\min \left\{\|p(x)\|_{\infty}\right.}_{\text {close to } 0}: p \in P_n,-1 \leq x \leq 1, p(y)=1\}
$$
is $1/|T_n(y)|$.
**Interpretation:** on the interval $[-1,1]$, of all polynomials of degree $n$ that are equal to 1 at the fixed point $y$ outside of interval, the polynomial $T_n(x) / T_n(y)$ has the smallest deviation from zero.

### 3. Least-squares data fitting
**Goal:** find a solution to the problem $\mathbf{Ax} =\mathbf{b}$.
### Residual
The residual vector $\mathbf{r}$ is defined as:
$$\mathbf{r}=\mathbf{A} \hat{\mathbf{x}}-\mathbf{b}$$
#### Minimising the error in the $l_2$ norm
Find
$$\min _{\hat{\mathbf{x}} \in \mathbb{C}^n}\|\mathbf{A} \hat{\mathbf{x}}-\mathbf{b}\|_2$$
This is equivalent to minimising the squared error:
$$\begin{aligned} r(\hat{\mathbf{x}})=\|\mathbf{A} \hat{\mathbf{x}}-\mathbf{b}\|_2^2 & =(\mathbf{A} \hat{\mathbf{x}}-\mathbf{b})^H(\mathbf{A} \hat{\mathbf{x}}-\mathbf{b}) \\ & =\hat{\mathbf{x}}^H \mathbf{A}^H \mathbf{A} \hat{\mathbf{x}}-\hat{\mathbf{x}}^H \mathbf{A}^H \mathbf{b}-\mathbf{b}^H \mathbf{A} \hat{\mathbf{x}}+\mathbf{b}^H \mathbf{b} \end{aligned}$$

Hence it is a **least-squares method.**

The solution is 
$$
\mathbf{A}^H \mathbf{A} \hat{\mathbf{x}}=\mathbf{A}^H \mathbf{b}
$$
Re-arranging the least-squares problem:
$$\boxed{\begin{aligned} \hat{\mathbf{x}} & =\left(\mathbf{A}^H \mathbf{A}\right)^{-1} \mathbf{A}^H \mathbf{b} \\ & =\mathbf{A}^{+} \mathbf{b}\end{aligned}}$$

#### Pseudoinverse
The matrix $\mathbf{A}^{+}=\left(\mathbf{A}^H \mathbf{A}\right)^{-1} \mathbf{A}^H$ is known as the **pseudoinverse** or the Moore-Penrose inverse.

## IV. Iterative methods for linear systems
**Goal:** solve a system of the form $\mathbf{Ax} =\mathbf{b}$.
### 1. Power iteration
**Usage:** find the eigenvector associated with the largest absolute eigenvalue of a matrix.

Multiply $\mathbf{x}$ repeatedly by $\mathbf{A}$:
$$
\underbrace{\mathbf{A A} \ldots \mathbf{A}}_{k \text { times }} \mathbf{x}=\mathbf{A}^k \mathbf{x}=\sum_{i=1}^n \alpha_i \lambda_i^k \mathbf{u}_i,
$$
If the largest eigenvalue is distinct, the resulting vector will be aligned with the **eigenvector of the largest eigenvalue.**

### 2. Rayleigh quotient
**Goal:** estimate the eigenvector $\mathbf{x}$ of the matrix $\mathbf{A}$, subject to:
$$\mathbf{A} \mathbf{x} \approx \lambda \mathbf{x}$$

Transform into a minimisation problem in the 2-norm:
$$\min _{\lambda^{\star} \in \mathbb{C}}\left\|\mathbf{A} \mathbf{x}-\lambda^{\star} \mathbf{x}\right\|_2$$
**Solution:**
$$\boxed{\lambda^{\star}=R(\mathbf{A}, \mathbf{x})=\frac{\mathbf{x}^H \mathbf{A} \mathbf{x}}{\mathbf{x}^H \mathbf{x}}}$$

$R$ is the **Rayleigh quotient.**

Rayleigh quotient is real-valued for Hermitian matrices. The error in the eigenvector is second order.

### 3. Stationary methods
Decompose the matrix operator such that $\mathbf{A} = \mathbf{N} - \mathbf{P}$.

#### Method
**Repeat until convergence:**
Compute an approximate solution $\mathbf{x}_{k+1}$ for
$$
\mathbf{Nx}_{k+1} = \mathbf{b} + \mathbf{Px}_k
$$
where $\mathbf{x}_k$ is the most recent known estimate of the solution.

**Classic choices of $\mathbf{N}$:**
- Richardson iteration: $\mathbf{N = I}$
- Jacobi method: $\mathbf{N} = \operatorname{diag}(\mathbf{A})$
- Gauss-Seidel: $\mathbf{N} = L(\mathbf{A})$ is the lower triangular part of $\mathbf{A}$

#### Convergence
Defining the error at the $k$ th iterate $\mathbf{e}_k=\mathbf{x}_{\text {exact }}-\mathbf{x}_k$, from eq. (9) we have:
$$
\mathbf{N e}_{k+1}=\mathbf{P} \mathbf{e}_k
$$
and therefore
$$
\mathbf{e}_{k+1}=\mathbf{N}^{-1} \mathbf{P} \mathbf{e}_k .
$$

With $\mathbf{e}_0$ decomposed into linear combinations of eigenvectors of $\mathbf{N}^{-1} \mathbf{P}$, $\mathbf{e}_k$ can be expressed as:
$$\mathbf{e}_k=\left(\mathbf{N}^{-1} \mathbf{P}\right)^k \mathbf{e}_0=c_1 \lambda_1^k \mathbf{u}_1+\ldots+c_n \lambda_n^k \mathbf{u}_n$$

$\Longrightarrow$ the method will converge only is the absolute value of every eigenvalue is less than 1.

Define $\rho(\mathbf{A})$ as the **spectral radius** -- the largest absolute eigenvalue of a matrix $\mathbf{A}$.

**The stationary methods will converge if:**
$$
\boxed{\rho(\mathbf{N}^{-1}\mathbf{P}) < 1}
$$
(the smaller the spectral radius, the faster the convergence)

### 4. Conjugate gradient method
**Note:** the CG method is for Hermitian positive definite matrices **only**.

#### Method
Consider a set $P$ of non-zero vectors that are A-conjugate:
$$
P=\left\{\mathbf{p}_0, \mathbf{p}_1, \ldots, \mathbf{p}_{n-1}\right\}
$$

A-conjugate implies that
$$
\mathbf{p}_i^H \mathbf{A} \mathbf{p}_j=0 \quad \text { if } i \neq j
$$
Multiplying $\mathbf{Ax} =\mathbf{b}$ by $\mathbf{p}_j^H$:
$$\mathbf{p}_j^H \mathbf{A} \mathbf{x}=\sum_{i=0}^{n-1} \alpha_i \mathbf{p}_j^H \mathbf{A} \mathbf{p}_i=\alpha_j \mathbf{p}_j^H \mathbf{A} \mathbf{p}_j=\mathbf{p}_j^H \mathbf{b}$$
Hence:
$$\alpha_j=\frac{\mathbf{p}_j^H \mathbf{b}}{\mathbf{p}_j^H \mathbf{A} \mathbf{p}_j}$$

#### Convergence
- The CG method is monotone in the A-norm (the A-norm of the error gradually decreases)
- The number of iterations required to solve exactly equal to the number of distinct eigenvalues of $\mathbf{A}$
- The rate of convergence is affected by the condition number $\kappa_2(\mathbf{A})$:
$$\frac{\left\|\mathbf{e}_k\right\|_A}{\left\|\mathbf{e}_0\right\|_A} \leq 2\left(\frac{\sqrt{\kappa_2}-1}{\sqrt{\kappa_2}+1}\right)^k$$

#### Preconditioning
If $\mathbf{P}^{-1} \approx \mathbf{A}^{-1}$, the condition number of the $\mathbf{P}^{-1} \mathbf{A}$ will be better than $\mathbf{A}$, and the CG method will therefore converge faster.
$$\mathbf{P}^{-1} \mathbf{A} \mathbf{x}=\mathbf{P}^{-1} \mathbf{b}$$
This is known as 'left preconditioning'. 


## V. Single value decomposition (SVD)
### 1. Matrix diagonalisation
For a **Hermitian** matrix $M$:
$$
\mathbf{Q}^H \mathbf{M} \mathbf{Q}=\mathbf{\Lambda}
$$
where the columns of $\mathbf{Q}$ are the normalised (in $l_2$) eigenvectors of $\mathbf{M}$ and $\boldsymbol{\Lambda}$ is a diagonal matrix of the eigenvalues of $\mathbf{M}$ (which are real).

Eigenvectors of a Hermitian matrix are orthogonal $\longrightarrow$ $\mathbf{Q}$ is unitary ($\mathbf{Q}^{-1} = \mathbf{Q}^H$)

Hence
$$\mathbf{M}=\mathbf{Q} \mathbf{\Lambda} \mathbf{Q}^H$$
**Limitations of matrix diagonalisation:**
- only valid for square matrices
- defective matrices can't be diagonalised

### 2. SVD definition
The singular value decomposition of an $m \times n$ matrix $\mathbf{A}$ is: $$ \mathbf{A}=\mathbf{U} \boldsymbol{\Sigma} \mathbf{V}^H $$ where 
- $\mathbf{U} \in \mathbb{C}^{m \times m}$ is a unitary matrix
- $\boldsymbol{\Sigma} \in \mathbb{R}^{m \times n}$ is a diagonal matrix, with diagonal entries $\sigma_i$ (the 'singular values') sorted such that $\sigma_1 \geq \sigma_2 \geq \ldots \geq \sigma_p \geq 0$, where $p=\min (m, n)$
- $\mathbf{V} \in \mathbb{C}^{n \times n}$ is a unitary matrix. 

If $\mathbf{A}$ was Hermitian, then $\mathbf{U}=\mathbf{V}=\mathbf{Q}$, and $\boldsymbol{\Sigma}=\boldsymbol{\Lambda}$.

What are $\mathbf{U, \Sigma, V}$?
- The columns of $\mathbf{V}$ are the (normalised) eigenvectors of $\mathbf{A}^H \mathbf{A}$
- The diagonal entries of $\boldsymbol{\Sigma}^H \boldsymbol{\Sigma}$ are the eigenvalues of $\mathbf{A}^H \mathbf{A}$
- The columns of $\mathbf{U}$ are the (normalised) eigenvectors of $\mathbf{A A}^H$
- The diagonal entries of $\boldsymbol{\Sigma} \boldsymbol{\Sigma}^H$ are the eigenvalues of $\mathbf{A A}^H$, which are the same as the eigenvalues of $\mathbf{A}^H \mathbf{A}$
- Use $\mathbf{A} \mathbf{v}_i=\sigma_i \mathbf{u}_i$ to deduce the sign for $\mathbf{u}_i$ given $\mathbf{v}_i$ (or vice versa)

### 3. Reduced SVD
![[reduced-svd.png | center | 500]]
### 4. Low-rank approximation
Expand the SVD:
$$\mathbf{A}=\sum_{i=1}^r \sigma_i \mathbf{u}_i \mathbf{v}_i^H$$
A **'low rank'** approximation of $\mathbf{A}$ is:
$$\mathbf{A}_k=\sum_{i=1}^k \sigma_i \mathbf{u}_i \mathbf{v}_i^H$$
where $k < r$.

**Note:** the rank of $\mathbf{A}_k$ is $k$, so it has fewer independent rows/columns than $\mathbf{A}$.

$\mathbf{A}_k$ is the **best** approximation of $\mathbf{A}$ with rank $k$.

### 5. Effective rank
The effective rank is the number of singular values that are **greater than the noise level.**

### 6. Least-squares solutions
Recall that the least-squares solution is
$$\hat{\mathbf{x}}=\left(\mathbf{A}^H \mathbf{A}\right)^{-1} \mathbf{A}^H \mathbf{b}=\mathbf{A}^{+} \mathbf{b}$$
#### Full rank case
Partition the SVD as:
$$\mathbf{A}=\left[\begin{array}{l:l}\mathbf{U}_1 & \mathbf{U}_2\end{array}\right]\left[\begin{array}{c}\boldsymbol{\Sigma}_1 \\ \mathbf{0}\end{array}\right] \mathbf{V}^H$$
The least-squares solution is:
$$\hat{\mathbf{x}}=\mathbf{V} \boldsymbol{\Sigma}_1^{-1} \mathbf{U}_1^H \mathbf{b}$$
(derivation in lecture notes)

With zero padding:
$$
\hat{\mathbf{x}}=\mathbf{V} \boldsymbol{\Sigma}^{+} \mathbf{U}^H \mathbf{b}
$$
where $\boldsymbol{\Sigma}^{+}$is the pseudo inverse of $\boldsymbol{\Sigma}$ :
$$
\boldsymbol{\Sigma}^{+}=\left[\begin{array}{lll}
1 / \sigma_1 & & \\
& \ddots & \\
& & 1 / \sigma_n \\
& &
\end{array}\right]
$$

**Note:**
The pseudoinverse of $\mathbf{A}$ becomes:
$$\mathbf{A}^{+}=\left(\mathbf{A}^H \mathbf{A}\right)^{-1} \mathbf{A}^H=\mathbf{V} \boldsymbol{\Sigma}_1^{-1} \mathbf{U}_1^H$$

#### Stability
$$\|\hat{\mathbf{x}}\|^2_2 \geq |\mathbf{u}_n^H \mathbf{b}|^2 / \sigma_{\text{min}}^2$$
This means that if the smallest singular value $\sigma_{\text{min}}$ is small, then the least squares solution will be large and very sensitive to changes in $\mathbf{b}$.

#### Rank deficient case
For rank deficient matrix, some of the singular values are zero (i.e. $\sigma_\text{min} = 0$) $\rightarrow$ the solution is unstable.

 Partition the SVD in an alternative form:
$$
\mathbf{A}=\left[\begin{array}{ll}
\mathbf{U}_1 & \mathbf{U}_2
\end{array}\right]\left[\begin{array}{cc}
\boldsymbol{\Sigma}_1 & \mathbf{0} \\
\mathbf{0} & \mathbf{0}
\end{array}\right]\left[\begin{array}{ll}
\mathbf{V}_1 & \mathbf{V}_2
\end{array}\right]^H
$$
where $\boldsymbol{\Sigma}_1$ has size $r \times r$. It follows that
$$
\mathbf{A}=\mathbf{U}_1 \boldsymbol{\Sigma}_1 \mathbf{V}_1^H
$$
The least-squares solution is:
$$\hat{\mathbf{x}}=\mathbf{V}_1 \boldsymbol{\Sigma}_1^{-1} \mathbf{U}_1^H \mathbf{b}+\mathbf{V}_2 \mathbf{z}$$
for all $\mathbf{z} \in \mathcal{C}^{n-r} \longrightarrow$ there are an infinite number of solutions.

when $\mathbf{V}_2 \mathbf{z} = 0$,
$$\hat{\mathbf{x}}=\mathbf{V}_1 \boldsymbol{\Sigma}_1^{-1} \mathbf{U}_1^H \mathbf{b}$$
is the minimiser to the least-squares problem with minimal $l_2$ norm.


## VI. Principal component analysis (PCA)
**What is PCA?**
- transform variables along directions which variance in the data is greatest
- Geometric interpretation: fits a hyper-ellipse to a dataset, the principal axes are the directions with the greatest variance

Generalising $d_i=\left(\begin{array}{ll}X_{i 1} & X_{i 2}\end{array}\right)\left(\begin{array}{ll}a_1 & a_2\end{array}\right)^T$, the component of each sample in the $\mathbf{a}$ direction is:
$$
\mathbf{d}=\mathbf{X a}
$$

**Goal:** find the direction a that **maximises the variance of $\mathbf{d}$**.

PCA finds the **orthogonal directions $\mathbf{a}_i$, from greatest to least variance.**

### 1. Sample mean and covariance
#### Sample data
$$\mathbf{X}=\left[\begin{array}{cccc}\uparrow & \uparrow & & \uparrow \\ \mathbf{x}_1 & \mathbf{x}_2 & \ldots & \mathbf{x}_p \\ \downarrow & \downarrow & & \downarrow\end{array}\right]$$

#### Sample mean
$$
\overline{\mathbf{x}}=\frac{1}{n} \mathbf{X}^T \mathbf{1}_n
$$
where $\mathbf{1}_n$ is column vector of ones with length $n$.

#### Sample covariance matrix
In terms of the sample matrix $\mathbf{X}$, the sample covariance matrix $(p \times p)$ is given by:
$$
\begin{aligned}
\mathbf{S} & =\frac{1}{n-1}\left(\mathbf{X}-\mathbf{1}_n \overline{\mathbf{x}}^T\right)^T\left(\mathbf{X}-\mathbf{1}_n \overline{\mathbf{x}}^T\right) \\
& =\frac{1}{n-1}\left(\mathbf{X}-\frac{1}{n} \mathbf{1}_{n \times n} \mathbf{X}\right)^T\left(\mathbf{X}-\frac{1}{n} \mathbf{1}_{n \times n} \mathbf{X}\right)
\end{aligned}
$$
where $\mathbf{1}_{n \times n}$ is an $n \times n$ matrix filled with ones.

#### Sample mean and variance of the data
Sample mean of $\mathbf{d}=\mathbf{X a}$ :
$$
\bar{d}:=\frac{1}{n} \sum_{i=1}^n(\mathbf{X} \mathbf{a})_i=\frac{1}{n} \mathbf{1}_n^T \mathbf{X} \mathbf{a}=\frac{1}{n} \mathbf{a}^T \mathbf{X}^T \mathbf{1}_n
$$

Sample variance of $\mathbf{d}=\mathbf{X a}$ :
$$q:=\frac{1}{n-1} \sum_{i=1}^n\left((\mathbf{X a})_i-\bar{d}\right)^2 = \mathbf{a}^T\mathbf{Sa}$$

### 2. Centering
Adjusting $\mathbf{X}$ to make it column centred, i.e. the columns of $\mathbf{X}$ have zero mean,
$$
\begin{aligned}
& \hat{\mathbf{X}}=\mathbf{X}-\frac{1}{n} \mathbf{I}_{n \times n} \mathbf{X} \\
& (n-1) \mathbf{S}=\hat{\mathbf{X}}^T \hat{\mathbf{X}}
\end{aligned}
$$

**Note:**
$$
\mathbf{C}_n=\mathbf{I}_{n \times n}-\frac{1}{n} \mathbf{1}_{n \times n}
$$
is known as the centering matrix. We have $\hat{\mathbf{X}}=\mathbf{C X}$.

### 3. Maximising variance
Given restriction $\|\mathbf{a}\|_2 = 1$, $\mathbf{a}^T\mathbf{Sa}$ is maximised when $\mathbf{a}$ is aligned with **eigenvector** associated with the **largest eigenvalue** of $\mathbf{S}$.

The eigenvalues of $\mathbf{S}$ are the **singular values** of $\hat{\mathbf{X}} \rightarrow$ PCA is and eigen decomposition (diagonalisation) of $\hat{\mathbf{X}}^T \hat{\mathbf{X}}$.

From $(n-1) \mathbf{S}=\hat{\mathbf{X}}^T \hat{\mathbf{X}}=\mathbf{U} \mathbf{\Lambda} \mathbf{U}^T$, the matrix $\mathbf{U}$ rotates the data to a 'new' coordinate system, ordered by decreasing variance.