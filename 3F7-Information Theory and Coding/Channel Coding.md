## I. Relative entropy and mutual information
### 1. Relative entropy
#### Definition
The relative or the Kullback-Leibler (KL) divergence between two pmfs $P$ and $Q$ is:
$$
D(P\mid\mid Q) = \sum_{x\in \mathcal{X}}P(x)\log\frac{P(x)}{Q(x)}
$$
- it is a measure of 'distance' between distributions $P$ and $Q$
- not a true distance: $D(P\mid\mid Q) \neq D(Q\mid\mid P)$

Relative entropy is always **non-negative**:
$D(P\mid\mid Q) \geq 0$ with equality if and only if $P=Q$
(Proof not included, use $\ln(x) \leq (x-1)$ with equality iff $x=1$)

#### Redundancy in source coding
Often the true distribution of the source is unknown, and we have to work with an estimated source distribution for compression. 
- true pmf: $P=\left\{p_1, \ldots, p_m\right\}$, and the estimated pmf: $\hat{P}=\left\{\hat{p}_1, \ldots, \hat{p}_m\right\}$. 
- We use $\hat{P}$ to design a compression code whose code lengths $\ell_i$ satisfy $$ \ell_i=\log \left(1 / \hat{p}_i\right) \quad \text { for } i=1, \ldots, m $$
$\implies$ the code is optimal for the distribution $\hat{P}$. 
How far away are we from the optimal that could be achieved by knowing the true distribution? 
The average code-length is $$ \begin{aligned} L=\sum_i p_i \ell_i & =\sum_i p_i \log \frac{1}{\hat{p}_i} \\ & =\sum_i p_i \log \frac{p_i}{p_i \hat{p}_i}=\sum_i p_i \log \frac{1}{p_i}+\sum_i p_i \log \frac{p_i}{\hat{p}_i} \\ & =H(P)+D(P \| \hat{P}) \quad \text { bits/symbol. } \end{aligned} $$
Therefore, $D(P || \hat{P})$ is the redundancy for designing the code using $\hat P$ rather than the true distribution $P$.
$\implies$ need to design a code that minimises the worse-case redundancy

#### Hypothesis testing
In a basic version of simple hypothesis testing, we have data $X_1, \ldots, X_n$, and the knowledge that one of the following is true.
$$
\begin{aligned}
& H_0: X_1, \ldots, X_n \sim \text { i.i.d. } P \\
& H_1: X_1, \ldots, X_n \sim \text { i.i.d. } Q
\end{aligned}
$$
$H_0$ is often called the **null hypothesis**.

A decision rule (or a test) is a function that maps the data $(X_1, \ldots, X_n)$ to a binary decision (0 for $H_0$, 1 for $H_1$)
With any decision rule, there are two kinds of errors:
**Type 1 error**: $H_0$ true but decision rule chooses $H_1$.
**Type 2 error**: $H_1$ true but decision rule chooses $H_0$.

For the problem of testing between distributions $P$ and $Q$, the optimal decision rule is a **likelihood-ratio thresholding rule**, i.e., 
For some threshold $T$ : Choose $H_1$ if $\frac{Q\left(X_1, \ldots, X_n\right)}{P\left(X_1, \ldots, X_n\right)} \geq T$; otherwise choose $H_0$ 
Equivalently, the optimal rule can be expressed using LLR: 
Choose $H_1$ if $\frac{1}{n} \log \frac{Q\left(X_1, \ldots, X_n\right)}{P\left(X_1, \ldots, X_n\right)} \geq t$; otherwise choose $H_0$ 
(Note that both tests are equivalent by choosing $T=2^{n t}$.)
The reason why this is optimal: If a thresholding test has probability of type-I error $\alpha$ and prob. of type-II error $\beta$, then any other test that has type-1 error prob. $\leq \alpha$ necessarily has type-II error prob. $\geq \beta$.

