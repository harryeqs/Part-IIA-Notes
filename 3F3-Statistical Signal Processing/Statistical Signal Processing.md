## I. Random processes revision
### 1. Discrete-time random process
A discrete time random process is defined as an ensemble of functions
$$
\{X_n(\omega)\}, \quad n = -\infty, ..., -1, 0, 1, ..., \infty
$$
where $\omega$ is a random variable having a probability density function $f(\omega)$.
### 2. Correlation functions
The **mean** of a random process $\{X_n\}$ is defined as $E[X_n]$.
The **autocorrelation** functions is defined as
$$
r_{XX}[n,m]=E[X_nX_m]
$$
The **cross-correlation** function between two processes $\{X_n\}$ and $\{Y_n\}$ is
$$
r_{XY}[n,m] =E[X_n Y_m]
$$
### 3. Stationarity
A stationary process has the same statistical characteristics irrespective of shifts along the time axis. i.e. the **Nth order density** for the process is unchanged with time shift, where the Nth order density function is
$$
f_{X_{n_1}, X_{n_2}, ... , X_{n_N}} (X_{n_1}, X_{n_2}, ... , X_{n_N})
$$
A random process is **strict-sense stationary** if, for any finite $c, N$ and $\left\{n_1, n_2, \ldots n_N\right\}$ :
$$
\begin{aligned}
f_{X_{n_1}, x_{n_2}, \ldots, X_{n_N}} & \left(\alpha_1, \alpha_2, \ldots, \alpha_N\right) \\
& =f_{X_{n_1+c}, X_{n_2+c}, \ldots, X_{n_N+c}}\left(\alpha_1, \alpha_2, \ldots, \alpha_N\right)
\end{aligned}
$$
### 4. Wide sense stationary
A random process is wide-sense stationary (WSS) iff (if and only if)
1. $\mu_n=\mathbb{E}\left[X_n\right]=\mu$, (mean is constant)
2. $r_{X X}[n, m]=r_{X X}[m-n]$, (autocorrelation function depends only upon the difference between $n$ and $m$ ).
3. The variance of the process is finite:
$$
\mathbb{E}\left[\left(X_n-\mu\right)^2\right]<\infty
$$
### 5. Power spectrum
For a wide-sense stationary random process $\{X_n\}$, the power spectrum is defined as the discrete-time Fourier transform (DTFT) of the discrete autocorrelation function
$$
\mathcal{S}_X\left(e^{j \Omega}\right)=\sum_{m=-\infty}^{\infty} r_{X X}[m] e^{-j m \Omega}
$$
where the normlised frequency $\Omega =\omega T$ is in radians per sample and $T$ is the sampling interval.
The autocorrelation function can thus be found from the power spectrum by inverting the transform using DTFT
$$
r_{X X}[m]=\frac{1}{2 \pi} \int_{-\pi}^\pi \mathcal{S}_X\left(e^{j \Omega}\right) e^{j m \Omega} d \Omega
$$
The power spectrum is a **real, positive, even and periodic** function of frequency.
### 6. White noise
A wide-sense stationary process is white noise if
$$
c_{X X}[m]=\mathbb{E}\left[\left(X_n-\mu\right)\left(X_{n+m}-\mu\right)\right]=\sigma_X^2 \delta[m]
$$
where $\delta[m]$ is the discrete impulse function:
$$
\delta[m]= \begin{cases}1, & m=0 \\ 0, & \text { otherwise }\end{cases}
$$
$\sigma_X^2=\mathbb{E}\left[\left(X_n-\mu\right)^2\right]$ is the variance of the process. If $\mu=0$ then $\sigma_X^2$ is the mean-squared value of the process, which we will sometimes refer to as the 'power'.
The power spectrum of zero mean white noise is
$$
\begin{aligned} \mathcal{S}_X\left(e^{j \omega T}\right) & =\sum_{m=-\infty}^{\infty} r_{XX}[m] e^{-j m \Omega} \\ & =\sigma_X^2\end{aligned}
$$
i.e. **flat across all frequencies**.

