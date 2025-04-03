## I. Probability review
### 1. Two key properties of jointly distributed random variables
1. Product rule:
$$
\begin{aligned}
P_{X Y Z} & =P_X P_{Y \mid X} P_{Z \mid Y X} \\
& =P_Y P_{X \mid Y} P_{Z \mid X Y} \\
& =P_Z P_{X \mid Z} P_{Y \mid X Z} \quad \text { etc. }
\end{aligned}
$$
2. Sum rule (marginalisation):
$$
\begin{aligned}
& P_{X Y}(x, y)=\sum_z P_{X Y Z}(x, y, z) \\
& P_X(x)=\sum_{y, z} P_{X Y Z}(x, y, z)=\sum_y P_{X Y}(x, y) \quad \text { etc. }
\end{aligned}
$$

These properties extend in the natural way to multiple jointly distributed random variables $\left(X_1, \ldots, X_n\right)$
### 2. Independence
Discrete random variables $X_1, X_2, \ldots, X_n$ are statistically independent if
$$
P_{X_1,\ldots,X_n} = (x_1,\ldots,x_n) = P_{X_1}(x_1)P_{X_2}(x_3)\ldots P_{X_n}(x_n)
\quad \forall(x_1, \ldots, x_n).
$$
When $X_1, X_2, \ldots, X_n$ are independent,
$$
P_{X_i \mid \{X_j\}j \neq i} = P_{X_i}
$$
## II. Entropy
The entropy of a discrete random variable $X$ with pmf $P$ is 
$$
H(X)=\sum_x P(x) \log \frac{1}{P(x)} \text { bits }
$$
- "log" in this course will mean $\log _2$
- $H(X)$ can be written as $\mathbb{E}\left[\log \frac{1}{P(X)}\right]$ 
- $H(X)$ is the uncertainty associated with the rv $X$.

Binary entropy:
$$
H_2(p)=p \log \frac{1}{p}+(1-p) \log \frac{1}{1-p}
$$
### 1. Properties of entropy
(for proof see lecture notes)
Let $X$ be discrete random variable taking values in $\mathcal{X}$. Denote the alphabet size $|\mathcal{X}|$ by $M$. Then:
1. $H(X) \geq 0$.
2. If we denote the alphabet size $|\mathcal{X}|$ by $M$, then $H(X) \leq \log M$
3. Among all random variables taking values in $\mathcal{X}$, the equiprobable distribution $\left(\frac{1}{M}, \ldots, \frac{1}{M}\right)$ has the maximum entropy, equal to $\log M$.
### 2. Joint and conditional entropy
The joint entropy of discrete rvs $X, Y$ with joint pmf $P_{X Y}$ is
$$
H(X, Y)=\sum_{x, y} P_{X Y}(x, y) \log \frac{1}{P_{X Y}(x, y)}
$$
The conditional entropy of $Y$ given $X$ is
$$
H(Y \mid X)=\sum_{x, y} P_{X Y}(x, y) \log \frac{1}{P_{Y \mid X}(y \mid x)}
$$
$H(Y \mid X)$ is the average uncertainty in $Y$ given $X$ :
$$
H(Y \mid X)=\sum_x P_X(x) \underbrace{\sum_y P_{Y \mid X}(y \mid x) \log \frac{1}{P_{Y \mid X}(y \mid x)}}_{H(Y \mid X=x)}
$$
$H(Y \mid X=x)$ is the uncertainty in $Y$ conditioned on the event $X=x$, while $H(Y \mid X)$ is the average uncertainty in $Y$ conditioned on the random variable $X$.
### 3. Joint entropy of multiple rvs
The joint entropy of $X_1, \ldots, X_n$ with joint pmf $P_{X_1 \ldots X_n}$ is
$$
H\left(X_1, X_2, \ldots, X_n\right)=\sum_{x_1, \ldots, x_n} P_{X_1 \ldots X_n}\left(x_1, \ldots, x_n\right) \log \frac{1}{P_{X_1 \ldots X_n}\left(x_1, \ldots, x_n\right)}
$$
**Chain Rule of Joint Entropy:**
The joint entropy can be decomposed as
$$
\begin{aligned}
H\left(X_1, X_2 \ldots, X_n\right) & =H\left(X_1\right)+H\left(X_2 \mid X_1\right)+\ldots+H\left(X_n \mid X_{n-1}, \ldots, X_1\right) \\
& =\sum_{i=1}^n H\left(X_i \mid X_{i-1}, \ldots, X_1\right)
\end{aligned}
$$
where the conditional entropy
$$
H\left(X_i \mid X_{i-1}, \ldots, X_1\right)=\sum_{x_1, \ldots, x_i} P_{X_1, \ldots, X_i}\left(x_1, \ldots, x_i\right) \log \frac{1}{P_{X_i \mid X_1, \ldots, x_{i-1}}\left(x_i \mid x_1, \ldots, x_{i-1}\right)}
$$
(This chain rule is a generalisation of $H(X, Y)=H(X)+H(Y \mid X)$. )

