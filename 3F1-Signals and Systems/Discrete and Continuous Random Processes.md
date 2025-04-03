## Overview
![[random-process-overview.png | center | 500]]
## I. Introduction to random processes
### 1. Definition of a random process
- A random process is a random signal (discrete or continuous) for which the joint density of any collection of any $n$ signal values $\left(X_{t_1}, X_{t_2}, \ldots, X_{t_n}\right)$ is known and well defined.
- Expectations $E\left[f\left(X_{t_1}, X_{t_2}, \ldots, X_{t_n}\right)\right]$ and other derived probabilistic quantities (e.g. entropy) are also well defined
### 2. Linear system and random processes
- For **deterministic** processes, a linear system is a linear Ordinary Differential Equation (ODE) or linear Ordinary Differential Equation (in discrete time) with constant coefficients
- For **random** processes, a linear system is a linear Stochastic Differential Equation (SDE) or linear Stochastic Differential Equation (in discrete time) with constant coefficients
### 3. Responses and transfer functions with random processes
- For random processes, the signals are "unknown": we can not simply take their Laplace/Fourier/$z$ transform/DTFT
- Since there is no known transform for the random processes, we can not apply the transfer functions on transforms
- However, we can take expectations of a transform
### 4. Expectations of a transform
For a zero-mean input $E\left[X_k\right]=0$, using a "sloppy" limit,
$$
\begin{aligned}
E[\operatorname{DTFT}(X)] &= E\left[\lim _{N \rightarrow \infty} \sum_{k=-N / 2}^{N / 2} X_k e^{-j \theta k}\right] \\ & =\lim _{N \rightarrow \infty} E\left[\sum_{k=-N / 2}^{N / 2} X_k e^{-j \theta k}\right] \\
& =\lim _{N \rightarrow \infty} \sum_{k=-N / 2}^{N / 2} E\left[X_k\right] e^{-j \theta k}=0
\end{aligned}
$$
$\longrightarrow$ the expected DTFT of the input and output in the linear difference equation is zero.

### 5. Properties of a random process
#### Stationarity
For any $n$ and any collection $\left(t_1, t_2, \ldots, t_n\right)$ of $n$ signal locations, and for any shift $\tau$ and for any values $\left(x_1, x_2, \ldots, x_n\right)$, the signal is stationary if:
$$
 f_{X_{t_1+\tau}, X_{t_2+\tau}, \ldots, X_{t_n+\tau}}\left(x_1, x_2, \ldots, x_n\right)=f_{X_{t_1}, x_{t_2}, \ldots, X_{t_n}}\left(x_1, x_2, \ldots, x_n\right)
$$
- the signal statistics are **shift-invariant**
- the signal statistics only depend on the relative positions of the signal locations, not on its absolute locations
#### Wide-sense stationarity
A random process is wide-sense stationary if
1. the mean $E\left[X_t\right]$ is independent of time
2. the autocorrelation depends only on the relative interval
$$
r_{X X}\left(t_1, t_2\right)=E\left[X_{t_1} X_{t_2}\right]=E\left[X_0 X_{t_2-t_1}\right]=r_{X X}\left(t_2-t_1\right)
$$
Motivation:
"Only verify that the mean and the autocorrelation behave as they would if the process were stationary, unsure about the stationarity."
#### Ergodicity
A stationary random process is ergodic if its statistics observed over time converge to its true probabilities ("ensemble statistics").
In particular, a stationary process is "mean ergodic" if
$$
E[X]=\lim _{N \rightarrow \infty} \frac{1}{N} \sum_{k=0}^{N-1} X_k
$$
and "autocorrelation ergodic" if
$$
r_{X X}(k)=E\left[X_0 X_k\right]=\lim _{N \rightarrow \infty} \frac{1}{N} \sum_{k=0}^{N-1} X_0 X_k
$$
Mean ergodic and autocorrelation ergodic are to ergodic as wide sense stationary to stationary: "Only verify ergodicity for the mean and autocorrelation behaviour"
### 6. Discrete-time white noise
The term "white noise" has been universally adopted to describe an independent and identically distributed (i.i.d.) discrete-time random process $\left\{\ldots, X_{-1}, X_0, X_1, X_2, \ldots\right\}$ with
$$
f_{X_{k_1}, x_{k_2}, \ldots, x_{k_n}}\left(x_1, \ldots, x_n\right)=f_X\left(x_1\right) \cdot f_X\left(x_2\right) \cdots f_X\left(x_n\right)
$$
for any $n$, any $\left(k_1, \ldots, k_n\right)$ and any $\left(x_1, \ldots, x_n\right)$. 
- **White noise is stationary and ergodic**
- can be regarded as a synonym for "i.i.d."

