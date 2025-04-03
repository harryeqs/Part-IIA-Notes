## I. Estimation theory
### 1. Introduction
Given signal measurements $\mathbf{x}$
$$
\mathbf{x}=\left[\begin{array}{c}
x_0 \\
x_1 \\
\vdots \\
x_{N-1}
\end{array}\right]
$$
we wish to infer the parameters $\boldsymbol{\theta}$
$$
\boldsymbol{\theta}=\left[\begin{array}{c}
\theta_0 \\
\theta_1 \\
\vdots \\
\theta_{P-1}
\end{array}\right]
$$
Usually $P \ll N$ and we have a lot more data than parameters.
#### Likelihood function
$$
p(\mathbf{x}\mid\boldsymbol{\theta})
$$
The likelihood function forms a **generative model** for data — how likely different realisations of the observed data $\mathbf{x}$ would be given the underlying model parameters $\boldsymbol{\theta}$.
#### Prior probability density function
$$
p(\boldsymbol{\theta})
$$
The prior probability density function represent prior belief about likely parameters configurations before any data have been seen.
Prior can be used to **regularise** the inference problem.
#### Estimation vs Inference
**Estimation:** the task is to formulate an estimate $\hat{\boldsymbol{\theta}}$ which is close (in some sense) to the true $\boldsymbol{\theta}$.
**Inference:** the task is to study the whole probability distribution of the unknown, including the uncertainties that remain about the values of $\boldsymbol{\theta}$ once the data $\mathbf{x}$ have been observed.
### 2. The general linear model
In the Linear Model it is assumed that the data $\mathbf{x}$ are generated as a linear function of the parameters $\boldsymbol{\theta}$ with an additive random modelling error term $e_n$ :
$$
x_n=\mathbf{g}_n^T \boldsymbol{\theta}+e_n
$$
where $\mathbf{g}_n$ is a $P$-dimensional column vector.
The expression may be written for the whole vector $\mathbf{x}$ as
$$
\mathbf{x}=\mathbf{G} \boldsymbol{\theta}+\mathbf{e}
$$
where
$$
\mathbf{G}=\left[\begin{array}{c}
{\mathbf{g}_0^T} \\
\mathbf{g}_1^T \\
\vdots \\
\mathbf{g}_{N-1}^T
\end{array}\right] \quad(\text{sized }N \times P)
$$
the matrix $\mathbf{G}$ is known as the **design matrix**.
### 3. Einstein-Wiener-Khinchin Theorem
(This section is included for completeness, could directly jump to the conclusion).
Take a time-windowed version of the signal $x_n$, having duration $2 N+$ 1 samples and zero elsewhere:
$$
x_n^N=w_n^N x_n
$$
where
$$
w_n^N= \begin{cases}1, & -N \leq n \leq N \\ 0, & \text { otherwise }\end{cases}
$$
Look at its DTFT:
$$
X^N\left(e^{j \Omega}\right)=\sum_{n=-\infty}^{+\infty} \overbrace{w_n^N x_n}^{x_n^N} e^{-j n \Omega}
$$
Expand its modulus squared
$$
\left|X^N\left(e^{j \Omega}\right)\right|^2=X^N\left(e^{j \Omega}\right) X^N\left(e^{j \Omega}\right)^*
$$
and hence we can write the following DTFT pair:
$$
\operatorname{DTFT}\left\{x_n^N * x_{-n}^N\right\}=X^N\left(e^{j \Omega}\right) X^N\left(e^{j \Omega}\right)^*=\left|X^N\left(e^{j \Omega}\right)\right|^2
$$
Now expand the time-domain convolution: 
$$ 
x_n^N * x_{-n}^N=\sum_{n=-\infty}^{+\infty} x_n^N x_{n-m}^N=\sum_{n=-\infty}^{+\infty} x_n w_n^N x_{n-m} w_{n-m}^N 
$$
so we have DTFT 
$$
\operatorname{DTFT}\left\{\sum_{n=-\infty}^{+\infty} x_n w_n x_{n-m} w_{n-m}\right\}=\left|X^N\left(e^{j \Omega}\right)\right|^2
$$
Now multiply both sides by one over the window duration $(2 N+1)$ and take expectations on both sides:
$$
\operatorname{DTFT}\left\{\mathbb{E}\left[\frac{1}{2 N+1} \sum_{n=-\infty}^{+\infty} x_n w_n^N x_{n-m} w_{n-m}^N\right]\right\}=\mathbb{E}\left[\frac{1}{2 N+1}\left|X^N\left(e^{j \Omega}\right)\right|^2\right]
$$
simplify the expectation in the DTFT
$$
\begin{gathered}\mathbb{E}\left[\frac{1}{2 N+1} \sum_{n=-\infty}^{+\infty} x_n w_n^N x_{n-m} w_{n-m}^N\right]=\frac{1}{2 N+1} \sum_{n=-\infty}^{+\infty} r_{X X}[m] w_n^N w_{n-m}^N \\ =r_{X X}[m] \frac{1}{2 N+1} \sum_{n=-\infty}^{+\infty} w_n^N w_{n-m}^N=r_{X X}[m] t[m]\end{gathered}
$$
where $t[m]$ is the deterministic autocorrelation function of the window function $w_n$.
Hence
$$
\operatorname{DTFT}\left\{r_{X X}[m] t[m]\right\}=\mathbb{E}\left[\frac{1}{2 N+1}\left|X^N\left(e^{j \Omega}\right)\right|^2\right]
$$
The DTFT of $r_{X X}$ is the power spectrum is $\mathcal{S}_x\left(e^{j \Omega}\right)$, hence
$$
\operatorname{DTFT}\left\{r_{X X}[m] t[m]\right\}=\mathcal{S}_X\left(e^{j \Omega}\right) * T\left(e^{j \Omega}\right)
$$
where $T\left(e^{j \Omega}\right)$ is the DTFT of $t[m]$. As $N$ increases $t[m]$ gets wider and flatter, $T(e^{j\Omega})$ tends to a delta function.
Thus the final limiting expression becomes
$$
\begin{aligned} \lim _{N \rightarrow \infty} \operatorname{DTFT}\left\{r_{X X}[m] t[m]\right\} & =\operatorname{DTFT}\left\{r_{X X}[m]\right\}=\mathcal{S}_x\left(e^{j \Omega}\right) \\ & =\lim _{N \rightarrow \infty} \mathbb{E}\left[\frac{1}{2 N+1}\left|X^N\left(e^{j \Omega}\right)\right|^2\right]\end{aligned}
$$
**Conclusion:** In the limit $N \rightarrow \infty$, the power spectrum is proportional to the expected value of the DTFT-squared to the data.
$$
\boxed{\lim _{N \rightarrow \infty} \mathbb{E}\left[\frac{1}{2 N+1}\left|X^N\left(e^{j \Omega}\right)\right|^2\right]=\mathcal{S}_x\left(e^{j \Omega}\right)}
$$
**i.e. The power spectrum is the expected value of the time-normalised DTFT-squared of the signal values.**

