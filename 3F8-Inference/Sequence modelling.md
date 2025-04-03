## I. Markov models
### 1. Definition
**Markov model = conditional independence relationship + product rule**
#### First order Markov (bi-gram)
Each state only depends on the previous state
$$
p(\{y_t\}^T_{t=1}) = p(y_1)\prod^T_{t=2}p(y_t \mid y_{t-1})
$$
#### Second order Markov (tri-gram)
$$
p(\{y_t\}^T_{t=1}) = p(y_1)p(y_2 \mid y_1)\prod^T_{t=2}p(y_t \mid y_{t-1}, y_{t-2})
$$
### 1. Discrete Markov model
#### First order Markov
States: $y_t \in \{1, \ldots, K\}$
Initial state probabilities: $p(y_1 = k) = \pi_k^0$
Transition probabilities: $p(y_t = k \mid y_{t-1} = l) = T_{k,l}$ (this makes up the stochastic matrix, where $\sum_{k=1}^K T_{k,l} = 1$)
#### Second order Markov
Transition probabilities:
$p(y_t = k \mid y_{t-1} = l, y_{t-2} = m) = T_{k,l,m}$
### 2. Continuous Markov model (auto-regressive Gaussian)
#### First order Markov
States: $y_t \in \mathbb{R}^D$
Initial state probabilities: $p(y_1) = \mathcal{G}(y_1; \mu_0, \Sigma_0)$
Transition density: $p(y_t \mid y_{t-1}) = \mathcal{G}(y_t; \Lambda y_{t-1}, \Sigma)$

#### Second order Markov
Transition density:
$p(y_t \mid y_{t-1}, y_{t-2}) = \mathcal{G}(y_t; \Lambda_1 y_{t-1} + \Lambda_2 y_{t-2}, \Sigma)$

## II. Hidden Markov models
**Motivation: Real data depend on latent variables**
![[hidden-markov-models.png | center | 400]]
### 1. Discrete hidden state
Discrete hidden state: $x_t \in \{1, \ldots, K\}$

Transition distribution: $p(x_t = k \mid x_{t-1} = l) = T_{k,l}$

Continuous observed state – emission density: $p(y_t \mid x_t = k) = \mathcal{G}(y_t; \mu_k, \Sigma_k)$

Discrete observed state – emission matrix: $p(y_t = l \mid x_t = k) = S_{l,k}$

### 2. Continuous hidden state (liner Gaussian state space model)
Continuous hidden state: $x_t \in \mathbb{R}^K$

Transition density: $p(x_t \mid x_{t-1}) = \mathcal{G}(x_t; Ax_{t-1},Q)$

Continuous observed state: $y_t \in \mathbb{R}^D$

Emission density: $p(y_t\mid x_t) = \mathcal{G}(y_t;Cx_t, R)$

## III. Inference for Markov models
### 1. Types of inference
#### Distributional estimates
![[types-of-inference.png | center | 500]]
#### Point estimates
$$x_t^*=\underset{x_t}{\arg \max } \,p\left(x_t \mid y_{1: T}\right) \quad x_{1: T}^{\prime}=\underset{x_{1: T}}{\arg \max } \,p\left(x_{1: T} \mid y_{1: T}\right)$$
corresponding to the most probable state and the most probable sequence respectively.

**Note:**
For LGSSMs: $x^*_{1:T} = x'_{1:T}$
For discrete HMM: $x^*_{1:T} \neq x'_{1:T}$
### 2. General filtering equations
**Motivation:** infer the hidden state using past observed states and emission density
$$\begin{aligned} p\left(x_t \mid y_{1: t}\right) & =p\left(x_t \mid y_t, y_{1: t-1}\right) \\ & =\frac{1}{p\left(y_t \mid y_{1: t-1}\right)} p\left(y_t \mid x_t, y_{1: t-1}\right) p\left(x_t \mid y_{1: t-1}\right) \\ & =\frac{1}{p\left(y_t \mid y_{1: t-1}\right)} p\left(y_t \mid x_t\right) p\left(x_t \mid y_{1: t-1}\right) \\ & \propto p\left(y_t \mid x_t\right) p\left(x_t \mid y_{1: t-1}\right)\end{aligned}$$
where

