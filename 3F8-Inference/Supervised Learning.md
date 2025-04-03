## I. Regression
**Goal:** 
- identify patterns and regularities in the mapping between input variables $\mathbf{x}_n$ and a corresponding continuous output variable $y_n$
- return a conditional distribution $p(y_* \mid \mathbf{x}_*)$ for the unknown $y_*$ given a new test input $x_*$
- prediction: predict output on unseen input
- interpretation: identify any relationship between input and output

### 1. Linear regression
For a data set $\mathcal{D}=\left\{\left(\mathbf{x}_n, y_n\right)\right\}_{n=1}^N$, the output of a linear regression model is
$$
y_n=w_0+w_1 x_{n, 1}+\cdots+w_D x_{n, D}+\epsilon_n=\underbrace{\left[w_0, \ldots, w_D\right]}_{\mathbf{w}^{\top}} \underbrace{\left[\begin{array}{c}
1 \\
x_{n, 1} \\
\vdots \\
x_{n, D}
\end{array}\right]}_{\widetilde{\mathbf{x}}_n}+\epsilon_n=\mathbf{w}^{\top} \widetilde{\mathbf{x}}_n+\epsilon_n,
$$
where $\epsilon_n \sim \mathcal{N}\left(0, \sigma^2\right)$ and $\widetilde{\mathbf{x}}_n=\left(1, \mathbf{x}_n\right)^{\top}, \boldsymbol{\theta}=\left\{\sigma^2, \mathbf{w}\right\}$. (note that $\widetilde{\mathbf{x}}_n$ is the augmented inputs, the 1 is for handling $w_0$ – the bias more easily)

**Mean:** $\mathbb{E}[y_n] = \mathbf{w}^\top \mathbf{x}_n$
**Variance:** $\operatorname{Var}[y_n] = \mathbb{E}[{\epsilon_n}^2] = \sigma^2$
**Likelihood:**
$$
p\left(y_n \mid \widetilde{\mathbf{x}}_n, \boldsymbol{\theta}\right)=\mathcal{N}\left(y_n \mid \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n, \sigma^2\right),
$$

### 2. Maximum likelihood estimate (MLE)
**Goal:** maximise $p\left(y_1, \ldots, y_n \mid \widetilde{\mathbf{x}}_1, \ldots, \widetilde{\mathbf{x}}_n, \boldsymbol{\theta}\right)$ w.r.t. $\boldsymbol{\theta}$.

For easier computation use **log-likelihood**:
$$ \begin{aligned} \mathcal{L}(\boldsymbol{\theta}) & =\log p\left(y_1, \ldots, y_n \mid \widetilde{\mathbf{x}}_1, \ldots, \widetilde{\mathbf{x}}_n, \boldsymbol{\theta}\right) \\ & =\log \prod_{n=1}^N p\left(y_n \mid \widetilde{\mathbf{x}}_n, \boldsymbol{\theta}\right)=\sum_{n=1}^N \log \mathcal{N}\left(y_n \mid \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n, \sigma^2\right) \\ & =\sum_{n=1}^N\left\{-\frac{1}{2} \log \left(2 \pi \sigma^2\right)-\frac{1}{2 \sigma^2}\left(y_n-\mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right)^2\right\} \\ & =-\frac{N}{2} \log \left(2 \pi \sigma^2\right)-\frac{1}{2 \sigma^2}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w})^{\top}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w}) \\ & 
= \underbrace{-\frac{N}{2} \log \left(2 \pi \sigma^2\right)-\frac{\mathbf{y}^{\top} \mathbf{y}}{2 \sigma^2}}_{\text{Independent of } \mathbf{w}} -\underbrace{\frac{\mathbf{w}^{\top} \widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{2 \sigma^2}}_{\text {Quadratic term }}+\underbrace{\frac{\mathbf{y}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{\sigma^2}}_{\text {Linear term }} . \end{aligned} $$
where $\mathbf{y}=\left(y_1, \ldots, y_n\right)^{\top}, \widetilde{\mathbf{X}}=\left(\widetilde{\mathbf{x}}_1 ; \ldots ; \widetilde{\mathbf{x}}_n\right)^{\top}$.

The gradient of the log-likelihood at the maximiser is zero:
$$
\begin{aligned} \frac{\partial \mathcal{L}(\theta)}{\partial \mathbf{w}} & =\frac{\partial}{\partial \mathbf{w}}\left(-\frac{\mathbf{w}^{\top} \widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{2 \sigma^2}+\frac{\mathbf{y}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{\sigma^2}\right) \\ & =-\frac{\widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{\sigma^2}+\frac{\widetilde{\mathbf{X}}^{\top} \mathbf{y}}{\sigma^2}=0 \end{aligned}
$$
(Detailed derivation in lecture notes with vector calculus reasoning)

The solution is
$$
\boxed{
\mathbf{w}=\left(\widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}}\right)^{-1} \widetilde{\mathbf{X}}^{\top} \mathbf{y}
}
$$

$\implies$ this is the linear least squares solution (LLSS)

And choice of $\sigma$:
$$
\begin{aligned} \frac{\partial \mathcal{L}(\boldsymbol{\theta})}{\partial \sigma^2} & =\frac{\partial}{\partial \sigma^2}\left(-\frac{N}{2} \log \left(2 \pi \sigma^2\right)-\frac{1}{2 \sigma^2}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w})^{\top}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w})\right) \\ & =-\frac{N}{2 \sigma^2}+\frac{1}{2 \sigma^4}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w})^{\top}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w})=0\end{aligned}
$$
The solution is
$$
\sigma^2 =\frac{1}{N}\left(\mathbf{y}-\widetilde{\mathbf{X}}_{\mathbf{w}}\right)^{\top}(\mathbf{y}-\widetilde{\mathbf{X}} \mathbf{w})
$$

