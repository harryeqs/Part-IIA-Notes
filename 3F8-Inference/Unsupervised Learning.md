
## I. Dimensionality reduction
**Goal:**
- find a low dimensional representation (**manifold**) of data
- which results in a mapping from data to manifold coordinates and back

### 1. Principal component analysis (PCA)
The data manifold are assumed to be **linear** -- PCA is a linear dimensionality reduction method
**Intuition:** finds the projection that minimises (the sum of) the square reconstruction error.

Given a dataset
$$
\mathcal{D} = \{\mathbf{x}_1, \ldots, \mathbf{x}_n\}, \text{ with } \mathbf{x}_n \in \mathbb{R}^D
$$
Divide $\mathbf{x}_n$ into projections on the orthonormal basis $\{\mathbf{u}_i\}^D_{i=1}$:
$$
\mathbf{x}_n =  
\underbrace{\sum_{i=1}^M\mathbf{x}_n^\top \mathbf{u}_i\mathbf{u}_i}_{\mathbf{x_n'}} + \underbrace{\sum_{i=M+1}^D \mathbf{x}_n^\top \mathbf{u}_i\mathbf{u}_i}_{\boldsymbol{\epsilon}_n}
$$
- $\mathbf{x}_n'$ is the **projected vector**
- $\boldsymbol{\epsilon}_n$ is the **reconstruction error**
- $\mathbf{u}_1,\ldots,\mathbf{u}_D$ are the **principal components vectors**
- $\mathbf{x}_n^\top \mathbf{u}_1,...,\mathbf{x}_n^\top \mathbf{u}_D, n = 1, \ldots, N$, are the **principal components scores**
![[pca-demo.png | center | 300]]


### 2. PCA cost function
PCA finds  $\mathbf{u}_1,\ldots,\mathbf{u}_D$ (the principal component vectors) by minimising the sum of square errors:
$$
\mathcal{L}({\{\mathbf{u}_i\}^D_{i=1}}) = \frac{1}{N}\sum_{n=1}^N \boldsymbol{\epsilon}_n^\top\boldsymbol{\epsilon}_n = \sum_{i=M+1}^{D}\mathbf{u}_i \hat{\mathbf{S}} \mathbf{u}_i
$$
where
$$
\hat{\mathbf{S}} = \frac{1}{N}\sum_{n=1}^N \mathbf{x}_n \mathbf{x}_n^\top
$$
is the covariance matrix for the data.

### 3. Lagrange multiplier
**Problem**: $\mathbf{u}_1,\ldots,\mathbf{u}_D$ should be constrained to have **unit norm** (since they are orthonormal)
**Solution:** use **Langrange multipliers**

Langrange multipliers allows solving problems with **equality constraints**.

Example: maixmise $f(x,y)$ subject to $g(x,y) = c$ (this specifies a contour line of $g(x,y)$).

At the solution, the gradients of $f(x,y)$ and $g(x,y)$ are **aligned**
**Intuition:** $f(x,y)$ can not be improved further along the contour
$\implies$ the solution should satisfy
$$
\nabla_{x,y}f(x,y) = -\lambda \nabla_{x,y} g(x,y) \text{ and } g(x,y)=c
$$

Achieved by maximising the Lagrangian function
$$
\mathcal{L}(x,y,\lambda) = f(x,y) + \lambda(g(x,y)-c)
$$
such that $\nabla_{x,y,\lambda}\mathcal{L}(x,y,\lambda) = \mathbf{0}$.

![[lagrange-multiplier.png | center | 600]]

### 4. PCA solution
The Lagrangian function is
$$
\mathcal{L}(\{\mathbf{u}_i\}_{i=M+1}^D, \lambda_{M+1},\ldots, \lambda_{D}) = \sum_{i=M+1}^D \left[\mathbf{u}_i^\top \hat{\mathbf{S}}\mathbf{u}_i + \lambda_i(1-\mathbf{u}_i^\top\mathbf{u}_i)\right]
$$
**Solution:**
$$
\hat{\mathbf{S}}\mathbf{u}_i = \lambda_i\mathbf{u}_i
$$
The $\mathbf{u}_i$ and $\lambda_i$ are **eigenvectors** and **eigenvalues** of $\hat{\mathbf{S}}$.

With this solution, the cost can be found:
$$
\mathcal{L}({\{\mathbf{u}_i\}^D_{i=1}}) = \sum_{i=M+1}^{D}\mathbf{u}_i \hat{\mathbf{S}} \mathbf{u}_i = \sum_{i=M+1}^D \lambda_i
$$
Hence:
- $\mathbf{u}_{M+1},\ldots,\mathbf{u}_D$ are eigenvectors of $\hat{\mathbf{S}}$ with $D-M$ smallest eigenvalues
- $\mathbf{u}_1,\ldots,\mathbf{u}_M$ are eigenvectors of $\hat{\mathbf{S}}$ with $M$ largest eigenvalues

Therefore, the PCA solution is also obtained by maximising $\sum_{i=1}^M \lambda_i \Longrightarrow$  maximising the **square projected data**.

## II. Clustering
### 1. K-means
#### Algorithm
$K$: number of clusters
$N$: number of data points

input: $\mathcal{D}=\left\{\boldsymbol{x}_1, \ldots, \boldsymbol{x}_N\right\}, \boldsymbol{x}_n \in \mathbb{R}$.
initialise: $\boldsymbol{m}_k \in \mathbb{R}^D$ for $k=1 \ldots K$ ==($\mathbf{m}_k$ is the cluster centre)==
repeat
	for $n=1 \ldots N$ (assignment step)
		$s_n=\underset{k}{\arg \min }\left\|\boldsymbol{x}_n-\boldsymbol{m}_k\right\|$ ==(assign the closest cluster centre)==
	endfor
	for $k=1 \ldots K$
		$\boldsymbol{m}_k=\operatorname{mean}\left(\boldsymbol{x}_n: s_n=k\right)$ ==(update step)== \[Edge case: if no data point assigned for this cluster, use the old mean from previous step\]
	endfor
until convergence ($s_n$ fixed)

#### K-means as optimisation
The cost function (a Lyupanov function)
$$
\mathcal{C}\left(\left\{s_{n, k}\right\},\left\{\boldsymbol{m}_k\right\}\right)=\sum_{n=1}^N \sum_{k=1}^K s_{n, k}\left\|\boldsymbol{x}_n-\boldsymbol{m}_k\right\|^2
$$
K-means tries to minimise the cost function $\mathcal{C}$ with respect to $\{s_{n,k}\}$ and $\{\mathbf{m}_k\}$, subject to $\sum_k s_{n,k} = 1$ and $s_{n,k} \in \{0,1\}$ (=1 if n is in cluster k)

K-means sequentially:
- minimises $\mathcal{C}$ w.r.t. $\{s_{n,k}\}$, holding $\{\mathbf{m}_k\}$ fixed (assignment step)
- minimises $\mathcal{C}$ w.r.t. $\{\mathbf{m}_k\}$, holding $\{s_{n,k}\}$ fixed (update step)

#### Pathologies of K-means
- strange results when clusters have very different shapes
- returns hard assignments
- initialisation delicate

### 2. Free energy
#### Kullback-Leibler divergence
$$
\mathcal{K} \mathcal{L}\left(p_1(z) \| p_2(z)\right)=\sum_z p_1(z) \log \frac{p_1(z)}{p_2(z)}
$$

Important properties:
- Gibb's inequality: $\mathcal{K} \mathcal{L}\left(p_1(z) \| p_2(z)\right) \geq 0$, equality at $p_1(z)=p_2(z)$ (proof via Jensen’s inequality or differentiation)
- Non-symmetric: $\mathcal{K} \mathcal{L}\left(p_1(z) \| p_2(z)\right) \neq \mathcal{K} \mathcal{L}\left(p_2(z) \| p_1(z)\right)$ – hence named divergence and not distance

#### Free energy
**Intuition:** the log-likelihood's **lower bound** when the KL divergence is maximised for a given distribution $q(\mathbf{s})$.

$$\underbrace{\mathcal{F}(q(\boldsymbol{s}), \theta)}_{\text {free-energy }}=\underbrace{\log p(\boldsymbol{x} \mid \theta)}_{\text {log-likelihood }}-\underbrace{\sum_{\boldsymbol{s}} q(\boldsymbol{s}) \log \frac{q(\boldsymbol{s})}{p(\boldsymbol{s} \mid \boldsymbol{x}, \theta)}}_{\substack{\text { KL-Divergence } \\ \mathcal{K} \mathcal{L}(q(\boldsymbol{s}) \| p(\boldsymbol{s} \mid \boldsymbol{x} \theta))}}$$
- Since KL-divergence is non-negative, $\mathcal{F}(q(\mathbf{s}),\theta) \leq \log p(\mathbf{x} \mid \theta)$
- Free-energy equal to log-likelihood when $q(\mathbf{s}) = p (\mathbf{s}\mid\mathbf{x},\theta)$

$$
\begin{aligned}
\mathcal{F}(q(s), \theta) &=\sum_s q(\boldsymbol{s}) \log \frac{(p(\boldsymbol{x} \mid \boldsymbol{s}, \theta) p(\boldsymbol{s} \mid \theta))}{q(\boldsymbol{s})} \\
&= \sum_s q(\boldsymbol{s}) \log (p(\boldsymbol{x} \mid \boldsymbol{s}, \theta) p(\boldsymbol{s} \mid \theta)) \underbrace{-\sum_s q(\mathbf{s})\log q(\mathbf{s})}_{\text {entropy}}
\end{aligned}$$

### 3. Expectation maximisation
![[expectation-maximisation.png]]
**Intuition:** sequentially update $q(\mathbf{s})$ and $\theta$ that maximise $\mathcal{F}$.

**E step (expectation):** for fixed $\theta_{t-1}$, maximise lower bound $\mathcal{F}\left(q(s), \theta_{t-1}\right)$ wrt $q(s)$. 
As log-likelihood $\log p(x \mid \theta)$ is independent of $q(\boldsymbol{s})$ this is equivalent to minimising $$\mathcal{K} \mathcal{L}\left(q(\boldsymbol{s}) \| p\left(\boldsymbol{s} \mid \boldsymbol{x}, \theta_{t-1}\right)\right)$$, so $q_t(\boldsymbol{s})=p\left(\boldsymbol{s} \mid \boldsymbol{x}, \theta_{t-1}\right)$. 
**M step (maximisation):** for fixed $q_t(\boldsymbol{s})$ maximise the lower bound $\mathcal{F}\left(q_t(s), \theta\right)$ wrt $\theta$.
Since the second term of $\mathcal{F}$ is the entropy of $q(\mathbf{s})$ independent of $\theta$, so the M step is $$
\begin{aligned}
\theta_t&=\underset{\theta}{\operatorname{argmax}} \sum_s q_t(\boldsymbol{s}) \log (p(\boldsymbol{x} \mid \boldsymbol{s}, \theta) p(\boldsymbol{s} \mid \theta))\\
&= \underset{\theta}{\operatorname{argmax}} \mathbb{E}_{q_t(\boldsymbol{s})}\left[\log p (\boldsymbol{x}, \boldsymbol{s}\mid \theta)\right]
\end{aligned}$$which is maximising expectation of log-likelihood.

**Justification:**
$$\log p\left(\boldsymbol{x} \mid \theta_{t-1}\right) \stackrel{\text { E step }}{=} \mathcal{F}\left(q_t(s), \theta_{t-1}\right) \stackrel{\text { M step }}{\leq} \mathcal{F}\left(q_t(s), \theta_t\right) \stackrel{\text { lower bound }}{\leq} \log p\left(\boldsymbol{x} \mid \theta_t\right)$$
hence each iteration can not decrease the log-likelihood.

### 4. Mixture of Gaussians
For each data point $1 \ldots N$
Sample cluster membership:
$$
p\left(s_n=k \mid \theta\right)=\pi_k,\quad \sum_{k=1}^K \pi_k=1
$$
Sample data-value given cluster membership:
$$
p\left(\boldsymbol{x}_n \mid s_n=k, \theta\right)=\mathcal{N}\left(\boldsymbol{x}_n ; \boldsymbol{m}_k, \Sigma_k\right)
$$
The likelihood is
$$
\log p (\{\mathbf{x}_n\}^N_{n=1}\mid \theta) = \sum_{n=1}^N \log \sum_{k=1}^K \pi_k \mathcal{N}(\mathbf{x}_n;\mu_k, \sigma_k^2)
$$

**Goal:** learn parameters of this model from data using the maximum-likelihood
$$\theta_{\mathrm{ML}}=\arg \max \log p\left(\left\{\boldsymbol{x}_n\right\}_{n=1}^N \mid \theta\right)$$
where
$$
\theta = \{\pi_k, \mu_k, \Sigma_k\}^K_{k=1}
$$
- $\pi_k$ is the mixing proportion
- $\mu_k$ is the cluster mean
- $\Sigma_k$ is the covariances (indicates direction)

$$p\left(x_n \mid s_n=k, \theta\right)=\frac{1}{\sqrt{2 \pi \sigma_k^2}} \mathrm{e}^{-\frac{1}{2 \sigma_k^2}\left(x_n-\mu_k\right)^2} ,\quad p\left(s_n=k \mid \theta\right)=\pi_k$$

#### E step
$$q\left(s_n=k\right)=p\left(s_n=k \mid x_n, \theta\right) \propto p\left(x_n, s_n=k \mid \theta\right)=\frac{\pi_k}{\sqrt{2 \pi \sigma_k^2}} \mathrm{e}^{-\frac{1}{2 \sigma_k^2}\left(x_n-\mu_k\right)^2}=u_{n k}$$
that is
$$
q(s_n = k) = r_{nk} = \frac{u_{nk}}{u_n} \text { where } u_n = \sum^K_{k=1} u_{nk}
$$

$r_{nk}$ is the **responsibility** that component $k$ takes for datapoint $n$.

#### M step
The lower bound is
$$\mathcal{F}(q(s), \theta)=\sum_{n=1}^N \sum_{k=1}^K q\left(s_n=k\right)\left[\log \left(\pi_k\right)-\frac{1}{2 \sigma_k^2}\left(x_n-\mu_k\right)^2-\frac{1}{2} \log \left(\sigma_k^2\right)\right]+ \text{const.}$$
The M step optimises $\mathcal{F}$ wrt the parameters $\theta$:
$$\begin{gathered}\frac{\partial \mathcal{F}}{\partial \mu_j}=\sum_{n=1}^N q\left(s_n=k\right) \frac{x_n-\mu_j}{\sigma_j^2}=0 \Rightarrow \mu_j=\frac{\sum_{n=1}^N q\left(s_n=j\right) x_n}{\sum_{n=1}^N q\left(s_n=j\right)}, \\ \frac{\partial \mathcal{F}}{\partial \sigma_j^2}=\sum_{n=1}^N q\left(s_n=j\right)\left[\frac{\left(x_n-\mu_j\right)^2}{2 \sigma_j^4}-\frac{1}{2 \sigma_j^2}\right]=0 \Rightarrow \sigma_j^2=\frac{\sum_{n=1}^N q\left(s_n=j\right)\left(x_n-\mu_j\right)^2}{\sum_{n=1}^N q\left(s_n=j\right)}, \\ \frac{\partial\left[\mathcal{F}+\lambda\left(1-\sum_k \pi_k\right)\right]}{\partial \pi_j}=\sum_{n=1}^N \frac{q\left(s_n=j\right)}{\pi_j}-\lambda=0 \Rightarrow \pi_j=\frac{1}{N} \sum_{n=1}^N q\left(s_n=j\right)\end{gathered}$$
Note that $\mu_j$ and $\sigma_j^2$ are posterior weighted centre of mass and variance.

**In summary**, MoG + EM algorithm = soft k-means clustering with non-axis aligned, non-equally weighted clusters.

**Limitations**
- MoF clusters still have simple shapes
- maximum likelihood can overfit
- coordinate ascent is often slow to converge

Backlinks:
[[Channel Coding]]
[[Probability]]
