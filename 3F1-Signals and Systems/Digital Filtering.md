## I. Continuous to discrete mappings and interfaces
### 1. Algebraic transformations
#### Linear approximation
Recall that the mapping between $s$ and $z$ planes is
$$
z \longrightarrow e^{s T}
$$

For small $T$, can approximate this as
$$
e^{s T}=1+s T+\frac{(s T)^2}{2}+o\left(T^3\right)
$$
a linear approximation yields $z=1+s T$ or
$$
s=\frac{z-1}{T}
$$

We can replace every occurrence of $s$ in a continuous time system by $(z-1) / T$, e.g.,
$$
\frac{s-1}{s+1} \longrightarrow \frac{z-1-T}{z-1+T}
$$
#### Quadratic approximation
Replacing every $s$ by a quadratic expression in $z$ would lead to an explosion in the number of poles / zeros. Simple designs in the $s$ domain would lead to higher order designs in the $z$ domain.

#### Common algebraic transformations
Cost of algebraic transformation: some **distortion** between the frequency response of the continuous-time system and the frequency response of the digital system.
$$H(z)=H_c(s)_{s=\psi(z)} \text{ where } \psi(\cdot) \text{ is given by
}
$$
- Euler's method or Forward difference $$
s=\frac{z-1}{T} \quad \text { (intuition: linear approximation) }
$$
- Backward difference $$
s=\frac{1-z^{-1}}{T} \quad (\text{intuition: } \dot{x} \simeq \frac{x(t)-x(t-T)}{T})
$$
- Bilinear (Tustin's) transformation $$
s=\frac{2}{T} \frac{z-1}{z+1} \quad \text { (or simply } \frac{z-1}{z+1} \text { ) }
$$
- Motivation of Tustin transformation:
	We can invert the expression $s=\frac{2}{T} \frac{z-1}{z+1}, s(z+1)=\frac{2}{T}(z-1)$, and hence $$
z=\frac{1+\frac{s T}{2}}{1-\frac{s T}{2}} $$
	For small $T$, we use the binomial theorem to write $$
\begin{aligned}
z & =\left(1+\frac{s T}{2}\right)\left(1+\frac{s T}{2}+\frac{(s T)^2}{4}+o\left(T^3\right)\right) \\
& =1+s T+\frac{(s T)^2}{2}+o\left(T^3\right)
\end{aligned}
$$this coincides with the quadratic expansion of $e^{s T}$

Each of these transformations corresponds to a certain mapping between $s$-plane and $z$-plane
![[s-z-mapping.png | center | 600]]
Backward difference and Tustin transformation applied to stable continuous systems **result in** stable discrete time systems -- not necessarily true for Euler's method!

Tustin transformation: stability is preserved (all the left plane poles get mapped into the unit disk)
$$
s=\psi(z)=\frac{z-1}{z+1}
$$
Solve for $z: ~ z=\psi^{-1}(s)=\frac{1+s}{1-s}$
For $s=\lambda+j \omega:$
$$
|z|^2=z z^*=\psi^{-1}(s)\left(\psi^{-1}(s)\right)^*=\frac{(1+\lambda)^2+\omega^2}{(1-\lambda)^2+\omega^2}
$$

If $\lambda=0$ then
$$
|z|^2=\frac{1+\omega^2}{1+\omega^2}=1 \rightarrow \text { unit circle }
$$

If $\lambda<0$ then $(1+\lambda)^2<(1-\lambda)^2$ thus
$$
|z|^2=\frac{(1+\lambda)^2+\omega^2}{(1-\lambda)^2+\omega^2}<1 \rightarrow \text { inside unit circle }
$$

#### Frequency warping of Tustin transformation
$$
s=\psi(z)=\frac{z-1}{z+1}
$$
Analog prototype filter: $G_c(s)$. Frequency response $G_c(j \omega)$.
Digital filter: $G(z)=G_c(\psi(z))$.
The normalised frequency response of the digital filter $(|\theta| \leq \pi)$ is given by
$$
G\left(e^{j \theta}\right)=G_c\left(\psi\left(e^{j \theta}\right)\right)
$$
where
$$
\begin{aligned}
& \qquad \begin{aligned}
\psi\left(e^{j \theta}\right)=\frac{e^{j \theta}-1}{e^{j \theta}+1}=\frac{e^{j \theta / 2}-e^{-j \theta / 2}}{e^{j \theta / 2}+e^{-j \theta / 2}}=\frac{j \sin (\theta / 2)}{\cos \theta / 2} & =j \tan (\theta / 2) \\
& =j \omega
\end{aligned}
\end{aligned}
$$
This is known as the frequency warping $$\boxed{G\left(e^{j \theta}\right)=G_c(j \tan (\theta / 2)) \quad}$$Inverse relation: the frequency response of the analog filter at $\omega$ is mapped into the frequency response of the digital filter at $\theta=2 \arctan (\omega)$.
$$
\begin{gathered}
\omega=\tan (\theta / 2) \rightarrow \theta=2 \arctan (\omega) \\
\boxed{G_c(j \omega)=G\left(e^{j 2 \arctan (\omega)}\right)}
\end{gathered}
$$
Note that the unit of the normalised frequency is **cycles / sample**
The normalised frequency of a given critical frequency $f_c$ sampled with frequency $f_s$ is $$\theta = 2\pi\frac{f_c}{f_s}$$
### 2. Response matching
![[DAC-ADC.png | center | 500]]
Goal: find the transfer function $G(z)$ from $\left\{u_k\right\}_{k \geq 0}$ to $\left\{y_k\right\}_{k \geq 0}$ 
Approach: take an appropriate input, find the output, take the ratio of the $z$ transform

#### Impulse invariance
$G_c(s)$ is the Laplace transform continuous-time filter. The impulse response of the corresponding impulse invariance digital filter $G(z)$ (with sampling $T$) is equal to the impulse response of the $G_c(s)$ sampled at $t=k T$.
$$
G(z)=\mathcal{Z}\left(\mathcal{L}^{-1}\left(G_c(s)\right)_{t=k T}\right)
$$
- For **bandlimited** filters the digital filter frequency response will closely approximate the continuous-time frequency response.
- Preserves stability:
$$
\Re(\beta)<0 \rightarrow \int\left|e^{\beta t}\right| d t<\infty \rightarrow \sum\left|e^{\beta T k}\right|<\infty
$$
Example:
$$
G_c(s)=\frac{\alpha}{s-\beta} \stackrel{\mathcal{L}^{-1}}{\rightarrow} \alpha e^{\beta t} \xrightarrow{\text { sample }} \alpha e^{\beta T k} \xrightarrow{\mathcal{Z}} \frac{\alpha}{1-e^{\beta T} z^{-1}}=G(z)
$$
This works well when a Laplace transfer function is known, but not to measure a response: no D / A converter will convert $\delta_k$ to $\delta(t)$.

#### Step invariance
Take a continuous time filter/system with Laplace transfer function $G_c(s)$. The corresponding step response invariance digital filter (with sampling period $T$) is a digital filter whose step response is equal to the step response of the continuous time filter sampled at $t=k T$.
1. Find the step response of the continuous system
2. Sample at time $t=k T$ and take the $z$-transform
3. Multiply by $(z-1) / z$.
$$
G_c(s) \xrightarrow{\text { step }} \frac{G_c(s)}{s} \xrightarrow {\mathcal{L}^{-1}} y(t) \xrightarrow{\text { sample }} y(k T) \xrightarrow{\mathcal{Z}} Y(z) \xrightarrow{\frac{1}{\text { step }}} \frac{z-1}{z} Y(z)=G(z)
$$
$$
G(z)=\frac{z-1}{z} \mathcal{Z}\left(\mathcal{L}^{-1}\left(\frac{G_c(s)}{s}\right)_{t=k T}\right)
$$

#### Ramp invariance
Take a continuous time filter/system with Laplace transfer function $G_c(s)$. The corresponding ramp response invariance digital filter (with sampling period $T$ ) is a digital filter whose ramp response is equal to the ramp response of the continuous time filter sampled at $t=k T$.
$$
G(z)=\frac{(z-1)^2}{T_z} \mathcal{Z}\left(\mathcal{L}^{-1}\left(\frac{G_c(s)}{s^2}\right)_{t=k T}\right)
$$

Note: any waveform invariance can be considered. The digital filter will preserve the properties of the continuous filter response to that particular waveform.

#### Choosing the waveform
- Depends on the properties of the conversion of analog to digital
- Choose a response to an analog signal that will be converted to its digital equivalent by the ADC
- For example, a digital ramp through a "sample and hold" DAC becomes a staircase function not analog ramp $\rightarrow$ step invariant response more suited

## II. Digital filtering
### 1. Desired frequency responses
![[desired-frequency-responses.png | center | 500]]
### 2. Ideal lowpass delta response
$$\begin{aligned} g_k & =\frac{1}{2 \pi} \int_{-\pi}^\pi G\left(e^{j \theta}\right) e^{j \theta k} d \theta=\frac{1}{2 \pi} \int_{-\theta_c}^{\theta_c} e^{j \theta k} d \theta \\ & =\frac{\sin \left(\theta_c k\right)}{\pi k}=\frac{\theta_c}{\pi} \operatorname{sinc}\left(\theta_c k\right)\end{aligned}$$
![[ideal-lp-delta-response.png | center | 400]]
- This response is **non-causal** as $g_k \neq 0 \text{ for } k < 0$ (two-sided)
- Not realisable as a real-time linear system since it is infinite

### 3. Realisable filter specs
![[realisable-filter.png | center | 500]]
### 4. FIR vs IIR filters
#### FIR
- FIR filters are simple
- Feed-forward or non-recursive
- Realised efficiently in hardware (FFT)
- Inherently stable: $G(z)=\frac{\sum_{k=0}^N g_k z^{N-k}}{z^N}$, all poles in 0

#### IIR
- Feedback: the output goes back to the filter
- Finite polynomial representation but infinite impulse response
- Typically meet a given set of specifications with a much lower filter order than FIR filters

| FIR Filters                                                  | IIR Filters                                                                                                                                            |
| ------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Simple, stable, feedforward, fast implementation (FFT)       | Can be unstable, use feedback                                                                                                                          |
| Can have exactly linear phase                                | Design methods:<br>Direct optimisation of the transfer function<br>or Generation of a digital filter from an analogue implementation of analog filters |
| Design methods are generally linear                          |                                                                                                                                                        |
| Higher filter order than IIR                                 | Lower filter order than FIR                                                                                                                            |
| Often greater delay than for an equal performance IIR filter | Shorter delay than for an equal performance FIR filter                                                                                                 |
### 5. IIR design
#### General method
Use the continuous to discrete mappings in the previous section.
1. translate the filter specs on $\theta$ (where appropriate) to analog specs in $\omega$
2. design an analog filter (we will see a few techniques)
3. either use algebraic transforms (forward difference, backward difference or Tustin transform) to obtain a discrete-time filter or use response matching (e.g. impulse invariant mapping)
4. check design obtained, adjust if necessary, verify stability

Note: response matching may be better suited for FIR design

#### Classical analog prototypes
![[classical-analog-prototypes.png | center | 500]]
#### Butterworth filter
$N$ th-order lowpass, $G_c(s)$ satisfies
$$
G_c(s) G_c(-s)=\frac{1}{1+\left(\frac{s}{j \omega_c}\right)^{2 N}}
$$

- Unit DC gain, $G_c(j 0)=1$.
- -3 dB cutoff frequency at $s=j \omega_c$.
- $G_c(s) G_c(-s)$ poles satisfies
$$
\left(\frac{s}{j \omega c}\right)^{2 N}=-1, \text { i.e. } s=j \omega_c e^{\frac{j(2 k+1) \pi}{2 N}}
$$

- If $p_i$ is a root of $G_c(s)$ then $-p_i$ is a root of $G_c(-s)$. Thus the poles of $G_c(s)$ are those roots lying in the left half plane (stability), so that
$$
G_c(s)=\prod_{i=1}^P \frac{1}{s+p_i}
$$

#### Band transformations
Prototypes are typically lowpass. Standard transformation can be used to convert a lowpass prototype into other types.

Assuming a lowpass prototype with cutoff at 1 :
- Lowpass to Lowpass: set $s=\frac{\bar{s}}{\omega_c}$ to change the cutoff frequency to $\omega_c$.
- Lowpass to Highpass: set $s=\frac{\omega_c}{\bar{s}}$ to get highpass with cutoff frequency at $\omega_c$.
- Lowpass to Bandpass:
set $s=\frac{\bar{s}^2+\omega_l \omega_u}{\bar{s}\left(\omega_\mu-\omega_l\right)}$ to get bandpass with lower cutoff at $\omega_l$ and upper cutoff at $\omega_u$.
- Lowpass to Bandstop: set $s=\frac{\bar{s}\left(\omega_u-\omega_l\right)}{\bar{s}^2+\omega_{\mid} \omega_u}$ to get bandstop with lower cutoff at $\omega_l$ and upper cutoff at $\omega_u$.
### 6. FIR filter design
![[FIR-shift-trunc.png | center | 400]]
- $h_k$ is non-causal impulse response of the ideal filter
- New filter G derived by
	- Shift
	- Truncation at $N + 1$ samples of the ideal response
	$\rightarrow$ Causality recovered!
$$G(z)=\sum_{k=0}^N g_k z^{-k} \quad g_k=h_{k-N / 2}$$
#### Truncated ideal filters
- Larger $N$ $\rightarrow$ smaller samples discarded $\rightarrow$ reduced distortion
- but longer filters are computationally more expensive and have larger delay

#### The DTFT's reverse convolution property
For DTFT: $$w_n=u_n v_n \longrightarrow W(\theta)=\frac{1}{2 \pi} \int_{-\pi}^\pi U(\varphi) V(\theta-\varphi) d \varphi$$
The DTFT has 2 convolution properties (from $k$ to $\theta$)
1. discrete convolution $\longrightarrow$ multiplication
2. multiplication $\longrightarrow$ periodic convolution

#### Truncation
Shifted desired impulse response
$$
\tilde{h}_k=h_{k-N / 2}
$$
Truncated unit sample response
$$
g_k=h_k \quad 0 \leq k \leq N
$$
Truncation $=$ multiplication by a rectangular window
$$
g_k=h_k w_k \quad w_k= \begin{cases}1 & 0 \leq k \leq N \\ 0 & \text { otherwise }\end{cases}
$$
Using the reverse convolution property of the DTFT:
$$
G(\theta)=\frac{1}{2 \pi} \int_{-\pi}^\pi H(\varphi) W(\theta-\varphi) d \varphi
$$
#### DTFT of the rectangular window
$$
\begin{aligned}
W(\theta) & =\sum_{k=-\infty}^{\infty} w_k e^{-j \theta k}=\sum_{k=0}^N e^{-j \theta k} \\
& =\frac{1-e^{-j \theta(N+1)}}{1-e^{-j \theta}} \\
& =e^{-\frac{j \theta N}{2}} \frac{\sin \left(\frac{\theta(N+1)}{2}\right)}{\sin \left(\frac{\theta}{2}\right)}
\end{aligned}
$$
if $N$ reasonably large, $\theta \frac{N+1}{2} \gg \theta / 2$ so the denominator is $\sin (\theta / 2) \approx \theta / 2$ and hence
$$
|W(\theta)| \approx(N+1) \operatorname{sinc}\left(\frac{\theta(N+1)}{2}\right), \quad-\frac{12 \pi}{N+1} \leqslant \theta \leqslant \frac{12 \pi}{N+1}
$$
This is approximately a sinc function.

#### The effect of truncation
![[window-function.png | center | 500]]
- Transition band is related to main lobe. It reduces as $N \rightarrow \infty$.
- Ripples of $G$ are related to the area under sidelobes, which remains constant as $N$ increases -- improved by redesigning the window function
#### Windows
Rectangular
$$
w_k= \begin{cases}1 & 0 \leq k \leq N \\ 0 & \text { otherwise }\end{cases}
$$
Bartlett (triangular)
$$
w_k= \begin{cases}2 k / N & 0 \leq k \leq N / 2 \\ 2-2 k / N & M / 2<k \leq N \\ 0 & \text { otherwise }\end{cases}
$$
Hanning
$$
w_k= \begin{cases}0.5-0.5 \cos (2 \pi k / N) & 0 \leq k \leq N \\ 0 & \text { otherwise }\end{cases}
$$
Hamming
$$
w_k= \begin{cases}0.54-0.46 \cos (2 \pi k / N) & 0 \leq k \leq N \\ 0 & \text { otherwise }\end{cases}
$$
#### Window plots
![[window-plots.png | center | 500]]

#### Window characteristics
![[window-characteristics.png | center | 600]]
#### Window method
- Design filters to approximate a given target response
- Does not explicitly impose amplitude response constraints, e.g. passband ripples or stopband attenuation
Steps:
1. Select a suitable window function $w_k$.
2. Specify an ideal frequency response $H$.
3. Compute the coefficients of the ideal filter $h_k$.
4. Multiply the ideal coefficients by the window function to give the filter coefficients and delay to make causal.
5. Evaluate the frequency response of the resulting filter and iterate 1-5 if necessary.
For detailed working example see lecture notes 9.

#### Multi-band FIR design
Design highpass, bandpass,. . . $\longrightarrow$ Composition of lowpass filters
The ideal bandpass filter
$$
\begin{aligned}
H\left(e^{j \theta}\right) & = \begin{cases}1 & \omega_1 \leq \theta \leq \omega_2 \\
0 & \text { otherwise }\end{cases} \\
& =\operatorname{Lowpass}_{\left[0, \omega_2\right]}\left(e^{j \theta}\right)-\operatorname{Lowpass}_{\left[0, \omega_1\right]}\left(e^{j \theta}\right)
\end{aligned}
$$
where
$$
\operatorname{Lowpass}_{\left[0, \omega_c\right]}\left(e^{j \theta}\right)= \begin{cases}1 & 0 \leq \theta \leq \omega_c \\ 0 & \text { otherwise }\end{cases}
$$
Ideal impulse response by linearity and antitransform:
$$
\begin{aligned}
h_k & =\mathcal{F}^{-1}(H)=\mathcal{F}^{-1}\left(\operatorname{Lowpass}_{\left[0, \omega_2\right]}\right)-\mathcal{F}^{-1}\left(\text { Lowpass }_{\left[0, \omega_1\right]}\right) \\
& =\frac{\sin \left(k \omega_2\right)}{\pi k}-\frac{\sin \left(k \omega_1\right)}{\pi k}
\end{aligned}
$$
Final filter by delay and multiplication with desired window $w_k$ :
$$
g_k=h_{k-N / 2} w_k
$$
#### Linear phase filter
![[linear-phase-filter.png | center | 500]]
Linear phase $G\left(e^{j \theta}\right)=\left|G\left(e^{j \theta}\right)\right| e^{-j \theta \frac{N}{2}}$ is achieved if $\mathbf{g}_{\mathbf{k}}=\mathbf{g}_{N-\mathbf{k}}$.
$$
\begin{aligned}
G\left(e^{j \theta}\right) & =\sum_{k=0}^N g_k e^{-j \theta k} \\
& =g_0 e^{-j \theta 0}+g_N e^{-j \theta N}+g_1 e^{-j \theta 1}+g_{N-1} e^{-j \theta(N-1)}+\ldots \\
& =e^{-j \theta \frac{N}{2}}(\underbrace{g_0 e^{j \theta \frac{N}{2}}+g_N e^{-j \theta \frac{N}{2}}}_{2 g_0 \cos \left(\theta \frac{N}{2}\right) \text { is real }}+\underbrace{g_1 e^{j \theta\left(\frac{N}{2}-1\right)}+g_{N-1} e^{-j \theta\left(\frac{N}{2}-1\right)}}_{2 g_1 \cos \left(\theta\left(\frac{N}{2}-1\right)\right) \text { is real }}+\ldots)
\end{aligned}
$$
Note: **window method gives linear phase filters.** The coefficients $w_k$ of all window functions satisfies $w_k=w_{N-k}$. If the desired impulse response $h_k$ is also symmetric $h_k=h_{N-k}$ then $g_k=h_k w_k$ is symmetric, that is, the resulting filter has linear phase.