**Proof of chain rule:**
Recall that
$$
P\left(x_1, \ldots, x_n\right)=P\left(x_1\right) P\left(x_2 \mid x_1\right) \ldots P\left(x_n \mid x_{n-1}, \ldots, x_1\right)=\prod_{i=1}^n P\left(x_i \mid x_{i-1}, \ldots, x_1\right)
$$
(For brevity, we drop the subscripts on $P_{X_1 \ldots X_n}$ )
$$
\begin{aligned}
H\left(X_1, X_2, \ldots, X_n\right) &=-\sum_{x_1, \ldots, x_n} P\left(x_1, \ldots, x_n\right) \log P\left(x_1, \ldots, x_n\right) \\
& =-\sum_{x_1, \ldots, x_n} P\left(x_1, \ldots, x_n\right) \log \prod_{i=1}^n P\left(x_i \mid x_{i-1}, \ldots, x_1\right) \\
& =-\sum_{x_1, \ldots, x_n} \sum_{i=1}^n P\left(x_1, \ldots, x_n\right) \log P\left(x_i \mid x_{i-1}, \ldots, x_1\right) \\
& =-\sum_{i=1}^n \sum_{x_1, \ldots, x_n} P\left(x_1, \ldots, x_n\right) \log P\left(x_i \mid x_{i-1}, \ldots, x_1\right) \\
& =-\sum_{i=1}^n \sum_{x_i} P\left(x_1, \ldots, x_i\right) \log P\left(x_i \mid x_{i-1}, \ldots, x_1\right) \\
&=\sum_{i=1}^n H\left(X_i \mid X_{i-1}, \ldots, x_1\right)
\end{aligned}
$$
### 4. Joint entropy of independent rvs
If $X_1, X_2, \ldots, X_n$ are independent random variables, then
$$
H\left(X_1, X_2, \ldots, X_n\right)=\sum_{i=1}^n H\left(X_i\right)
$$
Proof:
Due to independence, $P_{X_i \mid X_{i-1}, \ldots, X_1}=P_{X_i}$ for $i=2, \ldots, n$. Use this to show that for all $i$
$$
H\left(X_i \mid X_{i-1}, \ldots, X_1\right)=H\left(X_i\right)
$$
The result then follows from the chain rule.

## III. Law of large numbers and typicality
### 1. Estimating tail probabilities
#### Markov's inequality
For a non-negative rv $X$ and any $a>0$,
$$
P(X \geq a) \leq \frac{\mathbb{E}[X]}{a}
$$
Note that it is useful only for $a>\mathbb{E}[X]$.

Proof:
Define the indicator function $\mathbf{1}\{x \geq a\}= \begin{cases}1 & \text { if } x \geq a \\ 0 & \text { if } x<a\end{cases}$
Notice that for $x \geq 0$, we have $x \geq a \mathbf{1}\{x \geq a\}$. Therefore:
$$
\sum_{x \geq 0} x P(X=x) \geq \sum_{x \geq 0} a 1\{x \geq a\} P(X=x)
$$

The left side above equals $\mathbb{E}[X]$. The right side equals
$$
a \sum_{x \geq 0} 1\{x \geq a\} P(X=x)=a \sum_{x \geq a} P(X=x)=a P(X \geq a)
$$
Using this in (1), we obtain the result: $\mathbb{E}[X] \geq a P(X \geq a)$
#### Chebyshev's inequality
For any $\mathrm{rv} X$ and $a>0$,
$$
P(|X-\mathbb{E} X| \geq a) \leq \frac{\operatorname{Var}(X)}{a^2}
$$
Chebyshev's inequality bound the probability of deviations around the mean.