$$\begin{aligned} p\left(x_t \mid y_{1: t-1}\right) & =\int p\left(x_t, x_{t-1} \mid y_{1: t-1}\right) \mathrm{d} x_{t-1} \\ & =\int p\left(x_t \mid x_{t-1}, y_{1: t-1}\right) p\left(x_{t-1} \mid y_{1: t-1}\right)\mathrm{d} x_{t-1} \\ & =\int p\left(x_t \mid x_{t-1}\right) p\left(x_{t-1} \mid y_{1: t-1}\right) \mathrm{d} x_{t-1}\end{aligned}$$
i.e. predicting the current hidden state from past observed states.

### 3. Kalman filter (for LGSSM)
 ![[kalman-filter.png | center | 600]]

#### Starting point
$$p(x_{t-1} \mid y_{1:t-1}) = \mathcal{G}(x_{t-1}; \mu_{t-1}^{t-1}, V_{t-1}^{t-1})$$
The superscript is the **most recent data used in prediction**.
The subscript is the **variable being predicted**.

#### Diffusion via dynamics
$$
\begin{aligned}
p\left(x_t \mid y_{1: t-1}\right) &= \int p\left(x_t \mid x_{t-1}\right) p\left(x_{t-1} \mid y_{1: t-1}\right) \mathrm{d} x_{t-1} \\
&= \mathcal{G}(x_{t-1}; \mu_{t-1}^{t}, V_{t-1}^{t})
\end{aligned}
$$
where
$$
\begin{aligned}
\mu^{t-1}_t &= A\mu_{t-1}^{t-1} \\
V^{t-1}_t &= AV_{t-1}^{t-1} A^\top + Q
\end{aligned}
$$
#### Combine with likelihood
$$\begin{aligned} p\left(x_t \mid y_{1: t}\right) & \propto \underset{\text { prior }}{p\left(x_t \mid y_{1: t-1}\right)} \underset{\text{likelihood}}{p\left(y_t \mid x_t\right)} \\ p\left(x_t \mid y_{1: t}\right) & =\mathcal{G}\left(x_t ; \mu_t^t, V_t^t\right)\end{aligned}$$
where 
$$\begin{aligned} \mu_t^t & =\mu_t^{t-1}+K_t\left(y_t-C \mu_t^{t-1}\right) \\ V_t^t & =V_t^{t-1}-K_t C V_t^{t-1} \\ K_t & =V_t^{t-1} C^{\top}\left(C V_t^{t-1} C^{\top}+R\right)^{-1}\end{aligned}$$

$K_t$ is the **Kalman gain.**

### 4. Forward algorithm (for discrete HMM)
#### Starting point
$$p\left(x_{t-1}=k \mid y_{1: t-1}\right)=\rho_{t-1}^{t-1}(k)$$
#### Diffusion via dynamics
$$\begin{aligned} p\left(x_t=k \mid y_{1: t-1}\right) & =\sum_{l=1}^K p\left(x_t=k \mid x_{t-1}=l\right) p\left(x_{t-1}=l \mid y_{1:t-1}\right) \\ \quad \rho_t^{t-1}(k) & =\sum_{l=1}^K T(k, l) \rho_{t-1}^{t-1}(l)\end{aligned}$$
#### Combine with likelihood
$$\begin{aligned} p\left(x_t=k \mid y_{1: t}\right) & \propto \underset{\text { prior }}{p(x_t=k \mid y_{1: t-1})} \underset{\text { likelihood }}{p(y_t \mid x_t=k)} \\ \rho_t^t(k) & \propto \rho_t^{t-1}(k) p(y_t \mid x_t=k)\end{aligned}$$

#### Likelihood computation
$$p(y_{1:T}) = \prod^T_{t=1} p(y_t \mid y_{1:t-1})$$
Note that
$$\begin{aligned} p\left(x_t \mid y_{1: t}\right) & =\frac{1}{p\left(y_t \mid y_{1: t-1}\right)} p\left(y_t \mid x_t\right) p\left(x_t \mid y_{1: t-1}\right) \\ & \propto p\left(y_t \mid x_t\right) p\left(x_t \mid y_{1: t-1}\right)\end{aligned}$$
Hence $p(y_t \mid y_{1:t-1})$ is the normalising constant.

Backlinks:
[[State-Space Models]]
[[Controllability and State Feedback]]
[[Introduction to Inference]]
[[Probability]]
