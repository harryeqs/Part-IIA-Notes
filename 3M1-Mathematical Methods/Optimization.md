## I. Introduction to optimization
### 1. Definitions
#### Types of minima
Global minimum $\quad f\left(x^*\right) \leq f(y) \quad \forall y \in S$ 
Strong global minimum $\quad f\left(x^*\right)<f(y) \quad \forall y \in S, y \neq x^*$ 
Weak local minimum $\quad f\left(x^*\right) \leq f(y) \quad \forall y=x^*+\varepsilon d \in S, y \neq x^*$
Strong local minimum $\quad f\left(x^*\right) \quad \quad \forall y=x^*+\varepsilon d \in S$

#### Unimodality
A function is **unimodal** if it has a single extremum.
It is **strongly unimodal** if along a straight line from every point to extremum the gradient is negative (for a minimum) or positive (for a maximum).

#### Convex functions
A function is **convex** if its graph at any point $y$ is never below the tangent at any other point $x$.
Convex functions are unimodal.

### 2. Conditions for a local minimum
#### Necessary condition for a local minimum
A necessary condition for $x^*$ to be a local minimum of $f(x)$ in $S$ is
$$
\nabla f\left(x^*\right) \cdot d \geq 0
$$
for all feasible directions $d$.
If $x^*$ is an interior point, i.e., it is not at the boundary of the feasible region: since all directions are feasible, $x^*$ must be a stationary point when
$$
\nabla f\left(x^*\right)=0
$$

The condition is necessary but not sufficient for $x^*$ to be a minimum because the same condition holds for maxima and saddle points

#### Sufficient condition for a local minimum
**Univariate case**
If $x^*$ is a interior stationary point, it is a strong local minimum if
$$
f''(x^*) > 0
$$
If $f''(x^*) = 0$, need to examine higher order terms ($\geq$ 0 is necessary but not sufficient).

**Multivariate case**
If $x^*$ is an interior stationary point, $\nabla f\left(x^*\right)=0$. 

Let $d=x-x^*$. Then $x^*$ is a strong local minimum if
$$
d^T H\left(x^*\right) d>0 \quad \forall d
$$
- At a stationary point $x^*, d^T \boldsymbol{H}\left(x^*\right) d>0$ (the Hessian is positive definite) is a sufficient condition of strong local minimum.
- At a stationary point $x^*, d^T \boldsymbol{H}\left(x^*\right) d \geq 0$ (the Hessian is positive semidefinite) is a necessary condition of strong local minimum.

## II. Univariate search methods
### 1. General algorithm
1. Start with an initial guess, $x_0$, for the minimum of $f(x)$ 
2. Propose a search direction, $d_k$ 
3. Propose a step size $\alpha_k$ along $d_k$, typically, by an inner line search loop to find the lowest value of $f(x)$ along the direction $d_k$ 
4. Update the estimate of the minimum location, $x_{k+1}=x_k+\alpha_k d_k$ 
5. Back to 2 until convergence

### 2. Convergence criteria
Norm of the residual
$$
\left\|f\left(x_{k+1}\right)-f\left(x_k\right)\right\|<\varepsilon_f
$$

Norm of the error
$$
\left\|x_{k+1}-x_k\right\|<\varepsilon_x
$$

Norm of the gradient
$$
\left\|\nabla f\left(x_k\right)\right\|<\varepsilon_g
$$

Note that $\varepsilon$ are user-defined tolerances.

### 3. Rate of convergence
The rate of convergence of an algorithm quantifies how fast the approximate solution approaches the true minimum $x^*$, close to the minimum, iteration after iteration
$$
\lim _{k \rightarrow \infty} \frac{\left\|x_{k+1}-x^*\right\|}{\left\|x_k-x^*\right\|^p}=\beta
$$

- $\beta$ is the convergence ratio: the smaller the better
- $p$ is the order of convergence: the larger the better

### 4. Line search
**Linear search** is the search of the minimum of a univariate function.

If the gradient is not available, apply **interval reduction**.

#### Interval reduction
1. Start with three points, $x_1, x_2, x_3$ such that $$ f\left(x_1\right)>f\left(x_3\right) \quad \text { and } \quad f\left(x_3\right)<f\left(x_2\right) $$ $x_1$ and $x_2$ are the bounds, $x_3$ is the interior point 
2. There exists a minimum in the interval $I_1=\left[x_1, x_2\right]$. This this is called **bracketing** 
3. Compute $f\left(x_4\right)$ at a fourth point $x_4 \in I_1$ 4. If $f\left(x_4\right)>f\left(x_3\right)$, the minimum must be in $I_2=\left[x_4, x_2\right]$, otherwise the minimum is in $I_2^{\prime}=\left[x_1, x_3\right]$ 
4. Continue bracketing until the interval is smaller than a tolerance