Proof: 
Note that $P(|X-\mathbb{E} X| \geq a)=P\left(|X-\mathbb{E} X|^2 \geq a^2\right)$. Let $Y:=|X-\mathbb{E} X|^2$.
Since $Y$ is a non-negative rv, we can apply Markov's inequality to get
$$
P\left(Y \geq a^2\right) \leq \frac{\mathbb{E} Y}{a^2} \Rightarrow P(|X-\mathbb{E} X| \geq a) \leq \frac{\operatorname{Var}(X)}{a^2}
$$
where we have used $\mathbb{E} Y=\mathbb{E}\left[(X-\mathbb{E} X)^2\right]=\operatorname{Var}(X)$.
### 2. Weak law of large numbers (WLLN)
Essence: "Empirical average converges to the mean"

Let $X_1, X_2, \ldots$ be a sequence of i.i.d. random variables with finite mean $\mu$. Let $S_n=\frac{1}{n} \sum_{i=1}^n X_i$.
- Informal statement of WLLN: $S_n \rightarrow \mu$ as $n \rightarrow \infty$.
- Formal statement of WLLN: For any $\epsilon>0$, $\lim _{n \rightarrow \infty} P\left(\left|S_n-\mu\right| \geq \epsilon\right)=0$.

Proof: 
Assume that the variance of each $X_i$ is finite, say $\sigma^2$. By Chebyshev's inequality, we have
$$
P\left(\left|S_n-\mu\right| \geq \epsilon\right) \leq \frac{\operatorname{Var}\left(S_n\right)}{\epsilon^2}=\frac{\sigma^2}{n \epsilon^2}
$$

The last equality above is obtained using the independence of the $X_i$ 's:
$$
\operatorname{Var}\left(S_n\right)=\frac{1}{n^2} \operatorname{Var}\left(\sum_i X_i\right)=\frac{1}{n^2} \sum_{i=1}^n \operatorname{Var}\left(X_i\right)=\frac{1}{n^2} n \sigma^2=\frac{\sigma^2}{n}
$$

For any fixed $\epsilon>0$, note that $\frac{\sigma^2}{n \epsilon^2} \rightarrow 0$ as $n \rightarrow \infty$. 

Hence
$$
\lim _{n \rightarrow \infty} P\left(\left|S_n-\mu\right| \geq \epsilon\right)=0
$$
### 3. Typicality
#### Typical sequences
If $X_1, \ldots, X_n$ are chosen $\sim$ i.i.d. Bernoulli( $p$ ), then for large $n$ :
- With high probability, the fraction of ones in the observed sequence will be close to $p$ (due to WLLN).
- Equivalently: with high probability, the observed sequence will have probability close to $p^{n p}(1-p)^{n(1-p)}$
- Note that any number a can be written as $2^{\log a}$. Hence
$$
p^{n p}(1-p)^{n(1-p)}=\left(2^{\log p}\right)^{n p}\left(2^{\log (1-p)}\right)^{n(1-p)}=2^{-n H_2(p)}
$$
For large $n$, with high probability we will observe a typical sequence. 
Informally, **a typical sequence is one whose probability is close to $2^{-n H_2(p)}$.**

#### Asymptotic equipartition property (AEP)
If $X_1, X_2, \ldots$ are i.i.d. $\sim P_X$, then for any $\epsilon>0$
$$
\lim _{n \rightarrow \infty} \operatorname{Pr}\left(\left|\frac{-1}{n} \log P_X\left(X_1, X_2, \ldots, X_n\right)-H(X)\right|<\epsilon\right)=1
$$

Remarks:
$\frac{-1}{n} \log P_X\left(X_1, X_2, \ldots, X_n\right)$ is a random variable $\implies$ AEP says this rv converges in probability to $H(X)$, a constant, as $n \rightarrow \infty$.

Proof:
Let
$$
Y_i=-\log P_X\left(X_i\right), \quad \text { for } i=1, \ldots, n
$$

