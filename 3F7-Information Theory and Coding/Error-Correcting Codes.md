## I. Binary linear block codes
### 1. Block code
An $(n,k)$ binary block code maps every block of $k$ data bits into a length $n$ binary codeword.
- the **rate** $R$ of the code is $R = \frac{k}{n}$
- the size of the code (= number of codewords) is $M = 2^k$

**Goal:** Design a good code that has
- rate $R$ as high as possible
- low probability of decoding error
- computationally efficient to encode and decode

### 2. Minimum distance of a code

![[hamming-distance.png | center | 500]]

### 3. Optimal decoding of a block code
Given a block code $\mathcal{B}$ with codewords $\left\{\underline{c}_1, \ldots, \underline{c}_M\right\}$, the optimal decoder is the one that **minimises** the probability of decoding error. 
The optimal decoder given the received length-$n$ sequence $\underline{y}$ is the max-likelihood decoder given by: 
$$
\text { Decode } \underline{\hat{c}}=\arg\max _{\underline{c} \in\left\{\underline{c}_1, \ldots,,_M\right\}} \operatorname{Pr}(\underline{y} \mid \underline{c})
$$
Assumptions:
- channel described by $P_{Y \mid X}$, 
- the input bits/messages corresponding to the codewords are equally likely
#### Optimal decoding on the BSC
Given that codeword $\underline{c}$ was transmitted and $\underline{y}$ was received
- the number of channel errors is $d(\underline{y}, \underline{c})$
- the number of correctly received bits is $\underline{y}$ is $n-d(\underline{y}, \underline{c})$. 
Hence
$$
\operatorname{Pr}(\underline{y} \mid \underline{c})=p^{d(\underline{y}, \underline{c})}(1-p)^{n-d(\underline{y}, \underline{c})}=(1-p)^n\left(\frac{p}{1-p}\right)^{d(\underline{y}, \underline{c})}
$$

Thus, for $p<\frac{1}{2}$, the optimal decoding rule is:
$$
\text { Decode } \underline{\hat{c}}=\arg \min _{\underline{c} \in\left\{\underline{c}_1, \ldots, \underline{c}_M\right\}} d(\underline{y}, \underline{c})
$$
i.e., the optimal decoder for BSC **picks the codeword closest in Hamming distance** to $\underline{y}$.

![[bsc-decoder.png | center | 400]]
**Note:** from the diagram, it is shown that we can successfully correct any pattern of $t$ errors if $t \leq \left\lfloor \frac{d_{min} - 1}{2} \right\rfloor$, such that the spheres are not overlapping.

### 4. Linear block codes
A $(n, k)$ linear block code (LBC) is defined in terms of $k$ length-$n$ binary vectors, say $\underline{g}_1, \ldots, \underline{g}_k$. 
A sequence of $k$ data bits, say, $\underline{x}=\left(x_1, \ldots, x_k\right)$ is mapped to a length-$n$ codeword $\underline{c}$ as follows:
$$
\underline{c}=x_1 \underline{g}_1+x_2 \underline{g}_2+\ldots+\ldots+x_k \underline{g}_k .
$$

This can be compactly written as
$$
\underline{c}=\underline{x} G, \quad \text { where } G=\left[\begin{array}{c}
\underline{g}_1 \\
\underline{g}_2 \\
\vdots \\
g_k
\end{array}\right]
$$
- The $k \times n$ matrix $G$ is called a **generator matrix** of the code
- **$k$ is called the code dimension, $n$ is the block length**
The matrix multiplication is over the binary field:
$$
\text{For} \;x \in\{0,1\}: \quad x+x=0, x+\bar{x}=1, \quad x \cdot 0=0, x \cdot 1=x
$$
**Note:** 
- all the vectors are **row vectors**.
- the generator matrix for a code (i.e. a set of codewords) is not unique