For general $P$ and $Q$, the normalized log-likelihood ratio 
$$
\operatorname{LLR}\left(X_1, \ldots, X_n\right)=\frac{1}{n} \log \frac{Q\left(X_1, \ldots, X_n\right)}{P\left(X_1, \ldots, X_n\right)}
$$
satisfies the following: 
1. Under $H_1$, where $X_i \sim$ i.i.d. $Q$ : $\frac{1}{n} \log \frac{Q\left(X_1, \ldots, X_n\right)}{P\left(X_1, \ldots, X_n\right)} \rightarrow D(Q \| P)$ in probability. 
2. Under $H_0, X_i \sim$ i.i.d. $P$, therefore $\frac{1}{n} \log \frac{Q\left(X_1, \ldots, X_n\right)}{P\left(X_1, \ldots, X_n\right)} \rightarrow-D(P \| Q)$ in probability.
### 2. Mutual information
#### Definition
Consider two random variables $X$ and $Y$ with joint pmf $P_{XY}$. The mutual information between $X$ and $Y$ is defined as
$$
I(X;Y) = H(X) -H(X|Y) \quad \text{bits}
$$
Motif: "Reduction in the uncertainty of $X$ when you observe $Y$"
#### Property 1
$$
\begin{aligned}
I(X ; Y) & =H(X)+H(Y)-H(X, Y) \\
& =H(Y)-H(Y \mid X)
\end{aligned}
$$
Motif: "$X$ says as much about $Y$ as $Y$ says about $X$ "
Proof: 
From the chain rule of entropy,
$$
H(X, Y)=H(X)+H(Y \mid X)=H(Y)+H(X \mid Y)
$$
In the definition of $I(X ; Y)$, use $H(X \mid Y)=H(X, Y)-H(Y)$.

#### Property 2
$$ I(X ; Y)=D\left(P_{X Y} \| P_X P_Y\right) $$Motif: "The relative entropy between the joint pmf and the product of the marginals" 
Proof: $$ \begin{aligned} I(X ; Y) & =H(X)-H(X \mid Y) \\ & =-\sum_x P_X(x) \log P_X(x)+\sum_{x, y} P_{X Y}(x, y) \log P_{X \mid Y}(x \mid y) \\ & =\sum_{x, y} P_{X Y}(x, y) \log \frac{P_{X \mid Y}(x \mid y)}{P_X(x)} \\ & =\sum_{x, y} P_{X Y}(x, y) \log \frac{P_{X \mid Y}(x \mid y) P_Y(y)}{P_X(x) P_Y(y)} \\ & =D\left(P_{X Y} \| P_X P_Y\right) . \end{aligned} $$

### Property 3
$$
I(X;Y) \geq 0
$$
Proof:
Follows from property 2 because $D(P||Q) \geq 0$ for any pairs of pmfs $P, Q$.

**Implication**:
$$
H(X \mid Y) \leq H(X), \quad H(Y \mid X) \leq H(Y)
$$
Motif: "Knowing another random variable $Y$ can only reduce the average uncertainty in $X$" 

#### Conditional mutual information and chain rule
Given $X, Y, Z$ jointly distributed according to $P_{X Y Z}$, the conditional mutual information $I(X ; Y \mid Z)$ is defined as
$$
I(X ; Y \mid Z):=H(X \mid Z)-H(X \mid Y, Z)
$$

Mutual Information, like entropy, also obeys a chain rule:
For any sequence of random variables $X_1, X_2, \ldots, X_n$ jointly distributed with $Y$,
$$
I\left(X_1, X_2, \ldots, X_n ; Y\right)=\sum_{i=1}^n I\left(X_i ; Y \mid X_{i-1}, X_{i-2}, \ldots, X_1\right)
$$
where for each $i$
$$
\begin{aligned}
& I\left(X_i ; Y \mid X_{i-1}, X_{i-2}, \ldots, X_1\right) \\
& =H\left(X_i \mid X_{i-1}, X_{i-2}, \ldots, X_1\right)-H\left(X_i \mid Y, X_{i-1}, X_{i-2}, \ldots, X_1\right)
\end{aligned}
$$
## II. Discrete channels and channel capacity
### 0. Data transmission system
![[data-transmission.png | center | 500]]
Binary channel: binary-input, binary-output overall channel with error probability $p$.
### 1. Discrete channels
#### Discrete memoryless channel (DMC)
![[dmc.png | center | 500]]
Memoryless means that the channel acts independently on each input. 
For each time instant $k=1,2, \ldots$
$$
\operatorname{Pr}\left(Y_k=y \mid X_k=x, X_{k-1}, \ldots, X_1, Y_{k-1}, \ldots, Y_1\right)=P_{Y \mid X}(y \mid x) .
$$
"Given all the past, the current output depends only on the current input"