Functions of independent rvs are also independent rvs $\Rightarrow Y_1, \ldots, Y_n$ are i.i.d.

WLLN for $Y_i$ 's says that for any $\epsilon>0$
$$
\lim _{n \rightarrow \infty} \operatorname{Pr}\left(\left|\frac{1}{n} \sum_i Y_i-\mathbb{E}\left[Y_1\right]\right|<\epsilon\right)=1
$$

Note that
$$
\begin{aligned}
\sum_i Y_i=-\sum_i \log P_X\left(X_i\right) & =-\log \left[P_X\left(X_1\right) P_X\left(X_2\right) \ldots P_X\left(X_n\right)\right] \\
&=-\log P_X\left(X_1, X_2, \ldots, X_n\right)
\end{aligned}
$$
### 4. Typical set
Recall the AEP: 
If $X_1, X_2, \ldots$ are i.i.d. $\sim P$, then for any $\epsilon>0$ $$ \operatorname{Pr}\left(\left|-\frac{1}{n} \log P\left(X_1, X_2, \ldots, X_n\right)-H(X)\right|<\epsilon\right) \xrightarrow{n \rightarrow \infty} 1 . $$
**The typical set $A_{\epsilon, n}$ with respect to $P$ is the set of sequences $\left(x_1, \ldots, x_n\right) \in \mathcal{X}^n$ with the property** $$ 
\boxed{2^{-n(H(X)+\epsilon)} \leq P\left(x_1, \ldots, x_n\right) \leq 2^{-n(H(X)-\epsilon)}}
$$Hence the typical set consists of **"sequences whose probability is concentrated around $2^{-n H(X)}$"**

A sequence belonging to the typical set is called an $\epsilon$-typical sequence.

The typical set have 3 properties
#### Property 1
If $X^n=\left(X_1, \ldots, X_n\right)$ is generated i.i.d. $\sim P$, then
$$
\operatorname{Pr}\left(X^n \in A_{\epsilon, n}\right) \xrightarrow{n \rightarrow \infty} 1
$$

That is, the sequence $X_1, \ldots, X_n$ you observe is very likely to belong to the typical set.

Proof: 
From the definition of $A_{\epsilon, n}$, note that
$$
\begin{aligned}
X^n \in A_{\epsilon, n} & \Leftrightarrow 2^{-n(H(X)+\epsilon)} \leq P\left(X^n\right) \leq 2^{-n(H(X)-\epsilon)} \\
& \Leftrightarrow H(X)-\epsilon \leq-\frac{1}{n} \log P\left(X^n\right) \leq H(X)+\epsilon
\end{aligned}
$$

AEP says that
$$
\operatorname{Pr}\left(X^n \in A_{\epsilon, n}\right)=\operatorname{Pr}\left(H(X)-\epsilon \leq-\frac{1}{n} \log P\left(X^n\right) \leq H(X)+\epsilon\right) \xrightarrow{n \rightarrow \infty} 1 .
$$
#### Property 2
Let $\left|A_{\epsilon, n}\right|$ denote the number of elements in the typical set $A_{\epsilon, n}$. Then
$$
\left|A_{\epsilon, n}\right| \leq 2^{n(H(X)+\epsilon)}
$$

Proof:
$$
\begin{aligned}
1 & =\sum_{x^n \in \mathcal{X}^n} P\left(x^n\right) \\
& \geq \sum_{x^n \in A_{\epsilon, n}} P\left(x^n\right) \\
& \stackrel{(a)}{\geq} \sum_{x^n \in A_{\epsilon, n}} 2^{-n(H(X)+\epsilon)} \\
& =2^{-n(H(X)+\epsilon)}\left|A_{\epsilon, n}\right|
\end{aligned}
$$

Hence $\left|A_{n, \epsilon}\right| \leq 2^{n(H(X)+\epsilon)}$. (Inequality (a) follows from the definition of the typical set.)
#### Property 3 
For sufficiently large $n$,
$$
\left|A_{\epsilon, n}\right| \geq(1-\epsilon) 2^{n(H(X)-\epsilon)}
$$