## II. Linear systems and random processes
When a wide-sense stationary discrete random process $\left\{X_n\right\}$ is passed through a stable, linear time invariant (LTI) system with digital impulse response $\left\{h_n\right\}$, the output process $\left\{Y_n\right\}$, i.e.
$$
y_n=\sum_{k=-\infty}^{+\infty} h_k x_{n-k}=x_n * h_n
$$
**is also wide-sense stationary.**
### 1. Correlation functions
We can express the output correlation functions and power spectra in terms of the input statistics and the LTI system. The cross-correlation function at the output of a LTI system is
$$
\begin{aligned}
r_{X Y}[k] & =E\left[X_n Y_{n+k}\right]=E\left[X_n \sum_{l=-\infty}^{+\infty} h_l X_{n+k-l}\right] \\
& =\sum_{l=-\infty}^{\infty} h_l \, r_{X X}[k-l]=h_k * r_{X X}[k]
\end{aligned}
$$
The autocorrelation function at the output of a LTI system is
$$
\begin{aligned} r_{Y Y}[l] &= E\left[Y_n Y_{n+l}\right] \\ &= \sum_{k=-\infty}^{\infty} \sum_{i=-\infty}^{\infty} h_k \, h_i \, r_{X X}[l+i-k]=h_l * h_{-l} * r_{X X}[l]\end{aligned}
$$
Illustration of the correlation functions
![[linear-system-correlations.png | center | 500]]
### 2. Power spectrum
Taking DTFT of both sides of the previous equation, the power spectrum at the output of a LTI system is obtained
$$
\mathcal{S}_Y\left(e^{j \omega T}\right)=\left|H\left(e^{j \omega T}\right)\right|^2 \mathcal{S}_X\left(e^{j \omega T}\right)
$$
where $H(e^{j\omega T}) = \sum_{n = -\infty}^{+\infty}h_n e^{-jn\omega T}$ is the frequency response of the system.
### 3. Ergodic random processes
For an Ergodic random process we can estimate expectations by performing time-averaging on a single sample function, e.g.
$$
\begin{aligned}
\mu & =\mathbb{E}\left[X_n\right]=\lim _{N \rightarrow \infty} \frac{1}{N} \sum_{n=0}^{N-1} x_n \quad \text { (Mean ergodic) } \\
r_{X X}[k] & =\lim _{N \rightarrow \infty} \frac{1}{N} \sum_{n=0}^{N-1} x_n x_{n+k} \quad \text { (Correlation ergodic) }
\end{aligned}
$$
A **necessary and sufficient** condition for mean ergodicity is given by:
$$
\lim _{N \rightarrow \infty} \frac{1}{N} \sum_{k=0}^{N-1} c_{X X}[k]=0
$$
where $c_{X X}$ is the autocovariance function:
$$
c_{X X}[k]=\mathbb{E}\left[\left(X_n-\mu\right)\left(X_{n+k}-\mu\right)\right]
$$
and $\mu=\mathbb{E}\left[X_n\right]$.
A simpler **sufficient** condition for mean ergodicity is that $c_{X X}[0]<\infty$ and
$$
\lim _{N \rightarrow \infty} c_{X X}[N]=0
$$
Note: 
- sufficient condition proved $\rightarrow$ mean ergodicity
- sufficient condition not proved $\rightarrow$ prove necessary and sufficient condition
- necessary and sufficient condition proved $\rightarrow$ definitely ergodic

## III. Optimal filtering theory
### 1. Wiener filtering problem
![[wiener-filtering-problem.png | center | 500]]
A desired signal $d_n$ is observed in noise $v_n$: $x_n = d_n + v_n$.
**Goal:** optimally estimate $d_n$ given just the noisy observation $x_n$ and some assumptions about the statistics of the random signal and noise processes.
**Solution:** Wiener filter.
### 2. Discrete-time Wiener filter
![[wiener-filter.png | center | 500]]
In the most general case, we can filter the observed signal $x_n$ with an infinite dimensional filter, having a non-causal impulse response $h_p$ :
$$
\left\{h_p ; \; p=-\infty, \ldots,-1,0,1,2, \ldots, \infty\right\}
$$
Estimate $\hat{d}_n$ of the desired signal obtained by filtering the observed noisy signal using the filter $\left\{h_p\right\}$:
$$
\hat{d}_n=\sum_{p=-\infty}^{\infty} h_p x_{n-p}
$$
The criterion adopted for Wiener filtering is the mean-squared error (MSE) criterion. First, form the error signal $\epsilon_n$ :
$$
\epsilon_n=d_n-\hat{d}_n=d_n-\sum_{p=-\infty}^{\infty} h_p x_{n-p}
$$
The mean-squared error (MSE) is then defined as:
$$
J=\mathbb{E}\left[\epsilon_n^2\right]
$$
where the expectation is with respect to the random signal $d$ and the random noise $v$.
The Wiener filter **minimises $J$ with respect to the filter coefficients $\left\{h_p\right\}$.**
### 3. Derivation of Wiener filter
(included for completeness)
The Wiener filter assumes that $\{x_n\}$ and $\{d_n\}$ are jointly wide-sense stationary $\Rightarrow$ all autocorrelation and cross-correlation functions depend only on the time difference $m-n$ between data points.
In this derivation, $\{d_n\}$ and $\{v_n\}$ are assumed zero mean. i.e. $E[d_n]=0, E[v_n]=0$ (Non-zero mean processes can be dealt with by first subtracting the mean before filtering)