#### Binary symmetric channel (BSC)
![[bsc.png | center | 500]]
- $p$ is the "crossover probability"; the channel is called $\operatorname{BSC}(p)$
- BSC is a DMC

#### Binary erasure channel (BEC)
![[bec.png | center | 500]]
- BEC is a DMC
#### DMC communication
For a general DMC:
- we need to construct a set of input sequences which have non-intersecting sets of output sequences with high prob.
- these inputs sequences are "non-confusable" to the designated inputs

### 2. Channel capacity
![[channel-capacity.png | center | 400]]
The channel capacity of a discrete memoryless channel is defined as
$$
\mathcal{C} = \max_{P_X} I(X;Y)
$$
It is the **maximum transmission rate** over the DMC to get arbitrarily small probability of error.
**Note that** the maximising input distribution may not be unique.

For noiseless binary channel, $\mathcal{C} = 1$.
For BSC, $\mathcal{C} = 1 - H_2(p)$, obtained when input probability is $P_X  = (\frac{1}{2}, \frac{1}{2})$.
For BEC, $\mathcal{C} = 1 - \varepsilon$ ($\varepsilon$ is the probability of erasure), when the input probability is $P_X  = (\frac{1}{2}, \frac{1}{2})$.

## III. The channel coding theorem
### 0. Definition of a channel code
![[channel-code.png | center | 500]]


### 1. Joint typicality
#### The idea for a general DMC
Fix an input pmf $P_X$. Together with the channel $P_{Y \mid X}$, this gives
$$
P_{X Y}=P_X P_{Y \mid X}, \quad P_Y=\sum_x P_X P_{Y \mid X}
$$

If $X^n(1), X^n(2), \ldots, X^n\left(2^{n R}\right)$ are generated i.i.d $\sim P_X$, then:
- When $X^n(j)$ is transmitted, the set of highly likely $Y^n$ 's has approximately $2^{n H(Y \mid X)}$ sequences for each $j \in\left\{1, \ldots, 2^{n R}\right\}$
- These sets are non-intersecting with high probability
![[non-intersecting-sets.png | center | 500]]

#### Joint typical set
![[joint-typical-set.png | center | 600]]
#### The joint AEP
Let $\left(X^n, Y^n\right)$ be a pair of sequences drawn i.i.d. according to $P_{X Y}$, i.e., $$ \operatorname{Pr}\left(X^n=x^n, Y^n=y^n\right)=\prod_{i=1}^n P_{X Y}\left(x_i, y_i\right), \quad \text { for all }\left(x^n, y^n\right) $$ Then for any $\epsilon>0$ : 
1. $\operatorname{Pr}\left(\left(X^n, Y^n\right) \in A_{\epsilon, n}\right) \rightarrow 1$ as $n \rightarrow \infty$ 
2. $\left|A_{\epsilon, n}\right| \leq 2^{n(H(X, Y)+\epsilon)}$ 
3. If $\left(\tilde{X}^n, \tilde{Y}^n\right)$ are a pair of sequences drawn i.i.d. according to $P_X P_Y$ (i.e., $\tilde{X}^n$ and $\tilde{Y}^n$ are independent with the same marginals as $P_{X Y}$), then $$ \operatorname{Pr}\left(\left(\tilde{X}^n, \tilde{Y}^n\right) \in A_{\epsilon, n}\right) \leq 2^{-n(I(X ; Y)-3 \epsilon)} $$
Proof outline:
Claim 1: Uses the WLLN.
Claim 2: The probability of all joint sets sums to 1, which is larger than the probability of all joint typical sets.
Claim 3: Use the bounds on the number of joint typical sets and the probability of typical sets of individual variable.

### 2. Probability of error of a code
The maximal probability of error of the code is defined as $$ \max _{j \in\left\{1, \ldots, 2^{n R}\right\}} \operatorname{Pr}(\hat{W} \neq j \mid W=j) $$The average probability of error of the code is $$ \frac{1}{2^{n R}} \sum_{j=1}^{2^{n R}} \operatorname{Pr}(\hat{W} \neq j \mid W=j) $$$W$ and $\hat{W}$ denote the transmitted, and decoded messages respectively.
(Recall that $2^{nR}$ is the number of codewords in the codebook)

