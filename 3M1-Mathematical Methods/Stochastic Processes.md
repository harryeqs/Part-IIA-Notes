## I. Finite state-space Markov chains
### 1. Markov chain and transition matrix
#### Markov chain
A Stochastic Process $X_0, X_1, X_2, \ldots$ is a Markov chain **if and only if** for all times $i \geq 1$ $$ P\left(X_{i+1} \mid X_0=j_0, X_1=j_1, \ldots, X_i=j_i\right)=P\left(X_{i+1} \mid X_i=j_i\right)$$
i.e. **current state only depends on the last state.**

#### Transition matrix
Each element of the transition matrix $\mathbf{P}$ indicates:
$$
P_{j, k}=\operatorname{Prob}(j \rightarrow k), \quad \sum_k P_{j, k}=1, \quad P_{j, k} \geq 0
$$

For any time $n$
$$
\mathbf{x}^{(n)}=\mathbf{x}^{(0)} \mathbf{P}^n
$$
where $\mathbf{x}^{(n)}$ is the vector denoting the distribution of $X_n$.

#### Chapman-Kolmogorov equations
$$\begin{aligned} P\left(X_{i+n}=k \mid X_i=j\right) & =P_{j, k}^n \\ & =\left(\mathbf{P}^s \mathbf{P}^{n-s}\right)_{j, k} \\ & =\sum_l P_{j, l}^s P_{l, k}^{n-s} \\ & =\sum_l P\left(X_{i+s}=l \mid X_i=j\right) P\left(X_{i+n}=k \mid X_{i+s}=l\right)\end{aligned}$$
### 2. Properties of Markov chain
#### Stationary distribution
For any limiting distribution:
$$
\mathbf{x}^{(\infty)} \mathbf{P}=\mathbf{x}^{(\infty)}
$$
any distribution that satisfies this expression is a stationary distribution

#### Regular ergodic
A Markov Chain is **regular ergodic** if there exists a **unique stationary distribution** which is the limit point for all initial distributions and which puts positive mass on every element of the state-space $\mathcal{S}$ (i.e. visit every element in the state-space).

For an $n \times n$ transition matrix $\mathbf{P}$ then
1. $\lambda=1$ is an eigenvalue of $\mathbf{P}$
2. all eigenvalues satisfy $|\lambda| \leq 1$

#### Communicate
Two states of a Markov chain $j$ and $k$ **communicate** if, and only if, there exists integers $m$ and $n$ such that
$$
P_{j, k}^m>0 \text { and } P_{k, j}^n>0
$$

**Intuition:**
- there must be a route from state $j$ to $k$ (in $m$ steps)
- there must be a route from state $k$ to $j$ (in $n$ steps)

#### Recurrent set
Let $\mathcal{S}$ denote the set of all possible states of a Markov chain. 

A subset $\tilde{\mathcal{S}} \subseteq \mathcal{S}$ is a **recurrent set** if
1. all pairs of states in $\tilde{\mathcal{S}}$ communicate
2. if $j \in \tilde{\mathcal{S}}$ and $k \notin \tilde{\mathcal{S}}$ then $P_{j, k}^i=0$ for all $i \geq 0$

**Intuition:**
- it is possible to move between all states in a recurrent set
- cannot move from a member of a recurrent set to not a member

#### Recurrent and transient
If a state belongs to a recurrent set then it is recurrent, otherwise it is transient.
A transient state is **never returned.**

#### Irreducible
If all states in a Markov chain communicate with each other, then the Markov chain is **irreducible**.

#### Waiting time
**Approach:**
- set up equations to describe the scenario
- find expression for the waiting time from each state
- solve a series of linear equations of waiting time from each state

#### Periodicity
The period of a state $k$ of a Markov chain is the greatest common divisor of the set
$$
\begin{aligned}
& \left\{i \geq 0: P_{k, k}^i>0\right\} \\
& i=\text { number of steps }
\end{aligned}
$$