The expected error $J$ may be minimised w.r.t the impulse response values $h_q$. A sufficient condition for minimum is
$$
\frac{\partial J}{\partial h_q}=\frac{\partial \mathbb{E}\left[\epsilon_n^2\right]}{\partial h_q}=\mathbb{E}\left[\frac{\partial \epsilon_n^2}{\partial h_q}\right]=\mathbb{E}\left[2 \epsilon_n \frac{\partial \epsilon_n}{\partial h_q}\right]=0
$$
simultaneously for all $q \in\{-\infty, \ldots,-1,0,1,2, \ldots \infty\}$.
The term $\frac{\partial \epsilon_n}{\partial h_q}$ is then calculated as:
$$
\frac{\partial \epsilon_n}{\partial h_q}=\frac{\partial}{\partial h_q}\left\{d_n-\sum_{p=-\infty}^{\infty} h_p x_{n-p}\right\}=-x_{n-q}
$$
(since random terms $d_n$ and $x_{n-p}$ do not depend on $h_q$ and are hence treated as constant in the partial derivative)

Hence the coefficients must satisfy, for all $q$:
$$
\mathbb{E}\left[\epsilon_n \frac{\partial \epsilon_n}{\partial h_q}\right]=-\mathbb{E}\left[\epsilon_n x_{n-q}\right]=0
$$
i.e.
$$
\mathbb{E}\left[\epsilon_n x_{n-q}\right]=0 ; \quad-\infty<q<+\infty
$$
This is known as the **orthogonality principle**.