#### Golden section search
Impose a constant reduction factor $\beta$ for the interval length
$$
\frac{I_2}{I_1}=\frac{\Delta x}{I_2} \text { with } \Delta x=I_1-I_2
$$
set $\beta=I_2 / I_1$, and solve quadratic:
$$
\beta=\frac{\sqrt{5}-1}{2} \approx 0.618
$$
![[golden-section-search.png | center | 500]]

### 5. Fitting quadratic polynomials
**Motivation:** approximate the problem with a simpler one.

#### Newton's method
By Taylor expansion about $x_0$:
$$f(x) \approx q(x)=f\left(x_0\right)+\left(x-x_0\right) f^{\prime}\left(x_0\right)+\frac{1}{2}\left(x-x_0\right)^2 f^{\prime \prime}\left(x_0\right)$$

To calculate the minimum of $q(x)$, we set its derivative to zero
$$
\begin{aligned}
q^{\prime}(x) & =f^{\prime}\left(x_0\right)+\left(x-x_0\right) f^{\prime \prime}\left(x_0\right) \\
& =0
\end{aligned}
$$

The solution is
$$
\boxed{x=x_0-\frac{f^{\prime}\left(x_0\right)}{f^{\prime \prime}\left(x_0\right)}}
$$

**Remarks:**
- sensitive to initial input
- problematic when $f^{\prime \prime}\left(x_0\right)$ is zero or negative
- has a quadratic convergence

#### Quasi-Newton methods
For multivariate functions, the computations of the Hessian $H = \nabla^2 f(x)$ can be computationally prohibitive.

A simple method to approximate the second derivative is the **secant method** -- takes the current and previous points to estimate the second derivative of the current point:

$$f^{\prime \prime}\left(x_1\right) \approx \frac{f^{\prime}\left(x_1\right)-f^{\prime}\left(x_0\right)}{x_1-x_0}$$

The solution is
$$\boxed{x=x_1-f^{\prime}\left(x_1\right) \frac{x_1-x_0}{f^{\prime}\left(x_1\right)-f^{\prime}\left(x_0\right)}}$$

**Remarks:**
- convergence is superlinear -- the golden ratio 1.618

## III. Multivariate search methods
### 1. Steepest descent
#### Algorithm
1. Start with an initial guess for the minimum $x_0$ 
2. Set the search direction as the **negative gradient** (this step changes the direction) $$ d_k \equiv-\nabla f\left(x_k\right) $$
3. Determine by line search the step size $\alpha_k$ that minimizes (optimisation in 1D) $$ f(x) \quad \text{along}\quad d_k $$
4. Update the solution $x_{k+1}=x_k+\alpha_k d_k$
5. If not converged, back to 2.

**Note:** This is nested structure: main loop in step 2 and inner loop in step 3.

Ideally,
$$\frac{d f\left(x_k+\alpha_k d_k\right)}{d \alpha_k}=0$$

$\rightarrow$ gradient at $x_{k+1}$ is orthogonal to $d_k$ -- successive search directions are orthogonal to each other
$$
d_k^T d_{k+1} = 0
$$
(Geometrically, $f$ can't decrease any further along $d_k$)

The optimal step size is approximated using second-order Taylor expansion:
$$\alpha_k=-\frac{\nabla f\left(x_k\right)^T d_k}{d_k^T H\left(x_k\right) d_k}$$

#### Convergence
Steepest descent converges **linearly**.
$$\left\|x_{k+1}-x^*\right\|=\beta\left\|x_k-x^*\right\|$$
where
$$\beta \leq\left[\frac{k-1}{k+1}\right]^2$$
with $k$ being the condition number of the Hessian.

### 2. Newton-Raphson method
#### Algorithm
Taylor expansion of $f(x)$ about $f(x_k)$:
$$f(x) \approx q(x)=f\left(x_k\right)+\nabla f\left(x_k\right)^T\left(x-x_k\right)+\frac{1}{2}\left(x-x_k\right)^T H\left(x_k\right)\left(x-x_k\right)$$

The minimum of $q(x)$ occurs when $\nabla q(x) =0$:
$$\begin{aligned} \nabla q(x) & =\nabla f\left(x_k\right)+H\left(x_k\right)\left(x-x_k\right)=0 \\ x & =x_k-\left[H\left(x_k\right)\right]^{-1} \nabla f\left(x_k\right)\end{aligned}$$
The update rule is:
$$ x=x_{k+1}=x_k+\alpha_k d_k $$ with the search direction $d_k=-\left[H\left(x_k\right)\right]^{-1} \nabla f\left(x_k\right)$ and the step size $\alpha_k=1$.

**Extension:** Newton-Raphson method with line search -- the step size $\alpha_k$ is found by a linear search at each iteration.

#### Convergence
Newton-Rapson method converges **quadratically**.

It converges to the minimum in **one iteration** in a quadratic function.

**Note:** Newton-Raphson may never converge if the inital guess is not appropriate, and may converge to a stationary but non-minimum point if the Hessian is not positive definite.

### 3. Barzilai-Borwein method
**Motivation:** the multidimensional generalisation of the **secant method**.

$$x=x_1-\nabla f\left(x_1\right) \frac{\left(x_1-x_0\right)^T\left(\nabla f\left(x_1\right)-\nabla f\left(x_0\right)\right)}{\left.\mid \nabla f\left(x_1\right)-\nabla f\left(x_0\right)\right)\left.\right|^2}$$

