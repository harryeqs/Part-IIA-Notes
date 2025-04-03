## I. Definitions in probability
**Random experiment**: any situation which has a set of possible outcomes, each of which occurs with a particular probability
**Probability space:** $(\Omega, P)$
- $\Omega$ is a **sample space**: the set of all possible outcomes
- $P$ is a **probability functions**: a function from events to the unit interval $P: {E} \rightarrow [0, 1]$, with the following properties
	1. $P(\Omega)=1$ and $P(\emptyset)=0$
	2. If $A_1, A_2, \ldots$ are disjoint events, $A_i \cap A_j=\emptyset$, then
$$
P\left(\bigcup_{i=1}^{\infty} A_i\right)=\sum_{i=1}^{\infty} P\left(A_i\right)
$$
## II. Conditional probability
### 1. Definition
The conditional probability of $A$ given $B$ is
$$
P(A \mid B)=\frac{P(A \cap B)}{P(B)}
$$
### 2. Law of total probability
Let $B_1, B_2, \ldots, B_n$ be disjoint with $\bigcup_i B_i=\Omega, P\left(B_i\right)>0$, then $$ P(A)=\sum_{i=1}^n P\left(A \mid B_i\right) P\left(B_i\right)$$
### 3. Bayes' rule
$$P(A\mid B) = \frac{P(B \mid A)P(A)}{P(B)}$$
### 4. Chain rule for probability
$$P\left(\bigcap_{i=1}^n A_i\right)=P\left(A_1\right) P\left(A_2 \mid A_1\right) P\left(A_3 \mid A_2 \cap A_1\right) \ldots P\left(A_n \mid \cap_{i=1}^{n-1} A_i\right)$$
### 5. Independence
Events $A$ and $B$ are independent if
$$P(A \cap B) = P(A)P(B)$$
If $A$ and $B$ are independent, $P(A\mid B) = P(A)$.

## III. Random variables and probability distribution
### 1. Random variables
Given a probability space $(\Omega, P)$, a random variable is a function $X: \Omega \rightarrow \mathbb{R}$, ie. $X(\omega) \in \mathbb{R}$ (mapping from sample space to real place).
For $S \subseteq \mathbb{R}$ we write
$$
P(X \in S)=P(\{\omega: X(\omega) \in S\})
$$

A function of a random variable is a random variable
$$
Y=g(X) \Longrightarrow Y(\omega)=g(X(\omega))
$$
### 2. The cumulative distribution function
The cumulative distribution function for a random variable $X$ is the function
$$
\begin{aligned}
F_X(x) & =P(\{\omega: X(\omega) \leq x\}) \\
& =P(X \leq x)
\end{aligned}
$$

We frequently write $F(x)$ if its not ambiguous
- $0 \leq F(x) \leq 1$
- if $x<y$ then $F(x) \leq F(y)$
- $\lim _{x \rightarrow-\infty} F(x)=0, \lim _{x \rightarrow \infty} F(x)=1$
- $F$ is right continuous, $F(x)=\lim _{t \downarrow x} F(t)$
### 3. Discrete random variables
A random variable (rv) $X$ is discrete if it takes values in a countable subset of $\mathbb{R},\left\{x_1, x_2, \ldots\right\}$.
Discrete rvs have a probability mass function
$$
p\left(x_i\right)=P\left(X=x_i\right) \in[0,1]
$$
A set is countable if you can list the members (either finite, or one-to-one mapping with the natural numbers)
### 4. Continuous random variables
A rv $X$ is continuous if its distribution function can be written
$$
F(x)=\int_{-\infty}^x f(u) \mathrm{d} u
$$
for some $0 \leq f(u)<\infty$.
The function $f(x)$ is **probability density function** of the rv $X$.
### 5. Vector random variables
The joint cdf of multivariate rv $\boldsymbol{X}=\left(X_1, \ldots, X_n\right)^T$ on $(\Omega, P)$ is the function
$$
F_{\boldsymbol{X}}(\boldsymbol{x})=P\left(X_1 \leq x_1, X_2 \leq x_2, \ldots, X_n \leq x_n\right)
$$
- $\lim _{y \rightarrow \infty} F_X\left((x, y)^T\right)$
- for discrete, pmf $p(x)=P(\boldsymbol{X} = \boldsymbol{x})$
- for continuous, pdf $f(x)=\frac{\partial^n F_X(x)}{\partial x_1 \ldots \partial x_n}$
### 6. Independent random variables
$X$ and $Y$ are independent if
$$
F_{X,Y}(x,y)=F_X(x)F_Y(y)
$$
for all $x,y$.
In general,
$X_1, X_2, ..., X_n$ are independent if
$$
F_{\boldsymbol{X}}(\boldsymbol{x})=F_{X_1}\left(x_1\right) \ldots F_{X_n}\left(x_n\right)
$$
### 7. Conditional distributions
the conditional pdf of $Y$ given $X$ is
$$
\begin{gathered}
F_{Y \mid X}(y \mid x)=P(Y \leq y \mid X=x) \quad \text { (discrete) } \\
F_{Y \mid X}(y \mid x)=\frac{\int_{-\infty}^y f_{X, Y}(x, v) \mathrm{d} v}{f_X(x)} \quad \text { (continuous) }
\end{gathered}
$$
the conditional pmf/pdf of $Y$ given $X$ is
$$
\frac{f_{X, Y}(x, y)}{f_X(x)}
$$


