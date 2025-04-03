This section is listed separately for completeness.
### 1. Discrete-time state-space model
$$\begin{aligned} \underline{x}[k+1] & =A \underline{x}[k]+B \underline{u}[k] ; \quad \underline{x}[0]=\underline{x}_0 \\ \underline{y}[k] & =C \underline{x}[k]+D \underline{u}[k]\end{aligned}$$
### 2. State transition matrix
$$\begin{aligned} \underline{x}[k+1] & =A \underline{x}[k] \\ x[k+1] & =\Phi(k, 0) x_0 \quad \Phi(k, 0)=A^k\end{aligned}$$
### 3. Sampled-data control systems
![[sample-data-control-systems.png | center | 500]]
$$ \begin{aligned} \underline{x}((k+1) T) & =\underbrace{e^{A T}}_{\Phi} \underline{x}(k T)+\int_{k T}^{(k+1) T} e^{A((k+1) T-\tau)} B d \tau \underline{u}(k T) \\ & =\Phi \underline{x}(k T)+\Gamma \underline{u}(k T) \end{aligned} $$ where $$ \begin{aligned} \Gamma & =\int_0^T e^{A \tau^{\prime}} d \tau^{\prime} B=A^{-1}\left(e^{A T}-I\right) B, \text { if } \operatorname{det}(A) \neq 0 . \\ \underline{y}(k T) & =C \underline{x}(k T)+D \underline{u}(k T) \end{aligned} $$
**Note:** every continuous-time model has a sampled discrete-time version but the converse is not true. A discrete-time model is the sampling of a continuous time-model only if the matrix $A$ is real-valued.

### 4. Observability and controllability tests

**Observability test**
 $$\left[\begin{array}{c}y[0] \\ y[1] \\ \vdots \\ y[n-1]\end{array}\right]=Q x[0]$$

**Controllability test**
$$\underline{x}_f-A^n \underline{x}_0=\left[\begin{array}{lll}B \mid & \ldots & \mid A^{n-1} B\end{array}\right]\left[\begin{array}{c}\underline{u}[n-1] \\ \vdots \\ \underline{u}[0]\end{array}\right]$$