**Note:** This is usually more stable than Newton's method, but not much is known about its convergence.

![[quadratic-comparison.png | center | 600]]

### 4. Conjugate gradients
**Motivation:** step along the eigendirections -- directions of **maximum variation** -- to converge quickly.

However, the eigenvectors are expensive to compute $\rightarrow$ need to find a new coordinate system in which the search directions are **orthogonal** to each other.

So the goal is to find a set of directions $\{d_i\}$ for which
$$d_i^T A d_j=0 \quad \text{for} \quad i \neq j$$
-- this is **conjugacy**.

Collect the directions into a matrix,
$$
S=\left[\begin{array}{cccc}
\uparrow & \uparrow & \uparrow & \uparrow \\
d_1 & d_2 & \ldots & d_N \\
\downarrow & \downarrow & \downarrow & \downarrow
\end{array}\right]
$$

Transform the coordinates into $y=S^{-1} x$, and set up the problem in the new coordinate system $y$ :
$$
f(x)=f(S y)=\frac{1}{2}(S y)^T A(S y)-b^T S y=\frac{1}{2} y^T\left(S^T A S\right) y-\left(S^T b\right)^T y
$$
where
$$
S^T AS=\left[\begin{array}{cccc}d_1^T A d_1 & 0 & \ldots & 0 \\ 0 & d_2^T A d_2 & \ldots & 0 \\ \vdots & \vdots & \ddots & \vdots \\ 0 & 0 & \ldots & d_N^T A d_N\end{array}\right]
$$

#### Algorithm
Construct the new search direction as $$ d_k=-\nabla f\left(x_k\right)+\beta_k d_{k-1} $$Impose the conjugacy condition $$ \begin{aligned} & 0=d_{k-1}^T A d_k \\ & 0=d_{k-1}^T A\left(-\nabla f\left(x_k\right)+\beta_k d_{k-1}\right) \end{aligned} $$ which yields $$ \beta_k=\frac{d_{k-1}^T A \nabla f\left(x_k\right)}{d_{k-1}^T A d_{k-1}} $$
**Processes:** 
1. Initialise with steepest descent $d_0=-\nabla f\left(x_0\right)$ 
2. Update location and determine $\alpha_k$ with line search $$ x_{k+1}=x_k+\alpha_k d_k $$
3. Find new search direction: with this choice of $d_0$, it can be shown that $$ d_{k+1}=-\nabla f\left(x_{k+1}\right)+\left[\frac{\left|\nabla f\left(x_{k+1}\right)\right|}{\left|\nabla f\left(x_k\right)\right|}\right]^2 d_k $$

#### Remarks
- conjugate gradient converges after N iterations for an N dimensional quadratic form with exact line search
- numerical errors lead to loss of conjugacy
- the convergence is linear but $\beta$ can be very very small -- **'superlinear convergence'** (better than steepest descent)

### 5. Summary of multi-dimensional search-direction methods
![[summary-search-direction-methods.png | center | 500]]
### 6. Gauss-Newton method
#### Least-squares fitting
The residual vector $r(x)$ is defined as:
$$
r_j(x) = \phi_j(x) - y_j
$$
The total error to be minimised is
$$f(x)=\sum_{j=1}^m r_j^2(x)=r(x)^T r(x)$$

#### The Gauss-Newton method
**Assumption:** the residuals are small, i.e. the model gives a good fit.