**Problems of MLE**
- when $N < D + 1$ (number of samples smaller than feature dimension), the MLE is not defined
- many values of $\mathbf{w}$ fit the data equally well, achieving zero training error (but bad on test)
- the matrix $\widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}}$ is low rank and not invertible

### 3. Non-linear regression
**Motivation:** use linear regression to model non-linear relationships by replacing $\mathbf{x}$ with non-linear functions (basis functions) $\boldsymbol{\phi}(\mathbf{x})$ of the inputs:
$$
\boldsymbol{\phi}(\mathbf{x})=\left(\phi_1(\mathbf{x}), \ldots, \phi_M(\mathbf{x})\right)^{\top}
$$
e.g. polynomials $\phi_m(x) = x^m$.

**Gaussian radial basis functions**
$$
\begin{array}{r}\phi_m(\mathbf{x})=\exp \left\{-\frac{1}{2} s\left(\mathbf{x}, \mathbf{c}_m, s\right)^2\right\} \\ s\left(\mathbf{x}, \mathbf{c}_m, \boldsymbol{s}\right)=\sqrt{\left(\mathbf{x}-\mathbf{c}_m\right)^{\top}\left(\mathbf{x}-\mathbf{c}_m\right) / s^2}\end{array}
$$
Parameters:
$\mathbf{c}_m$: centre of basis functions
$s$: width of the basis function

**Sigmoidal basis functions**
$$
\begin{aligned} \phi_m(\mathbf{x}) & =\sigma\left(s\left(\mathbf{x}, \mathbf{c}_m, s\right)\right) \\ \sigma(x) & =\frac{1}{1+\exp (-x)} .\end{aligned}
$$

The basis functions are **uniformly** spread in input space to capture non-linearities everywhere.

### 4. Overfitting
A large number of basis functions ($M$) can lead to over-fitting: the model fits the training data well but performs poorly on new test data.

As $M$ increases, the magnitude of the MLE $\mathbf{w}^*$ becomes large -> large oscillations in the model's predictions.

**Solution:** Use a prior to enforce $\mathbf{w}$ to be small -> regularisation

## II. Bayesian linear regression
**Motivation:** add regularisation to make $\mathbf{w}$ small -> leads to smoother predictions

### 1. Bayesian inference
The **posterior** distribution of $\mathbf{w}$ given the dataset is:
$$
p(\mathbf{w} \mid \mathbf{y}, \widetilde{\mathbf{X}})=\frac{p(\mathbf{y} \mid \widetilde{\mathbf{X}}, \mathbf{w}) \overbrace{p(\mathbf{w})}^{p(\mathbf{w} \mid \widetilde{\mathbf{X}})}}{p(\mathbf{y} \mid \widetilde{\mathbf{X}})}
$$
(note that $p(\mathbf{w}) = p(\mathbf{w}\mid \widetilde{\mathbf{X}})$ since prior on $\mathbf{w}$ does not depend on the observations $\mathbf{\widetilde{\mathbf{X}}}$)

