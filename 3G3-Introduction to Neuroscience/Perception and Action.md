## I. Excitability
### 1. The membrane potential
Balance of chemical and electrical forces:
- high concentration of potassium (K+) ions inside
- K+ tends to diffuse down the concentration gradient
- positive charge accumulate on the outside and negative charge on the inside causing an electrical gradient that limit the diffusion
- when the chemical and electrical forces due to **concentration gradient and electrical gradient** cancel out there is no net flow
- membrane potential becomes the **Nernst potential**

The resting membrane potential:
- resting membrane potential interpolates between (a weighted combination) the Nernst potentials of all key players (K+, Na+ and Cl-)
- $V_{rest} \approx -70 \text{ mV}$

### 2. Neural communication
![[neural-communication.png | center | 500]]
![[passive-propagation.png | center | 500]]
**Passive propagation** that attenuates over time and distance
- Time constant: $\tau_m = C_m r_m$
- Length constant: $\lambda = \sqrt{\frac{R r_m}{2r_L}}$

$C_m$: membrane capacitance
$r_m$: specific membrane resistance \[$\Omega \cdot \text{mm}^2$\]
- **inversely proportional to** the ion channels density in the membrane
$r_L$: longitudinal (intracellular) resistivity \[$\Omega \cdot \text{mm}$\]

How to increase $\lambda$?
- $\lambda \propto \sqrt{\frac{R}{\rho}}$
- increase cable radius $R$
- decrease ion channel density $\rho$
- myelination to provide insulation
- do not rely entirely on passive propagation

### 3. The action potential
Hodgkin and Huxley's voltage clamp experiment:
- Goal: find out how the membrane current would behave -> can be used to find out conductances for individual channel types by blocking other channels
- set up a **high-gain negative feedback loop** to **inject into the cell a current** directly proportional to the difference between the momentary voltage and the target voltage
- the current need to be injected to maintain the voltage must be **equal and opposite** to the current flowing through the membrane through natural means (the current we want to find out)

The results from voltage clamp experiment:
![[voltage-clamp.png | center | 200]]
- Na+ channels **inactivate spontaneously**
- K+ channels do not inactivate spontaneously
- K+ channels have **slower dynamics** than Na+

Hodgkin-Huxley model:
The membrane current:
$$
C_m\frac{dV_m}{dt} = -g_{K+}(V_m - E_{K+}) -g_{Na+}(V_m - E_{Na+}) -g_{Cl-}(V_m - E_{Cl-})
$$

The gating equation of the **gate variables** $x = \{m, n, h\}$:
$$\tau_x(V_m)\frac{dx}{dt} = -x(t) + x_\infty(V_m)$$
- $m$ denotes the proportion of Na+ channels in the activated state (subunit activation)
- $h$ denotes the proportion of Na+ channels in the de-inactivated state (0 means all inactivated) (subunit inactivation)
- $n$ denotes the proportion of K+ channels in the activated state (subunit activation)

The momentary conductance for each ion species is given by a product of the associated gate variables (between 0 and 1), and their corresponding peak conductance ($\bar{g}_{K+}$ or $\bar{g}_{Na+}$):
$$
\begin{aligned}
g_{K+}(t) &= \bar{g}_{K+} n(t)^4 \\
g_{Na+}(t) &= \bar{g}_{Na+} m(t)^3 h(t)
\end{aligned}
$$
This models that a channel is **only open when all of its gates open.**

Dynamics of the gate variables:
- $m$ has the smallest time constant -> fastest response
- $h$ has the largest time constant -> slowest response
- as $V_m$ increases, both $n$ and $m$ gates open

![[HH-model.png | center | 500]]

Sequence of events during the action potential:
- as $V_m$ increases, both $m$ and $n$ gates open
- initially $|V_m - E_{Na+}| \gg |V_m - E_{K+}|$ Na+ ions flows in, $V_m$ grow further
- this activates both Na+ and K+ channels even more, but Na+ much faster than K+ ($m$ has smaller time constant) -- POSITIVE FEEDBACK
- this also decreases $h$, which inactivates Na+ channels -- NEGATIVE FEEDBACK
- once $h = 0$, the $K+$ channel dominates and brings $V_m$ back towards $E_{K+} = -85 \text{ mV}$
- at this stage, $h$ is still closed (since it has a large time constant) -> Na+ can't open -- refractory period

