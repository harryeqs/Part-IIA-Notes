## I. Controllability
### 1. Definition
A state-space model is controllable if given an initial state $\underline{x}_0$ and a final state $\underline{x}_f$, there exists an input signal $u(\cdot)$ that transfers the state from $\underline{x}(0)=\underline{x}_0$ to $\underline{x}(T)=\underline{x}_f$ in a finite time $T>0$.

The **controllability matrix** is defined as:
$$
P = \left[\begin{array}{lll} B \mid & \ldots & \mid A^{n-1} B \end{array}\right]
$$
**where $n$ is the dimension of the state vectors.

**The system is controllable if the controllability matrix $P$ has full rank.**
Any state in the **left-null space** of $P$ is reachable.

**Motivation:**
$$\underline{x}\left(t_1\right)=\underline{x}_1=e^{A t} \underline{x}\left(t_0\right)+\int_0^{t_1} e^{A(t-\tau)} B \underline{u}(t-\tau) d \tau $$Note that by Cayley-Hamilton theorem, $$ e^{A \tau}=I \alpha_0(\tau)+\cdots+A^{n-1} \alpha_{n-1}(\tau) $$Solve the linear system $$ \underline{x}\left(t_1\right)-e^{A t} \underline{x}\left(t_0\right)=\left[\begin{array}{lll} B \mid & \ldots & \mid A^{n-1} B \end{array}\right]\left[\begin{array}{c} \int_0^{t_1} \alpha_0(t-\tau) \underline{u}(t-\tau) d \tau \\ \vdots \\ \int_0^{t_1} \alpha_{n-1}(t-\tau) \underline{u}(t-\tau) d \tau \end{array}\right] $$
### 2. Controllability Gramian
The **controllability Gramian** is defined as:
$$W_c\left(t_1\right) \stackrel{\text { def }}{=} \int_0^{t_1} e^{A \tau} B B^T e^{A^T \tau} d \tau$$
Assume that $W_c\left(t_1\right)$ has an inverse and let $\underline{u}(t)=B^T e^{A^T\left(t_1-t\right)} W_c\left(t_1\right)^{-1} \underline{x}_1$:
$$\int_0^{t_1} \underline{u}_o(t)^T \underline{u}_o(t) d t=\underline{x}_1^T W_c\left(t_1\right)^{-1} \int_0^{t_1} e^{A\left(t_1-t\right)} B B^T e^{A^T\left(t_1-t\right)} d t W_c\left(t_1\right)^{-1} \underline{x}_1=\underline{x}_1^T W_c\left(t_1\right)^{-1} \underline{x}_1$$

The **inverse of the controllability Gramian** defines the input energy required to transfer the state from $x_0 = 0$ to $x_1$.
If the Gramian is nearly singular, some states are difficult to reach -- they require large input energy.

#### Minimum energy transfer
The input, $\underline{u}(t)=\underline{u}_o(t)=B^T e^{A^T\left(t_1-t\right)} W_c\left(t_1\right)^{-1} \underline{x}_1$, takes the state from $\underline{x}(0)=\underline{0}$ to $\underline{x}\left(t_1\right)=\underline{x}_1$ with **minimum energy.**
(Proof available in lecture notes)

## II. State-feedback
### 1. State-feedback controller
The state-feedback controller is defined as:
$$
u = -Kx
$$
The closed loop poles will be the eigenvalues of $(A-B K)$ which can be placed arbitrarily by choice of $K$ **if and only if $(A, B)$ is controllable.**

**Criteria on pole placement**
- all poles in the left half plane for closed-loop stability
- ensure sufficiently damped and fast enough response
- avoid high gain (to avoid actuator saturation and poor robustness)

### 2. State-feedback for regulation
![[regulation-state-feedback.png | center | 400]]

State-space model:
$$
\begin{aligned}
\dot{x} &= A x+B u \\
y &= C x
\end{aligned}
$$
State-feedback controller :
$$
u=-K x+M r
$$
Steady-state response:
$$
\dot{x}=0 \Rightarrow y=C(-A+B K)^{-1} B M r
$$
Feedforward design : choose $M$ to ensure $C(-A+B K)^{-1} B M \approx I$

### 3. Observer-based feedback design
![[observer-based-feedback.png | center | 500]]