A state $k$ is **aperiodic if it has period 1.**
i.e. A state $k$ is aperiodic if for some time $i$:
$$
P_{k, k}^i>0 \text { and } P_{k, k}^{i+1}>0
$$

If a chain is **irreducible and aperiodic** then it is **regular ergodic** it will have a limiting distribution.

#### Detailed balance
A transition matrix $\mathbf{P}$ and a distribution $\boldsymbol{\pi}$ are in **detailed balance** if
$$
\pi_j P_{j, k}=\pi_k P_{k, j}
$$
where $\mathcal{S}$ is the state-space of the Markov chain.

The detailed balanced distribution $\pi$ is a **stationary distribution** of $\mathbf{P}$.

## II. Continuous state-space systems
### 1. Birth process (Yule-Furry process)
#### Definition
**Set-up:**
- $\lambda$: birth rate for a cell per unit time
- $n(t)$: the number of cells at time instance $t$
- $n(0)= n_0$: number of cells initially

The process is described by the equation:
$$
n(t + \Delta t) = n(t) + n(t) \lambda \Delta t
$$
The process it **continuous** in time and **Markovian**.

**Standard solution:**
$$
n(t) = n_0 \exp(\lambda t)
$$

#### Probabilistic approach
The probability of $n$ cells at time $t$ is denoted
$$
P(n(t) = n) = P_n(t)
$$

Consider time slot $t \rightarrow t + \Delta t$:
$$
P_n(t + \Delta t) = P_n(t)\underbrace{(1 - n\lambda \Delta t)}_{\text{ prob. of no birth in }\Delta t} + P_{n-1}(t)\underbrace{((n-1)\lambda\Delta t)}_{\text{prob. of birth in }\Delta t}
$$
- the first term considers the case where no birth occurs -- stay in the same state
- the second term considers the case where birth occurs -- move from the previous state

Take the limiting condition $\Delta t \rightarrow 0$:
$$
\frac{dP_n(t)}{dt} = -n\lambda P_n(t) + (n-1) \lambda P_{n-1}(t)
$$

#### Birth process chain
For continuous time the **transition rate matrix** $\mathbf{Q}$ is used:
$$
\frac{d \mathbf{x}(t)}{d t}=\mathbf{x}(t) \mathbf{Q} ; \quad x_n(t)=P_n(t) \quad \sum_{n=1}^{\infty} P_n(t)=1
$$
where (note rows sum to zero - probability mass conserved)
$$
\mathbf{Q}=\left[\begin{array}{ccccc}
-\lambda & \lambda & 0 & 0 & \cdots \\
0 & -2 \lambda & 2 \lambda & 0 & \cdots \\
0 & 0 & -3 \lambda & 3 \lambda & \ddots \\
\vdots & \vdots & \ddots & \ddots & \ddots
\end{array}\right]
$$
#### Solution
Assuming $n(0) = n_0$,
$$P_n(t)=\binom{n-1}{n-n_0} \exp \left(-\lambda n_0 t\right)(1-\exp (-\lambda t))^{n-n_0}$$
There is **no** steady-state distribution.

#### Birth-death process
Introduce **death-rate** for a cell per unit time: $\mu$.
$$\begin{aligned} P_n(t+\Delta t)&= \underbrace{P_n(t)(1-n \lambda \Delta t-n \mu \Delta t)}_{\text{stay in the same state}}+ \underbrace{P_{n-1}(t)((n-1) \lambda \Delta t)}_\text{birth occurs} \\ & +\underbrace{P_{n+1}(t)((n+1) \mu \Delta t)}_{\text{death occurs}}\end{aligned}$$

### 2. Brownian motion (Wiener process)
**Note:** the Brownian motion is a Markov process.

**Assumptions in the following derivation:**
- treated the system as discrete (finite small changes in $\tau$ ) in time
- distribution $p(\Delta)$ will depend on $\tau$
- finite Taylor Series expansions were used
- smoothness assumption of the particle density function
- assumption that $p(\Delta)$ does not change with position, $x$
#### Particle density
Denote the particle density at time $t$ and position $x$ as:
$$
f(x,t)
$$
**Assuming** smoothness in the particle density over space and time, apply Taylor expansion:

