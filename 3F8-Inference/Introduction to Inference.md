## I. Probabilistic approach

In the expressions below there is only a single parameter $\lambda$. The rules could be extended to high-dimensional parameters $\boldsymbol{\theta}$.

**Joint distribution:** probability of everything
$$
p(x_{1:N}, \lambda) = p(\lambda)p(x_{1:N}\mid \lambda)
$$
**Likelihood:** distribution of observations given parameters
$$
p(x_{1:N}\mid \lambda)
$$
**Prior:** expected distribution of the parameters
$$
p(\lambda)
$$
**Posterior:** distribution of parameters given observations
$$
p(\lambda \mid x_{1:N})
$$

**Bayes' rule:** used to form the posterior
$$
p\left(\lambda \mid \mathrm{x}_{1: N}\right)=\frac{1}{p\left(\mathrm{x}_{1: N}\right)} p(\lambda) p\left(\mathrm{x}_{1: N} \mid \lambda\right)
$$

**Maximum a posteriori (MAP) estimate**
$$
\lambda^{\mathrm{MAP}}=\underset{\lambda}{\arg \max } \;p\left(\lambda \mid \mathrm{x}_{1: N}\right)
$$
**Maximum likelihood estimate**
$$
\lambda^{\mathrm{ML}}=\underset{\lambda}{\arg \max } p\left(\mathrm{x}_{1: N} \mid \lambda\right)
$$
$\lambda^{\text{MAP}} = \lambda^{\text{ML}}$ when the priors are flat (uniform).

## II. Bayesian decision theory
Conditional reward:
$$
\mathrm{R}(t \mid b) = \sum_{a} R(a,t)p(a \mid b)
$$
$\mathrm{R}(t \mid b):$ the conditional reward
$t$: the action
$\sum_a$: sum over possible worlds (variable $a$)
$R(a,t)$: reward for action in that world (given as by reward matrix)
$p(a \mid b)$: posterior probability of the world

The goal is to take actions that maximise the reward.

Backlinks:
[[Estimation Theory and Inference]]