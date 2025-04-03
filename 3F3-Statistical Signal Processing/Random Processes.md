## I. Definition of random process
A random process is a set of random variables $\{X_t: t \in T\}$, where $T$ is an index set.
inFor discrete time random process, $X_t$ is the state at time (or space) $t$, and it evolves over time in some random way.

## II. Markov process
A discrete time random process has the Markov property if
$$
f_{X_t \mid X_{t-1}, \ldots, X_0}\left(x_t \mid x_{t-1}, \ldots, x_0\right)=f_{X_t \mid X_{t-1}}\left(x_t \mid x_{t-1}\right)
$$
for all $t$. Such a process is called a Markov chain.
$\implies$ only need to know the current state to predict the next state (system is "memoryless")

### Homogeneous Markov chain
A homogeneous Markov chain is one where
$$
f_{X_t \mid X_{t-1}}(x\mid y) = f_{X_1 \mid X_0}(x\mid y)
$$
The transition matrix $Q$ for a homogeneous Markov chain on a discrete space is 
$$
Q_{ij} = P(X_{t+1}=j \mid X_t = i)
$$
Note that $Q_{ij}$ is a distribution in $j$, so $\sum_j Q_{ij} = 1$.
For initial condition $\boldsymbol{p}^{(0)}$ and transition matrix $Q$, we have
$$
\boldsymbol{p}^{(n)}=P\left(X_n\right)=\boldsymbol{p}^{(0)} Q^n
$$

## III. Characteristics of random processes
### 1. Stationarity
A discrete time random process $X_0, X_1, \ldots$ is (strictly) stationary if
$$
f_{X_0, \ldots, x_k}\left(x_0, \ldots x_k\right)=f_{X_m, \ldots, x_{m+k}}\left(x_m, \ldots x_{m+k}\right)
$$
for all $m$ and $k$.
In other words, $\left(X_0, \ldots, X_k\right)$ and $\left(X_m, \ldots, X_{m+k}\right)$ have exactly the same distribution and cannot be distinguished.
For Markov chain, stationary if $\pi Q = \pi$
### 2. Irreducibility and current states
A Markov chain is **irreducible** if every state is reachable from every other. 
- An irreducible Markov chain on a finite space has a **unique stationary distribution** $\pi Q =\pi$.
The state $i$ is **recurrent** if a chain that starts in state $i$ will eventually return to $i$ with probability of 1.
- **Positive recurrent** if the average time taken to return is finite
- a state that is not recurrent is **transient**
### 3. Period of state
The period of state $i$ is the largest divisor of $\{n: (Q^n)_{ii} > 0\}$. If the period is 1, the period is **aperiodic**.
### 4. Irreducible aperiodic chain
An irreducible aperiodic chain is on in which all states are reachable form one another and all the states are aperiodic. This is also known as a "nice" chain since it converges.
If $(Q^n)_{ij} > 0$ for all $i, j$ for some $n$, the chain is irreducible and aperiodic.
For an irreducible aperiodic Markov chain, we approach $\pi$ if the chain is positive recurrent. If the state space is finite, we **always** approach $\pi$.
Rate of approach is determined by $|\lambda_2|$, second eigenvalue of the transition matrix $Q$.
### 5. Ergodicity
Let $\boldsymbol{x}=\left(x_1, x_2, \ldots\right)$ be a sample from $\left(X_1, X_1, \ldots\right)$ and let $f(x)$ be some function of the states.
The time average for a particular realisation is
$$
\langle f(x)\rangle=\lim _{T \rightarrow \infty} \frac{1}{T} \sum_{t=1}^T f\left(x_t\right)
$$

A process is **ergodic** if $\langle f(x)\rangle$ **converges to the same value** for any realisation.
- When distinguishing from the time average, we call $E[f]$ the ensemble average
- In general, $\langle f\rangle \neq E[f]$
- Irreducible aperiodic positive recurrent Markov chain $\Longrightarrow$ ergodicity
### 6. Wide sense stationary
A process $\{X_t\}$ is wide sense stationary (WSS) if
- $E[X_t] = \mu$ for all $t$
- $E[X_t X_{t+k}] = E[X_0 X_k] < \infty$ for all $t, k$
Any stationary process with $E[X_t^2] < \infty$ is WSS.
### 7. Autocorrelation function
The autocorrelation function for process $\{X_t\}$ is
$$
R_X(t, t+k) = E[X_t X_{t+k}]
$$
For a WSS process, this does not depend on $t$, hence
$$
R_X(t, t+k) = E[X_t X_{t+k}] = E[X_0 X_k]
$$
$\implies$ $R_X(k)$ indicates WSS
- $R_X$ is an even function
- $R_X(0) \ge 0$
- $|R_X(k)| \le R_X(0)$