Consider a small shift in the position $x$ to $x+\Delta$:
$$
f(x+\Delta, t) \approx f(x, t)+\Delta \frac{\partial f(x, t)}{\partial x}+\frac{\Delta^2}{2!} \frac{\partial^2 f(x, t)}{\partial x^2}+\mathcal{O}\left(\Delta^3\right)
$$

Consider a (very) small change in time from $t$ to $t+\tau$
$$
f(x, t+\tau) \approx f(x, t)+\tau \frac{\partial f(x, t)}{\partial t}+\mathcal{O}\left(\tau^2\right)
$$

#### Expected movement of particles
![[particle-movement.png | center | 400]]
To find the particles at location $x$ at time $t + \tau$:
$$
f(x, t+\tau)=\int_{-\infty}^{\infty} f(x+\Delta, t) p(-\Delta) d \Delta
$$
where $p(\Delta)$ is the probability of a particle moving $\Delta$ in time $\tau$
(This is a continuous form of Chapman-Kolmogorov)

Assume that $p(\Delta)$ is symmetric and combining with the Taylor series expansion gives:
$$\begin{aligned} f(x, t+\tau) & =\int_{-\infty}^{\infty} f(x+\Delta, t) p(\Delta) d \Delta \\ & \approx \int_{-\infty}^{\infty}\left(f(x, t)+\Delta \frac{\partial f(x, t)}{\partial x}+\frac{\Delta^2}{2!} \frac{\partial^2 f(x, t)}{\partial x^2}\right) p(\Delta) d \Delta \\
&= f(x,t) + \frac{\partial^2 f(x, t)}{\partial x^2}\int_{-\infty}^{\infty}\frac{\Delta^2}{2!} p(\Delta) d\Delta \\
& \approx f(x,t) + \tau \frac{\partial f(x,t)}{\partial t}\end{aligned}$$

#### Simple diffusion equation
Since both $\tau$ and $\Delta$ are small, the last two lines from above gives the **simple diffusion equation** (a Fokker-Planck equation):
$$\frac{\partial f(x, t)}{\partial t}=D \frac{\partial^2 f(x, t)}{\partial x^2}, \quad D=\frac{1}{2 \tau} \int_{-\infty}^{\infty} \Delta^2 p(\Delta) d \Delta$$

#### Properties
At time $t$, examine the Wiener Process - $W_t$

**Independence:**
$W_t - W_s$ is independent of $\{W_\tau\}_{\tau \leq s}$ for any $0 \leq s \leq t$

**Stationarity:**
The distribution of $W_{t+s} - W_s$ is independent of $s$

**Gaussianity:**
$W_t$ is Gaussian with
$$\mathcal{E}\left\{W_t\right\}=0 ; \quad \mathcal{E}\left\{W_t W_s\right\}=2 \alpha \min (t, s)$$

**Continuity:**
$W_t$ is a continuous function with $t$

#### Wiener process with drift
$$\frac{\partial p(x, t)}{\partial t}=m \frac{\partial p(x, t)}{\partial x}+D \frac{\partial^2 p(x, t)}{\partial x^2}$$

#### Orstein-Uhlenbeck process
$$\frac{\partial}{\partial t} p(x, t)=\frac{\partial}{\partial x}(\beta x p(x, t))+\frac{\partial^2}{\partial x^2}(B p(x, t))$$
- $\beta x$ controls the drift
- $B$ controls the diffusion

## III. Markov Chain Monte Carlo
**Goal:** 
- estimate complicated integrals in the form of 
$$
\int h(\mathbf{x}) d\mathbf{x}
$$
- generate random samples $\mathbf{x}^{(i)}$
### 1. Monte Carlo integration
**Motivation:** rather than traversing the whole histogram, sample from a weighting function $w(\mathbf{x})$ and use the sample to estimate the integral.