Substituting for $\epsilon_n$ gives
$$\begin{aligned} \mathbb{E}\left[\epsilon_n x_{n-q}\right] & =\mathbb{E}\left[\left(d_n-\sum_{p=-\infty}^{\infty} h_p x_{n-p}\right) x_{n-q}\right] \\ &= \mathbb{E}\left[d_n x_{n-q}\right]-\sum_{p=-\infty}^{\infty} h_p \mathbb{E}\left[x_{n-q} x_{n-p}\right] \\ &= r_{x d}[q]-\sum_{p=-\infty}^{\infty} h_p r_{x x}[q-p] \\ &= 0\end{aligned}$$
Hence the solution must satisfy
$$
\boxed{\sum_{p=-\infty}^{\infty} h_p r_{x x}[q-p]=r_{x d}[q], \quad-\infty<q<+\infty}
$$
This is known as the **Wiener-Hopf** equations.
Rewrite the Wiener-Hopf equation as convolution
$$
h_q * r_{x x}[q]=r_{x d}[q], \quad-\infty<q<+\infty
$$
Taking discrete-time Fouxier transorms (DTFT) of both sides:
$$
H\left(e^{j \Omega}\right) \mathcal{S}_x\left(e^{j \Omega}\right)=\mathcal{S}_{x d}\left(e^{j \Omega}\right)
$$
Here the term $\mathcal{S}_{x d}\left(e^{j \Omega}\right)$, is defined as the the DTFT of $r_{x d}[q]$ and is termed the **cross-power spectrum** of $d$ and $x$. It measures the **coherence** between two processes at a particular frequency.
The cross power spectrum has the property
$$
\mathcal{S}_{x d}\left(e^{j \Omega}\right)=\mathcal{S}_{d x}\left(e^{j \Omega}\right)^*
$$
Hence, rearranging:
$$
\boxed{H\left(e^{j \Omega}\right)=\frac{\mathcal{S}_{x d}\left(e^{j \Omega}\right)}{\mathcal{S}_x\left(e^{j \Omega}\right)}}
$$
### 4. Mean-squared value for the optimal filter
Performance of the optimal filter can be assessed form the mean-squared error value of the filter
$$
\begin{aligned} J=\mathbb{E}\left[\epsilon_n^2\right]&=\mathbb{E}\left[\epsilon_n\left(d_n-\sum_{p=-\infty}^{\infty} h_p x_{n-p}\right)\right] \\ &=\mathbb{E}\left[\epsilon_n d_n\right]-\sum_{p=-\infty}^{\infty} h_p \mathbb{E}\left[\epsilon_n x_{n-p}\right]\end{aligned}
$$
For optimal filter, the last term is zero, hence the minimum error is
$$
\begin{aligned} J_{\min } & =\mathbb{E}\left[\epsilon_n d_n\right] \\ & =\mathbb{E}\left[\left(d_n-\sum_{p=-\infty}^{\infty} h_p x_{n-p}\right) d_n\right] \\ & =r_{d d}[0]-\sum_{p=-\infty}^{\infty} h_p r_{x d}[p]\end{aligned}
$$
The minimum error can also be assessed in the frequency domain
$$
J_{\min }=\frac{1}{2 \pi} \int_{-\pi}^{+\pi} \mathcal{S}_d\left(e^{j \Omega}\right)-H\left(e^{j \Omega}\right) \mathcal{S}_{x d}^*\left(e^{j \Omega}\right) d \Omega
$$
### 5. Important special case: uncorrelated signal and noise processes
A very typical scenario is that the desired signal processes $\{d_n\}$ is uncorrelated with the noise process $\{v_n\}$, e.g. $v$ might be environmental noise that is independent of the desired signal. 
i.e.
$$
r_{d v}[k]=\mathbb{E}\left[d_n v_{n+k}\right]=0, \quad-\infty<k<+\infty
$$
Recall the Wiener-Hopf equations
$$
\sum_{p=-\infty}^{\infty} h_p r_{x x}[q-p]=r_{x d}[q], \quad-\infty<q<+\infty
$$
Under this special case,
$$
\begin{aligned}
r_{x d}[q]&=\mathbb{E}\left[x_n d_{n+q}\right]=\mathbb{E}\left[\left(d_n+v_n\right) d_{n+q}\right] \\
&=\mathbb{E}\left[d_n d_{n+q}\right]+\mathbb{E}\left[v_n d_{n+q}\right]=r_{d d}[q]
\end{aligned}
$$
since $\left\{d_n\right\}$ and $\left\{v_n\right\}$ are uncorrelated.
Taking DTFT
$$
\mathcal{S}_{x d}\left(e^{j \Omega}\right)=\mathcal{S}_d\left(e^{j \Omega}\right)
$$
For $r_{XX}$
$$
\begin{aligned} r_{x x}[q] & =\mathbb{E}\left[x_n x_{n+q}\right]=\mathbb{E}\left[\left(d_n+v_n\right)\left(d_{n+q}+v_{n+q}\right)\right] \\ & =\mathbb{E}\left[d_n d_{n+q}\right]+\mathbb{E}\left[v_n v_{n+q}\right]+\mathbb{E}\left[d_n y_{n+q}\right]+\mathbb{E}\left[v_n d_{n+q}\right] \\ & =\mathbb{E}\left[d_n d_{n+q}\right]+\mathbb{E}\left[v_n v_{n+q}\right]=r_{d d}[q]+r_{v v}[q]\end{aligned}
$$
Taking DTFT
$$
\mathcal{S}_x\left(e^{j \Omega}\right)=\mathcal{S}_d\left(e^{j \Omega}\right) + \mathcal{S}_v\left(e^{j \Omega}\right)
$$
Thus the Wiener filter becomes
$$
H\left(e^{j \Omega}\right)=\frac{\mathcal{S}_{x d}\left(e^{j \Omega}\right)}{\mathcal{S}_x\left(e^{j \Omega}\right) } = \frac{\mathcal{S}_d\left(e^{j \Omega}\right)}{\mathcal{S}_d\left(e^{j \Omega}\right) + \mathcal{S}_v\left(e^{j \Omega}\right)} = \frac{1}{1 + \frac{1}{\rho(\Omega)}} \in (0,1)
$$
where $\rho(\Omega) = \mathcal{S}_d\left(e^{j \Omega}\right)/ \mathcal{S}_v\left(e^{j \Omega}\right)$ is the frequency dependent signal-to-noise (SNR) power ratio.

