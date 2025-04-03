## I. Revision of feedback control
### 1. The standard feedback loop
![[standard-feedback-loop.png]]
For multivariate systems, return ratio depends on where you break the loop -- the order matters!

### 2. Sensitivity and complementary sensitivity

Let $L(s)$ be the open loop transfer function (or return ratio): $L(s) = H(s)G(s)K(s)$

**Complementary sensitivity:**
$$
T(s) = \frac{L(s)}{1 + L(s)}
$$
(Multivariate case: $T(s) = [I + L(s)]^{-1}L(s)$)
$$\bar{y}=T H^{-1} \bar{r}=-T \bar{n} \quad(\bar{n}=\text { sensor noise }) $$

$T \approx 1 \Rightarrow$ good "tracking" but no noise filtering.


**Sensitivity:**
$$
S(s) = \frac{1}{1+L(s)}
$$
(Multivariate case: $S(s) = [I+L(s)]^{-1}$)
$$
\bar{e}=S \bar{r}, \quad \bar{y}=G S \bar{d}_i+S \bar{d}_o, \quad S=\frac{d T / T}{d G / G}
$$

Small $|S| \Rightarrow$ feedback is beneficial.

Hence trade-off:
- Small $|S(j \omega)|$ at low frequencies
- Small $|T(j \omega)|$ at high frequencies.

### 3. Steady-state error
![[steady-state-error.png | center | 500]]
### 4. The Nyquist stability theorem
- Plot $L(j \omega)$ on the Argand diagram, for $-\infty<\omega<+\infty$ - the Nyquist plot.
- The closed loop is stable if and only if the Nyquist plot encircles the point $(-1+j 0) \; p_u$ times counterclockwise, where $p_u$ is the number of **unstable poles** of $L(s)$.

## II. The root-locus method

**Motivation:** find the location of poles as the controller $k$ varies.

Closed loop poles are the roots of the closed-loop characteristic equations (CLCE):
$$
1 + kG(s) = 0
$$
where
$$G(s)=\frac{n(s)}{d(s)}=\frac{c\left(s-z_1\right)\left(s-z_2\right) \ldots\left(s-z_m\right)}{\left(s-p_1\right)\left(s-p_2\right) \ldots\left(s-p_n\right)}$$
### 1. The angle condition for poles
Suppose that $s_0$ (a test point) is on the root-locus:
$$ 1+k G\left(s_0\right)=0 \Rightarrow G\left(s_0\right)=-\frac{1}{k} $$
Hence the angle condition for $s_0$ to be on the root-locus is:
$$\angle G\left(s_0\right)=(2 \ell+1) \pi \rightarrow \text{ real and negative}$$
which means that (assuming $c>0$)
$$\sum_{i=1}^m \angle\left(s_0-z_i\right)-\sum_{i=1}^n \angle\left(s_0-p_i\right)=(2 \ell+1) \pi$$
### 2. Finding gain from the root-locus plot
$$k=\frac{1}{\left|G\left(s_0\right)\right|}=\frac{1}{|c|} \times \frac{\left|s_0-p_1\right| \times\left|s_0-p_2\right| \times \cdots \times\left|s_0-p_n\right|}{\left|s_0-z_1\right| \times\left|s_0-z_2\right| \times \cdots \times\left|s_0-z_m\right|}$$
### 3. Root-locus plot construction rules
**Rule 1:** The root-locus diagram is symmetric with respect to the real axis and consists of $n$ branches.

**Proof of Rule 1:** If $G(s)=n(s) / d(s)$ then $1+k G(s)=0 \Longleftrightarrow n(s)+k d(s)=0$, which is a real degree $n$ polynomial. So it has $n$ roots and any complex solutions occur as **conjugate pairs**.


**Rule 2:** For $k=0$ the $n$ branches start at the open loop poles $p_i$. As $k \rightarrow \infty, m$ branches tend to the zeros $z_i$ and $n-m$ branches tend to infinity.

**Proof of Rule 2:** $$ d\left(s_0\right)+k n\left(s_0\right)=0 $$
So if $k=0$ then $d\left(s_0\right)=0 \Rightarrow$ Branches start at poles. 

Also, for any fixed $k$, $$\frac{1}{k} d\left(s_0\right)+n\left(s_0\right)=0 $$So, as $k \rightarrow \infty$ the finite roots tend to zeros (i.e. finite branches end at zeros). There can be at most $m$ of them.


**Rule 3:** Points on the real axis which lie to the left of an **odd number of poles and zeros** are on the root-locus.