## II. Perception
### 1. Definitions
Sensation = receiving input from sensors
Perception = interpreting the sensory inputs

Sensory evidence is often ambiguous and incomplete ->
perception is merging sensory evidence with expectations (via probabilistic inference)

Origins of uncertainty in sensory perception:
- the **sensory transduction process** is always noisy (e.g. photoreceptors exhibit spontaneous voltage fluctuations)
- the **sensory representation of the world would remain ambiguous** due to the physical properties of the world and of our sensors (e.g. only 2 eyes and the front of an object always obstructs its back)

### 2. Bayesian perception
Hypothesis: the brain computes the posterior distribution
$$
p(x|s) \propto p(s|x)p(x)
$$
where $x$ is the stimulus (or state variables) in the world, and $s$ is the sensory input.

The brain needs:
- the likelihood function $p(s|x)$ -- accounts for sensory noise and quantifies the extent to which any $x$ is compatible with the sensory evidence $s$ (hard to make it sharper due to limit imposed by brain intrinsic noise, but can be made wider by lowering SNR)
- the prior $p(x)$ -- the belief in probability distribution of the world ($x$) before observing $s$
- both must be learned through experience

**Assumption for the form of the likelihood function:** sensory evidence typically involving many independent receptors in the periphery -> the likelihood function can be assumed to be **bell-shaped**.

With prior, **perception shifts towards prior mean, especially for large sensory noise.**

![[Bayesian-perception.png | center | 500]]



### 3. Sensation
Four dimensions of sensation:
1. Modality: the nature of the transducer that converts physical stimulus into action potentials sent to the brain (energies -> neural activity)
	- the receptors and neural channels for the different sense are independent
	- each sensory neuron responds to only one modality (no matter how the eye is stimulated, the resulting sensation is always visual)
2. Location: the location of the sensory stimulus in physical space or in a more abstract space of stimulus features
3. Intensity
4. Timing

Encoding location:
- the **spatial distribution** of sensory neurons activated by a stimulus conveys information about the stimulus location
- the **receptive field** characterises a **subset of sensory space** in which an appropriate stimulus elicits a reaction in the neuron, i.e. properties of a stimulus that gives a response in a neuron
- the resolution of sensory systems determined by:
	- the density of sensory receptors
	- the size of receptive fields
	- the neuronal noise level

Location coding schemes:
- local coding scheme
	- tile sensory space with receptive fields
	- advantage: easy discrimination of stimuli
	- disadvantage: combinatorial explosion -- need to many neurons
	![[local-coding.png | center | 300]]
- intensity coding scheme
	- each neuron codes for one dimension by firing at different rates
	- advantage: fewer neurons needed
	- disadvantages: 
		- noise limit resolution
		- estimating spike rate takes time
		- hard to represent multiple stimulus
		![[intensity-coding.png | center | 300]]
- coarse / ensemble coding scheme
	- neurons have large overlapping receptive fields
	- position encoded by many neurons **simultaneously**
	- can represent multiple stimuli
	- advantages: 
		- no need to estimate the rate over long time periods
		- noise in single neuron responses can be averaged out since a large number of neurons are activated -> increase encoding resolution
		![[ensemble-coding.png | center | 300]]


Spike train -- representation of information in action potentials
- a sequence of action potentials emitted by a neuron over a certain time window
- typically discretised using some finite time resolution
- represented as long binary word
- high dimensional mathematical objects
- low-dimensional features (e.g. spike count, first-spike latency, rank-order population code etc) carry most of the information

### 4. Representation of uncertainty
Two possible solutions listed in lectures:
1. Use neural activity to represent parameters of $p(x|s)$
	- the posterior distribution is represented as a weighted sum of basis functions
	- each neuron contributes one basis funciton
	- activity of M neurons = M parameters (weights)
	![[activity-parameter.png | center | 300]]
2. Use neural activity as samples from $p(x|s)$
	- needs only one neuron per variable to represent
	- after enough time, $p(x|s)$ can be reconstructed from the collected samples
	![[activity-sample.png | center | 300]]
	