$$
\begin{aligned}
\operatorname{SYSTEM}&\left\{\begin{array}{l}\underline{\dot{x}}=A \underline{x}+B \underline{u} \\ \underline{y}=C \underline{x}\end{array}\right. \\
\operatorname{OBSERVER} &\left\{\begin{aligned} \underline{\dot{\hat{x}}} & =A \underline{\hat{x}}+B \underline{u}+L(\underline{y}-\underline{\hat{y}})=(A-L C) \underline{\hat{x}}+B \underline{u}+L \underline{y} \\ \underline{\hat{y}} & =C \underline{\hat{x}}\end{aligned}\right. \\
\operatorname{CONTROLLER} & \left\{\underline{u}=-K \underline{\hat{x}}+M \underline{r}\right.
\end{aligned}$$

$$
\begin{aligned}
\text{Error: }& \underline{e}=\underline{x}-\underline{\hat{x}} \\
& \underline{\dot{e}}=(A-L C) \underline{e} \\
& \underline{u}=-K(\underline{x}-\underline{e})+M \underline{r} \\
& \underline{\dot{x}}=(A-B K) \underline{x}+B K \underline{e}+B M \underline{r}
\end{aligned}
$$

$$\Rightarrow\left\{\begin{aligned} {\left[\begin{array}{c}\underline{\dot{x}} \\ \underline{\dot{e}}\end{array}\right] } & =\left[\begin{array}{cc}A-B K & B K \\ 0 & A-L C\end{array}\right]\left[\begin{array}{l}\underline{x} \\ \underline{e}\end{array}\right]+\left[\begin{array}{c}B M \\ 0\end{array}\right] \underline{r} \\ \underline{y} & =\left[\begin{array}{ll}C & 0\end{array}\right]\left[\begin{array}{l}\underline{x} \\ \underline{e}\end{array}\right]\end{aligned}\right.$$

The closed-loop poles are the **union** of the poles resulting from the pole placement by 
- the state feedback (eigenvalues of $A-BK$)
- and the observer design (eigenvalues of $A-LC$)

The eigenvalues can be chosen arbitrarily if the state-space model is **BOTH** controllable and observable.

### 4. Kalman decomposition
**Motivation:** Isolate the observable and controllable subspace.

$\operatorname{Im} P \cap \operatorname{Ker} Q$ controllable and unobservable subspace

$\operatorname{Im} P \cap(\operatorname{Ker} Q)^{\perp}$ observable and controllable subspace

$\operatorname{Ker} Q \cap(\operatorname{Im} P)^{\perp}$ unobservable and uncontrollable subspace

$(\operatorname{Im} P)^{\perp} \cap(\operatorname{Ker} Q)^{\perp}$ observable and uncontrollable subspace

Note:
$\operatorname{Im} P$ = column space -- controllable subspace
$(\operatorname{Im} P)^{\perp}$ = left-null space
$\operatorname{Ker} Q$ = null space
($\operatorname{Ker} Q)^{\perp}$ = row space -- observable subspace

### 5. Minimal realisation
**Definition:** A set of state equations given by $(A, B, C, D)$ is called a minimal realisation of its transfer function, $G(s)=D+C(s I-A)^{-1} B$, if there does not exist a state space realisation of $G(s)$ with a lower state dimension (use a minimum number of states).

A realisation is **minimal** if and only if it is **both controllable and observable.**

## III. Optimality
**Motivation:** trade-offs in observer and state-feedback design
- For observer, noise measurement vs model error
- For state-feedback, input energy vs state energy

### 1. Linear quadratic regulator (LQR)
Choose the input signal to minimise the **quadratic cost:**
$$\int_0^{\infty} x(t)^T Q x(t)+u(t)^T R u(t) d t$$
where
$R=R^T>0 \quad$  is positive definite
$Q=Q^T \geq 0 \quad$ is positive semidefinite

(This is the infinite horizon problem)

**Solution:**
$$u=-\underbrace{R^{-1} B^T P}_K x$$
where $P$ is the unique positive definite solution of the algebraic Riccati equation (ARE)
$$P A+A^T P-P B R^{-1} B^T P+Q=0$$
### 2. Linear quadratic estimator (LQE) -- Kalman filter
**Motivation:** Given the observation of the e**ntire past of the input and output**, minimise the model mismatch energy and the noise measurement energy to **estimate the current state.**

Given model:
$$\begin{aligned} & \dot{x}(t)=A x(t)+B(u(t)+d(t)) \\ & y(t)=C x(t)+n(t)\end{aligned}$$
Minimise:
$$\int_{-\infty}^t d(\tau)^T B^T B d(\tau)+\mu n(\tau)^T n(\tau) d \tau$$
The first term is the **model mismatch energy** and the second term is the **noise measurement energy**.

(This is the infinite horizon estimation problem)

**Solution:**
$$
\dot{\hat{x}}=A \hat{x}+B u-S C^T(y-C \hat{x})
$$
where $S$ is the unique positive definite solution of the ARE
$$
A S+S A^T+B B^T-\frac{1}{\mu} S C^T C S=0
$$

Note: Linear-Quadratic-Gaussian control (LQG) combins LQE and LQG.