Proof:
From Property $1, \operatorname{Pr}\left(X^n \in A_{\epsilon, n}\right) \rightarrow 1$ as $n \rightarrow \infty$. This means that for any $\epsilon>0$, for sufficiently large $n$ we have $\operatorname{Pr}\left(X^n \in A_{\epsilon, n}\right)>1-\epsilon$. Thus, for sufficiently large $n$ : 
$$
\begin{aligned} 1-\epsilon & <\operatorname{Pr}\left(X^n \in A_{\epsilon, n}\right) \\ & =\sum_{x^n \in A_{\epsilon, n}} P\left(x^n\right) \\& \stackrel{(b)}{\leq} \sum_{X^n \in A_{\epsilon, n}} 2^{-n(H(X)-\epsilon)} \\ & =2^{-n(H(X)-\epsilon)}\left|A_{\epsilon, n}\right|\end{aligned}
$$

Hence $\left|A_{n, \epsilon}\right| \geq(1-\epsilon) 2^{n(H(X)-\epsilon)}$. (Inequality (b) follows from the definition of the typical set.)

**Summary**:
For large $n$
- with high probability the sequence will be typical — its probability is close to $2^{-nH(X)}$
- if the pmf $P$ assigns non-zero probabilities to the symbols denoted $a, b, c$ etc., the typical set is essentially the set of sequences whose fraction of a's is close to $P(a)$, fraction of $b$ 's is close to $P(b)$, and so on.
- the number of typical sequences is close to $2^{nH(X)}$
## III. Compression
**Goal:** To compress a source producing symbols $X_1, X_2, \ldots \in \mathcal{X}$ that are i.i.d. $\sim P$ — come up with a code (a mapping) that has **small expected code length**

For any $n$, a compression code is defined as follows:
- To each source sequence $X^n:=\left(X_1, \ldots, X_n\right)$, the code assigns a unique binary sequence $c\left(X^n\right)$.
- $c\left(X^n\right)$ is called the codeword for the source sequence $X^n$.
- Let $\ell\left(X^n\right)$ be the length of the codeword assigned to $X^n$, i.e., the number of bits in $c\left(X^n\right)$.
- The expected code length is defined as
$$
\mathbb{E}\left[\ell\left(X^n\right)\right]=\sum_{x^n} P\left(x^n\right) \ell\left(x^n\right)
$$
### 1. A naive compression code
List all the $|\mathcal{X}|^n$ possible length $n$ sequences.
- Index these as $\left\{0,1, \ldots,|\mathcal{X}|^n-1\right\}$ using $\left\lceil\log |\mathcal{X}|^n\right\rceil$ bits $\Rightarrow$ Length of codeword for each sequence $=n \log |\mathcal{X}|$ (5n for English)
- Expected code length: $\mathbb{E}\left[\ell\left(X^n\right)\right]=n \log |\mathcal{X}|$
- Expected number of bits/symbol: $\mathbb{E}\left[\ell\left(X^n\right)\right] / n=\log |\mathcal{X}|$ (5 bits/symbol for English)
### 2. Compression via the typical set
#### Compression scheme
- There are at most $2^{n(H(X)+\epsilon)} \; \epsilon$-typical sequences.
- Index each sequence in $A_{\epsilon, n}$ using $\left\lceil\log 2^{n(H(X)+\epsilon)}\right\rceil$ bits. Prefix each of these by a flag bit 0 .
$$
\text { Bits/typical seq. }=\lceil n(H(X)+\epsilon)\rceil+1 \leq n(H(X)+\epsilon)+2
$$

- Index each sequence not in $A_{\epsilon, n}$ using $\left\lceil\log |\mathcal{X}|^n\right\rceil$ bits. Prefix each of these by a flag bit 1.
$$
\text { Bits/non-typical seq. }=\lceil n \log |\mathcal{X}|\rceil+1 \leq n \log |\mathcal{X}|+2
$$

This code assigns a unique codeword to each sequence in $|\mathcal{X}|^n$

![[typical-set.png| center | 500]]