### 3. The channel coding theorem
#### Statement
![[channel-coding-theorem.png | center | 600]]

### 4. Proof of achievability of the channel coding theorem
(Included for completeness)
#### Cookbook generation
Fix rate $R<\mathcal{C}$ and input pmf $P_X$. We generate each of the $2^{n R}$ codewords independently according to the distribution 
$$ 
\operatorname{Pr}\left(X^n(k)=\left(x_1, \ldots, x_n\right)\right)=\prod_{i=1}^n P_X\left(x_i\right) \quad \text { for } k=1, \ldots, 2^{n R} 
$$
each message has length $k$ and becomes codewords of length $n$.

Think of the codebook $\mathcal{B}$ as a $2^{n R} \times n$ matrix:  
$$
\begin{array}{cc}
\mathcal{B}=\left[\begin{array}{cccc}X_1(1) & X_2(1) & \ldots & X_n(1) \\ X_1(2) & X_2(2) & \ldots & X_n(2) \\ \vdots & \vdots & \ddots & \vdots \\ X_1\left(2^{n R}\right) & X_2\left(2^{n R}\right) & \ldots & X_n\left(2^{n R}\right)\end{array}\right]
\end{array}
$$
(assignment of each codeword bit given the message to encode)
Each entry in the matrix is chosen i.i.d according to $P_X$. The probability that we generate a particular codebook $\left\{x^n(1), \ldots, x^n\left(2^{n R}\right)\right\}$ is $\prod_{w=1}^{2^{n R}} \prod_{i=1}^n P_X\left(x_i(w)\right)$.

#### Encoding
1. A codebook $\mathcal{B}$ is generated as described previously. The codebook is revealed to both sender and receiver, who also know the channel transition matrix $P_{Y \mid X}$. 
2. To transmit message $W$, the encoder sends $X^n(W)$ over the channel. 
3. The receiver receives a sequence $Y^n$ generated according to 
$$ 
\prod_{i=1}^n P_{Y \mid X}\left(Y_i \mid X_i(W)\right) 
$$
#### Joint typicality decoder
From $Y^n$, the decoder guesses which message was sent.
The decoder declares that the message $\hat{W}$ was sent if both the following conditions are satisfied:
- $\left(X^n(\hat{W}), Y^n\right)$ is jointly typical with respect to $P_X P_{Y \mid X}$.
- There exists no other message $W^{\prime} \neq \hat{W}$ such that $\left(X^n\left(W^{\prime}\right), Y^n\right)$ is jointly typical.
If no such $\hat{W}$ is found or there is more than one such, an error is declared.

#### Error analysis
The average probability of error for a given codebook $\mathcal{B}$ is
$$
\frac{1}{2^{n R}} \sum_{w=1}^{2^{n R}} \operatorname{Pr}(\hat{W} \neq w \mid \mathcal{B}, W=w)
$$

Analysing this for a specific codebook is hard $\rightarrow$ calculate the average of (2) over all codebooks, i.e.,
$$
\begin{aligned}
& \bar{P}_e=\frac{1}{2^{n R}} \sum_{\mathcal{B}} \sum_{w=1}^{2^{n R}} \operatorname{Pr}(\hat{W} \neq w \mid \mathcal{B}, W=w) \operatorname{Pr}(\mathcal{B}) . \\
& \bar{P}_e=\frac{1}{2^{n R}} \sum_{w=1}^{2^{n R}} \sum_{\mathcal{B}} \operatorname{Pr}(\hat{W} \neq w \mid \mathcal{B}, W=w) \operatorname{Pr}(\mathcal{B}) .
\end{aligned}
$$