The Hessian of $f(x)$ can be approximated as:
$$H(x) \approx \tilde{H}(x)=2 J(x)^T J(x)$$
where $J(x)$ is the Jacobian matrix of $r(x)$
$$
\boldsymbol{J}(x)=\left[\begin{array}{ccc}
\frac{\partial r_1}{\partial x_1} & \cdots & \frac{\partial r_1}{\partial x_n} \\
\vdots & \ddots & \vdots \\
\frac{\partial r_m}{\partial x_1} & \cdots & \frac{\partial r_m}{\partial x_n}
\end{array}\right]
$$

The search direction is then
$$
\begin{aligned}
d_k & =-\left[\tilde{H}\left(x_k\right)\right]^{-1} \nabla f\left(x_k\right) \\
& =-\left[2 J\left(x_k\right)^T J\left(x_k\right)\right]^{-1} \nabla f\left(x_k\right) \\
& =-\frac{1}{2}\left[J\left(x_k\right)^T J\left(x_k\right)\right]^{-1} 2 J\left(x_k\right)^T r\left(x_k\right) \\
& =-J\left(x_k\right)^{+} r\left(x_k\right)
\end{aligned}
$$
where $J^{+}=\left[J\left(x_k\right)^T J\left(x_k\right)\right]^{-1} J\left(x_k\right)^T$ is the pseudoinverse matrix.

**Notes:** The Gauss-Newton methods converges nearly quadratically is the residuals are small.

## IV. Linear constrained optimization
### 1. Linear programming
(For worked example see lecture notes)

#### Remarks
Consider $m$ constraints $Ax = b$ defining a subspace of $\mathbb{R}^n$
- The bounds defines the **feasible region**
- The feasible region has a number of corners called **extremal points** or **basic solutions**
- $n - m$ control variables are zero at the extremal points -- these are **free variables**
- $m$ basic variables are non-zero

### 2. The simplex algorithm
Phase 1. Start the algorithm 
- Start with an extremal feasible solution, which is a vertex of the feasible region with $m$ nonzero control variables
 
Phase 2. Move from one vertex to another until the minimum is found 
- Move along an edge of the feasible region to another vertex where $f$ is smaller (decide the **entering** variable from the **reduced cost**)
- Continue until you find a vertex where every edge leading away would increase $f$  (positive reduced cost)
- This is the minimum

In practice use the Tableau!

### 3. Slack variables to tackle inequality constraints
The tableau contains **equality constraints and zero bounds** -- the standard form of an LP problem. If there are inequality constraints of the form $$ a_j^T x \geq b_j $$
We can convert them into an equality constraints by introducing a new slack variable, $s_j$, $$ s_j=a_j^T x-b_j $$
with the constraint $s_j \geq 0$.

### 4. Simple method Phase 1
- Construct an auxiliary optimization problem, with the objective function being the "error" that measures by how much the constraints are violated
- Create $m$ slack variables, add one to each of the constraint equations
- The new objective function is the sum of the slack variables
- **The initial feasible solution has the slack variables $\left(s_i\right)$ as basic, and the actual variables of the problem $\left(x_i\right)$ as zero**

## V. Non-linear constrained optimization

### 1. Problem formation
Minimize
$$
f(x), \quad x=\left(x_1, x_2, \ldots, x_N\right)^T
$$

Subject to
$$
\begin{array}{ll}
h_i(x)=0, & i=1,2, \ldots m \\
g_j(x) \leq 0, & j=1,2, \ldots n
\end{array}
$$
- $f$ is in general nonlinear
- $h_i$ are the equality constraints
- $g_i$ are the inequality constraints
- The set of equality and inequality constraints defines the feasible region
- Calculating the minimum of $-f(x)$ is the same as calculating the maximum of $f(x)$

Constraints are active if $x$ is not allowed to change infinitesimally in at least one direction
- Equality constraints are always active by definition.
- Inequality constraints can be active or inactive depending on the location of the point $x$ in the feasible region
	$g_j(x)=0 \quad$ is active
	$g_j(x)<0 \quad$ is inactive

### 2. Optimality conditions
#### Optimality condition on active constraints
**On a single active constraint:**
$x$ is a minimum if $d^T \nabla f(x) = 0$
Geometrically, the gradient at the minimum is **perpendicular** to the **tangent** directions to the constraint.
$\longrightarrow$ the gradient of the function is parallel to the gradient of the constraint:
$$
\nabla f\left(x^*\right) \| \nabla h\left(x^*\right)
$$