**Proof of Rule 3:**
Consider a point $s_0$, a pole $p_i$, and a zero $z_i$, all on the real axis.
$$
\angle\left(s_0-p_i\right)=\left\{\begin{array}{l}
0 \text { if } s_0>p_i \\
\pi \text { if } s_0<p_i
\end{array}\right.
$$
And the same holds for $\angle(s_0 - z_i)$.


**Rule 4:** The breakaway points are those points on the root-locus for which $\frac{d}{d s} G(s)=0$.

**Proof of Rule 4:**
$$
\begin{aligned}
& \text { repeated roots at } s=s_0 \\
& \qquad 1+k G(s)=\left(s-s_0\right)^2 \times(\cdots) \\
& \Rightarrow \frac{d kG}{d s}=2\left(s-s_0\right) \times(\cdots)+\left(s-s_0\right)^2 \frac{d}{d s}(\cdots) \\
& \Rightarrow \frac{d G}{d s}=0 \text { at } s=s_0
\end{aligned}
$$

**Rule 5:** As $k \rightarrow \infty$, the $n-m$ branches which tend to infinity do so along straight line asymptotes at angles $(2 \ell+1) \pi /(n-m)$ to the + ve real axis $(\ell=0, \ldots, n-m-1)$, and emanate from the point
$$
\frac{\sum_{i=1}^n p_i-\sum_{i=1}^m z_i}{n-m}
$$

**Proof of Rule 5:**
$$
\begin{aligned}
-k=\frac{1}{L(s)}&=\frac{\left(s-p_1\right)\left(s-p_2\right) \cdots}{c\left(s-z_1\right)\left(s-z_2\right) \cdots} \\
-k c&=\frac{s^n-\sum p_i s^{n-1}+\cdots}{s^m-\sum z_i s^{m-1}+\cdots} \\
& \approx s^{n-m} \frac{\left(1-\sum p_i / s\right)}{\left(1-\sum z_i / s\right)} \quad \text { for large } s \\
& \approx s^{n-m}\left(1-\sum p_i / s\right)\left(1+\sum z_i / s\right) \\
& \approx s^{n-m}\left(1-\left(\sum p_i / s-\sum z_i / s\right)\right) \\
& \approx s^{n-m}\left(1-\frac{\left(\sum p_i / s-\sum z_i / s\right)}{n-m}\right)^{n-m} \\
&=\left(s-\frac{\left(\sum p_i-\sum z_i\right)}{n-m}\right)^{n-m} \\
& \Longrightarrow \angle\left(s-\frac{\left(\sum p_i-\sum z_i\right)}{n-m}\right) \rightarrow \frac{(2 \ell+1) \pi}{n-m}
\end{aligned}
$$

### 4. Root-locus for negative $k$
If either $k$ or $c$ are negative then we can write the angle condition as
$$
\sum_{i=1}^m \angle\left(s_0-z_i\right)-\sum_{i=1}^n \angle\left(s_0-p_i\right)=(2 \ell) \pi \quad \text { (real and positive) }
$$

In this case,
- Rules 1, 2, 4 remain unchanged.
- Rule 3: Replace 'odd' by 'even'.
- Rule 5: Angles of asymptotes become $2 \ell \pi /(n-m)$. (Points from which asymptotes emanate remain unchanged.)

### 5. Parameter variation
Put the closed-loop characteristic equation into the form 
$$1 + \lambda L(s) = 0$$
where $\lambda$ is the parameter that is varying.

## III. The Routh-Hurwitz criterion
The Routh-Hurwitz criterion tests whether a polynomial has any roots with non-negative real part – hence tests for asymptotic stability.

The closed-loop characteristic equation
$$
1 + G(s)K(s) = 0
$$
has the same root as
$$
d_G(s)d_K(s) + n_G(s)n_K(s) = 0
$$
which is a polynomial.

Consider the polynomial (assume $a_0>0$ ):
$$
a_0 s^n+a_1 s^{n-1}+a_2 s^{n-2}+\cdots+a_{n-1} s+a_n
$$

A **Routh array** can be constructed for arbitrary $n$.
For $n=2,3,4$ simplifies as follows:
These are in Electrical and Information Data Book
All the roots of have negative real parts if and only if:
$$
\begin{aligned}
& n=2: \quad a_i>0, \quad \text { No other conditions } \\
& n=3: \quad a_i>0, \quad a_1 a_2>a_0 a_3 \\
& n=4: \quad a_i>0, \quad a_1 a_2 a_3>a_0 a_3^2+a_4 a_1^2
\end{aligned}
$$