## III. Multi-sensory integration

**Effect of combining sensory modalities:**
1. reduces detection thresholds
2. reduces variability in estimates of stimulus properties

### 1. Detection threshold
Detection threshold = lowest stimulus intensity that subject can detect

Measuring detection threshold: (all prone to response bias)
![[detection-threshold-measurement.png | center | 550]]

Two-alternative forced choice (2AFC) paradigm **(detection task)**:
- present two stimuli
- one but not the other has the stimulus
- vary intensity $x$ and plot percent correct vs. $x$
- the resulting curve is a sigmoid curve with steepness determined by the uncertainty $\sigma$ 
![[2AFC.png | center | 500]]

### 2. Multi-sensory enhancement
Behaviour test in cats:
- cat fixate directly ahead 
- walk to stimulus: sound (A), light (V) or both (AV)
- cat rewarded for correct location
- results:
	- low intensity unimodal stimuli often missed
	- bimodal stimuli improved by **more than the sum** of correct to each cue
	- performance drops with two cues if they conflict, cat usually goes between A & V
	- visual-auditory fusion is obligatory

Neurons in superior colliculus show **strong multi-sensory enhancement**:
- inverse effectiveness rule (enhancement is greater for weak stimuli since neuron activity may saturate for already strong stimuli)
- spatial rule (A and V must be co-located in space)
- temporal rule (A and V must be co-located in time)

### 3. Bayesian hypothesis and multi-sensory integration
![[combining-cues.png | center | 600]]
- The mean will shift towards the mean of the sharper likelihood function (one with lower uncertainty)
- The combined uncertainty is smaller than any of the individual uncertainties

Visual-vestibular integration experiment **(discrimination task)**:
- monkey sits on a motion platform that can be translated in any direction at a small angle $\alpha$ relative to straight heading
- a VR headset involving a 3D dot cloud allows the simulation of the visual flow consistent with any translation of the platform (which may or may not occur physically)
- monkey needs to choose whether the platform is going left or right
- measure the visual and vestibular inputs to the monkeys brain
![[psychometric-curve.png | center | 500]]

The plot on the left is a **psychometric curve**
- presents the proportion of rightward choices as a function of heading direction $\alpha$
- the smoothness / steepness reflects the uncertainties (or standard deviations) $\sigma$
- **the steeper the curve, the lower the uncertainty**
The plot on the right shows that that the detection threshold decreases with multi-sensory integration.

Neural correlates:
- extracellular recordings made in monkey MSTd (dorsal medial superior temporal)
- there are congruent cells: tuned similarly to heading directions under visual and vestibular cues
- and incongruent cells: tuned differently to heading directions under visual and vestibular cues
- congruency quantified to be -1 ~ 1 (not matches ~ matched)
![[multisensory-neural-activity.png | center | 500]]


- recordings on a single congruent cell (top-left) shows increased sensitivity when cues are combined (steeper slope)
- neural psychometric function (bottom-left, obtained from distribution of firing rates at different heading directions) shows decreased uncertainty
- **congruent cells are Bayes optimal and have choice probability > 0.5**
- choice probability: probability that a draw (at a random firing rate) from the "positive heading angle" distribution (response distributions when the monkey choose positive heading angle) is greater than the an independent draw from the "negative heading angle" distribution

## IV. Decision making
![[decision-making-overview.png | center | 500]]

### 1. Optimal decision making
![[optimal-decision-making.png | center | 200]]
- loss function $\mathcal{L}(a,x)$ characterises the cost of taking action $a$ in state $x$
- make decision so as to minimise the expected loss over $p(x|s)$ (the uncertainty about the world): 
	$$
	a^\star = \arg\min_a \langle \mathcal{L}(x, a) \rangle
	$$
- there could be an extra layer of variability of $\mathcal{L}$

Pointing task:
![[pointing-task.png | center | 400]]
- tightly controlled -- $\mathcal{L}(x,a)$ known, uncertainty due to motor variability of fingers, $p(z|z^\star)$
- $z$ is where the finger ends up and $z^\star$ is the aim
- for optimal decision, need to find $z^\star$ that maximises $\int r(z)p(z|z^\star) dz$
- optimal shift depends on the separation of the two circles
- results show that subjects are near-optimal