## II. Simple estimators and linear estimations
### 1. Simple estimators
An estimator is **unbiased** if
$$
\mathbb{E}[\hat{\mu}] = \mu
$$
where the expectation is taken w.r.t. the distribution of all of the random variables $X_i$.
The standard mean estimator is unbiased:
$$
\begin{aligned} \mathbb{E}[\hat{\mu}] & =\mathbb{E}\left[\frac{1}{N} \sum_{i=1}^N X_i\right] \\ & =\frac{1}{N} \sum_{i=1}^N \mathbb{E}\left[X_i\right]=\frac{1}{N} N \mu \\ & =\mu\end{aligned}
$$
Looking at the variance of $\hat{\mu}$ ($\mathbb{E}[\hat{\mu}]$ is the sum of autocorrelations of $X$):
$$
\operatorname{var}(\hat{\mu})=\mathbb{E}\left[\hat{\mu}^2\right]-\mathbb{E}[\hat{\mu}]^2=\frac{\sigma^2}{N}
$$
$\implies$ **the variance tends to zero as $N$ tends to infinity.**
Unbiased + var $\rightarrow 0$ as $N \rightarrow \infty$ = **consistent** — such estimator will get the correct answer with enough data.
(estimators can be designed to have no bias and minimum variance — minimum variance unbiased (MVU) estimators)
### 2. Ordinary least squares (OLS) estimator
Recall that the general linear model has the form
$$
\mathbf{x}=\mathbf{G} \boldsymbol{\theta}+\mathbf{e}
$$
The goal is to find the model that minimises the square errors
$$
J=\sum_{n=0}^{N-1} e_n^2=\mathbf{e}^T \mathbf{e}
$$
Expand this using $\mathbf{e}=\mathbf{x}-\mathbf{G} \boldsymbol{\theta}$,
$$
\mathbf{e}^T \mathbf{e}=(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})^T(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})=\mathbf{x}^T \mathbf{x}+\boldsymbol{\theta}^T \mathbf{G}^T \mathbf{G} \boldsymbol{\theta}-2 \boldsymbol{\theta}^T \mathbf{G}^T \mathbf{x}
$$
Th vector gradient is defined as
$$
\nabla \phi=\frac{d \phi(\boldsymbol{\theta})}{d \boldsymbol{\theta}}=\left[\begin{array}{c}\frac{\partial \phi(\boldsymbol{\theta})}{\partial \theta_0} \\ \frac{\partial \phi(\boldsymbol{\theta})}{\partial \theta_1} \\ \vdots \\ \frac{\partial \phi(\boldsymbol{\theta})}{\partial \theta_{P-1}}\end{array}\right]
$$
we obtain:
$$
\frac{d J}{d \boldsymbol{\theta}}=2 \mathbf{G}^T \mathbf{G} \boldsymbol{\theta}-2 \mathbf{G}^T \mathbf{x}
$$
and finally, at a stationary point, setting $\frac{d J}{d \theta}=\mathbf{0}$,
$$
\mathbf{G}^T \mathbf{G} \boldsymbol{\theta}=\mathbf{G}^T \mathbf{x}
$$
or, for invertible $\mathbf{G}^{T} \mathbf{G}$:
$$
\boxed{\boldsymbol{\theta}^{O L S}=\left(\mathbf{G}^T \mathbf{G}\right)^{-1} \mathbf{G}^T \mathbf{x}}
$$
i.e. the classical Ordinary Least Squares estimate of $\boldsymbol{\theta}$.
### 3. Properties of the linear estimator
The OLS estimator of the general linear model is a linear estimator.
#### Bias of OLS estimator
$$
\mathbb{E}\left[\boldsymbol{\theta}^{O L S}\right]=\mathbb{E}\left[\left(\mathbf{G}^T \mathbf{G}\right)^{-1} \mathbf{G}^T \mathbf{x}\right]=\left(\mathbf{G}^T \mathbf{G}\right)^{-1} \mathbf{G}^{T}(\mathbb{E}[\mathbf{x}])
$$
For the linear model $\mathbf{x}=\mathbf{G} \boldsymbol{\theta}+\mathbf{e}$,
$$
\mathbb{E}[\mathbf{x}]=\mathbf{G} \boldsymbol{\theta}+\mathbf{0}=\mathbf{G} \boldsymbol{\theta}
$$
since the noise $\{e_n\}$ has zero mean.
Substituting back gives
$$
\mathbb{E}\left[\boldsymbol{\theta}^{O L S}\right]=\left(\mathbf{G}^T \mathbf{G}\right)^{-1} \mathbf{G}^T \mathbf{G} \boldsymbol{\theta}=\left(\mathbf{G}^T \mathbf{G}\right)^{-1}\left(\mathbf{G}^T \mathbf{G}\right) \boldsymbol{\theta}=\boldsymbol{\theta}
$$
$\implies$ the OLS is unbiased
#### Covariance of OLS estimator
Define the OLS matrix term as
$$
\mathbf{C}=\left(\mathbf{G}^T \mathbf{G}\right)^{-1} \mathbf{G}^T
$$
Then examine the variance of any other unbiased estimator, which we write as:
$$
\hat{\boldsymbol{\theta}}=\mathbf{D x}
$$
where
$$
\mathbf{D}=\mathbf{C}+\Delta
$$
and $\Delta$ is some matrix perturbation away from the OLS solution.
For $\mathbf{D x}$ to be unbiased we require as above that
$$
\mathbb{E}[\mathbf{D} \mathbf{x}]=\boldsymbol{\theta}
$$
i.e.
$$
\mathbb{E}[(\mathbf{C}+\Delta) \mathbf{x}]=(\mathbf{C}+\boldsymbol{\Delta}) \mathbb{E}[\mathbf{x}]=(\mathbf{C}+\boldsymbol{\Delta}) \mathbf{G} \boldsymbol{\theta}=\boldsymbol{\theta}+\boldsymbol{\Delta} \mathbf{G} \boldsymbol{\theta}=\boldsymbol{\theta}
$$
and therefore we require
$$
\Delta \mathbf{G}=\mathbf{0}
$$
since it must work for all $\boldsymbol{\theta}$.
For unbiased estimators $\mathbb{E}[\hat{\boldsymbol{\theta}}]=\boldsymbol{\theta}$ $\implies$ the covariance matrix of the estimation error is:
$$
\operatorname{cov}(\hat{\boldsymbol{\theta}})=\mathbb{E}\left[(\hat{\boldsymbol{\theta}}-\boldsymbol{\theta})(\hat{\boldsymbol{\theta}}-\boldsymbol{\theta})^T\right]=\mathbb{E}\left[\hat{\boldsymbol{\theta}} \hat{\boldsymbol{\theta}}^T\right]-\boldsymbol{\theta} \boldsymbol{\theta}^T
$$
For the linear estimator $\hat{\boldsymbol{\theta}}=\mathbf{D x}$, we have
$$
\mathbb{E}\left[\hat{\boldsymbol{\theta}} \hat{\boldsymbol{\theta}}^T\right]=\mathbb{E}\left[\mathbf{D} \mathbf{x} \mathbf{x}^T \mathbf{D}^T\right]=\mathbf{D} \mathbb{E}\left[\mathbf{x} \mathbf{x}^T\right] \mathbf{D}^T
$$
while,
$$
\mathbf{x x}^T=(\mathbf{G} \boldsymbol{\theta}+\mathbf{e})(\mathbf{G} \boldsymbol{\theta}+\mathbf{e})^T=\mathbf{G} \boldsymbol{\theta} \boldsymbol{\theta}^T \mathbf{G}^T+\mathbf{e} \mathbf{e}^T+\mathbf{e} \boldsymbol{\theta} \mathbf{G}^T+\mathbf{G} \boldsymbol{\theta} \mathbf{e}^T
$$
(the expectation of the last two terms are zero since $\mathbb{E}[\mathbf{e}] = 0$)
$$
\mathbb{E}\left[\mathbf{x x}^T\right]=\mathbf{G} \boldsymbol{\theta} \boldsymbol{\theta}^T \mathbf{G}^T+\sigma_e^2 \mathbf{I}
$$
since $\left\{e_n\right\}$ is zero mean white noise with variance $\sigma_e^2$.
Now the expectation is obtained as
$$
\begin{aligned}
\mathbb{E}\left[\hat{\boldsymbol{\theta}} \hat{\boldsymbol{\theta}}^T\right] & =\mathbf{D}\mathbb{E}\left[\mathbf{x} \mathbf{x}^T\right] \mathbf{D}^T \\
& =\mathbf{D}\left(\mathbf{G} \boldsymbol{\theta} \boldsymbol{\theta}^T \mathbf{G}^T+\sigma_e^2 \mathbf{I}\right) \mathbf{D}^T \\
& =\boldsymbol{\theta} \boldsymbol{\theta}^T+\sigma_e^2 \mathbf{D D}^T
\end{aligned}
$$
(this last line is obtained by substituting for $\mathbf{D}=\mathbf{C}+\Delta$ and using the unbiasedness criterion, $\boldsymbol{\Delta} \mathbf{G}=\mathbf{0}$).
Hence
$$
\begin{aligned}
& \operatorname{cov}(\hat{\boldsymbol{\theta}})=\mathbb{E}\left[\hat{\boldsymbol{\theta}} \hat{\boldsymbol{\theta}}^T\right]-\boldsymbol{\theta} \boldsymbol{\theta}^T=\sigma_e^2 \mathbf{D D}^T \\
& =\sigma_e^2(\mathbf{C}+\Delta)(\mathbf{C}+\boldsymbol{\Delta})^T \\
& =\sigma_e^2\left(\mathbf{C} \mathbf{C}^T+\boldsymbol{\Delta} \boldsymbol{\Delta}^T+\Delta \mathbf{C}^T+\mathbf{C} \boldsymbol{\Delta}^T\right) \\
& =\sigma_e^2\left(\mathbf{C C}^T+\boldsymbol{\Delta} \boldsymbol{\Delta}^T\right)\\
& =\sigma_e^2\left((\mathbf{G}^T\mathbf{G})^{-1} + \boldsymbol{\Delta}\boldsymbol{\Delta}^T\right)
\end{aligned}
$$
Clearly with $\boldsymbol{\Delta}=\mathbf{0}$ we have the OLS estimator covariance, so
$$
\operatorname{cov}(\hat{\boldsymbol{\theta}})=\operatorname{cov}\left(\boldsymbol{\theta}^{O L S}\right)+\sigma_e^2 \boldsymbol{\Delta} \boldsymbol{\Delta}^T
$$
Since $\boldsymbol{\Delta} \boldsymbol{\Delta}^T \ge 0$, the **OLS estimator is the minimum variances unbiased estimator** — this is a **best linear unbiased estimator (BLUE)**.