therefore, there must exist a scalar $\lambda$ such that
$$
\nabla f\left(x^*\right)=-\lambda \nabla h\left(x^*\right)
$$

**On multiple active constraints:**
$$\begin{aligned} \nabla f(x) & =-\sum_{i=1}^m \lambda_i \nabla h_i(x) \\ & =-\nabla h(x)^T \lambda \quad \text { at a minimum } \quad x=x^* \\ h_i(x) & =0 \quad i=1,2, \ldots, m\end{aligned}$$

### 3. Lagrangian
#### For equality constraints
The optimality condition can be recovered by defining an unconstrained minimisation problem with a new cost function $L$
$$
L\left(x, \lambda_i\right)=f(x)+\sum_{i=1}^m \lambda_i h_i(x)
$$
where $L$ is the Lagrangian and $\lambda_i$ are the **Lagrange multipliers**, which are scalars.

$x^*$ is a stationary point of the Lagrangian, $L(x)$ if
$$
\nabla L\left(x^*, \lambda\right)=0 \Longrightarrow \nabla f\left(x^*\right)+\left[\nabla h\left(x^*\right)\right]^T \lambda=0
$$
and
$$
h_i(x)=0 \quad i=, 2, \ldots, m
$$

Necessary condition for minimum:
$$
\nabla L = 0
$$

Sufficient condition for minimum:
$$
d^T \nabla^2 L(x^*)d > 0 \quad d\in \text{ space tangent to all constraints}
$$

#### For inequality constraints
The Lagrangian is
$$L\left(x, \mu_j\right)=f(x)+\sum_{j=1}^n \mu_j g_j(x)$$
$\mu_j$ are called the **KKT multipliers**.

**Karush-Kuhn-Tuck (KKT) conditions:**
If $x^*$ is stationary point of $L(x)$, then
$$
\nabla L\left(x^*, \mu_j\right)=0 \Longrightarrow \nabla f\left(x^*\right)+\left[\nabla g\left(x^*\right)\right]^T \mu=0
$$
and
$$
\begin{aligned}
\mu_j g_j(x) & =0 \\
\mu_j & \geq 0, \quad j=1,2, \ldots, n
\end{aligned}
$$
For active constraints, $g_j(x)=0$ and the constraint becomes an equality constraint.
For inactive constraints, $g_j(x)<0$ and $\mu_j=0 \rightarrow$ just optimise $f(x)$!

**With both equality and inequality constraints**
$$L(x, \lambda, \mu)=f(x)+\sum_{i=1}^m \lambda_i h_i(x)+\sum_{j=1}^n \mu_j g_j(x)$$

#### Sensitivity
$$\begin{aligned} \delta x^T \nabla f\left(x^*\right) & =-\delta x^T\left(\left[\nabla h\left(x^*\right)\right]^T \lambda+\left[\nabla g\left(x^*\right)\right]^T \mu\right) \\ \delta f\left(x^*\right) & =-\delta h\left(x^*\right)^T \lambda-\delta g\left(x^*\right)^T \mu\end{aligned}$$
Therefore, $-\lambda_i$ and $-\mu_j$ are the sensitivities of $f$ to an infinitesimal change in the constraint $h_i$ and $g_j$, respectively.

### 4. Approximated unconstrained optimization
**Motivation:** do not enforce the constraints exactly, but only approximately and controllably.
#### Penalty function
Define a new unconstrained problem
$$
q(x, \kappa)=f(x)+\kappa \sum_{i=1}^m h_i(x)^2
$$
where $\kappa$ is the penalty parameter, which is user defined, and the second term on the left hand side is a penalty function.

**Remarks:**
- For large $\kappa, h(x)$ needs to be very small and the problem is close to the constrained one 
- For small $\kappa, h(x)$ does not need to be very small and the constraint is violated to a larger degree.

#### Barrier function
For inequality constraints, $g(x) \leq 0$, we can use an asymmetric penalty function such as $\kappa \max [0, g(x)]^2$.

The feasibility is enforced exactly by using a penalty that **diverges** (i.e. grows quickly) as it gets closer to the boundary of the constraint.

Inverse barrier function:
$$
q(x, \kappa)=f(x)-\frac{1}{\kappa} \sum_j^m \frac{1}{g_j(x)}
$$

Logarithmic barrier function:
$$
q(x, \kappa)=f(x)-\frac{1}{\kappa} \sum_j^m \ln \left[-g_j(x)\right]
$$

For both, the larger $\kappa$, the closer the solutions are to the constraint boundary.