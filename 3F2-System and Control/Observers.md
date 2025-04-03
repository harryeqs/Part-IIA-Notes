## I. Observability
### 1. Definition
A system is called **observable** if we can deduce the state, $\underline{x}(t)$, from measurements of $\underline{u}(\tau)$ and $\underline{y}(\tau)$ over some time interval. 

If two initial states $\underline{x}_0 \neq \underline{x}_1$ give the same outputs then $\underline{0}=C e^{A t}\left(\underline{x}_1-\underline{x}_0\right)$ 
A state $\underline{x}_0$ such that $C e^{A t} \underline{x}_0=\underline{0}$ for all $t$ is called an **unobservable state.**

The **observability matrix** $Q$ is defined as:
$$Q=\left[\begin{array}{c}C \\ C A \\ \vdots \\ C A^{n-1}\end{array}\right]$$
**where $n$ is the number of columns of $C$ (= dimension of the state vectors).**

**The system is observable if and only if $Q$ is full rank.**
Any states in the **null space** of $Q$ are unobservable.

**Motivation:** differentiate $\underline{y}(t)$ to give
$$\underbrace{\left[\begin{array}{c}\underline{y}(t) \\ \underline{\dot{y}}(t) \\ \underline{\ddot{y}}(t) \\ \vdots \\ \underline{y}^{(n-1)}(t)\end{array}\right]}_{\text {known }}=\underbrace{\left[\begin{array}{c}C \\ C A \\ C A^2 \\ \vdots \\ C A^{n-1}\end{array}\right]}_Q \underbrace{\underline{x}(t)}_?+\underbrace{\left[\begin{array}{l}\underline{0} \\ C B \underline{u}(t) \\ C A B \underline{u}(t)+C B \underline{\dot{u}}(t) \\ \vdots \\ C A^{n-2} B \underline{u}+\cdots+C B \underline{u}^{(n-2)}\end{array}\right]}_{\text {known }}$$
To solve the above equation uniquely for $\underline{x}(t)$, $Q$ has to be full rank (which ensures that $Q$ is invertible).

### 2. Cayley-Hamilton theorem
**Motif:** Any square matrix is solution of its characteristic polynomial.
$$A^n+\alpha_1 A^{n-1}+\cdots+\alpha_n I=0$$
Hence any power $n$ of $A$ is a linear combination of $I, A, A^2, \ldots, A^{n-1}$.

By Cayley Hamilton theorem, the matrix $CA^n$ is a linear combination of the $n$ matrices
$$CA^{n-1}, CA^{n-2}, \ldots, C$$
Hence the rank of the observability matrix $Q$ will not increase further with output derivatives.

### 3. Unobservable states
Any state $\underline{x}_0$ in the null space of $Q$ is **unobservable** -- i.e. if and only if $Q\underline{x}_0 = \underline{0}$.
(Can be proven using Cayley-Hamilton theorem)

### 4. Observability Gramian
**Motif:** "Energy" considerations about observability.

The energy of the output trajectory over a time horizon $T$ is
$$
\begin{aligned}
\int^T_0 || y(t) ||^2 dt &= \int^T_0 y^\top(t)y(t)dt \\
&= \int^T_0 x_0^\top e^{A^\top t}C^\top C e^{At}x_0 \quad\text{(assuming initial condition } \underline{x}(0)=x_0 \text{ and zero inputs)} \\
&= x_0^\top \underbrace{\int^T_0  e^{A^\top t}C^\top C e^{At}}_{W_T} x_0 \\
& = x_0^\top W_T x_0
\end{aligned}
$$

$W_T = \int^T_0  e^{A^\top t}C^\top C e^{At}$ is the **observability Gramian.**

$W_T$ is **positive definite if and only is the system is observable.**

If all the eigenvalues of $A$ are in the left half plane, i.e. the system is stable, $W_\infty$ exists as the solution of equation
$$W_{\infty} A+A^\top W_{\infty}=-C^\top C$$

**Interpretation:** The eigenvalues of the observability Gramian **quantify** the directions of "strong observability" and directions of "weak" observability.
A small change along the direction of "strong observability" leads to a significant change in the output.

## II. Observers
### 1. Luenberger observer
$$\left\{\begin{array}{l}\underline{\dot{\hat{x}}}=A \underline{\hat{x}}+B \underline{u}+L(\underline{y}-\underline{\hat{y}}) \\ \underline{\hat{y}}=C \underline{\hat{x}}\end{array}\right.$$
Consider the error $\underline{e}(t)=\underline{x}(t)-\underline{\hat{x}}(t)$
$$
\begin{aligned}
\underline{\dot{e}} &= \underline{\dot{x}}-\underline{\dot{\hat{x}}}=(A \underline{x}+B \underline{u})-(A \underline{\hat{x}}+B \underline{u}+L(\underline{y}-\underline{\hat{y}})) \\
&= A(\underline{x}-\underline{\hat{x}})-L C(\underline{x}-\underline{\hat{x}})\\
&=(A-L C) \underline{e}
\end{aligned}
$$

**Goal:** Let $e^{(A-LC)t} \rightarrow 0$ quickly as $t$ increases.
$\Longrightarrow$ achieved if the eigenvalues of $(A-LC)$ are large and negative.

**Notes**
- $L = 0$ might be sufficient if $A$ is a stable matrix
- a high gain observer results in high noise injection

### 2. Trade-offs
Consider disturbance $d(t)$ that affects the states $\underline{x}(t)$ (the model) and measurement noise $n(t)$ that affects the outputs $\underline{y(t)}$.

$d$ large, $n$ small: Believe the measurements, don't trust the model. Use large $L$ and react quickly.
$d$ small, $n$ large: Don't trust the measurements, believe model. Use small $L$ and smooth the measurements.

**Kalman filter** optimises this trade-off.