## III. Likelihood-based inference
### 1. Multivariate Gaussian PDF
In this section and the next on Bayesian estimation, we will require the Multivariate Gaussian density function, for a length $N$ random column vector $\mathbf{X}$
$$
f_{\mathbf{X}}(\mathbf{x})=\frac{1}{\sqrt{2 \pi}^N \operatorname{det}\left(\mathbf{C}_{\mathbf{X}}\right)^{\frac{1}{2}}} \exp \left(-\frac{1}{2}(\mathbf{x}-\boldsymbol{\mu})^T \mathbf{C}_{\mathbf{X}}{ }^{-1}(\mathbf{x}-\boldsymbol{\mu})\right)
$$
- $\mu=E[\mathbf{X}]$ is the mean vector
- $\mathbf{C}_{\mathbf{x}}=E\left[(\mathbf{X}-\boldsymbol{\mu})(\mathbf{X}-\boldsymbol{\mu})^T\right]$ is the Covariance Matrix
- Elementwise, $[\mathbf{C}_\mathbf{X}]_{i j}=c_{X_i X_j}$ the covariance between elements $X_{i-1}$ and $X_{j-1}$.
### 2. Maximum likelihood estimate
The likelihood $L(\mathbf{x} ; \boldsymbol{\theta})$ is known as the p.d.f for $\mathbf{x}$ when the value of $\boldsymbol{\theta}$ is known, defined as:
$$
L(\mathbf{x} ; \boldsymbol{\theta})=p(\mathbf{x} \mid \boldsymbol{\theta})
$$
Note: it is often more convenient to maximise the **log-likelihood.**
The Maximum Likelihood (ML) estimate for $\boldsymbol{\theta}$ is then that value of $\boldsymbol{\theta}$ which maximises the likelihood for given observations $\mathbf{x}$: 
$$
\boldsymbol{\theta}^{ML}=\underset{\boldsymbol{\theta}}{\operatorname{argmax}}\{p(\mathbf{x} \mid \boldsymbol{\theta})\}
$$
$\implies$ the ML solution corresponds to the parameter vector which could have generated the observed data $\textbf{x}$ with the highest probability.