#### Systematic generator matrices
A **systematic generator matrix** takes the form:
$$
G=\left[\begin{array}{l|l}\mathrm{I}_k & \mathrm{P}\end{array}\right]
$$
For a systematic $G=\left[\begin{array}{l|l}\mathrm{I}_k & \mathrm{P}\end{array}\right]$, the codeword corresponding to length- $k$ data vector $\underline{x}$ is
$$
\underline{c}=\underline{x} G=\underline{x} \cdot\left[\begin{array}{l|l}
\mathrm{I}_k & \mathrm{P}]=[\underline{x} \mid \underline{x} \mathrm{P}]
\end{array}\right.
$$
**Note:** In a systematic code, the length-$n$ codeword consists of the $k$ data bits $\underline{x}$, followed by $(n-k)$ parity bits $\underline{x}P$.

Given any generator matrix, the systematic version can be found by:
1. Row operations
2. Swap columns (which changes the components of the codeword)

#### LBCs as subspaces
Let $\mathcal{C}$ be an $(n, k)$ LBC with codewords $\left\{c_0, \ldots, c_{M-1}\right\}$.
$\mathcal{C}$ is a **subspace** of $\{0,1\}^n$, i.e., it is closed under vector addition and scalar multiplication.

To proof: show that
1. For any codewords $\underline{c}_i, \underline{c}_j \in \mathcal{C}, \underline{c}_i+\underline{c}_j$ is also in $\mathcal{C}$, 
2. If $\underline{c} \in \mathcal{C}$, then $0 \cdot \underline{c}$ and $1 \cdot \underline{c}$ are in $\mathcal{C}$.

**Note:** 
- sum of any two codewords is also in a codeword
- the all-zero codeword $\underline{0}$ always belong to $\mathcal{C}$

### 5. The parity check matrix
Define $\mathcal{C}^{\perp}$: The orthogonal complement of $\mathcal{C}$ – the set of all vectors in $\{0,1\}^n$ that are orthogonal to each vector in $\mathcal{C}$.
$\mathcal{C}^{\perp}$ is a subspace: if $\underline{u}, \underline{v} \in \mathcal{C}^{\perp}$, then for any $\underline{c} \in \mathcal{C}$, $\underline{c} \,\underline{u}^T=0$ and $\underline{c} \,\underline{v}^T=0 \Rightarrow \underline{c}(\underline{u}+\underline{v})^T=0 \Rightarrow(\underline{u}+\underline{v}) \in \mathcal{C}^{\perp}$

Since $\mathcal{C}$ has dimension $k$, can be shown that $\mathcal{C}^{\perp}$ has dimension $(n-k)$.
$\implies$ we can find a basis $\left\{\underline{h}_1, \ldots, \underline{h}_{n-k}\right\}$ for $\mathcal{C}^{\perp}$, expressed as
$$
H=\left[\begin{array}{c}
\underline{h}_1 \\
\underline{h}_2 \\
\vdots \\
\underline{h}_{n-k}
\end{array}\right]
$$

- the $(n-k) \times n$ matrix $H$ is called the **parity check** matrix 
- each codeword $\underline{c} \in \mathcal{C}$ is orthogonal to each row of $H$, i.e.,
$$
\underline{c} H^T=\underline{0} \Rightarrow \underline{x} G H^T=\underline{0} \text { for all } \underline{x} \Rightarrow G H^T=0
$$
**To find H:**
Given a systematic generator matrix $G=\left[I_k \mid P\right]$, then take
$$
H=\left[\mathrm{P}^T \mid \mathrm{I}_{n-k}\right]
$$
Recall that P is $k \times(n-k)$. Hence $\mathrm{P}^T$ is $(n-k) \times k$.

**Note:**
- the parity matrix $H$ is a complete description of the linear code (just like $G$)
- the codewords are precisely the binary sequences $\underline{c} \in\{0,1\}^n$ that satisfy $$ \underline{c} H^T=0 $$ i.e., the binary dot-product of a codeword with each row of $H$ is 0 .

### 6. Minimum distance of an LBC
The Hamming distance between two binary vectors $\underline{u}, \underline{v}$ can be expressed as
$$
d(\underline{u}, \underline{v})=w t(\underline{u}+\underline{v})
$$
where $wt$ refers the Hamming weight of the vector, i.e., the number of ones in it.

Recall that the minimum distance of a code is
$$
d_{\text {min }}=\min _{i \neq j} d\left(\underline{c}_i, \underline{c}_j\right)=\min _{i \neq j} w t\left(\underline{c}_i+\underline{c}_j\right)
$$