Normalise to make it a valid PDF:
$$p(\mathbf{x})=\frac{w(\mathbf{x})}{\int w(\mathbf{x}) d \mathbf{x}}$$

Consider uniform distribution over 'volume' $V$: $p(\mathbf{x}) = 1/V$.

Integration over the histogram can then be written as:
$$\int h(\mathbf{x}) d \mathbf{x}=\int \frac{h(\mathbf{x})}{p(\mathbf{x})} p(\mathbf{x}) d \mathbf{x} \approx \underbrace{\frac{1}{N}\sum_{i=1}^N \frac{h\left(\mathbf{x}^{(i)}\right)}{p\left(\mathbf{x}^{(i)}\right)}}_{\text{expectation of } h(\mathbf{x})/p(\mathbf{x}) \text{ over } p(\mathbf{x})}=\frac{V}{N} \sum_{i=1}^N h\left(\mathbf{x}^{(i)}\right)$$
**Note:** the samples $\mathbf{x}^{(i)}$ are drawn from $p(\mathbf{x})$.

### 2. Mean and variance of estimate
Expected value of a function:
$$\mathcal{E}\{f(\mathbf{x})\}=\int f(\mathbf{x}) p(\mathbf{x}) d \mathbf{x} \approx \frac{1}{N} \sum_{i=1}^N f\left(\mathbf{x}^{(i)}\right)$$
Expected value of the estimate using $N$ independent samples:
$$\operatorname{mean}(N)=\frac{1}{N} \sum_{i=1}^N \operatorname{mean}(1)=\frac{1}{N} \sum_{i=1}^N \int f(\mathbf{x}) p(\mathbf{x}) d \mathbf{x}=\mathcal{E}\{f(\mathbf{x})\}$$

Variance of the estimate using one sample
$$\operatorname{var}(1)=\int(f(\mathbf{x})-\mu)^2 p(\mathbf{x}) d \mathbf{x}$$

Variance of the estimate using $N$ independent samples
$$\operatorname{var}(N)=\frac{1}{N} \operatorname{var}(1)$$

### 3. Importance sampling
**Motivation:** can't sample from $p(\mathbf{x})$ but must use another PDF $q(\mathbf{x})$.

Draw samples from the distributions $q(\mathbf{x})$:
$$\mathcal{E}\{f(\mathbf{x})\}=\int\left(f(\mathbf{x}) \frac{p(\mathbf{x})}{q(\mathbf{x})}\right) q(\mathbf{x}) d \mathbf{x} \approx \frac{1}{N} \sum_{i=1}^N f\left(\mathbf{x}^{(i)}\right) \frac{p\left(\mathbf{x}^{(i)}\right)}{q\left(\mathbf{x}^{(i)}\right)}$$

The ratio $\frac{p\left(\mathbf{x}^{(i)}\right)}{q\left(\mathbf{x}^{(i)}\right)}$ is the **'importance'** of the drawn sample.
- some regions over-represented in samples with $p(\mathbf{x}) > q(\mathbf{x})$
- some regions under-represented in samples with $p(\mathbf{x}) < q(\mathbf{x})$

#### Importance sampling for numerical integration
$$\int h(\mathbf{x}) d \mathbf{x}=\int\left(\frac{h(\mathbf{x})}{p(\mathbf{x})}\right) p(\mathbf{x}) d \mathbf{x}=\int\left(\frac{h(\mathbf{x})}{p(\mathbf{x})}\right) \frac{p(\mathbf{x})}{q(\mathbf{x})} q(\mathbf{x}) d \mathbf{x} \approx \frac{1}{N} \sum_{i=1}^N \frac{h\left(\mathbf{x}^{(i)}\right)}{q\left(\mathbf{x}^{(i)}\right)}$$
The ratio $\frac{h\left(\mathbf{x}^{(i)}\right)}{q\left(\mathbf{x}^{(i)}\right)}$ is similar to the 'importance' of the drawn sample.