For Gauss-Markov model (aka linear Gaussian model, where the error term $\mathbf{e}$ is drawn from i.i.d., zero-mean Gaussian distribution), the probability of the error term $p(\mathbf{e})$ is
$$
\begin{aligned} \prod_{n=0}^{N-1} \frac{1}{\sqrt{2 \pi \sigma_e^2}} e^{-\frac{1}{2 \sigma_e^2} e_n^2} & =\frac{1}{{\sqrt{2 \pi \sigma_e^2}}^N} e^{-\frac{1}{2 \sigma_e} \sum_{n=0}^{N-1} e_n^2} \\ & =\frac{1}{\sqrt{2 \pi \sigma_e^2}^N} e^{-\frac{1}{2 \sigma_e^2} \mathbf{e}^T \mathbf{e}}\end{aligned}
$$
$\implies$ multivariate Gaussian distribution with mean zero and covariance matrix $\sigma_e^2\textbf{I}$:
$$
p(\mathbf{e})=\mathcal{N}\left(\mathbf{e} \mid \mathbf{0}, \sigma_e^2 \mathbf{I}\right)
$$
The likelihood $p(\mathbf{x} \mid \boldsymbol{\theta})$ can be obtained from a change of variables from $\textbf{e} \rightarrow \textbf{x}$ with unity Jacobian (since $\mathbf{x}=\mathbf{G} \boldsymbol{\theta}+\mathbf{e}$)
$$
L(\mathbf{x} ; \boldsymbol{\theta})=p(\mathbf{x} \mid \boldsymbol{\theta})=p_{\mathbf{e}}(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})
$$
Expand and take log
$$
\begin{aligned} \log L(\mathbf{x} ; \boldsymbol{\theta}) & =-(N / 2) \log \left(2 \pi \sigma_e^2\right)-\frac{1}{2 \sigma_e^2}(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})^T(\mathbf{x}-\mathbf{G} \boldsymbol{\theta}) \\ & =-(N / 2) \log \left(2 \pi \sigma_e^2\right)-\frac{1}{2 \sigma_e^2} \sum_{n=0}^{N-1}\left(x_n-\mathbf{g}_n^T \boldsymbol{\theta}\right)^2 \\ & =-\frac{1}{2 \sigma_e^2} \sum_{n=0}^{N-1}\left(x_n-\mathbf{g}_n^T \boldsymbol{\theta}\right)^2+\text { Const. }\end{aligned}
$$
Maximising the function w.r.t. $\boldsymbol{\theta}$ = minimising the sum-squared of the error sequence
$$
J=\sum_{n=0}^{N-1}\left(x_n-\mathbf{g}_n^T \boldsymbol{\theta}\right)^2
$$
$\implies$ the same criterion for ordinary least squares (OLS) estimation.
Hence the ML estimator is the same as the OLS estimator
$$
\boxed{{\boldsymbol{\theta}^{M L}}=\boldsymbol{\theta}^{O L S}=\left(\mathbf{G}^T \mathbf{G}\right)^{-1} \mathbf{G}^T \mathbf{x}}
$$
### 3. Estimating the noise variance
The log-likelihood function at the optimal parameter estimate $\boldsymbol{\theta}^{ML}$ can be considered as a function of $\sigma_e^2$
$$
\begin{aligned}
\log L\left(\mathbf{x} ; \boldsymbol{\theta}^{M L}, \sigma_e^2\right) & =-(N / 2) \log \left(2 \pi \sigma_e^2\right) \\
& -\frac{1}{2 \sigma_e^2}\left(\mathbf{x}-\mathbf{G} \boldsymbol{\theta}^{M L}\right)^T\left(\mathbf{x}-\mathbf{G} \boldsymbol{\theta}^{M L}\right) \\
& =-(N / 2) \log \left(2 \pi \sigma_e^2\right)-\frac{1}{2 \sigma_e^2} J^{M L}
\end{aligned}
$$
where $J^{M L}$ is the minimum squared error term corresponding to the ML optimisation.
Differentiate wrt $\sigma_e^2$ and set to zero to get:
$$
\frac{\partial \log L\left(\mathbf{x} ; \boldsymbol{\theta}^{M L}, \sigma_e^2\right)}{d \sigma_e^2}=-\frac{(N / 2)}{\sigma_e^2}+\frac{J^{M L}}{2\left(\sigma_e^2\right)^2}=0
$$
and hence
$$
\sigma_e^2{ }^{M L}=J^{M L} / N
$$
i.e. the just mean-squared error at the ML parameter solution.