The **predictive distribution** for $y_\star$ given a new corresponding test $\mathbf{x}_\star$ is:
$$
p\left(y_{\star} \mid \widetilde{\mathbf{x}}_{\star}, \mathbf{y}, \widetilde{\mathbf{X}}\right)=\int \underbrace{p\left(y_{\star} \mid \widetilde{\mathbf{x}}_{\star}, \mathbf{w}\right)}_{p\left(y_{\star} \mid \widetilde{\mathbf{x}}_{\star}, \mathbf{y}, \widetilde{\mathbf{X}}, \mathbf{w}\right)} \underbrace{p(\mathbf{w} \mid \mathbf{y}, \widetilde{\mathbf{X}})}_{p\left(\mathbf{w} \mid \widetilde{\mathbf{x}}_{\star}, \mathbf{y}, \tilde{\mathbf{X}}\right)} d \mathbf{w}
$$
Exact inference is possible if prior and noise distributions are **Gaussian**.

### 2. Multivariate Gaussian distribution
#### Definition
The density of a $D$-dimensional vector $\mathbf{x}$ is:
$$
\mathcal{N}(\mathbf{x} \mid \mathbf{m}, \mathbf{V}) = \frac{1}{\sqrt{(2 \pi)^D|\mathbf{V}|}} \exp \left\{-\frac{1}{2}(\mathbf{x}-\mathbf{m})^{\top} \mathbf{V}^{-1}(\mathbf{x}-\mathbf{m})\right\}
$$
The density is proportional to the exponential of a **quadratic function** of $\mathbf{x}$ : 
$$ 
\begin{aligned} \mathcal{N}(\mathbf{x} \mid \mathbf{m}, \mathbf{V}) & =\frac{1}{\sqrt{(2 \pi)^D|\mathbf{V}|}} \exp \left\{-\frac{1}{2} \mathbf{x}^{\top} \mathbf{V}^{-1} \mathbf{x}+\mathbf{m}^{\top} \mathbf{V}^{-1} \mathbf{x}-\frac{1}{2} \mathbf{m}^{\top} \mathbf{V}^{-1} \mathbf{m}\right\} \\ & \propto \exp \left\{-\frac{1}{2} \mathbf{x}^{\top} \mathbf{V}^{-1} \mathbf{x}+\mathbf{m}^{\top} \mathbf{V}^{-1} \mathbf{x}\right\} \end{aligned} 
$$

$\mathbf{m}$ is the $D$-dimensional mean vector and $\mathbf{V}$ is the $D \times D$ covariance matrix:
$$
\mathbf{m}=\mathbf{E}[\mathbf{x}], \quad \mathbf{V}=\mathbf{E}\left[(\mathbf{x}-\mathbf{m})(\mathbf{x}-\mathbf{m})^{\top}\right]=\mathbf{E}\left[\mathbf{x x}^{\top}\right]-\mathbf{m} \mathbf{m}^{\top}
$$

$\mathbf{m}$ determines **mode location** and $\mathbf{V}$ **scales and rotates** the space.

#### Linear combination of Gaussian random variables
**Key idea:** Linear combinations of Gaussian random variables are Gaussian

Let $p(\mathbf{x})=\mathcal{N}\left(\mathbf{x} \mid \mathbf{0}, \mathbf{V}_1\right)$ and $p(\mathbf{e})=\mathcal{N}\left(\mathbf{e} \mid \mathbf{0}, \mathbf{V}_2\right)$ and $\mathbf{y}=\mathbf{W} \mathbf{x}+\mathbf{e}$.

$p(\mathbf{y})$ is Gaussian with mean
$$
\mathbf{m}_3=\mathbf{E}[\mathbf{y}]=\mathbf{E}[\mathbf{W} \mathbf{x}+\mathbf{e}]=\mathbf{W E}[\mathbf{x}]+\mathbf{E}[\mathbf{e}]=\mathbf{0}
$$
and covariance matrix
$$
\mathbf{V_3} = \mathbf{WV_1W}^\top + \mathbf{V_2}
$$

#### Completing the square
**Goal:** Write $\mathbf{m}$ and $\mathbf{V}$ in terms of $\mathbf{P}$ and $\mathbf{a}$.
$$
\begin{aligned}
& p(\mathbf{x}) \propto \exp \left\{-\frac{1}{2} \mathbf{x}^{\top} \mathbf{V}^{-1} \mathbf{x}+\mathbf{m}^{\top} \mathbf{V}^{-1} \mathbf{x}\right\} \\
& q(\mathbf{x})=\exp \left\{-\frac{1}{2} \mathbf{x}^{\top} \mathbf{P} \mathbf{x}+\mathbf{a}^{\top} \mathbf{x}\right\}
\end{aligned}
$$
Therefore, $\mathbf{V}=\mathbf{P}^{-1}$ and $\mathbf{m}=\mathbf{V a}$.