**The closer $q(\mathbf{x})$ is to $h(\mathbf{x})$ the better** $\rightarrow$ sample from regions of higher 'score' and don't sample from areas of zero 'score'

### 4. Rejection sampling
**Outline:**
- accept the sample points under the 'curve' -- the functions
- take the $x$ values of the accepted samples
- reject samples above the curve

**Rejection rate**: the percentage of samples rejected.
Can be computed by consider areas of the sampling region and the area under the curve.

### 5. Metropolis-Hastings algorithm
**Goal:** Draw samples from a distribution $p(\mathbf{x})$. Given a current sample $\mathbf{x}^{(i)}$, generate another sample, $\mathbf{x}^{(\star)}$, from $p\left(\mathbf{x} \mid \mathbf{x}^{(i)}\right)$ -- the **proposal distribution**.

**Process:**
Accept the sample $\mathbf{x}^{(i+1)}=\mathbf{x}^{(*)}$ with probability $\alpha$, where $$\alpha=\min \left\{\frac{p\left(\mathbf{x}^{(\star)}\right) p\left(\mathbf{x}^{(i)} \mid \mathbf{x}^{(\star)}\right)}{p\left(\mathbf{x}^{(i)}\right) p\left(\mathbf{x}^{(\star)} \mid \mathbf{x}^{(i)}\right)}, 1\right\}$$
Else reject the sample $\mathbf{x}^{(i+1)}=\mathbf{x}^{(i)}$
(No assumption of symmetry required $p\left(\mathbf{x}^{(i)} \mid \mathbf{x}^{(\star)}\right) \neq p\left(\mathbf{x}^{(\star)} \mid \mathbf{x}^{(i)}\right)$)


### 6. Sampling from a finite state-space Markov chain
**Goal:** Given a **limiting distribution** $\boldsymbol{\pi}$, generate samples from a process with this limiting distribution.
Need a transition matrix $\mathbf{R}$ as the **proposal function**.

**Process:** 
1. Choose an arbitrary starting state $X_0, i=0$ 
2. Given $X_i$, select $\hat{X}_{i+1}$ by sampling from the $i^{\text {th }}$ row of $\mathbf{R}$ 
3. Accept $\left(X_{i+1}=\hat{X}_{i+1}\right)$ this sample with probability $\alpha$ $$ \alpha=\min \left\{\frac{\pi_{\hat{X}_{i+1}} r_{\hat{X}_{i+1}, X_i}}{\pi_{X_i} r_{X_i, \hat{X}_{i+1}}}, 1\right\} $$
4. else reject sample $\left(X_{i+1}=X_i\right), i=i+1$, goto (2)

#### Stationary distribution of Metropolis-Hastings
The above process is the equivalent of a transition matrix $\mathbf{P}$ with:
$$
p_{j, k}=r_{j, k} \min \left\{\frac{\pi_k r_{k, j}}{\pi_j r_{j, k}}, 1\right\} \quad \text { if } j \neq k, \quad p_{j, j}=1-\sum_{k \neq j} r_{j, k} \min \left\{\frac{\pi_k r_{k, j}}{\pi_j r_{j, k}}, 1\right\}
$$

Need to show that $\mathbf{P}$ and $\boldsymbol{\pi}$ are in detailed balance
$$
\begin{aligned}
\pi_j p_{j, k} & =\pi_j r_{j, k} \min \left\{\frac{\pi_k r_{k, j}}{\pi_j r_{j, k}}, 1\right\} \\
& =\min \left\{\pi_k r_{k, j}, \pi_j r_{j, k}\right\} \\
& =\pi_k r_{k, j} \min \left\{1, \frac{\pi_j r_{j, k}}{\pi_k r_{k, j}}\right\}=\pi_k p_{k, j}
\end{aligned}
$$

The process is also irreducible and aperiodic - so regular ergodic.
The above criteria are sufficient to show that $\boldsymbol{\pi}$ is the limiting distribution