## IV. Bayesian inference
### 1. Bayesian methods
A **prior** probability density function can be included to express some highly qualitative prior knowledge (subjective information).

Applying Bayes' Theorem to estimation of random parameters $\boldsymbol{\theta}$ from a random vector $\mathbf{x}$ of observations, gives the posterior or a posteriori probability for the parameter:
$$
p(\boldsymbol{\theta} \mid \mathbf{x})=\frac{p(\mathbf{x} \mid \boldsymbol{\theta}) p(\boldsymbol{\theta})}{p(\mathbf{x})}
$$
- $p(\mathbf{x} \mid \boldsymbol{\theta})$ is the likelihood
- $p(\boldsymbol{\theta})$ is the prior or a priori distribution for the parameters
- $p(\boldsymbol{\theta} \mid \mathbf{x})$ is the posterior or a posteriori distribution, which expresses the probability of $\boldsymbol{\theta}$ given the observed data $\mathbf{x}$ —this is now a true measure of how 'probable' a particular value of $\boldsymbol{\theta}$ is, given the observations $\mathbf{x}$ (whereas likelihood expresses how probable the observations are given the parameters)
- $p(\textbf{x})$ is the marginal likelihood (aka evidence in machine learning) is a useful quantity in model selection problems and is constant for any given observation $\mathbf{x}$