For any two codewords $\underline{c}_i, \underline{c}_j$ of an LBC, note that $\underline{c}_i+\underline{c}_j$ is also a codeword, say, $\underline{c}_k$. Therefore
$$
d_{\min }=\min _{i \neq j} w t\left(\underline{c}_i+\underline{c}_j\right)=\min _{\underline{c}_k \neq \underline{0}} w t\left(\underline{c}_k\right) .
$$
**The minimum distance of an LBC equals the minimum Hamming weight among the non-zero codewords.**

This leads to a useful property of the parity check matrix:
Let $\mathcal{C}$ be an linear block code with parity check matrix $H$. The minimum distance of $\mathcal{C}$ is the **smallest number of column**s of $H$ that sum to $\underline{0}$. (for proof see examples paper 3)

**Note:**
- $d_{min}$ gives only gives the **guaranteed** error correction capability of the code, which may be pessimistic
- there may still be many error patterns of weight $> \lfloor (d_{min}-1) /2\rfloor$ that can be corrected (just not guaranteed that every pattern can be corrected)
- so the code may be able to correct many more error patterns

## II. Low density parity check (LDPC) codes for the binary erasure channel

**Note:** 
- recall that the capacity of the BEC is $(1-\varepsilon)$
- the goal is to construct linear block codes with rate close to this capacity & have fast decoding algorithms & low probability of decoding error
### 1. Linear codes for the BEC
To recover erased bits in $\underline{y}$, use the property of a codeword $\underline{c}H^\top = 0$

#### Method 1: Gaussian-elimination
Outline:
- contribution to dot products form known bits of $\underline{y}$ can be computed first and moved to RHS
- solve for linear variables (erased bits) from linear equations
- Use matrix inversion / Gaussian-elimination

The complexity of this decoder is $n^3$.

#### Method 2: Iterative decoding
Outline:
- look for a row in $H^\top$ which has exactly one 1 among the erased locations (note that the dimension of the row = dimension of the codeword)
- setting the binary dot-product of $\underline{y}$ with this row = 0 to find the erased bit at the location where there is an 1
- update the bit and repeat the steps above

Iterative decoding won't always work $\rightarrow$ it is possible whenever the effective matrix can be triangulated by just row swaps (whereas Gaussian elimination need linear combination of rows)

For this to happen for most erasure patterns, the parity check matrix needs to have a **low density of ones.**

### 3. Low-density parity check (LDPC) matrix
#### Regular vs irregular LDPC codes
In a regular LDPC code, all rows have the **same weight**, and all columns have the same weight.
The weight of a row/column is the number of ones in the row/column.
#### Regular LDPC codes
![[ldpc-example.png | center | 500]]
In a regular $(n, k)$ LDPC code: 
- Each of the $n$ codeword bits is involved in $d_v$ parity check equations ('v' $\rightarrow$ variable)
- Each of the $(n-k)$ parity check equations involves $d_c$ code bits. ('c' $\rightarrow$ check) 

#### The design rate
(derived by considering the number of 1s is $d_v n = d_c(n-k)$)
The design rate of a regular LDPC code is
$$
\frac{k}{n} = 1 - \frac{d_v}{d_c}
$$
The design rate is the true code rate if the rows of the parity check matrix are linearly independent. (otherwise there are redundant rows which can be removed from the parity check matrix)

#### Factor graph of a linear code
![[factor-graph.png | center | 500]]
### 4. Iterative decoding as message passing
![[message-passing.png | center | 500]]
In each step of message passing (it is a class of iterative algorithms):
1. each variable node $v$ sends a message to each check node $c$ that it is connected to (blue arrows in the left figure)
2. each check node $c$ sends a message to each variable node $v$ that it is connected to (red arrows in the right figure)