#### Expected code length
Let $\ell\left(X^n\right)$ be length of the codeword assigned to sequence $X^n$.
$$
\begin{aligned}
\mathbb{E}\left[\ell\left(X^n\right)\right] &=\sum_{x^n} P\left(x^n\right)\ell\left(x^n\right)\\
&=\sum_{x^n \in A_{\epsilon, n}} P\left(x^n\right) \ell\left(x^n\right)+\sum_{x^n \notin A_{\epsilon, n}} P\left(x^n\right) \ell\left(x^n\right) \\
&\leq \sum_{x^n \in A_{\epsilon, n}} P\left(x^n\right)(n(H(X)+\epsilon)+2)+\sum_{x^n \notin A_{\epsilon, n}} P\left(x^n\right)(n \log |\mathcal{X}|+2) \\
&\leq 1 \cdot n(H(X)+\epsilon)+\epsilon \cdot n \log |\mathcal{X}|+2\left(\sum_{x^n \in A_{\epsilon, n}} P\left(x^n\right)+\sum_{x^n \notin A_{\epsilon, n}} P\left(x^n\right)\right) \\
&=n\left(H(X)+\epsilon\right)+\epsilon n \log |\mathcal{X}|+2 & \\
&=n\left(H(X)+\epsilon^{\prime}\right)
\end{aligned}
$$
where $\epsilon^{\prime}=\epsilon+\epsilon \log |\mathcal{X}|+\frac{2}{n}$.
$\epsilon^{\prime}$ can be made arbitrarily small by picking $\epsilon$ small enough and then $n$ sufficiently large.
### 3. Fundamental limit of compression
Let $X^n$ be i.i.d. $\sim P$. Fix any $\epsilon>0$. For $n$ sufficiently large, there exists a code that maps sequences $x^n$ of length $n$ into binary strings such that the mapping is one-to-one and
$$
\mathbb{E}\left[\frac{1}{n} \ell\left(X^n\right)\right] \leq H(X)+\epsilon
$$

In fact, the expected length of **any** uniquely decodable code satisfies
$$
\mathbb{E}\left[\frac{1}{n} \ell\left(X^n\right)\right] \geq H(X)
$$
**Hence entropy is the fundamental limit of lossless compression**

### IV. Lossless source coding theorem
### 1. Prefix-free code
A code is called **prefix-free** or **instantaneously decodable** is no codeword is the prefix of another.
#### Uniquely decodability
Given a binary code $C$ for alphabet $\mathcal{X}$, the extension code $C^n$ is the code applied symbol-by-symbol to string in $x^n \in \mathcal{X}^n$:
$$
C(x_1 x_2 \ldots x_n) = C(x_1) C(x_2) \ldots C(x_n)
$$
- $C^n$ is **uniquely decodable** if for each binary codeword in $C^n$, there is only one possible source string that can produce it
- **prefix-free codes are uniquely decodable**
- not all uniquely decodable codes are prefix-free
#### Prefix condition on a tree
- full tree of depth $l_{max}$ has $2^{l_{max}}$ leaves
- each codeword of length $l$ leads to a set of $2^{l_{max}-l}$ unusable leaves at depth $l_{max}$ (since all the descendants of the codeword are removed from the tree)
- the total number of unusable leaves at level $l_{max}$ for a code with word lengths $\{l_1, l_2, \cdots, l_N\}$ is
$$
\sum_{i=1}^N 2^{l_{max}-l_i}
$$
#### Kraft inequality
The total number of unusable leaves must not be more than the total number of leaves (at level $l_{max}$)
Hence,
$$
\sum_{i=1}^N 2^{l_{max}-l_i} \leq 2^{l_{max}} \implies \sum_{i=1}^N 2^{-l_i} \leq 1
$$
This is the **Kraft inequality** — a **sufficient and necessary** condition for any prefix-free code with word lengths $\{l_1, l_2, \cdots, l_N\}$.
(The Kraft inequality is actually satisfied by **any** uniquely decodable code)