#### Product of Gaussian densities
**Key idea:** Product of Gaussian densities may be formatted into Gaussian
Let $p(\mathbf{x})=\mathcal{N}\left(\mathbf{x} \mid \mathbf{m}_1, \mathbf{V}_1\right)$ and $q(\mathbf{x})=\mathcal{N}\left(\mathbf{x} \mid \mathbf{m}_2, \mathbf{V}_2\right)$ -> find $t(\mathbf{x}) \propto p(\mathbf{x}) q(\mathbf{x})$ $\mathcal{N}\left(\mathbf{x} \mid \mathbf{m}_3, \mathbf{V}_3\right)$

$$ \begin{aligned} p(x) q(x)= & \;\mathcal{N}\left(\mathbf{x} \mid \mathbf{m}_1, \mathbf{V}_1\right) \,\mathcal{N}\left(\mathbf{x} \mid \mathbf{m}_2, \mathbf{V}_2\right) \\ = & \frac{1}{\sqrt{(2 \pi)^D\left|\mathbf{V}_1\right|}} \exp \left\{-\frac{1}{2} \mathbf{x}^{\top} \mathbf{V}_1^{-1} \mathbf{x}+\mathbf{m}_1^{\top} \mathbf{V}_1^{-1} \mathbf{x}-\frac{1}{2} \mathbf{m}_1^{\top} \mathbf{V}_1^{-1} \mathbf{m}_1\right\} \\ & \frac{1}{\sqrt{(2 \pi)^D\left|\mathbf{V}_2\right|}} \exp \left\{-\frac{1}{2} \mathbf{x}^{\top} \mathbf{V}_2^{-1} \mathbf{x}+\mathbf{m}_2^{\top} \mathbf{V}_2^{-1} \mathbf{x}-\frac{1}{2} \mathbf{m}_2^{\top} \mathbf{V}_2^{-1} \mathbf{m}_2\right\} \\ \propto & \,\exp \{-\frac{1}{2} \mathbf{x}^{\top} \underbrace{\left(\mathbf{V}_1^{-1}+\mathbf{V}_2^{-1}\right)}_{\mathbf{v}_3^{-1}} \mathbf{x}+\underbrace{\left(\mathbf{m}_1^{\top} \mathbf{V}_1^{-1}+\mathbf{m}_2^{\top} \mathbf{V}_2^{-1}\right)}_{\mathbf{m}_3^{\top} \mathbf{V}_3^{-1}} \mathbf{x}\} . \end{aligned} $$
Therefore, $\mathbf{V}_3=\left(\mathbf{V}_1^{-1}+\mathbf{V}_2^{-1}\right)^{-1}$ and $\mathbf{m}_3=\mathbf{V}_3\left(\mathbf{m}_1^{\top} \mathbf{V}_1^{-1}+\mathbf{m}_2^{\top} \mathbf{V}_2^{-1}\right)^{\top}$.
(by completing the squares)
### 3. Posterior distribution
Recall that the likelihood function under Gaussian noise is $$ p(\mathbf{y} \mid \widetilde{\mathbf{X}}, \mathbf{w})=\prod_{n=1}^N \mathcal{N}\left(y_n \mid \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n, \sigma^2\right) \propto \exp \left\{-\frac{\mathbf{w}^{\top} \widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{2 \sigma^2}+\frac{\mathbf{y}^{\top} \widetilde{\mathbf{X}} \mathbf{w}}{\sigma^2}\right\} $$ Choose the prior for $\mathbf{w}$ to be a **zero-mean isotropic Gaussian:** 
$$
p(\mathbf{w})=\mathcal{N}\left(\mathbf{w} \mid \mathbf{0}, \lambda^{-1} \mathbf{I}\right) \propto \exp \left\{-\frac{1}{2} \mathbf{w}^{\top} \lambda \mathbf{l} \mathbf{w}\right\}
$$

 The posterior is then Gaussian: 
$$ \begin{aligned} p\left(\mathbf{w} \mid \mathbf{y}, \widetilde{\mathbf{X}}, \sigma^2\right) & \propto p(\mathbf{y} \mid \widetilde{\mathbf{X}}, \mathbf{w}) p(\mathbf{w}) \\ & \propto \exp \{-\frac{1}{2} \mathbf{w}^{\top} \underbrace{\left(\widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}} \sigma^{-2}+\lambda \mathbf{I}\right)}_{\mathbf{V}^{-1}} \mathbf{w}+\underbrace{\mathbf{y}^{\top} \widetilde{\mathbf{X}} \sigma^{-2}}_{\mathbf{m}^{\top} \mathbf{V}^{-1}} \mathbf{w}\} \end{aligned} $$