These messages are denoted by $\left\{m_{v c}\right\}$ and $\left\{m_{c v}\right\}$, respectively, for $v \in\left\{v_1, v_2 \ldots,\right\}$ and $c \in\left\{c_1, c_2, \ldots\right\}$
- The message $m_{c v}$ (red arrow in left figure) is a function of the messages $\left\{m_{v^{\prime} c}\right\}$ coming in from variable nodes $v^{\prime}$ connected to $c$ (excluding $v$ ).
- The message $m_{v c}$ (blue arrow in right figure) is a function of the messages $\left\{m_{c^{\prime} v}\right\}$ coming in from check nodes $c^{\prime}$ connected to $v$ (excluding $\left.c\right)$.

#### Message passing rule
In the first step:
- $m_{vc}$ is the channel output corresponding to bit $v: (0, 1, \text{or ?})$
- all the check nodes $c$ send $m_{cv} = ?$

In each subsequent step:
![[message-passing-rule-bec.png | center | 500]]
**Summary:**
In each step of the message passing decoder:
- $m_{vc}$: variable node $v$ tells check node $c$ its best guess of its own value (based one the other incoming messages from the other check nodes)
- $m_{cv}$: check node $c$ tells variable node $v$ what it thinks the value of $v$ should be (based on the other in coming messages from the other variable nodes)