## IV. Important random processes
### 1. White noise
A WSS process $\left\{W_t\right\}$ is white if
$$
R_W(k)= \begin{cases}\sigma^2 & \text { for } k=0 \\ 0 & \text { otherwise }\end{cases}
$$
e.g. white Gaussian noise, $W_t \sim N\left(0, \sigma^2\right)$.
Any sequence of uncorrelated variances is white.
### 2. Autoregressive (AR) process
Let $\left\{W_t\right\}$ be white noise, $E\left[W_t\right]=0$ and $R_W(k)=\delta_{0, k} \omega_W^2$. Then $\operatorname{AR}(p)$ is the process $\left(\ldots, X_{-1}, X_0, X_1, \ldots\right)$ where
$$
X_t=\sum_{i=1}^p a_i X_{t-i}+W_t
$$
for constants $a_1, \ldots, a_p$.
- $p$ is called the order, so $\operatorname{AR}(1)$ is 1st order, $\operatorname{AR}(2)$ 2nd order.
- $\operatorname{AR}(1)$ is WSS if $a < 1$.
### 3. Moving average (MA) process
Moving average process, $\operatorname{MA}(q)$ Let $\left\{W_t\right\}$ be white noise, $E\left[W_t\right]=0$ and $R_W(k)=\delta_{0, k} \omega_W^2$. Then $\operatorname{MA}(q)$ is the process $\left(\ldots, X_{-1}, X_0, X_1, \ldots\right)$ where $$ X_t=\sum_{i=1}^q b_i W_{t-i}+W_t $$ for constants $b_1, \ldots, b_q$. 
- $\mathrm{MA}(q)$ is WSS.
### 4. Linear time-invariant systems
If the input to a LTI system is WSS, the output is also WSS.
For an LIT system we can write
$$
Y_t=\sum_{k=-\infty}^{\infty} h_k X_{t-k}
$$
If $X$ is WSS, so is $Y$.
Assumption: $\sum_{k=-\infty}^{\infty}\left|h_k\right|<\infty$
### 5. Autoregressive moving average (ARMA) process
Let $\left\{W_t\right\}$ be white noise, $E\left[W_t\right]=0$ and $R_W(k)=\delta_{0, k} \omega_W^2$. Then $\operatorname{ARMA}(p, q)$ is the process $\left(\ldots, X_{-1}, X_0, X_1, \ldots\right)$ where
$$
X_t=\sum_{i=1}^p a_i X_{t-i}+\sum_{i=0}^q b_i W_{t-i}
$$
for constants $a_1, \ldots, a_p$ and $b_0, \ldots, b_q$. We often assume $b_0=1$.
- $\operatorname{ARMA}(p, q)$ can be represented as the output of an LTI system stimulated with white noise
- Hence, it is WSS
### 6. Power spectrum
Let $R_X(k)=E\left[X_t X_{t+k}\right]$ be the autocorrelation function for WSS $\left\{X_t\right\}$.
The **power spectral density** is the Fourier transform of $R_X(k)$
$$
S_X\left(e^{i \omega}\right)=\sum_{k=\infty}^{\infty} R_X(k) e^{-i k \omega}
$$
The inversion is
$$
R_X(k)=\frac{1}{2 \pi} \int_{-\pi}^\pi S_X\left(e^{i \omega}\right) e^{i k \omega} \mathrm{~d} \omega
$$
For real WSS $\left\{X_t\right\}, S_X\left(e^{i \omega}\right)$ is
- even, $S_X\left(e^{i \omega}\right)=S_X\left(e^{-i \omega}\right)$
- real, $S_X\left(e^{i \omega}\right)=S_X^*\left(e^{i \omega}\right)$
- non-negative $S_X\left(e^{i \omega}\right) \geq 0$
For an LTI system $Y_t=\sum_{k=-\infty}^{\infty} h_k X_{t-k}$, let $H\left(e^{i \omega}\right)=\sum_{t=-\infty}^{\infty} h_t e^{-i t \omega}$. Then,
$$
S_Y\left(e^{i \omega}\right)=S_X\left(e^{i \omega}\right)\left|H\left(e^{i \omega}\right)\right|^2
$$
For any desired $S_X\left(e^{i \omega}\right)$, we can generate white noise and apply transfer function
$$
H\left(e^{i \omega}\right)=\left(S_X\left(e^{i \omega}\right)\right)^{\frac{1}{2}}
$$
to get process with the same power spectrum.

Backlinks:
[[Discrete and Continuous Random Processes]]