## II. The PSD for discrete-time signals
### Setup
Consider the following scenario the system convolves its delta response with the input signal $$ \left\{Y_k\right\}=\left\{h_k\right\} \star\left\{X_k\right\} $$The input is i.i.d. (white noise) with $E\left[X_k\right]=0$ and $E\left[X_k^2\right]=1$
### Derivation
To avoid taking "sloppy" limits, consider a signal $X_k$ consisting of i.i.d. random variables from time $\lfloor-N / 2+1\rfloor$ to time $\lfloor N / 2\rfloor$, and zero elsewhere its DTFT is
$$
X(\theta)=\sum_{k=-\lfloor N / 2+1\rfloor}^{\lfloor N / 2\rfloor} x_k e^{-j k \theta}
$$
Compute the **expected squared DTFT magnitude**:
$$\begin{aligned} \frac{1}{N} E\left[|X(\theta)|^2\right] & =\frac{1}{N} E\left[X(\theta) X^*(\theta)\right] \\ & =\frac{1}{N} E\left[\left(\sum_{k=-\lfloor N / 2+1\rfloor}^{\lfloor N / 2\rfloor} X_k e^{-j k \theta}\right)\left(\sum_{k=-\lfloor N / 2+1\rfloor}^{\lfloor N / 2\rfloor} X_k e^{j k \theta}\right)\right] \\ & =\frac{1}{N} \sum_{k=-\lfloor N / 2+1\rfloor}^{\lfloor N / 2\rfloor}\left(E\left[X_k^2\right]+\sum_{m \neq k} E\left[X_k X_m\right] e^{j(m-k) \theta}\right) \\ & =1 \text { for all } \theta\end{aligned}$$
where $E[X_kX_m] = E[X_k]E[X_m] = 0$.
### Power spectral density of white noise
The power spectral density (PSD) of white noise
$$
S_{X X}(\theta)=\lim _{N \rightarrow \infty} \frac{1}{N}|X(\theta)|^2=1
$$
is **constant for all** $\theta$. 
In other words, all frequencies are present in equal measure in an i.i.d. signal
$\rightarrow$ "white" in analogy with white light that can be obtained by mixing all colours.

### PSD through a linear system
$$\begin{aligned} S_{Y Y}(\theta) & =\lim _{N \rightarrow \infty} \frac{1}{N} E\left[|Y(\theta)|^2\right] \\ & =\lim _{N \rightarrow \infty} \frac{1}{N} E\left[|H(\theta) X(\theta)|^2\right] \\ & =|H(\theta)|^2 S_{X X}(\theta) \end{aligned}$$
For any discrete stationary process.
### Power spectral density vs autocorrelation
$$\begin{aligned} \frac{1}{N} E\left[|X(\theta)|^2\right] & =\frac{1}{N} E\left[X(\theta) X^*(\theta)\right] \\ & =\frac{1}{N} E\left[\left(\sum_k X_k e^{-j k \theta}\right)\left(\sum_k X_k e^{j k \theta}\right)\right] \\ & =\frac{1}{N} \sum_k \sum_m E\left[X_k X_m\right] e^{-j k \theta} e^{j m \theta} \\ & =\frac{1}{N} \sum_k \sum_n E\left[X_k X_{k-n}\right] e^{-j k \theta} e^{j(k-n) \theta} \quad(m=k-n) \\ & =\frac{1}{N} \sum_k \sum_n r_{X X}(n) e^{-j n \theta}=\sum_n r_{X X}(n) e^{-j n \theta}\end{aligned}$$
- Hence, the power spectral density (PSD) is the DTFT of the autocorrelation function (ACF)
- The PSD is real by definition and the ACF is symmetric $r_{xx}(n)=r_{xx}(-n)$
The relation that in the frequency domain when filtering white noise through a linear system
$$
\Phi_{Y Y}(\theta)=|H(\theta)|^2
$$
becomes in the time domain
$$
r_{Y Y}(n)=\left\{h_k\right\} *\left\{h_{-k}\right\}
$$
### Cross-correlation and cross-spectral-density
Cross-correlation between input and output
$$
r_{X Y}(n)=E\left[X_k Y_{k+n}\right]
$$
with its DTFT being the cross-spectral density $\Phi_{X Y}(\theta)$ for which
$$
S_{X Y}(\theta)=H(\theta) S_{X X}(\theta)
$$