**Interpretations:**
- the gain is always non-negative and ranges between 0 and 1 $\rightarrow$ the filter will never boost a particular frequency component, but rather acts as an optimal attenuation rule
- at frequencies with large SNR, the gain of the filter tends to unity
- at frequencies with small SNR, the gain of the filter tends to a small value
- when the signal is very noisy, the best estimate the filter can make (w.r.t MSE) is zero
- **the filter can be think of as the gain of a voltage divider with load resistance $\mathcal{S}_d\left(e^{j \Omega}\right)$ and source resistance $\mathcal{S}_v\left(e^{j \Omega}\right)$.**

The minimum expected error in this case is
$$
\begin{aligned} J_{\min } & =\frac{1}{2 \pi} \int_{-\pi}^{+\pi} \mathcal{S}_d\left(e^{j \Omega}\right)\left(1-\frac{\mathcal{S}_d\left(e^{j \Omega}\right)}{\mathcal{S}_d\left(e^{j \Omega}\right)+\mathcal{S}_v\left(e^{j \Omega}\right)}\right) d \Omega \\ & =\frac{1}{2 \pi} \int_{-\pi}^{+\pi} \mathcal{S}_d\left(e^{j \Omega}\right)\left(1-\frac{1}{1+1 / \rho(\Omega)}\right) d \Omega \\ & =\frac{1}{2 \pi} \int_{-\pi}^{+\pi} \mathcal{S}_d\left(e^{j \Omega}\right)\left(\frac{1}{1+\rho(\Omega)}\right) d \Omega\end{aligned}
$$
### 6. The FIR Wiener filter
With a Pth order finite impulse response (FIR) Wiener filter, the signal estimate is formed as
$$
\hat{d_n} = \sum_{p=0}^{P}h_p x_{n-p}
$$
As before, we need to solve for
$$
\frac{\partial \epsilon_n}{\partial h_q}=\frac{\partial}{\partial h_q}\left\{d_n-\sum_{p=0}^{P} h_p x_{n-p}\right\}=-x_{n-q}
$$
leading to an orthogonality principle:
$$
\mathbb{E}\left[\epsilon_n x_{n-q}\right]=0 ; \quad q=0, \ldots, P-1
$$
and Wiener-Hopf equations
$$
\sum_{p=0}^P h_p r_{x x}[q-p]=r_{x d}[q], \quad q=0,1, \ldots, P
$$
The equations can be written in matrix form as
$$
\mathbf{R}_x \mathbf{h}=\mathbf{r}_{x d}
$$
where
$$
\mathbf{h}=\left[\begin{array}{c}h_0 \\ h_1 \\ \vdots \\ h_P\end{array}\right] \quad \mathbf{r}_{x d}=\left[\begin{array}{c}r_{x d}[0] \\ r_{x d}[1] \\ \vdots \\ r_{x d}[P]\end{array}\right]
$$
and
$$
\mathbf{R}_x=\left[\begin{array}{cccc}r_{x x}[0] & r_{x x}[1] & \cdots & r_{x x}[P] \\ r_{x x}[1] & r_{x x}[0] & \cdots & r_{x x}[P-1] \\ \vdots & \vdots & & \vdots \\ r_{x x}[P] & r_{x x}[P-1] & \cdots & r_{x x}[0]\end{array}\right]
$$
$\mathbf{R}_x$ is known as the **correlation matrix**.
Note that $r_{xx}[k] = r_{xx}[-k]$ so that the correlation matrix $\mathbf{R}_x$ is symmetric and has constant diagonals.
The coefficient vector can be found be matrix inversion:
$$
\mathbf{h}=\mathbf{R}_x^{-1} \mathbf{r}_{xd}
$$
In summary, it requires a-priori knowledge of the autocorrelation matrix $\mathbf{R}_x$ of the input process $\{x_n\}$ and the cross-correlation $\mathbf{r}_d$ between the input $\{x_n\}$ and the desired signal process $\{d_n\}$.
The minimum MSE error is given by
$$
\begin{aligned}
J_{\min }&=\mathbb{E}\left[\epsilon_n d_n\right] \\
& =\mathbb{E}\left[\left(d_n-\sum_{p=0}^P h_p x_{n-p}\right) d_n\right] \\
& =r_{d d}[0]-\sum_{p=0}^P h_p r_{x d}[p] \\
& =r_{d d}[0]-\mathbf{r}_{x d}^T \mathbf{h}=r_{d d}[0]-\mathbf{r}_{x d}^T{\mathbf{R}_x{ }^{-1} \mathbf{r}_{x d}}
\end{aligned}
$$
### 7. Extending the Wiener filter
The formula for the FIR case
$$
\mathbf{h}=\mathbf{R}_x^{-1} \mathbf{r}_{xd}
$$
applies to whatever the form of the desired signal and the 'noisy' signal, provided the necessary correlation functions can be calculated.
Standard examples that could come up in the exam:
- Prediction of a noisy signal $\{u_n\}$, the desired signal is the predicted value of the signal $d_n = u_{n+p}$, where $p$ is the desired prediction interval.
- Smoothing of a noisy signal — use the current samples to get an better estimate of the signal at some point in the past: $d_n = u_{n-p}$, where $p$ is the amount of 'lookahead' allowed.
- Deconvolution: extract a signal $u_n$ from a noisy convolved version of itself:
$$
x_n=\sum_{q=0}^Q h_q u_{n-q}+v_n
$$
## IV. Optimal detection
**Goal:** detecting a deterministic signal $s_n, n = 0, \ldots, N - 1$ buried in a random noise $v_n$ (so that $x_n = s_n + v_n$).
**Solution:** matched filter.
### Matched filter
To formulate the problem, first 'vectorise' the equation
$$
\begin{gathered}
\mathbf{x}=\mathbf{s}+\mathbf{v} \\
\mathbf{s}=\left[s_0, s_1, \ldots, s_{N-1}\right]^T, \mathbf{x}=\left[x_0, x_1, \ldots, x_{N-1}\right]^T
\end{gathered}
$$
The goal is to design an optimal FIR filter for performing the detection task. Suppose the filter has coefficients $h_m$, for $m=0,1, \ldots, N-1$, then the output of the filter at time $N-1$ is:
$$
\begin{aligned}
y_{N-1} & =\sum_{m=0}^{N-1} h_m x_{N-1-m}=\mathbf{h}^T \tilde{\mathbf{x}}=\mathbf{h}^T(\tilde{\mathbf{s}}+\tilde{\mathbf{v}})=\mathbf{h}^T \tilde{\mathbf{s}}+\mathbf{h}^T \tilde{\mathbf{v}} \\
& =y_{N-1}^s+y_{N-1}^n
\end{aligned}
$$
where $\tilde{\mathbf{x}}=\left[x_{N-1}, x_{N-2}, \ldots, x_0\right]^T$ is the **'time-reversed'** vector, and $\tilde{\mathbf{s}}$ defined similarly. 
$y_{N-1}^s$ is defined as the output from the signal-only part and $y_{N-1}^n$ is the output from just the noise going through the filter.