**Complexity:**
The complexity of the message passing decoder is proportional to the (# of edges in the graph)(# of iterations).
(# of edges in the graph = # 1s in the LDPC matrix $H$)
$\implies$ low density of ones in $H$ $\longrightarrow$ low complexity of decoder

### 5. Degree distributions
![[degree-distributions.png | center | 500]]
#### Node-perspective definition
The degree distributions of the variable and check nodes are often written in terms of the following **"node-perspective"** polynomials: 
$$
L(x)=\sum_{i=1}^{d_{v, \max }} L_i x^i, \quad R(x)=\sum_{i=1}^{d_{c, \text { max }}} R_i x^i
$$

- The average degree of a variable node is 
$$ 
\bar{d}_v=\sum_{i=1}^{d_{v, \text { max }}} i L_i=L^{\prime}(1) 
$$
- The average degree of a check node is 
$$
\bar{d}_c=\sum_{i=1}^{d_{c, \max }} i R_i=R^{\prime}(1) 
$$ 
- The total number of edges in the graph (number of ones in $H)$ is $\bar{d}_v n=\bar{d}_c(n-k)$. 

Hence the design rate of the code is 
$$
\frac{k}{n}=1-\left(\bar{d}_v / \bar{d}_c\right)
$$

#### Edge-perspective definition
$\lambda_i$ : Fraction of edges connected to variable nodes of degree $i$, i.e., the fraction of ones in $H$ in columns of weight $i$.
$\rho_i$ : Fraction of edges connected to check nodes of degree $i$, i.e., the fraction of ones in $H$ in rows of weight $i$.

The edge-perspective polynomials are
$$
\lambda(x)=\sum_{i=1}^{d_{v, \max }} \lambda_i x^{i-1}, \quad \rho(x)=\sum_{i=1}^{d_{c, \max }} \rho_i x^{i-1}
$$

The avg. variable node degree and avg. check node degree satisfy
$$
\bar{d}_v=\left(\int_0^1 \lambda(x) d x\right)^{-1}, \text { and } \bar{d}_c=\left(\int_0^1 \rho(x) d x\right)^{-1}
$$

Hence the design rate can also be expressed as
$$
\frac{k}{n}=1-\left(\bar{d}_v / \bar{d}_c\right)=1-\left(\int_0^1 \rho(x) d x \;/ \int_0^1 \lambda(x) d x\right)
$$
### 6. Density evolution
#### Regular LDPC codes
$p_t$: Probability that an outgoing $v \rightarrow c$ message is a "?" in step $t$
$q_t$: Probability that an outgoing $c \rightarrow v$ message is a "?" in step $t$
($q_0 = 1$ as the first $c \rightarrow v$ messages are all erasures, and $p_0 = \varepsilon$)

**Key assumption:** 
For $t \geq 1$, assume all the incoming messages at each variable / check node are **independent**.
(strictly true only if there are no cycles in the factor graph – the graph is a tree, but independence assumption is usually close enough for large $n$ (need to avoid short cycles))

$m_{vc}$: The probability that the variable AND all the $d_v-1$ incoming messages being erased is:
$$
p_t=\varepsilon\left(q_{t-1}\right)^{d_v-1}
$$
(in this case, $v = ?$ and ALL the incoming messages $m_{c'v} = ?$)

$m_{cv}$: The probability that at least one of the $d_c-1$ incoming messages is erased is:
$$
q_t=1-\left(1-p_t\right)^{d_c-1}
$$
(note that $m_{cv} = ?$ when at least one of the incoming messages $m_{v'c} = ?$)

Combining the two equations, we get:
$$
p_t=\varepsilon\left(1-\left(1-p_{t-1}\right)^{d_c-1}\right)^{d_v-1}
$$

**This density evolution recursion predicts the fraction of erased bits at the end of each step $t$.**

The density evolution gives an threshold $\varepsilon^{MP}$ above which $p_t$ does not converge to 0 with growing $t$.
The Shannon limit, i.e. the maximum possible $\varepsilon$ for reliable decoding with any rate $R$ code is $\varepsilon^* = 1 - R$ (recall that capacity of BEC $\mathcal{C} = 1 - \varepsilon$).
$\longrightarrow$ the aim is to **make the threshold $\varepsilon^{MP}$ close to the Shannon limit $\varepsilon^*$**

#### Irregular LDPC codes
Irregular LDPC provides more flexibility in the code design and can be optimised to get the threshold closer to the Shannon limit.

Consider the probabilities using the **edge-perspective degree distributions** $\lambda(x)$ and $\rho(x)$.

$m_{vc}$: The probability that an outgoing message from a variable node with deg. $i$ is erased is $p_{t, i}=\varepsilon q_{t-1}^{i-1}$.
Hence the probability that a randomly picked edge has $m_{v c}= ?$  is $$ p_t=\sum_i \lambda_i p_{t, i}=\varepsilon \sum_i \lambda_i q_{t-1}^{i-1}=\varepsilon \lambda\left(q_{t-1}\right) $$
$m_{cv}$: The probability that an outgoing message from check node with deg. $j$ is erased is $q_{t, j}=1-\left(1-p_t\right)^{j-1}$. 
Hence the probability that a randomly picked edge has $m_{c v}= ?$  is $$ q_t=\sum_j \rho_j q_{t, j}=1-\sum_j \rho_j\left(1-p_t\right)^{j-1}=1-\rho\left(1-p_t\right) $$
Combining the two equations, we get the density evolution equation for a $(\lambda(x), \rho(x))$ ensemble:
$$
p_t=\varepsilon \lambda\left(1-\rho\left(1-p_{t-1}\right)\right) .
$$

## III. Low density parity check (LDPC) codes for general binary input channels

### 1. Optimal decoding: block-wise vs bit-wise
Optimal decoding rule to minimise the probability of block (codeword) decoding error:
$$
\hat{\hat{c}}=\underset{\underline{c} \in \mathcal{C}}{\arg \max } P(\underline{c} \mid \underline{y}) \stackrel{(a)}{=} \underset{\underline{c} \in \mathcal{C}}{\arg \max } P(\underline{y} \mid \underline{c})
$$
where (a) holds provided the codewords are all equally likely $\rightarrow P(\underline{c})$ is constant, while
$$
P(\underline{c} \mid \underline{y})=\frac{P(\underline{c}) \cdot P(\underline{y} \mid \underline{c})}{P(\underline{y})}
$$

Optimal decoding rule to minimise the probability of bit decoding error, i.e., the probability of decoding bit $c_j$ wrongly for $j \in\{1, \ldots, n\}$:
$$
\hat{c}_j=\underset{c_j \in\{0,1\}}{\arg \max } P\left(c_j \mid \underline{y}\right) \quad \text { for } j=1, \ldots, n
$$
Both the block-wise and bit-wise optimal decoding are hard.
### 2. Message passing decoding (belief propagation)
![[message-passing-decoding.png | center | 500]]
**Motivation:** find a message algorithm that approximately computes the desired bit-wise **a posteriori probabilities (APPs)** $P(c_j = 0 | \underline{y})$.

In each iteration, the message passing decodes computes:
**Variable-to-check messages:**
- Each v-node $j$ sends a message $m_{j i}$ to each c-node $i$ that it is connected to.
- **Significance:** $m_{j i}(0)$ is an updated estimate of the posterior probability (or belief) that **the code bit $c_j=0$**.
- $m_{j i}$ is computed using the channel evidence $P\left(c_j \mid y_j\right)$ and all the incoming messages into $j$ except from c-node $i$.

**Check-to-variable messages:**
- Each c-node $i$ sends a message $m_{i j}$ to each v-node $j$ that it is connected to.
- **Significance:** $m_{i j}(0)$ is an updated estimate of the probability that the **parity check equation $i$ is satisfied** when $c_j=0$.
- $m_{i j}$ is computed using all the incoming messages into $i$ except from v-node $j$.

**Assumption:** the incoming messages at each node are independent!!!

#### Variable-to-check messages
![[v-to-c.png | center | 500]]
Using Bayes theorem (and assuming independence of incoming messages):
$$
m_{j i}(0)=\frac{a_0}{a_0+a_1}, \quad m_{j i}(1)=\frac{a_1}{a_0+a_1}
$$
where:
$$
\begin{aligned}
a_0 & =\operatorname{Pr}\left(c_j=0 \;\& \text { checks } i_1, i_2, i_3 \text { are all satisfied } \mid y_j\right) \\
& =P\left(c_j=0 \mid y_j\right) m_{i_1 j}(0) m_{i_2 j}(0) m_{i_3 j}(0)
\end{aligned}
$$
$$
\begin{aligned}
a_1 & =\operatorname{Pr}\left(c_j=1 \;\& \text { checks } i_1, i_2, i_3 \text { are all satisfied } \mid y_j\right) \\
& =P\left(c_j=1 \mid y_j\right) m_{i_1 j}(1) m_{i_2 j}(1) m_{i_3 j}(1)
\end{aligned}
$$

At the first iteration ($t = 1$), $m_{ji}(0) = P(c_j = 0 \mid y_j)$
For $t > 1$:
$$
\begin{aligned} & m_{j i}(0)=\frac{P\left(c_j=0 \mid y_j\right) \prod_{i^{\prime} \backslash i} m_{i^{\prime} j}(0)}{P\left(c_j=0 \mid y_j\right) \prod_{i^{\prime} \backslash i} m_{i^{\prime} j}(0)+P\left(c_j=1 \mid y_j\right) \prod_{i^{\prime} \backslash i} m_{i^{\prime} j}(1)}, \\ & m_{j i}(1)=1-m_{j i}(0)\end{aligned}
$$

#### Check-to-variable messages
![[c-to-v.png | center | 300]]
$$
\begin{aligned} m_{i j}(0) & =m_{j_1 i}(0) m_{j_2 i}(0) m_{j_3 i}(0)+m_{j_1 i}(1) m_{j_2 i}(1) m_{j_3 i} (0) \\ & +m_{j_1 i}(1) m_{j_2 i}(0) m_{j_3 i} (1) +m_{j_1 i}(0) m_{j_2 i}(1) m_{j_3 i}(1) \end{aligned}
$$
$m_{ij}(0)$ is obtained by multiplying the incoming $m_{j'i}$ such that an **even number** of these are evaluated at 1 and the rest at 0 (thus summing to 0, satisfying the parity).

Consider a sequence of $M$ independent binary digits $b_1, \ldots, b_M$ such that $P\left(b_k=1\right)=p_k$ for all $k$. Then the probability that the sequence $\left(b_1, \ldots, b_M\right)$ contains an even number of ones is
$$
\frac{1}{2}+\frac{1}{2} \prod_{k=1}^M\left(1-2 p_k\right)
$$
(Can be proofed by induction)

Hence,
$$
\begin{aligned}
& m_{i j}(0)=\frac{1}{2}+\frac{1}{2} \prod_{j^{\prime} \backslash j}\left(1-2 m_{j^{\prime} i}(1)\right), \\
& m_{i j}(1)=1-m_{i j}(0) .
\end{aligned}
$$
#### Belief propagation
The message passing algorithm above is often called the sum-product algorithm or belief propagation (as the beliefs of each code being 0/1 are updated in each step).

### 3. A posteriori probabilities
The a posteriori probabilities (APPs) $P(c_j \mid y_j)$ can be calculated using Bayes rule and the channel transition probabilities
$$
P\left(c_j \mid y_j\right)=\frac{P\left(c_j\right) P\left(y_j \mid c_j\right)}{P\left(y_j\right)}
$$
1. $\operatorname{BEC}(\varepsilon): y_j \in\{0,1, ?\}$ 
$$ 
P\left(c_j=0 \mid y_j\right)= \begin{cases}1, & \text { if } y_j=0 \\ 0, & \text { if } y_j=1 \\ 1 / 2, & \text { if } y_j=?\end{cases} 
$$
2. $\operatorname{BSC}(p): y_j \in\{0,1\}$ 
$$ 
P\left(c_j=0 \mid y_j\right)=\left\{\begin{array}{cc} 1-p, & \text { if } y_j=0, \\ p, & \text { if } y_j=1, \end{array}\right. 
$$
3. B-AWGN channel: $y_j \in \mathbb{R}$  ($X \in \{-1, +1\}$, 0 code-bit $\rightarrow X = +1$)
$$ \begin{aligned} P\left(c_j=0 \mid y_j\right) & =P\left(X_j=+1 \mid y_j\right) \\ & =\frac{p_{Y \mid X}\left(y_j \mid+1\right) P_X(+1)}{p_{Y \mid X}\left(y_j \mid+1\right) P_X(+1)+p_{Y \mid X}\left(y_j \mid-1\right) P_X(-1)} \\ & =\frac{\frac{1}{\sqrt{2 \pi \sigma}} e^{-\frac{\left(y_j-1\right)^2}{2 \sigma^2}} \cdot 1 / 2}{\frac{1}{\sqrt{2 \pi} \sigma} e^{-\frac{\left(y_j-1\right)^2}{2 \sigma^2}} \cdot 1 / 2+\frac{1}{\sqrt{2 \pi \sigma}} e^{-\frac{\left(y_j+1\right)^2}{2 \sigma^2}} \cdot 1 / 2} \\ & =\frac{1}{1+e^{\frac{-2 y_j}{\sigma^2}}} \end{aligned} 
$$
In all the cases, $P(c_j = 1 \mid y_j) = 1 - P(c_j = 0 \mid y_j)$.

### 4. Log-domain message passing
**Motivation:** multiplication of probabilities can be numerically unstable $\longrightarrow$ implement with log-likelihood ratios, turn most of the multiplications into additions.

$$
L_{j i}:=\ln \frac{m_{j i}(0)}{m_{j i}(1)}, \quad L_{i j}:=\ln \frac{m_{i j}(0)}{m_{i j}(1)}
$$

To update the messages, we also need the channel evidence in LLR form:
$$
L\left(y_j\right):=\ln \frac{P\left(c_j=0 \mid y_j\right)}{P\left(c_j=1 \mid y_j\right)}=\ln \frac{P\left(c_j=0\right) P\left(y_j \mid c_j=0\right)}{P\left(c_j=1\right) P\left(y_j \mid c_j=1\right)}=\ln \frac{P\left(y_j \mid c_j=0\right)}{P\left(y_j \mid c_j=1\right)}
$$
The LLR-based belief propagation updates are given below, where $j$ denotes v-node and $i$ denotes c-node
![[llr-message-passing.png | center | 500]]
#### Algorithm termination
The algorithm is run for a pre-determined number of steps, and the final LLRs for each code bit are computed as
$$
L_j=L\left(y_j\right)+\sum_{i^{\prime}} L_{i^{\prime} j}, \quad \text { for } j=1, \ldots, n
$$
The final decoded codeword is $\underline{\hat{c}}=\left(\hat{c}_1, \ldots, \hat{c}_n\right)$ where 
$$ 
\hat{c}_j= \begin{cases}0 & \text { if } L_j \geq 0 \\ 1, & \text { if } L_j<0\end{cases} 
$$
**To improve complexity**, "min-sum" algorithms can be used.

Backlinks:
[[Information Theory Fundamentals and Source Coding]]
[[Channel Coding]]