## III. The PSD for continuous time signals
### Continuous-time white noise
- In the real world, white noise can only be observed through a linear filter
- Any measurement device is a linear filter
- A continuous time device is **unobservable**
### Modelling the white noise
- Think of continuous-time white noise as a limit of weighted pulses
- Construct a signal starting at $-T / 2$ and ending at $T / 2$, consisting of pulses modulated with independent Gaussian random variables $X_k \sim \mathcal{N}(0,1 / b)$ of variance $1 / b$
$$
X(t)=\sum_{k=\frac{-T}{2 b}}^{\frac{T}{2 b}-1} x_k p(t-k b)
$$
![[continuous-time-white-noise.png | center | 400]]

### Analysis
The Fourier transform of a unit step $u(t)$ is $\pi \delta(\omega)+\frac{1}{j \omega}$ (from Info data book)
Since $p(t)=u(t)-u(t-b)$, the Fourier transform of the rectangular pulse (using shift property of Fourier transform) is
$$
P(\omega)=\left(\pi \delta(\omega)+\frac{1}{j \omega}\right)\left(1-e^{-j b \omega}\right)
$$
Hence the Fourier transform of the input signal is 
$$
X(\omega)=\sum_{k=\frac{-T}{2 b}}^{\frac{T}{2 b}-1} X_k\left(\pi \delta(\omega)+\frac{1}{j \omega}\right)\left(1-e^{-j b \omega}\right) e^{-j k b \omega}
$$
For $\omega \neq 0$, ignore the pulse function in the expression to obtain
$$
X(\omega)=\sum_{k=\frac{-T}{2 b}}^{\frac{T}{2 b}-1} x_k \frac{1-e^{-j b \omega}}{j \omega} e^{-j k b \omega}
$$
by analogy with the discrete case where we found that $\mathcal{S}_{X X}(\theta)=\lim _{N \rightarrow \infty} \frac{1}{N} E\left[|X(\theta)|^2\right]$,
$$
\begin{aligned}
& \frac{1}{T} E\left[|X(\omega)|^2\right]=\frac{1}{T} E\left[X(\omega) X^*(\omega)\right] \\
& =\frac{1}{T} E\left[\left(\sum_{k=\frac{-T}{2 b}}^{\frac{T}{2 b}-1} X_k \frac{1-e^{-j b \omega}}{j \omega} e^{-j k b \omega}\right)\left(\sum_{\ell=\frac{-T}{2 b}}^{\frac{T}{2 b}-1} X_{\ell} \frac{1-e^{j b \omega}}{-j \omega} e^{j \ell b \omega}\right)\right] \\
& =\frac{1}{T} \sum_{k=\frac{-T}{2 b}}^{\frac{T}{2 b}-1} E\left[X_k^2\right] \frac{2-2 \cos (b \omega)}{\omega^2} \text { since } E\left[X_k X_{\ell}\right]=0 \text { for } k \neq \ell
\end{aligned}
$$
the expression does no depend on $k$ and recall that $E\left[X_k^2\right]=1 / b$ hence we have
$$
\frac{1}{T} E\left[X(\omega) X^*(\omega)\right]=\frac{1}{T} \frac{T}{b} \frac{1}{b} \frac{2-2 \cos (b \omega)}{\omega^2}=\frac{1}{b^2} \frac{2-2 \cos (b \omega)}{\omega^2}
$$
we now take the limit as $b \rightarrow 0$ to obtain
$$
\lim _{b \rightarrow 0} \frac{2-2 \cos (b \omega)}{b^2 \omega^2}=\lim _{b \rightarrow 0} \frac{2-2\left(1-\frac{b^2 \omega^2}{2}+O\left(b^4\right)\right)}{b^2 \omega^2}=1
$$
we have shown that, for $\omega \neq 0$,
$$
\mathcal{S}_{X X}(\omega)=\lim _{b \rightarrow 0} \frac{1}{T} E\left[|X(\omega)|^2\right]=1
$$
which is the same result we obtained in discrete time
### PSD through a linear system
$$\begin{aligned} \mathcal{S}_{Y Y}(\omega) & =\lim _{b \rightarrow 0} \frac{1}{T} E\left[|Y(\omega)|^2\right] \\ & =\lim _{b \rightarrow 0} \frac{1}{T} E\left[|H(\omega) X(\omega)|^2\right] \\ & =|H(\omega)|^2 \mathcal{S}_{X X}(\omega)\end{aligned}$$
### Extra points
- for any continuous stationary ergodic random process $X(t)$, the $\operatorname{PSD} \mathcal{S}_{X X}(\omega)$ is the Fourier transform of the auto-correlation function
$$
r_{X X}(\tau)=E[X(t) X(t+\tau)]
$$
- all the other properties regarding CSD $S_{XY}(\omega)$ are the same as for discrete time