Since $p(\textbf{x})$ is constant, it may be ignored if we are only interested in the relative posterior probabilities of different parameters $\boldsymbol{\theta}$.
This gives Bayes' theorem in the form
$$
\boxed{
p(\boldsymbol{\theta} \mid \mathbf{x}) \propto p(\mathbf{x} \mid \boldsymbol{\theta}) \; p(\boldsymbol{\theta})
}
$$
$p(\textbf{x})$ may be calculated by integration and serves as the normalising constant for the posterior density.

### 2. Posterior inference
Posterior p.d.f. with values well defined for all $\boldsymbol{\theta}$ gives a fully interpretable probability distribution rather than a single estimate of $\boldsymbol{\theta}$.
To find a single point estimate for $\boldsymbol{\theta}$, it can be assessed through a cost function $C(\hat\theta, \theta)$.
A simple and intuitive way to perform Bayesian estimation is the maximum a posteriori (MAP) estimate
$$
\boxed{\boldsymbol{\theta}^{\mathrm{MAP}}=\underset{\boldsymbol{\theta}}{\operatorname{argmax}}\{p(\boldsymbol{\theta} \mid \mathbf{x})\}}
$$
#### MAP estimation scheme (under linear Gaussian model)
Suppose that the prior on the parameter $\boldsymbol{\theta}$ is the multivariate Gaussian
$$
\begin{aligned}
p(\boldsymbol{\theta}) & =\mathcal{N}\left(\mathbf{m}_{\boldsymbol{\theta}}, \mathbf{C}_{\boldsymbol{\theta}}\right) \\
& =\frac{1}{(2 \pi)^{P / 2}\left|\mathbf{C}_{\boldsymbol{\theta}}\right|^{1 / 2}} \exp \left(-\frac{1}{2}\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right)^T \mathbf{C}_{\boldsymbol{\theta}}^{-1}\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right)\right)
\end{aligned}
$$
where $\mathbf{m}_{\boldsymbol{\theta}}$ is the prior parameter mean vector, $\mathbf{C}_{\boldsymbol{\theta}}$ is the parameter covariance matrix and $P$ is the number of parameters in $\boldsymbol{\theta}$.
The posterior distribution is:
$$ 
\begin{aligned} p(\boldsymbol{\theta} \mid \mathbf{x}) \propto & p(\boldsymbol{\theta}) p(\mathbf{x} \mid \boldsymbol{\theta}) \\ \propto & \frac{1}{(2 \pi)^{P / 2}\left|\mathbf{C}_{\boldsymbol{\theta}}\right|^{1 / 2}} \exp \left(-\frac{1}{2}\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right)^T \mathbf{C}_{\boldsymbol{\theta}}^{-1}\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right)\right) \quad \text{[prior]}\\ & \frac{1}{\left(2 \pi \sigma_e^2\right)^{N / 2}} \exp \left(-\frac{1}{2 \sigma_e^2}(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})^T(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})\right) \quad \text{[likelihood]} \end{aligned}
$$
$-2$ times the log-probability:
$$
\begin{aligned}
-2 \log (p(\boldsymbol{\theta} \mid \mathbf{x}))
&=\left(\boldsymbol{\theta}-\mathbf{m}_\theta\right)^T \mathbf{C}_{\boldsymbol{\theta}}^{-1}\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right)+\frac{1}{\sigma_e^2}(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})^T(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})+\text { Const } \\
&=\boldsymbol{\theta}^T\left(\boldsymbol{C}_\boldsymbol{\theta}^{-1}+\frac{\mathbf{G}^T \mathbf{G}}{\sigma_e^2}\right) \boldsymbol{\theta}+2 \boldsymbol{\theta}^T \left(-\boldsymbol{C}_\boldsymbol{\theta}^{-1} \boldsymbol{m}_\boldsymbol{\theta}-\frac{\mathbf{G}^T \mathbf{x}}{\sigma_e^2}\right)+ \text{Const}
\end{aligned}
$$
Taking the gradient:
$$
\nabla_{\boldsymbol{\theta}}\,\log (p(\boldsymbol{\theta} \mid \mathbf{x})) = 2\left(\boldsymbol{C}_\boldsymbol{\theta}^{-1}+\frac{\mathbf{G}^T \mathbf{G}}{\sigma_e^2}\right)\boldsymbol{\theta} - 2\left(\boldsymbol{C}_\boldsymbol{\theta}^{-1} \boldsymbol{m}_\boldsymbol{\theta}+\frac{\mathbf{G}^T\mathbf{x}}{\sigma_e^2}\right)
$$
Hence the MAP estimate $\boldsymbol{\theta}^\mathrm{MAP}$ is:
$$
\boxed{\boldsymbol{\theta}^{\mathrm{MAP}}=\left(\mathbf{G}^T \mathbf{G}+\sigma_e^2 \mathbf{C}_{\boldsymbol{\theta}}^{-1}\right)^{-1}\left(\mathbf{G}^T \mathbf{x}+\sigma_e^2 \mathbf{C}_{\boldsymbol{\theta}}^{-1} \mathbf{m}_{\boldsymbol{\theta}}\right)}
$$
- As the prior becomes more diffuse, i.e. the diagonal elements of $\mathbf{C}_\boldsymbol{\theta}$ increase both in magnitude and relative to the off-diagonal elements — we impose less prior information on the estimate
- In the limit the prior tends to a uniform prior with all $\boldsymbol{\theta}$ equally probable, $\mathbf{C}_\boldsymbol{\theta}^{-1} = 0$ and the estimate is identical to the ML estimate $\implies$ ML estimate = MAP estimate with a uniform prior assigned to $\boldsymbol{\theta}$.
- The MAP estimate also tends to towards the ML estimate when the likelihood is strongly 'peaked' about its maximum compared with the prior
- As the sample size $N$ tends to infinity, the Bayesian solution tends to the ML solution
- The choice of Gaussian prior makes the Bayesian calculations straightforward and available in closed form — it is a 'conjugate' prior
#### The complete posterior distribution
By completing the square:
$$
\begin{aligned}
-2 \log (p(\boldsymbol{\theta} \mid \mathbf{x})) &= \frac{1}{\sigma_e^2}(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})^T(\mathbf{x}-\mathbf{G} \boldsymbol{\theta})+\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right)^T \mathbf{C}_{\boldsymbol{\theta}}{ }^{-1}\left(\boldsymbol{\theta}-\mathbf{m}_{\boldsymbol{\theta}}\right) \theta \\ &=\frac{1}{\sigma_e^2}\left(\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\mathrm{MAP}}\right)^T \boldsymbol{\Phi}\left(\boldsymbol{\theta}-\boldsymbol{\theta}^{\mathrm{MAP}}\right)+\mathbf{x}^T \mathbf{x}+\sigma_e^2 \mathbf{m}_{\boldsymbol{\theta}}{ }^T \mathbf{C}_{\boldsymbol{\theta}}{ }^{-1} \mathbf{m}_{\boldsymbol{\theta}}-\boldsymbol{\Theta}^T \boldsymbol{\theta}^{\mathrm{MAP}}\right)\end{aligned}
$$
with terms defined as
$$
\begin{aligned}
\boldsymbol{\theta}^{\mathrm{MAP}} & =\boldsymbol{\Phi}^{-1} \boldsymbol{\Theta} \\
\boldsymbol{\Phi} & =\mathbf{G}^T \mathbf{G}+\sigma_e^2 \mathbf{C}_{\boldsymbol{\theta}}^{-1} \\
\boldsymbol{\Theta} & =\mathbf{G}^T \mathbf{x}+\sigma_e^2 \mathbf{C}_{\boldsymbol{\theta}}{ }^{-1} \mathbf{m}_{\boldsymbol{\theta}}
\end{aligned}
$$
The first term is in the form for the exponent of a multi-variate Gaussian, with mean vector and covariance matrix as $\mathbf{m}_{\boldsymbol{\theta}}^{\text {post }}=\boldsymbol{\theta}^{\mathrm{MAP}}$ and $\mathbf{C}_{\boldsymbol{\theta}}^{\text {post }}=\sigma_e^2 \boldsymbol{\Phi}^{-1}$.
Since the remaining terms do not depend on $\boldsymbol{\theta}$ $\implies$ **the posterior distribution is a multivariate Gaussian**
$$
p(\boldsymbol{\theta} \mid \mathbf{x})=\mathcal{N}\left(\boldsymbol{\theta}^{\mathrm{MAP}}, \sigma_e^2 \boldsymbol{\Phi}^{-1}\right)
$$
### 3. MMSE estimation
The cost function $C(\hat\theta,\theta)$ expresses the cost of estimating the parameter as $\hat\theta$ when the true value is $\theta$.
We can write the expected cost over all of the unknown parameters, conditional upon the observed data $\mathbf{x}$ : 
$$ 
\mathbb{E}[C(\hat{\theta}, \theta)]=\int_\theta C(\hat{\theta}, \theta) \,p(\theta \mid \mathbf{x}) d \theta
$$
The form of the cost function will depend on the requirements of a particular problem.
(Note that due to the random properties of the model, we can only calculate the expected cost of a particular estimator)