Recall that $\operatorname{Pr}(\mathcal{B})$ is the probability corresponding to picking each symbol of $\mathcal{B}$ i.i.d. $\sim P_X$. (probability of choosing a specific codebook)
Since all the messages are equally likely, we can assume that the first message is the transmitted one. Thus
$$
\bar{P}_e=\sum \operatorname{Pr}(\hat{W} \neq 1 \mid \mathcal{B}, W=1) \operatorname{Pr}(\mathcal{B})
$$
Assuming $W=1$ was transmitted, there are two sources of error:
1. $X^n(1)$ is not jointly typical with the output $Y^n$
2. $X^n(k)$ is jointly typical with $Y^n$ for some $k \neq 1$.
(Note: The joint typicality is with respect to $P_{X Y}$ )
Let $E_k$ be the event that $X^n(k)$ and $Y^n$ are jointly typical.
Then:
$$
\begin{aligned}
\bar{P}_e & =P\left(E_1^c \cup E_2 \cup \ldots \cup E_{2^{n R}}\right) \\
& \leq P\left(E_1^c\right)+P\left(E_2\right)+\ldots+P\left(E_{2^{n R}}\right)
\end{aligned}
$$
![[cct-proof-1.png | center | 500]]
![[cct-proof-2.png | center | 500]]

Putting the two parts together:
$$
\begin{aligned}
\bar{P}_e & \leq P\left(E_1^c\right)+P\left(E_2\right)+\ldots+P\left(E_{2^{n R}}\right) \\
& \leq \epsilon+2^{n R} 2^{-n(I(X ; Y)-3 \epsilon)} \\
& \stackrel{(a)}{\leq} \epsilon+\epsilon
\end{aligned}
$$
(a) is true when $R<I(X ; Y)-3 \epsilon$ and $n$ is sufficiently large.
#### Final code
1. Choose $P_X$ to be one that maximises $I(X ; Y)$.
2. Get rid of average over codebooks: As $\bar{P}_e \leq 2 \epsilon$, there exists at least one codebook $\mathcal{B}^*$ with
$$
P_e\left(\mathcal{B}^*\right)=\frac{1}{2^{n R}} \sum_{w=1}^{2^{n R}} \operatorname{Pr}\left(\hat{W} \neq w \mid \mathcal{B}^*, W=w\right) \leq 2 \epsilon
$$
1. Throw away the worst half of the codewords in $\mathcal{B}^*$ : For $\mathcal{B}^*$, the probability of error averaged over all messages is $\leq 2 \epsilon$. Thus the probability of error must be $\leq 4 \epsilon$ for at least half the messages.

The number of codewords in this improved version of $\mathcal{B}^*$ is $2^{n R} / 2$. Its rate is
$$
\frac{\log \left(2^{n R} / 2\right)}{n}=R-\frac{1}{n}
$$

Since $R$ is any rate less than $\mathcal{C}-3 \epsilon$, we have shown the existence of a code with rate
$$
\mathcal{C}-4 \epsilon-\frac{1}{n}
$$
whose maximal probability of error satisfies
$$
\max _w \operatorname{Pr}(\hat{W} \neq w \mid W=w) \leq 4 \epsilon
$$

Since $\epsilon>0$ is an arbitrary constant, we have shown that for any $R<\mathcal{C}$, for sufficiently large $n$ there exists a code with arbitrarily small maximal error probability.

#### Key ideas
- allow an arbitrarily small but non-zero probability of error
- use the channel many times in succession, so that the law of large numbers comes into effect
- random coding: calculate the average probability of error over a random choice of codebooks, which can be used to show the existence of at least one good code

### 5. Data processing inequality and Fano's inequality
#### Data processing inequality
![[data-processing-inequality.png | center | 500]]

#### Fano's inequality
![[fanos-inequality.png | center | 500]]

#### Fano's inequality applied to a channel code
Consider a length $n$, rate $R$ channel code, i.e., $2^{n R}$ codewords
- $\hat{W}$ is a guess of $W$ based on $Y^n$
- $W$ uniformly distributed in $\left\{1, \ldots, 2^{n R}\right\}$
- $P_e=\operatorname{Pr}(\hat{W} \neq W)=\frac{1}{2^{n R}} \sum_{k=1}^{2^{n R}} \operatorname{Pr}(\hat{W} \neq k \mid W=k)$