Therefore, 
$$
\boxed{
p\left(\mathbf{w} \mid \mathbf{y}, \widetilde{\mathbf{X}}, \sigma^2\right)=\mathcal{N}(\mathbf{w} \mid \mathbf{m}, \mathbf{V})
}
$$

where 
$$ \mathbf{V}=\left(\tilde{\mathbf{X}}^{\top} \tilde{\mathbf{X}} \sigma^{-2}+\lambda \mathbf{I}\right)^{-1}, \quad \mathbf{m}=\mathbf{V} \sigma^{-2} \tilde{\mathbf{X}}^{\top} \mathbf{y} $$

### 4. Bayesian predictive distribution
The predictive distribution for the $y_{\star}$ of a given new corresponding $\widetilde{\mathbf{x}}_{\star}$ is
$$
\begin{aligned}
p\left(y_{\star} \mid \widetilde{\mathbf{x}}_{\star}, \mathbf{y}, \widetilde{\mathbf{X}}\right)&= \int p\left(y_{\star} \mid \widetilde{\mathbf{x}}_{\star}, \mathbf{w}\right) p(\mathbf{w} \mid \mathbf{y}, \widetilde{\mathbf{X}}) d \mathbf{w} \\ &= \int \mathcal{N}(y_{\star} \mid \mathbf{w}^{\top} \widetilde{\mathbf{x}}_{\star}, \sigma^2) \mathcal{N}(\mathbf{w} \mid \mathbf{m}, \mathbf{V}) d \mathbf{w} \\
& = \mathcal{N}(y_\star \mid m_\star, v_\star)
\end{aligned}
$$
where $m_{\star}=\mathbf{m}^{\top} \widetilde{\mathbf{x}}_{\star}$ and $v_{\star}=\widetilde{\mathbf{x}}_{\star}^{\top} \mathbf{V} \widetilde{\mathbf{x}}_{\star}+\sigma^2$.
(since $y_\star = \mathbf{w}^\top \mathbf{x_\star} + e_\star$ and use rules of linear combination of Gaussians)
### 5. MAP inference
$$
\begin{aligned} \mathbf{w}_{\mathrm{MAP}} & =\underset{\mathbf{w}}{\arg \max } p(\mathbf{w} \mid \mathbf{y}, \widetilde{\mathbf{X}}) \\ & =\underset{\mathbf{w}}{\arg \max } p(\mathbf{y} \mid \mathbf{w}, \widetilde{\mathbf{X}}) p(\mathbf{w}) \\ & =\underset{\mathbf{w}}{\arg \max }\{\log p(\mathbf{y} \mid \mathbf{w}, \widetilde{\mathbf{X}})+\log p(\mathbf{w})\} .\end{aligned}
$$
The $\log p(\mathbf{w})$ term acts as a **regularisation** (without the prior it would just be MLE).

For $p(\mathbf{w})=\mathcal{N}\left(\mathbf{w} \mid \mathbf{0}, \lambda^{-1} \mathbf{I}\right)$:
$$ \mathbf{w}_{\mathrm{MAP}}=\underset{\mathbf{w}}{\arg \max }\left\{\log p(\mathbf{y} \mid \mathbf{w}, \widetilde{\mathbf{X}})-\frac{\lambda}{2} \mathbf{w}^{\top} \mathbf{w}\right\}=\left(\widetilde{\mathbf{X}}^{\top} \widetilde{\mathbf{X}}^{-2}+\lambda \mathbf{I}\right)^{-1} \sigma^{-2} \widetilde{\mathbf{X}}^{\top} \mathbf{y} $$

## III. Classification
**Goal:**
- divide the input space into decision regions, one for each class
- each new input is assign the class of its corresponding decision region
- get a measure of confidence (probability) in the decisions

The decision regions are separated by **decision boundaries**.
These are points at which classes have **equal predictive probability**.