A classic estimation technique related to the Wiener filtering object function is the minimum mean-squared error (MMSE) estimation method. Given some data $\mathbf{x}$ we attempt to find an estimator $\hat{\theta}(\mathbf{x})$ which has minimum squared error, on average:
$$
\min _{\hat{\theta}} \mathbb{E}\left[(\hat{\theta}-\theta)^2\right]
$$
The MSE is:
$$
J=\mathbb{E}\left[(\hat{\theta}-\theta)^2\right]=\int_\theta(\hat{\theta}-\theta)^2 \, p(\theta \mid \mathbf{x}) d \theta
$$
Differentiate with respect to $\hat\theta$:
$$
\begin{aligned} \frac{d J}{d \hat{\theta}} & =\frac{d}{d \hat{\theta}} \int_\theta(\hat{\theta}-\theta)^2 p(\theta \mid \mathbf{x}) d \theta \\ & =\int_\theta \frac{d}{d \hat{\theta}}(\hat{\theta}-\theta)^2 p(\theta \mid \mathbf{x}) d \theta \\ & =\int_\theta 2(\hat{\theta}-\theta) p(\theta \mid \mathbf{x}) d \theta\end{aligned}
$$
Setting the gradient to zero:
$$\int_\theta \hat{\theta} p(\theta \mid \mathbf{x}) d \theta=\hat{\theta} \int_\theta p(\theta \mid \mathbf{x}) d \theta=\hat{\theta} \times 1=\int_\theta \theta p(\theta \mid \mathbf{x}) d \theta=\mathbb{E}[\theta \mid \mathbf{x}]$$
Hence the solution is
$$
\boxed{\hat{\theta}^{\mathrm{MMSE}}=\mathbb{E}[\theta \mid \mathbf{x}]=\int_\theta \theta p(\theta \mid \mathbf{x}) d \theta}
$$
For the linear Gaussian model, the posterior distribution was obtained as:
$$
p(\boldsymbol{\theta} \mid \mathbf{x})=\mathcal{N}\left(\boldsymbol{\theta}^{\mathrm{MAP}}, \sigma_e^2 \boldsymbol{\Phi}^{-1}\right)
$$
$\implies$ the mean value of this distribution is $\boldsymbol{\theta}^{\mathrm{MAP}}$
Hence the MMSE estimator for the linear Gaussian model is:
$$
\boldsymbol{\theta}^\textrm{MMSE} = \boldsymbol{\theta}^\textrm{MAP}
$$

## V. Summary of estimators
### Least squares
Pros:
- requires no knowledge of probability distributions
- usually the simplest scheme to implement
- guarantee of performance as BLUE estimator

Cons:
- cannot incorporate prior knowledge about the parameter probability distributions
- no guarantees of the performance compared to non-linear estimators
### Maximum likelihood
Pros:
- performance guaranteed to be optimal when the amount of data is large

Cons:
- requires knowledge of noise probability distribution
- cannot incorporate prior knowledge about the parameter probability distributions
- can be more complicated to implement than LS in the non-Gaussian case
### Bayesian (MAP and MMSE)
Pros:
- incorporates prior knowledge about the parameter probability distributions
- performance guaranteed to be optimal for any amount of data (provided prior distribution is correct)

Cons:
- requires knowledge of noise probability distribution (because likelihood is needed to compute the posterior distribution)
- can be more complicated to implement than LS or ML (depending on form of likelihood and prior)

Backlinks:
[[Probability]]