Fano's inequality applied to this problem gives:
$$
H(W \mid \hat{W}) \leq 1+P_e \log 2^{n R}=1+P_e n R
$$
#### A little lemma
Let $Y^n$ be the result of passing a sequence $X^n$ through a DMC of channel capacity $\mathcal{C}$. Then
$$
I\left(X^n ; Y^n\right) \leq n \mathcal{C}
$$
regardless of the distribution of $X^n$.

#### Proof of the converse of the channel coding theorem
Consider any $\left(2^{n R}, n\right)$ channel code with average probability of error $P_e$. We have:
$$
\begin{aligned}
n R & \stackrel{(a)}{=} H(W) \\
& \stackrel{(b)}{=} H(W \mid \hat{W})+I(W ; \hat{W}) \\
& \stackrel{(c)}{\leq} 1+P_e n R+I(W ; \hat{W}) \\
& \stackrel{(d)}{\leq} 1+P_e n R+I(X^n ; Y^n) \\
& \stackrel{(e)}{\leq} 1+P_e n R+n\mathcal{C} \\
\end{aligned}
$$

This implies:
$$
P_e \geq 1-\frac{\mathcal{C}}{R}-\frac{1}{n R}
$$

Thus, unless $R \leq \mathcal{C}, P_e$ is bounded away from 0 as $n \rightarrow \infty$.

Justification for steps $(a)-(e)$ :
(a) $W$ is uniform over $\left\{1, \ldots, 2^{n R}\right\}$
(b) $I(W ; \hat{W})=H(W)-H(W \mid \hat{W})$
(c) Fano applied to $H(W \mid \hat{W})$
(d) Data processing inequality applied to $W-X^n-Y^n-\hat{W}$.
(e) From the little lemma shown above

## IV. Information theory with continuous random varaibles
### 1. The additive white gaussian noise (AWGN) channel
![[awgn.png | center | 500]]
Usual assumptions on the channel: 
1. Input $X(t)$ is **power-limited** to $P$ $\Rightarrow$ Average energy over time $T$ must be $\leq P$ for large $T$
2. $X(t)$ is **band-limited** to $W$ $\Rightarrow$ Fourier Transform of $X(t)$ must be zero outside $[-W, W]$ 
3. Noise $N(t)$ is a random process assumed to be white Gaussian 

We will focus on discrete-time AWGN channel

![[discrete-time-awgn.png | center | 500]]

### 2. Differential entropy
The differential entropy of a continuous random variable $X$ with pdf $f_X$ is
$$
h(X) = \int_{-\infty}^{\infty}f_X(u)\log\frac{1}{f_X(u)}du
$$
#### The differential entropy of a gaussian random variable
Gaussian random variable
Let $X \sim \mathcal{N}\left(\mu, \sigma^2\right)$. The pdf $\phi$ is given by
$$
\phi(x)=\frac{1}{\sqrt{2 \pi \sigma^2}} e^{\frac{-(x-\mu)^2}{2 \sigma^2}}
$$

The differential entropy is
$$
\begin{aligned}
h(X) & =-\int \phi(x) \frac{\ln \phi(x)}{\ln 2} d x \\
& =-\frac{1}{\ln 2} \int \phi(x)\left[-\frac{(x-\mu)^2}{2 \sigma^2}-\ln \sqrt{2 \pi \sigma^2}\right] d x \\
& =\frac{1}{\ln 2}\left[\frac{\operatorname{Var}(X)}{2 \sigma^2}+\frac{1}{2} \ln 2 \pi \sigma^2\right] \\
& =\frac{1}{\ln 2}\left[\frac{1}{2}+\frac{1}{2} \ln 2 \pi \sigma^2\right] \\
& =\frac{1}{\ln 2}\left[\frac{1}{2} \ln e+\frac{1}{2} \ln 2 \pi \sigma^2\right]=\frac{1}{2} \log 2 \pi e \sigma^2
\end{aligned}
$$
#### Differential entropy of multiple RVs
If $(X, Y)$ have joint density $f_{X Y}$ :
The joint differential entropy of $X, Y$ is
$$
h(X, Y)=\int f_{X Y}(u, v) \log \frac{1}{f_{X Y}(u, v)} d u d v
$$

The conditional differential entropy of $X$ given $Y$ is
$$
h(X \mid Y)=\int f_{X Y}(u, v) \log \frac{1}{f_{X \mid Y}(u \mid v)} d u d v
$$