i.e.
A binary prefix-free code with codeword lengths $\{l_1, l_2, \cdots, l_N\}$ exists **if and only if**
$$
\boxed{\sum_{i=1}^N 2^{-l_i} \leq 1}
$$
### 2. Lossless source coding theorem
#### Coding theorem for a random variable
Let $X$ be a random variable taking values in $\mathcal{X}$ with entropy $H(X)$. The expected codeword length $L$ of any binary prefix-free code for $X$ satisfies
$$
L \geq H(X)
$$
(Proof not included here: use inequality $\ln(x) \leq x-1 \,\text{for all}\, x > 0$ and Kraft's inequality for proof.)
#### Coding theorem for block of source symbols
If $X$ is an iid source with entropy $H(X)$, then
$$
H(X^N) = NH(X) \implies \frac{\mathbb{E}[\ell(X^N)]}{N} \geq H(X)
$$
## V. Practical source coding
### 1. Shannon-Fano coding
Since the codeword lengths $\ell_i$ are integers, an obvious way to choose them is
$$
\ell_i=\left\lceil\log _2 \frac{1}{p_i}\right\rceil
$$
where $\lceil x\rceil$ is the rounding up operation.
Note that $x \leq\lceil x\rceil<x+1$. Therefore
$$
L=\sum_i p_i \ell_i<\sum_i p_i\left(\log _2 \frac{1}{p_i}+1\right)=H(X)+1 .
$$
Verify that Kraft inequality is satisfied:
$$
\sum_i 2^{-\ell_i}=\sum_i 2^{-\left\lceil\log _2 \frac{1}{p_i}\right\rceil} \leq \sum_i 2^{-\log _2 \frac{1}{p_i}}=\sum_i p_i=1
$$
$\implies$ we can construct a prefix-free code with this set of lengths.
### 2. Huffman coding
Huffman coding gives an **optimal** prefix-free code for a given set of probabilities.

An optimal prefix-free code have the following properties:
1. The length are ordered inversely with the probabilities (i.e. if $p_j > p_k$, then $\ell_j \leq \ell_k$).
2. The two least probable symbols have the same length and are on neighbouring leaves in the binary tree (i.e. they differ only the in the last digit).

#### Algorithm
1. Take the two least probable symbols in the alphabet (which will have the longest codeword, equal length, and differ only in the last digit).
2. Combine these two symbols into a single symbol, and repeat.

A working example:
![[Huffman-coding.png | center | 500]]
#### Optimality of Huffman coding
For a given set of probabilities, there is no prefix-free code that has smaller expected length than the Huffman code.
(Note: we can have different Huffman codes for the same source, but they will have the same expected code length.)
For Huffman coding, the expected code length is less than $H(X) + 1$.

#### Weakness of Huffman code
- symbol-by-symbol Huffman coding may give an expected length closer to $H(X) + 1$ bits/symbol rather than $H(X)$
- to reduce this overhead of 1 bit/symbol, could use Huffman code for blocks of $k$ symbols
- however, this increases the complexity as the alphabet size is now $|\mathcal{X}|^k$ and a block of $k$ symbols have to be decoded at a time

### 3. Interval coding
#### Algorithm
**Key idea:** Each symbol can be represented as an interval inside $[0, 1]$, with length of the interval equal to the symbol probability.

A source with $m$ symbols with probabilities $\{p_1, \ldots, p_m\}$ is represented using the $m$ intervals
$$
[0, p_1), [p_1, p_1 + p_2), \ldots, [\sum_{i=1}^{m-1}p_i,\sum_{i=1}^{m-1}p_i + p_m)
$$
In general, the binary codeword for a symbol with probability $p$ represented by the interval $[a, a+p)$ can be obtained as follows:
1. Find the largest dyadic interval of the form $\left[\frac{j}{2^{\ell}}, \frac{j+1}{2^{\ell}}\right)$ that lies within $[a, a+p)$. (Here $j, \ell$ are integers)
2. Take the binary representation of the lower end-point of the dyadic interval as the codeword. (This will be the integer $j$ converted to binary and represented using $\ell$ bits.)
#### Code length
In interval coding, the length of the binary codeword for a symbol with probability $p$ is either $\left\lceil \log_2 \frac{1}{p} \right\rceil$ or $\left\lceil \log_2 \frac{1}{p} \right\rceil + 1$ bits.

The expected code length can therefore be bounded as
$$
L=\sum_i p_i \ell_i \leq \sum_i p_i\left(1+\left\lceil\log _2\left(1 / p_i\right)\right\rceil\right)< H(X)+ 2
$$
Note that the performance is not as good as Huffman codes or even Shannon-Fano codes — but it is the basis for arithmetic coding.

### 3. Arithmetic coding
#### Algorithm overview
**Key ideas**:
- each length $n$ string $(x_1, \ldots, x_n)$ is represented by a **disjoint** interval with length equal to the probability of the string
- the interval for $(X_1 = x, X_2 = y)$ is a **sub-interval** of the interval for $X_1 = x$
- similarly, for any symbols $x, y, z$, $P(X_1 = x, X_2 = y, X_3 = z)$ is a sub-interval of $P(X_1 = x, X_2 = y)$, and so on

Example: Find the code word for the source sequence $(X_1 = b, X_2 = c, X_3 = a, X_4 = c)$, where $\{a,b,c\}$ has probabilities $\{0.2, 0.45, 0.35\}$.
![[arithmetic-coding.png | center | 600]]
Finding the code word:
- the binary codeword for an interval of length $p$ is obtained by finding the largest dyadic interval of the form $[\frac{j}{2^{\ell}}, \frac{j+1}{2^\ell})$ that is contained within the interval
- the code word length is either either $\left\lceil \log_2 \frac{1}{p} \right\rceil$ or $\left\lceil \log_2 \frac{1}{p} \right\rceil + 1$ bits (as mentioned for interval coding)

Decoding:
- use the binary codeword to sequentially zoom in to the interval
- decode the symbols while going along (find which symbols belong to that interval)

#### Expected code length
- Arithmetic coding can be performed for any sequence of length $n$
- any sequence can be represented by an interval of length $p(x_1, \ldots, x_n)$, which gives a binary codeword of length at most $\left\lceil \log_2 \frac{1}{p(x_1, \ldots, x_n)} \right\rceil + 1$
The expected code length for length $n$ sequences is bounded as
$$
L_n=\sum_{x^n} p\left(x^n\right) \ell\left(x^n\right)<\sum_{x^n} p\left(x^n\right)\left(\log _2 \frac{1}{p\left(x_1, \ldots, x_n\right)}+2\right)=H\left(X^n\right)+2
$$
The expected code length per symbol is 
$$
\frac{L_n}{n}<\frac{H\left(X^n\right)}{n}+\frac{2}{n}=H(X)+\frac{2}{n},
$$
where the last equality holds if $X_1, X_2, \ldots$ are iid $\sim P_X$.
$\implies$ with growing $n$, arithmetic coding can achieve expected code length/symbol that is arbitrarily close to the source entropy.

#### Arithmetic coding for non-iid sources
![[arithmetic-coding-non-iid.png | center | 500]]
To code $X_2$, divide the chosen interval for $X_1$ in the proportions of the symbol probabilities for $X_2 \mid X_1$.
In general, to code symbol $X_n$, use the **conditional** distribution of $X_n$ given the observed $(x_1, \ldots, x_{n-1})$.

#### Encoding algorithm (formal)
- Let the source alphabet $\mathcal{A}$ be $\left\{a_1, \ldots, a_m\right\}$. 
- We are given a source sequence $x_1, x_2, \ldots, x_n$ where each $x_i \in \mathcal{A}$. 
- Both encoder and decoder know the conditional distributions $$ P_{X_1}, P_{X_2 \mid X_1}, \ldots, P_{X_n \mid X_1, \ldots, X_{n-1}} $$
- The encoding algorithm computes the interval using the following lower and upper cumulative probabilities. For $i=1, \ldots, m$ and for $k=1, \ldots, n$, we define $$ \begin{aligned} & L_k\left(a_i \mid x_1, \ldots, x_{k-1}\right):=\sum_{i^{\prime}=1}^{i-1} P\left(X_k=a_{i^{\prime}} \mid X_1=x_1, \ldots, X_{k-1}=x_{k-1}\right) \\ & U_k\left(a_i \mid x_1, \ldots, x_{k-1}\right):=\sum_{i^{\prime}=1}^i P\left(X_k=a_{i^{\prime}} \mid X_1=x_1, \ldots, X_{k-1}=x_{k-1}\right) \end{aligned} $$![[arithmetic-coding-encoding-algo.png]]

Backlinks:
[[Probability]]
[[Channel Coding]]
[[Error-Correcting Codes]]