Intrinsic loss functions:
- if the lost function is in the form of $|x^\star - x|^\alpha$: 
	- when $\alpha$ is small, the average cost is less influenced by the outliers
	- when $\alpha$ is large, the average cost is strongly influenced by the outliers
- human are robust estimators with an intrinsic lost function close to the **Huber loss**: quadratic for small errors but linear for large errors
- hence we are robust to outliers
![[intrinsic-loss-function.png | center | 300]]

Objective of decision making:
- "achieve desired outcomes, avoid undesired ones"
- desired outcomes:
	- reward
	- getting it right
	- arousal, excitement, curiosity
- undesired outcomes:
	- punishment
	- getting it wrong
	- boredom
- get the reward as soon as possible -- **temporal discounting of value**

Suboptimal behaviours:
- there is a certain "reference level" in mind: above the level the outcomes are gains, below the level the outcomes are losses
- risk-averse or risk-seeking
- diminishing sensitivity to gains and losses
- nonlinear probability weighting

### 2. Signal detection theory
- evidence is provided for one of two alternatives $x_1$ and $x_2$
- detect $s$ and decide $x$ based on a threshold $\theta$, opt for $x_2$ if $s > \theta$
![[SDT.png | center | 200]]

- define hit rate as $p(s > \theta | x = x_2)$, and false alarm rate as $p(s > \theta | x = x_1)$
- an **receiver operating characteristic (ROC)** curve can be sketched -- it is hit rate vs false alarm rate as the threshold goes from $-\infty$ to $+\infty$
- ideal ROC should be close to the point (0,1) -- high hit rate while having low false alarm rate
![[ROC.png | center | 200]]

- to maximise value, choose $x_2$ when log probability ratio $LPR > \log \frac{v_{11} - v_{12}}{v_{22} - v_{21}}$, where $v_{ij}$ is the value of deciding for $x_j$ when $x_i$ is true
- SDT provides a flexible framework to incorporate evidence, priors, and value into decisions to achieve a variety of goals
- the log variability ratio or any monotonic function of it could be used as a decision variable

### 3. Temporal integration

Neural correlates of evidence and choice:
- neurons in the primary sensory cortex encode sensory evidence
- neurons in the ventral premotor cortex might encode a decision variable

Evidence accumulation -- case study with coin flip
- two coins, one biased with $p(H) = 0.6$ and one unbiased
- use flips to decide which coin is biased
- define the decision variable as $DV_n = \log \frac{p(s_1, ... , s_n | \text{biased})}{p(s_1, ... s_n | \text{unbiased})} = \log \frac{p( \text{biased} | s_1, ... , s_n)}{1- p( \text{biased} | s_1, ... , s_n)}$
- update rule: $DV_n = DV_{n-1} + 0.182$ if $s_n = H$, or $DV_n = DV_{n-1} -0.223$ if $s_n =T$ -> a simple online summation
![[temporal-integration.png | center | 400]]

Random dot motion task:
- c% of dots move coherently and (100-c)% move randomly
- the monkey saccades to indicate which direction it believes the dots are moving towards
- the larger the c, the easier the task -- need shorter time to decide and better correct rate
- performance improves with viewing time

Drift diffusion model:
![[drift-diffusion-model.png | center | 400]]
- equation: $dx = \mu dt + \sigma dW$
- for small $dt:$ $x_{t+dt} = x_t + \mu dt + \sigma \sqrt{dt} \varepsilon_t,  \varepsilon_t \sim \mathcal{N}(0,1)$ 
- model parameters:
	- drift rate = stimulus strength (coherence)
	- decision bound = speed-accuracy tradeoff
	- starting point = response bias
- the model describes:
	- decision probabilities
	- distribution of reaction times

Recordings in MT:
- majority of neurons in the middle-temporal area (MT) are selective to a specific motion direction
- noisy but steady activity during the trial

Recordings in LIP:
- firing rates in LIP rise according to stimulus strength (coherence)
- saccades occur when firing rate reaches a threshold (the **same** threshold all the time)
- rise in firing rate is faster for shorter reaction time
![[LIP-recording.png | centern | 400]]