## III. Change of variables
### 1. Change of variables (univariate)
If the rv $Y$ is a function of the rv $X$, $Y = g(x)$, the distribution for $Y$ is:
- If $g$ is invertible and increasing
$$
f_Y(y) = f_x(g^{-1}(y))\frac{\mathrm{d}g^{-1}}{\mathrm{d}x}
$$
- In general, if $g(x_1)= ... = g(x_n)=y$ then 
$$
f_Y(y)=\sum_{k=1}^{n}\frac{f_X{x_k}}{|g'(x_k)|}
$$
**The goal of sampling:** generate samples form the distribution with pdf $h(x)$
### 2. Change of variables (multivariate)
If $\mathbf{Y}=g(\mathbf{X})$ and $g$ is invertible,
$$
g^{-1}(g(\mathbf{x}))=\mathbf{x}
$$

The Jacobian of $g^{-1}$ at $y$ is
$$
J(\boldsymbol{y})=\left(\begin{array}{ccc}
\frac{d g_1^{-1}}{d y_1} & \ldots & \frac{d g_1^{-1}}{d y_n} \\
\vdots & \ddots & \vdots \\
\frac{d g_n^{-1}}{d y_1} & \cdots & \frac{d g_n^{-1}}{d y_n}
\end{array}\right)
$$
then
$$
f_Y(\boldsymbol{y})=f_X\left(g^{-1}(\boldsymbol{y})\right)|\operatorname{det} J(\boldsymbol{y})|
$$
(this result is from calculus - not specific to probability).
## IV. Sampling
### 1. Defining a probability space from a density
1. sample space $\Omega$
2. probability map $P$
3. function $X(\omega)$
4. $X$ implies $f_X(x)$
Let $f(x) \geq 0$ and $\int_{-\infty}^{\infty} f(x) \mathrm{d} x=1$
The indicator function
$$
\mathbb{I}_A(x)= \begin{cases}1 & \text { if } x \in A \\ 0 & \text { if } x \notin A\end{cases}
$$
then probability space $(\mathbb{R}, P)$ where $P(A)=\int_{-\infty}^{\infty} \mathbb{I}_A(x) f(x) \mathrm{d} x$.
### 2. Inverse transform sampling
Assume we can compute the inverse to the cdf, $H^{-1}(x)$
1. Let $U \sim \mathrm{Unif}(0,1)$
2. Return $H^{-1}(U)$
### 3. Rejection sampling
Assume we can sample from distribution with pdf $g(x)$, and there exists a constant such that $g(x)>\frac{h(x)}{M}$ for all $x$
1. Sample $U \sim \mathrm{Unif}(0,1)$ and $X$ from $g$
2. If $U \leq \frac{h(X)}{M g(X)}$ return $X$, else return to step 1.

## V. More definitions on random variables
### 1. Expectation
The expected value of $X$ is
$$
E[\boldsymbol{X}]= \begin{cases}\sum_x x p(x) & \text { discrete } \\ \int x f_x(x) d^n \boldsymbol{x} & \text { continuous }\end{cases}
$$
Law of the unconscious statistician
$$
E[g(X)]= \begin{cases}\sum_x g(x) p(x) & \text { discrete } \\ \int g(x) f_x(\boldsymbol{x}) d^n \boldsymbol{x} & \text { continuous }\end{cases}
$$
### 2. Moments
- The $k$th moment of $X$ is $\mu_k = E[X^k]$
- The variance of $X$ is $\text{Var}[X] = E[X^2] - E[X]^2$
### 3. Covariance
- The covariance $X$ and $Y$ is $\text{Cov}[X,Y] = E[X,Y] - E[X]E[Y]$
- $X$ and $Y$ are uncorrelated if $E[X,Y] = E[X]E[Y]$
- **Independence implies uncorrelated, but uncorrelated does not imply independence**
### 4. Covariance matrix
For a vector rv $\boldsymbol{X}$, the covariance matrix is
$$
\operatorname{Cov}\left(X_i X_j\right)=\Sigma_{i j}=E\left[X_i X_j\right]-E\left[X_i\right] E\left[X_j\right]
$$
in matrix notation
$$
\boldsymbol{\Sigma}=E\left[\boldsymbol{X} \boldsymbol{X}^T\right]-E[\boldsymbol{X}] E[\boldsymbol{X}]^T
$$
- $\boldsymbol{\Sigma}$ is positive semi-definite + Symmetric
- it has a "square root" $\boldsymbol{\Sigma}=\boldsymbol{S} \boldsymbol{S}^T$
### 5. Important rules
Let $X_1, X_2, \ldots$ be a sequence of iid random variables with finite mean $E[X]=\mu$, and let $S_n=\sum_i X_i$ be the partial sums.

**Law of large numbers:** Let $M$ be a rv that always takes value $\mu$. As $n \rightarrow \infty$, the distribution for the rv $\frac{1}{n} S_n$ approaches M.
**Central limit theorem:** Suppose also that $\operatorname{Var}[X]=\sigma^2$ is finite. Then $\frac{S_n-n \mu}{\sqrt{n \sigma^2}} \sim N(0,1)$.
### 6. Conditional expectation
The conditional expectation of $Y$ given $X$ is
$$
E[Y \mid X]=\left\{\begin{array}{l}
\sum_y y\, p_{Y \mid X}(y \mid x) \\
\int_{-\infty}^{\infty} y \, f_{Y \mid X}(y \mid x) \mathrm{d} y
\end{array}\right.
$$
ie., it is expectation in the conditional distribution.
The tower rule/law of iterated expectation
$$
\begin{aligned}
E[E[Y \mid X]] & =E\left[\sum_y y \frac{P_{X Y}(x, y)}{P_x(x)}\right] \\
& =\sum_x\left(\sum_y y \frac{P_{XY}(x, y)}{P_x(x)}\right) P_x(x) \\
& =\sum_y y P_Y(y)\\
& =E[Y]\\
\end{aligned}
$$
<div class="page-break" style="page-break-before: always;"></div>

## VI. Special functions
### 1. Generating functions
The generating function of $X$ is
$$
G_X(z) = E\left[z^X\right] = \begin{cases} \sum_x z^xp(x) \\
\int_{-\infty}^{\infty} z^x f(x) \mathrm{d}x
\end{cases}
$$
For independent $X, Y, G_{X+Y}(z)=G_X(z) G_Y(z)$
- $G_{a X}(z)=G_X\left(z^a\right)=E\left[z^{a X}\right]=E\left[\left(z^a\right)^X\right]$
- $G_X(1)=1=E\left[1^X\right]$
- $G_X^{\prime}(1)=E[X]=E\left[X z^{x-1}\right]$
- For discrete $X, G_X^{(k)}(0)=k!p(k)$
### 2. Characteristic function
The characteristic function of $X$ is
$$
\varphi_X(t)=E\left[e^{i t x}\right]=G_X\left(e^{i t}\right)
$$
$\varphi_x(t)=\int_{-\infty}^{\infty} e^{i t x} f(x) \mathrm{d} x \quad \leftarrow \quad$ Fourier transform
The inversion formula is
$$
f(x)=\frac{1}{2 \pi} \int_{-\infty}^{\infty} e^{-i t x} \varphi_X(t) \mathrm{d} t
$$
- $\varphi_X^{(k)}(0)=i^k E\left[X^k\right]$
- $\varphi_{X+a}(t)=\varphi_X(t) e^{i a t}$
- For $X, Y$ independent, $\varphi_{aX+bY}(t) = \varphi_X(at) \varphi_Y(bt)$
- If $\varphi_X(t)=\varphi_Y(t)$, $X$ and $Y$ have the same distribution
### 3. Multivariate generating and characteristic function
The generating function for multivariate rv $\boldsymbol{X}$ is
$$
G_X(z)=E\left[\prod_i z_i^{X_i}\right]
$$

The characteristic function for multivariate $\mathrm{rv} \boldsymbol{X}$ is
$$
\varphi_{\boldsymbol{x}}(\boldsymbol{t})=E\left[e^{i \boldsymbol{t} \cdot \boldsymbol{X}}\right]=E\left[\prod_i e^{i t_i X_i}\right]
$$
Fact:
$$
\varphi_{A \boldsymbol{X}+\boldsymbol{b}}(\boldsymbol{t})=e^{i \boldsymbol{t}^T \boldsymbol{b}} \varphi_{\boldsymbol{X}}\left(A^T \boldsymbol{t}\right)
$$
