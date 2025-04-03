## Introduction
The **states** are a set of system variables chosen to represent the memory of a dynamical system.

For $\underline{x}(\cdot)$ to be a valid state for a dynamical system it must satisfy two properties:
1. for any $t_0 < t_1$, $\underline{x}(t_1)$ can always be determined from $\underline{x}(t_0)$ and $\{\underline{u}(\tau)， t_0 \leq \tau \leq t_1\}$.
2. the outputs $\underline{y}$ at time $t_1$, are a **memoryless** function of (depends only on) $\underline{x}(t_1)$ and $\underline{u}(t_1)$.

Standard form for a **state-space dynamical system model:**
$$\mathcal{S}\left\{\begin{array}{l}\underline{\dot{x}}(t)=\underline{f}(\underline{x}(t), \underline{u}(t), t) \\ \underline{y}(t)=\underline{g}(\underline{x}(t), \underline{u}(t), t)\end{array}\right.$$
## I. Linearisation
Let $\underline{x}_e$ be an equilibrium state for the system when $\underline{u}(t)=\underline{u}_e$ (constant) 
i.e. $\underline{f}\left(\underline{x}_e, \underline{u}_e\right)=\underline{0}$ and also let $\underline{y}_e=\underline{g}\left(\underline{x}_e, \underline{u}_e\right)$.

For small $\underline{\delta x}$ and $\underline{\delta u}$:
$$ \begin{aligned} & \delta \dot{x}_i=\left[\frac{\partial f_i}{\partial x_1}, \cdots, \frac{\partial f_i}{\partial x_n}\right] \delta \underline{x}+\left[\frac{\partial f_i}{\partial u_1}, \cdots \frac{\partial f_i}{\partial u_2}\right] \delta \underline{u} \\ & \underline{\delta x} \cong A \underline{\delta x}+B \underline{\delta u} \end{aligned} $$
where
$$A=\left.\frac{\partial \underline{f}}{\partial \underline{x}}\right|_{\underline{x}_{=}=\underline{x}_e, \underline{u}=\underline{u}_e}=\left[\begin{array}{cccc}\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \cdots & \frac{\partial f_1}{\partial x_n} \\ \frac{\partial f_2}{\partial x_1} & \cdots & & \frac{\partial f_2}{\partial x_n} \\ \vdots & & & \vdots \\ \frac{\partial f_n}{\partial x_1} & \cdots & & \frac{\partial f_n}{\partial x_n}\end{array}\right]_{\underline{x}=\underline{x}_e, \underline{u}=\underline{u}_e}$$
and 
$$B=\left.\frac{\partial \underline{f}}{\partial \underline{u}}\right|_{\underline{x}=\underline{x}_e, \underline{u}=\underline{u}_e}=\left[\begin{array}{cccc}\frac{\partial f_1}{\partial u_1} & \frac{\partial f_1}{\partial u_2} & \cdots & \frac{\partial f_1}{\partial u_m} \\ \vdots & & & \vdots \\ \frac{\partial f_n}{\partial u_1} & \cdots & & \frac{\partial f_n}{\partial u_m}\end{array}\right]_{\underline{x}=\underline{x}_e, \underline{u}=\underline{u}_e}$$
Similarly $\underline{\delta y}=C \underline{\delta x}+D \underline{\delta u}$ where $C=\left.\frac{\partial \underline{g}}{\partial \underline{x}}\right|_{\underline{x}=\underline{x}_e, \underline{u}=\underline{u}_e}$ and $D=\left.\frac{\partial \underline{g}}{\partial \underline{u}}\right|_{\underline{x}_{\underline{x}}=\underline{x}_e, \underline{u}=\underline{u}_e}$

The linearised system equations are therefore:
$$\left\{\begin{array}{l}\dot{\delta x}=A \underline{\delta x}+B \underline{\delta u} \\ \underline{\delta y}=C \underline{\delta x}+D \underline{\delta u}\end{array}\right.$$
**Special case: implicit state equations**
The system equation is written as $\underline{F}(\underline{\dot x}, \underline{x}, \underline{u}) = \underline{0}$ instead of $\underline{\dot x} = \underline{f}(\underline{x}, \underline{u})$.
Linearize $\underline{F}$ about $\left(\underline{0}, \underline{x}_e, \underline{u}_e\right)$ (note that $\underline{F}\left(\underline{0}, \underline{x}_e, \underline{u}_e\right)$) to get $$ \begin{aligned} & \underbrace{\left.\frac{\partial \underline{F}}{\partial \dot{x}}\right|_{\left(\underline{0}, x_e, \underline{u}_e\right)}}_L \dot{\delta \underline{x}}+\underbrace{\left.\frac{\partial \underline{F}}{\partial \underline{x}}\right|_{\left(\underline{0}, \underline{x}_e, \underline{u}_e\right)}}_M \delta \underline{x}+\underbrace{\left.\frac{\partial \underline{F}}{\partial \underline{u}}\right|_{\left(\underline{0}, x_e, \underline{u}_e\right)}}_N \delta \underline{u} \simeq \underline{0} \\ & L \underline{\dot{\delta x}}+M \underline{\delta x}+N \underline{\delta u} \simeq \underline{0} \Longrightarrow \underline{\delta x} \simeq-L^{-1} M \underline{\delta x}-L^{-1} N \underline{\delta u} \end{aligned} $$

## II. Transfer function and state transition
### 1. Solving linear state equations using Laplace transforms
Taking Laplace transforms of
$$\begin{aligned} & \dot{\underline{x}}(t)=A \underline{x}(t)+B \underline{u}(t) ; \quad \underline{x}(0)=\underline{x}_0 \\ & y(t)=C \underline{x}(t)+D \underline{u}(t)\end{aligned}$$
$$\begin{aligned} \left(s \underline{X}(s)-\underline{x}_0\right) &= A \underline{X}(s)+B \underline{U}(s) \\ (s I-A) \underline{X}(s) &= \underline{x}_0+B \underline{U}(s) \\ \underline{X}(s) &=(s I-A)^{-1} \underline{x}_0+(s I-A)^{-1} B \underline{U}(s) \\
\underline{Y}(s) &= \underbrace{C(s I-A)^{-1} \underline{x}_0}_{\text {initial condition response }}+\underbrace{\left(D+C(s I-A)^{-1} B\right) \underline{U}(s)}_{\text {input response }}\end{aligned}$$
For $\underline{x}_0 = \underline{0}$,
$$
G(s) = D + C(sI - A)^{-1}B
$$
This is called the **transfer function matrix.

### 2. Transfer function poles
Poles are values of $s$ at which the transfer function becomes infinite.
$\Longrightarrow$ can only happen when the matrix $(sI-A)$ is singular
$\Longrightarrow \det(sI-A) = 0$
Hence $s$ are at the eigenvalues of $A$.

Therefore:
**Poles of $G(s) \subseteq$ eigenvalues of $A$**

### 3. State transition matrix
For $\underline{u}(t) = 0, \quad \underline{X}(s) = (sI-A)^{-1}\underline{x_0}$
Hence
$$
\underline{x}(t) = \mathcal{L}^{-1}((sI-A)^{-1})\underline{x_0} = \Phi(t)\underline{x_0}
$$
where
$$\begin{aligned} \Phi(t) &=\mathcal{L}^{-1}\left\{(s I-A)^{-1}\right\} \\ &=\mathcal{L}^{-1}\left\{\sum_{k \geq 0} A^k s^{-(k+1)}\right\} （\text{ from binomial expansion }）\\\
&= I + At + A^2 t^2/2! + \cdots + A^kt^k/k! \\
&= e^{At} \quad(\text {reverse Taylor expansion}) \end{aligned}$$
$\Phi(t)$ is known as the **state transition matrix**.

With $\underline{x}(t) = \Phi(t)\underline{x_0}$,
$$\begin{aligned} \frac{d}{d t} \underline{x}(t)=\frac{d}{d t}\left\{\Phi(t) \underline{x}_0\right\} & =A e^{A t} \underline{x}_0=A\left\{\Phi(t) \underline{x}_0\right\}=A \underline{x}(t) \\ \Phi(0) & =I \\ \Rightarrow \quad \underline{x}(0) & =\underline{x}_0\end{aligned}$$
### 4. Properties of the state transition matrix
#### Change of state coordinates
If $A = T^{-1}\bar{A}T \Longrightarrow A^k = T^{-1}\bar{A}^k T$
Hence
$$
e^{At} = T^{-1}e^{\bar{A}t}T
$$

If $\underline{\dot{x}}(t)=A \underline{x}(t)$ and $\underline{z}=T \underline{x}$, then
$$
\begin{aligned}
\underline{\dot{z}}(t) & =T \underline{\dot{x}}(t) \\
& =T A \underline{x}(t) \\
& =T A T^{-1} z(t) \\
& =\bar{A} z(t) \\
\underline{z}(t) & =e^{\bar{A} t} \underline{z}(0) \\
\text { Also: } \underline{x}(t) & =T^{-1} e^{\bar{A} t} T \underline{x}(0)
\end{aligned}
$$

**Special case: Eigenvectors as coordinate axes**
A non-defective matrix $A$ have eigenvector decomposition
$$A = W\Lambda W^{-1}$$
where $\Lambda$ is a diagonal matrix of eigenvalues and $W$ has eigenvectors as columns.

For $T = W^{-1}$:
$$\begin{aligned} & \bar{A}=T A T^{-1}=W^{-1} A W=\Lambda=\left[\begin{array}{llll}\lambda_1 & & & \\ & \lambda_2 & & \\ & & \ddots & \\ & & & \lambda_n\end{array}\right]=\operatorname{diag}\left\{\lambda_i\right\} \\ & \\ & e^{\Lambda t}=\sum_{k=0}^{\infty} \Lambda^k t^k / k!=\operatorname{diag}\left\{\sum \lambda_i^k t^k / k!\right\} \\ &=\operatorname{diag}\left\{e^{\lambda_i t}\right\} .\end{aligned}$$
#### Semigroup property
$$\begin{aligned} e^{A\left(t_1+t_2\right)} & =e^{A t_1} e^{A t_2}=e^{A t_2} e^{A t_1} \\ \text { since } \underline{x}\left(t_1+t_2\right) & =\Phi\left(t_1+t_2\right) \underline{x}(0) \\ & =\Phi\left(t_2\right) \underline{x}(t_1) \\ & =\Phi\left(t_2\right) \Phi\left(t_1\right) \underline{x}(0) \text{ for all }\underline{x}(0)\end{aligned}$$

#### Inverse
$$
(e^{At})^{-1} = e^{-At}
$$
#### Derivative
$$
\frac{d}{dt}e^{At} = Ae^{At} = e^{At}A
$$

#### Integral
$$\begin{aligned} \int_0^t e^{A \tau} d \tau & =\int_0^t \sum_{k=0}^{\infty} A^k \tau^k / k!d \tau \\ & =\sum_{k=0}^{\infty}\left[A^k \tau^{k+1} /(k+1)!\right]_0^t \\ & =A^{-1}\left\{\sum_{k=0}^{\infty} A^{k+1} t^{k+1} /(k+1)!-0\right\} \\ & =A^{-1} e^{A t}-A^{-1} \text { if } \operatorname{det}(A) \neq 0\end{aligned}$$

## III. State-space trajectories
Trajectories can be derived from:
$$\underline{\dot{x}} = \underline{f}(x) \Longrightarrow \underline{x}(t + \delta t) \simeq \underline{x}(t) + \underline{f}(\underline{x}(t))\delta t$$
![[state-space-trajectory.png | center]]


### 1. For linear systems
Eigenvalues and eigenvectors of $A$ show the stability of an equilibrium

| Real part of $\lambda$    | Complex part $\lambda$         |
| ------------------------- | ------------------------------ |
| > 0: points out (diverge) | = 0: linear                    |
| < 0: points in (converge) | $\neq$ 0: spiral (oscillatory) |
- linear region **near** equilibria
- eigenvectors indicates directions

For non-linear regions:
- trajectory tangents have slope $\frac{\dot{x_2}}{\dot{x_1}}$
- watch out for eigenvalues that decay or increase quickly (i.e. large magnitudes)
- trajectories at each equilibrium should join up smoothly with each other

### 2. For non-linear systems
When the states an inputs are far away from the equilibrium values, the linearised equations may no longer works – there might be limit cycles.

**Limit cycle** is a trajectory that the system will **converge to over time**.
![[limit-cycle.png | center | 500]]
In this case it is **stable limit cycle + unstable equilibrium**.

## IV. Properties of linear state-space system

### Convolution integral
$$
\underline{x}(t) = e^{At}\underline{x_0} + \int^t_0 e^{A(t-\tau)}B\underline{u}(\tau) d\tau
$$
and
$$\underline{y}(t)=\underbrace{C e^{A t} \underline{x}_0}_{\text {initial condition response }}+\underbrace{D \underline{u}(t)+\int_0^t C e^{A(t-\tau)} B \underline{u}(\tau) d \tau}_{\text {input response }}$$
### Impulse response matrix
$$H(t)=\left\{\begin{array}{cc}D \delta(t)+C e^{A t} B & t \geq 0 \\ 0 & t<0\end{array}\right.$$
Hence
$$\underline{y}(t) = \int_0^t H(t-\tau)\underline{u}(\tau)d\tau = H(t) * \underline{u}(t)$$
Note that the transfer function $G(s) = \mathcal{L}(H(t))$.
### Stability of the system
Stability of systems is the behaviour of $\underline{x}(t)$ as $t \rightarrow \infty$
- $\underline{x}(t) \rightarrow 0$ (stable)
- $\underline{x}(t) \rightarrow \infty$ (unstable)
- $\underline{x}(t)$ bounded (marginal stability)

Let eigenvalues of $A$ be $\lambda_i = \sigma_i + j\omega_i$ then $|e^{\lambda_i t}| = e^{\sigma_i t}|e^{j\omega_i t}| = e^{\sigma_i t}$
- $\underline{x}(t) \rightarrow \underline{0}$ as $t \rightarrow \infty$ (i.e. system is stable) for all $\underline{x}_0$ **if and only if all** $\lambda_i$ satisfy $Re(\lambda_i) < 0$
- $\underline{x}(t)$ remain bounded as $t \rightarrow \infty$ (i.e. marginally stable) **if and only if** $Re(\lambda_i) \leq 0$ and there are **no repeated** eigenvalues (no multiple roots on the imaginary axis).

### Frequency response
Let input be sinusoidal:
 $$ u_j(t)=A_j \cos \left(\omega_o t+\theta_j\right), j=1,2, \cdots, m $$ then $$ y_i(t) \rightarrow B_i \cos \left(\omega_o t+\phi_i\right) \text { as } t \rightarrow \infty$$ where $$ B_i e^{j \phi_i}=g_{i 1}\left(j \omega_o\right) A_1 e^{j \theta_1}+g_{i 2}\left(j \omega_o\right) A_2 e^{j \theta_2}+\cdots+g_{i m}\left(j \omega_o\right) A_m e^{j \theta_m} $$
 i.e. **the sum of the sinusoidal responses from each input.**
### Composite systems
#### Cascade
![[cascade.png | center | 400]]


Let $G_1(s)$ be realized by the state equation: $$ \left\{\begin{aligned} \underline{\dot{x}}_1(t) & =A_1 \underline{x}_1(t)+B_1 \underline{u}(t) \\ \underline{w}(t) & =C_1 \underline{x}_1(t)+D_1 \underline{u}(t) \end{aligned}\right. $$ and $G_2(s)$ be realized by, (input $\underline{w}$, output $\underline{y}$ )
 $$ \left\{\begin{aligned} \underline{\dot{x}}_2(t) & =A_2 \underline{x}_2(t)+B_2 \underline{w}(t) \\ \underline{y}(t) & =C_2 \underline{x}_2(t)+D_2 \underline{w}(t) \end{aligned}\right. $$then $\underline{Y}(s)=G_2(s) G_1(s) \underline{U}(s)$ is realized by $$ \begin{aligned} & \underbrace{\frac{d}{d t}\left[\begin{array}{l} \underline{x}_1(t) \\ \underline{x}_2(t) \end{array}\right]}_{\dot{x}(t)}=\underbrace{\left[\begin{array}{cc} A_1 & 0 \\ B_2 C_1 & A_2 \end{array}\right]}_A \underbrace{\left[\begin{array}{c} \underline{x}_1(t) \\ \underline{x}_2(t) \end{array}\right]}_{\underline{x}(t)}+\underbrace{\left[\begin{array}{c} B_1 \\ B_2 D_1 \end{array}\right]}_B \underline{u}(t) \\ & \underline{y}(t)=\underbrace{\left[\begin{array}{ll} D_2 C_1 & C_2 \end{array}\right]}_C \underline{x}(t)+\underbrace{D_2 D_1 \underline{u}(t)}_D \end{aligned} $$
#### Parallel combination
![[parallel-combination.png | center | 400]]
Let $G_1(s)$ be realized by the state equation:
$$
\left\{\begin{array}{l}
\dot{x}_1(t)=A_1 \underline{x}_1(t)+B_1 \underline{u}(t) \\
\underline{y}_1(t)=C_1 \underline{x}_1(t)+D_1 \underline{\underline{u}}(t)
\end{array}\right.
$$
and $G_2(s)$ be realized by, (input $\underline{u}$, output $\underline{y}_2$ )
$$
\left\{\begin{array}{l}
\dot{x}_2(t)=A_2 \underline{x}_2(t)+B_2 \underline{u}(t) \\
\underline{y}_2(t)=C_2 \underline{x}_2(t)+D_2 \underline{u}(t)
\end{array}\right.
$$
then $\underline{Y}(s)=\left(G_1(s)+G_2(s)\right) \underline{U}(s)$ is realized by
$$
\begin{aligned}
& \underbrace{\frac{d}{d t}\left[\begin{array}{l}
\underline{x}_1(t) \\
\underline{x}_2(t)
\end{array}\right]}_{\dot{x}(t)}=\underbrace{\left[\begin{array}{cc}
A_1 & 0 \\
0 & A_2
\end{array}\right]}_A \underbrace{\left[\begin{array}{l}
\underline{x}_1(t) \\
\underline{x}_2(t)
\end{array}\right]}_{\underline{x}(t)}+\underbrace{\left[\begin{array}{l}
B_1 \\
B_2
\end{array}\right]}_B \underline{u}(t) \\
& \underline{y}(t)=\underbrace{\left[\begin{array}{ll}
C_1 & C_2
\end{array}\right]}_C \underline{x}(t)+\underbrace{\left(D_1+D_2\right)}_D \underline{u}(t)
\end{aligned}
$$
#### Feedback combination
![[feedback-combination.png | center | 400]]
Let $G_1(s)$ be realized by the state equation:
$$
\left\{\begin{array}{l}
\underline{\dot{x}}_1(t)=A_1 \underline{x}_1(t)+B_1\left(\underline{r}(t)-\underline{y_2}(t)\right) \\
\underline{y}_1(t)=C_1 \underline{x}_1(t)+D_1\left(\underline{r}(t)-\underline{y_2}(t)\right)
\end{array}\right.
$$
and $G_2(s)$ be realized by, (input $\underline{y}_1$, output $\underline{y}_2$ )
$$
\left\{\begin{array}{l}
\dot{x}_2(t)=A_2 \underline{x}_2(t)+B_2 \underline{y}_1(t) \\
\underline{y}_2(t)=C_2 \underline{x}_2(t)
\end{array} \longleftarrow \right. \text { no "D" matrix for simplicity }
$$
then $\underline{Y}(s)=G_1(s)\left(1-G_2(s) G_1(s)\right)^{-1} \underline{U}(s)$ is realized by
$$
\begin{aligned}
& \underbrace{\frac{d}{d t}\left[\begin{array}{l}
\underline{x}_1(t) \\
\underline{x}_2(t)
\end{array}\right]}_{\dot{\dot{x}}(t)}=\underbrace{\left[\begin{array}{cc}
A_1 & -B_1 C_2 \\
B_2 C_1 & A_2-B_2 D_1 C_2
\end{array}\right]}_A \underbrace{\left[\begin{array}{c}
\underline{x}_1(t) \\
\underline{x}_2(t)
\end{array}\right]}_{\underline{x}(t)}+\underbrace{\left[\begin{array}{c}
B_1 \\
B_2 D_1
\end{array}\right]}_B \underline{r}(t) \\
& \underline{y}_1(t)=\underbrace{\left[\begin{array}{ll}
C_1 & -D_1 C_2
\end{array}\right]}_C \underline{x}(t)+\underbrace{D_1}_D \underline{r}(t)
\end{aligned}
$$