Joint differential entropy obeys a chain rule:
$$
h(X, Y)=h(X)+h(Y \mid X)
$$

Mutual information is similar to the discrete case:
$$
I(X ; Y)=h(X)-h(X \mid Y)=h(X)+h(Y)-h(X, Y)=h(Y)-h(Y \mid X)
$$
#### Relative entropy between two continuous RVs
The relative entropy between two densities $f$ and $g$ is
$$
D(f||g) = \int f(u)\log\frac{f(u)}{g(u)}
$$
**Note:**
- mutual information and relative entropy are non-negative, same as for discrete rvs 
- chain rules for differential entropy and mutual information hold for continuous rvs – analogous to the discrete case
- the main difference is that differential entropy can be **negative**
- differential entropy should be interpreted as uncertainty relative to a **baseline**

### 3. Capacity of the discrete-time AWGN channel
Recall the format of the discrete-time AWGN channel:
$$
Y_k = X_k + Z_k, \quad k = 1, 2, \ldots
$$
The capacity of this channel is the maximum of $I(X;Y)$, where
$$
\begin{aligned} I(X ; Y) & =h(Y)-h(Y \mid X) \\ & =h(Y)-h(X+Z \mid X) \\ & =h(Y)-h(Z \mid X) \\ & =h(Y)-h(Z)\end{aligned}
$$
Note that $h(Z | X) = h(Z)$ since $Z$ is independent of $X$.

$Z \sim \mathcal{N}\left(0, \sigma^2\right)$. Hence $h(Z)=\frac{1}{2} \log 2 \pi e \sigma^2$ 
Note that 
$$
\begin{aligned} \mathbb{E} Y^2=\mathbb{E}(X+Z)^2 & =\mathbb{E} X^2+2 \mathbb{E}(X Z)+\mathbb{E} Z^2 \\ & =\mathbb{E} X^2+\sigma^2 \end{aligned}
$$
$X, Z$ are independent $\Rightarrow \mathbb{E}(X Z)=\mathbb{E} X \mathbb{E} Z=0)$ 
Therefore $\mathbb{E} X^2 \leq P$ implies $\mathbb{E} Y^2 \leq P+\sigma^2$ (with equality if $\left.\mathbb{E} X^2=P\right)$

**Key fact:** 
Among all random variables $Y$ with $\mathbb{E} Y^2 \leq\left(P+\sigma^2\right)$, the maximum differential entropy is achieved when $Y$ is Gaussian $\mathcal{N}\left(0, P+\sigma^2\right)$

Since $Y=X+Z$ and $\mathbb{E} Y^2 \leq\left(P+\sigma^2\right)$, the key fact implies
$$
h(Y) \leq \frac{1}{2} \log 2 \pi e\left(P+\sigma^2\right)
$$
with equality if $X$ is distributed as $\mathcal{N}(0, P)$. 

For this choice of $X$ :
$$
\begin{aligned}
I(X ; Y) & =h(Y)-\frac{1}{2} \log 2 \pi e \sigma^2 \\
& =\frac{1}{2} \log 2 \pi e\left(P+\sigma^2\right)-\frac{1}{2} \log 2 \pi e \sigma^2 \\
& =\frac{1}{2} \log \left(1+\frac{P}{\sigma^2}\right) .
\end{aligned}
$$

Hence, the capacity of the discrete-time AWGN channel with input power constraint $P$ and noise variance $\sigma^2$ is 
$$
\mathcal{C}=\frac{1}{2} \log \left(1+\frac{P}{\sigma^2}\right) \quad \text { bits/transmission } 
$$
$\implies \mathcal{C}$ depends only on the signal-to-noise ratio (snr) $\frac{P}{\sigma^2}$ 
If the channel has (baseband) bandwidth $W$, it can be used $2 W$ times per second. Therefore, the capacity in bits/s is 
$$
2 W \cdot \frac{1}{2} \log \left(1+\frac{P}{\sigma^2}\right)=W \log \left(1+\frac{P}{\sigma^2}\right) \text { bits } / \mathrm{sec}
$$

Backlinks:
[[Information Theory Fundamentals and Source Coding]]
[[Error-Correcting Codes]]
[[Random Processes]]