Instead of minimising the mean-squared error, we aim to **maximise the signal-to-noise ratio (SNR)** at the output of the filter.
The output SNR is defined as
$$
\frac{\mathbb{E}\left[\left|y_{N-1}^s\right|^2\right]}{\mathbb{E}\left[\left|y_{N-1}^n\right|^2\right]}=\frac{\mathbb{E}\left[\left|\mathbf{h}^T \tilde{\mathbf{s}}\right|^2\right]}{\mathbb{E}\left[\left|\mathbf{h}^T \tilde{\mathbf{v}}\right|^2\right]}=\frac{\left|\mathbf{h}^T \tilde{\mathbf{s}}\right|^2}{\mathbb{E}\left[\left|\mathbf{h}^T \tilde{\mathbf{v}}\right|^2\right]}
$$
(since numerator is not a random quantity).
#### Signal output energy
The signal component at the output is $y_{N-1}^s=\mathbf{h}^T \tilde{\mathbf{s}}$, with energy
$$
\left|\mathbf{h}^T \tilde{\mathbf{s}}\right|^2=\left(\mathbf{h}^T \tilde{\mathbf{s}}\right)\left(\tilde{\mathbf{s}}^T \mathbf{h}\right)=\mathbf{h}^T\left(\tilde{\mathbf{s}} \tilde{\mathbf{s}}^T\right) \mathbf{h}
$$
To analyse this, consider the matrix $\mathbf{M}=\tilde{\mathbf{s}} \tilde{\mathbf{s}}^T$.
Recall the definition of eigenvectors (e) and eigenvalues $(\lambda)$
$$
\mathbf{M e}=\lambda \mathbf{e}
$$
Try $\mathbf{e}=\tilde{\mathbf{s}}:$
$$
\mathbf{M} \tilde{\mathbf{s}}=\left(\tilde{\mathbf{s}} \tilde{\mathbf{s}}^T\right) \tilde{\mathbf{s}}=\tilde{\mathbf{s}}\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right)=\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right) \tilde{\mathbf{s}}
$$
**Hence the unit length vector $\mathbf{e}_0=\tilde{\mathbf{s}} /|\tilde{\mathbf{s}}|$ is an eigenvector and $\lambda=\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right)$ is the corresponding eigenvalue.**
Consider any vector $\mathbf{e}^{\prime}$ which is orthogonal to $\mathbf{e}_0$ (i.e. $\tilde{\mathbf{s}}^T \mathbf{e}^{\prime}=0$ ):
$$
\mathbf{M} \mathbf{e}^{\prime}=\tilde{\mathbf{s}} \tilde{\mathbf{s}}^T \mathbf{e}^{\prime}=0
$$
$\Rightarrow$ any such $\mathbf{e}^{\prime}$ is also an eigenvector, but with eigenvalue $\lambda^{\prime}=0$. 
Since we can construct a set of $N-1$ orthonormal (unit length and orthogonal to each other) vectors which are orthogonal to $\tilde{\mathbf{s}}$, call these $\mathbf{e}_1, \mathbf{e}_2, \ldots, \mathbf{e}_{N-1}$, we have now discovered all $N$ eigenvectors/eigenvalues of $\mathbf{M}$.
Since the $N$ eigenvectors form an orthonormal basis, we may represent any filter coefficient vector $\mathbf{h}$ as a linear combination of these:
$$
\mathbf{h}=\alpha \mathbf{e}_0+\beta \mathbf{e}_1+\gamma \mathbf{e}_2+\ldots+\ldots \mathbf{e}_{N-1}
$$
Thus we can express 
$$ 
\begin{aligned} \mathbf{M h} & =\mathbf{M}\left(\alpha \mathbf{e}_0+\beta \mathbf{e}_1+\gamma \mathbf{e}_2+\ldots+\ldots \mathbf{e}_{N-1}\right) \\ & =\alpha \mathbf{M} \mathbf{e}_0+\beta \mathbf{M} \mathbf{e}_1+\gamma \mathbf{M} \mathbf{e}_2+\ldots+\ldots \mathbf{M} \mathbf{e}_{N-1} \\ & =\alpha\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right) \mathbf{e}_0+0+0+\ldots 0 \\ &=\alpha\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right) \mathbf{e}_0 \end{aligned}
$$
since all but the first eigenvalue is zero. 
Now, consider the signal output energy again: 
$$
\begin{aligned} \mathbf{h}^T \tilde{\mathbf{s}} \tilde{\mathbf{s}}^T \mathbf{h} & =\mathbf{h}^T \mathbf{M h} \\ & =\mathbf{h}^T \alpha\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right) \mathbf{e}_0 \\ & =\alpha\left(\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right) \mathbf{h}^T \mathbf{e}_0 \\ & =\left(\alpha \tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\right)\left(\alpha \mathbf{e}_0+\beta \mathbf{e}_1+\gamma \mathbf{e}_2+\ldots+\ldots \mathbf{e}_{N-1}\right)^T \mathbf{e}_0 \\ & =\alpha^2 \tilde{\mathbf{s}}^T \tilde{\mathbf{s}}\end{aligned}
$$
since the eigenvectors are orthonormal.
#### Noise output energy
Now, consider the expected noise output energy, which may be simplified as follows: 
$$ 
\mathbb{E}\left[\left|\mathbf{h}^T \tilde{\mathbf{v}}\right|^2\right]=\mathbb{E}\left[\mathbf{h}^T \tilde{\mathbf{v}} \tilde{\mathbf{v}}^T \mathbf{h}\right]=\mathbf{h}^T \mathbb{E}\left[\tilde{\mathbf{v}} \tilde{\mathbf{v}}^T\right] \mathbf{h} 
$$
Consider the case where the noise is white and zero mean with variance $\sigma_v^2$. Then, for any time indexes $i=0, \ldots, N-1$ and $j=0, \ldots, N-1$ : 
$$ 
\mathbb{E}\left[v_i v_j\right]= \begin{cases}\sigma_v^2, & i=j \\ 0, & i \neq j\end{cases} 
$$
and hence 
$$
\mathbb{E}\left[\tilde{\mathbf{v}} \tilde{\mathbf{v}}^T\right]=\sigma_v^2 \mathbf{I}
$$
where $\mathbf{I}$ is the $N \times N$ identity matrix (diagonal elements correspond to $i=j$ terms and off-diagonal to $i \neq j$ terms).
Hence, the expression for the noise output energy is:
$$
\mathbb{E}\left[\left|\mathbf{h}^T \tilde{\mathbf{v}}\right|^2\right]=\mathbf{h}^T \sigma_v^2 \mathbf{l} \mathbf{h}=\sigma_v^2 \mathbf{h}^T \mathbf{h}
$$
and once again expand $\mathbf{h}$ in terms of the eigenvectors of $\mathbf{M}$ :
$$
\sigma_v^2 \mathbf{h}^T \mathbf{h}=\sigma_v^2\left(\alpha^2+\beta^2+\gamma^2+\ldots\right)
$$
again, since $\mathbf{e}_i^T \mathbf{e}_j=\delta[i-j]$ (orthonormal eigenvectors).
#### SNR maximisation
The SNR may now be expressed as:
$$
\frac{\left|\mathbf{h}^T \tilde{\mathbf{s}}\right|^2}{\mathbb{E}\left[\left|\mathbf{h}^T \tilde{\mathbf{v}}\right|^2\right]}=\frac{\alpha^2 \tilde{\mathbf{s}}^T \tilde{\mathbf{s}}}{\sigma_v^2\left(\alpha^2+\beta^2+\gamma^2+\ldots\right)}
$$
Clearly, scaling $\mathbf{h}$ by some factor $\rho$ will not change the SNR since numerator and denominator will both then scale equally by $\rho^2$ $\Rightarrow$ fix $|\mathbf{h}|=1$ and then maximise.
With $|\mathbf{h}|=1$ we have $\left(\alpha^2+\beta^2+\gamma^2+\ldots\right)=1$ and the SNR becomes just equal to $\alpha^2 \tilde{\mathbf{s}}^T \tilde{\mathbf{s}} /\sigma_v^2$.
The largest possible value of $\alpha$ given that $|\mathbf{h}|=1$ corresponds to $\alpha=1$, which implies then that $\beta=\gamma=\ldots=0$, and finally we have the solution as: 
$$ 
\mathbf{h}^{\mathrm{opt}}=1 \times \mathbf{e}_0=\frac{\tilde{\mathbf{s}}}{|\tilde{\mathbf{s}}|}, \text { since } \mathbf{e}_0=\frac{\tilde{\mathbf{s}}}{|\tilde{\mathbf{s}}|} 
$$
**i.e. the optimal filter coefficients are just the (normalised) time-reversed signal**
The SNR at the optimal filter setting is given by
$$
\mathrm{SNR}^{\mathrm{opt}}=\frac{\tilde{\mathbf{s}}^T \tilde{\mathbf{s}}}{\sigma_v^2}
$$
Clearly, the performance depends (as expected) very much on the energy of the signal $s$ and the noise $v$.
**Note:** We have only proved that the SNR is maximised at one single filter output time $n = N -1$. In fact, the signal output power term for the optimal filter is always less than that computed for $n = N - 1$ since the deterministic correlations function of $s_n$ always has its maximum at lag zero (correlation function is important here since the matched filter is the time-reversed $\textbf{s}$).

Backlinks:
[[Probability]]
[[Digital Filtering]]