### 1. Deterministic vs probabilistic linear classification

#### Deterministic linear classification 
Maps the output of the linear model into discrete class label.

The decision boundary is where $\mathbf{w}^\top \widetilde{\mathbf{x}} = 0 \rightarrow \mathbf{w}$ is orthogonal to the decision boundary.

**Problems:**
- misclassification errors are not allowed
- cannot use gradient-based methods to find the MLE

#### Probabilistic linear classification 
Maps the output of the linear model into **class probabilities**.

The output is 
$$
p(y_n = 1\mid \widetilde{\mathbf{x}}, \mathbf{w}) = \sigma(\mathbf{w}^\top \widetilde{\mathbf{x}})
$$
where $\sigma(\cdot)$ is a monotonically increasing function that maps $\mathbb{R} \rightarrow [0,1]$.

Examples of $\sigma$: 
- The logistic function: $\sigma(x)=1 /(1+\exp (-x))$. 
- The probit function or Gaussian CDF: $\sigma(x)=\int_{-\infty}^x \mathcal{N}(z \mid 0,1) d z$.

This likelihood function can deal with the problems mentioned above.

### 2. Gradient ascent for MLE
Assume $\sigma(x)$ is the logistic function and that $y_n \in\{-1,1\}$. 

Then
$$
p\left(y_n \mid \mathbf{x}_n, \mathbf{w}\right)=\underbrace{\frac{1+y_n}{2}}_{= 1 \text{ if } y_n = 1} \sigma\left(\mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right)+\underbrace{\frac{1-y_n}{2}}_{= 1 \text{ if } y_n = -1}\left(1-\sigma\left(\mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right)\right)=\sigma\left(y_n \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right)
$$
since $1-\sigma(x)=\sigma(-x)$. 

For $\mathcal{D}=\left\{\mathbf{x}_n, y_n\right\}_{n=1}^N$, the log-likelihood is
$$
\begin{aligned}
\mathcal{L}(\mathbf{w}) & =\log p\left(y_1, \ldots, y_n \mid \mathbf{x}_1, \ldots, \mathbf{x}_N, \mathbf{w}\right) \\
\mathcal{L}(\mathbf{w}) & =\sum_{n=1}^N \log p\left(y_n \mid \mathbf{x}_n, \mathbf{w}\right)=\sum_{n=1}^N \log \sigma\left(y_n \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right) .
\end{aligned}
$$

With $d \sigma(x) / d x=\sigma(x)(1-\sigma(x))$, the gradient is:
$$
\frac{d \mathcal{L}(\mathbf{w})}{d \mathbf{w}}=\sum_{n=1}^N y_n \underbrace{\left(1-\sigma\left(y_n \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right)\right)}_{\text {Error Probability }} \widetilde{\mathbf{x}}_n .
$$

The batch **gradient ascent** rule to maximize $\mathcal{L}(\mathbf{w})$ is
$$
\begin{aligned}
\mathbf{w}^{\mathrm{new}} &=\mathbf{w}^{\mathrm{old}}+\alpha \frac{d \mathcal{L}(\mathbf{w})}{d \mathbf{w}} \\
&=\mathbf{w}^{\text {old }}+\alpha \sum_{n=1}^N y_n\left(1-\sigma\left(y_n \mathbf{w}^{\top} \widetilde{\mathbf{x}}_n\right)\right) \widetilde{\mathbf{x}}_n
\end{aligned}
$$
where $\alpha>0$ is the learning rate.

![[learning-rate.png | center | 500]]

The learning rate $\alpha$ need to be chosen carefully:
- $\alpha$ too large: the optimisation bounces around the maximum -> could diverge
- $\alpha$ too small: the convergence to the maximum is very slow

### 3. Multi-class classification
Use the **soft-max** function to map the outputs into class probabilities:
$$
p\left(y_n=k \mid \mathbf{w}_1, \ldots, \mathbf{w}_K, \widetilde{\mathbf{x}}_n\right)=\frac{\exp \left(\mathbf{w}_k^{\top} \widetilde{\mathbf{x}}_n\right)}{\sum_{k^{\prime}=1}^K \exp \left(\mathbf{w}_{k^{\prime}}^{\top} \widetilde{\mathbf{x}}_n\right)}
$$
### 4. Non-linear logistic regression
Replace $\mathbf{x}$ with non-linear basis functions, inference remains the same.

Backlinks:
[[Introduction to Inference]]
[[Probability]]
[[Estimation Theory and Inference]]