## I. Introduction to learning
![[intro-to-learning.png | center | 500]]
Genotype and phenotype:
- the genotype determines the phenotype, which in turn determine the **fitness** of the organism in a given environment
- nervous system and behaviour it produces are part of the phenotype and a major determinant of fitness
- behaviour changes the environment and provided feedback to the nervous system in the form of sensory inputs
- learning is a process of **reconfiguring the nervous system based on experience** -> change the behaviours -> ultimately change the fitness

The importance of learning:
- when the environment and thus the fitness landscape is non-stationary or is very 'spiky' (difficult fitness landscape), changes in genome may have too low a probability to find high fitness regions of the fitness landscape
- learning helps by acting on **faster time scales** than genetic changes -> mitigating the effects of the environment non-stationarity
- learning also **provides mechanisms** by which organisms can adaptively change their phenotype rather than 'random search' of genetic modifications



## II. Synaptic transmission
### 1. Synaptic transmission mechanism
![[synaptic-transmission.png | center | 600]]

Full transmission process (EPSP example):
1. action potential generated in the presynaptic neuron propagates along the axon of the presynaptic cell
2. presynaptic action potential arrives at the presynaptic terminal, depolarising the membrane potential
3. voltage dependent Ca2+ channels open in the presynaptic membrance
4. intracellular Ca2+ entry causes vesicle fusion
5. the neurotransmitter in the vesicles are released into the synaptic cleft
6. neurotransmitter diffuse across the cleft
7. neurotransmitter binds with the receptors and open ion channels in the postsynaptic membrane
8. Na+ enters (increase membrane potential) and K+ leaves the ion channels (decrease membrane potential)
9. on balance more Na+ enters than K+ leaving the postsynaptic cell -> cell becomes depolarised

Note:
- In the process, only the fusion of vesicles require direct energy expenditure. 
- However, events that involve the crossing of ions through ion channels leads to indirect energy expenditure of selective molecular pumps.
- Ca2+ is a second messenger that reacts with calmodulin kinase

Dale's principle: All efferent (output) synapses of a given neuron onto other neurons **have the same 'sign'** -- either excitatory or inhibitory.
- excitatory neurotransmitter: glutamate
- inhibitory neurotransmitter: GABA

What determines whether a synapse is excitatory or inhibitory?
- the sign is determined by the neurotransmitter, which binds to a specific group of receptor in the postsynaptic membrane -- the receptor have either excitatory or inhibitory effects
- the effect is determined by whether the reversal potential of the ion channel controlled by the receptor is **above** (excitatory) or **below** (inhibitory) the spiking threshold potential
- even if the reversal potential is above the resting membrane potential but below the threshold, it is still inhibitory -- the cell will act as a **'shunt'** (aka shunt inhibitory), increasing the total membrane conductance, making it harder for the post-synaptic cell to reach the threshold

### 2. Receptor types
Receptor types:
![[receptor-types.png | center | 500]]
- ionotropic receptor directly opens ion channel open binding with the neurontrasmitter
- metabotropic receptor activates biomedical pathway through second messengers, which would open the channel

Ionotropic glutamate receptors:
![[NMDA-AMPA.png]]
- for AMPA receptor, the conductance of the ion channel is **constant** -- contribute to the early current
- for NMDA receptor, the conductance is **voltage dependent** -- contribute to the late current
	- the current is small for low membrane potential
	- the current increases when the membrane potential exceeds a threshold
	- the current is linear for high membrane potentials
- the NMDA receptor has a Mg2+ block that is removed only when the postsynaptic membrane is depolarised
- Ca2+ ions (act as a second messenger) can enter after the Mg2+ block is removed AND glutamate binds to the receptor -> it is a **molecular coincidence detector** of BOTH presynaptic and postsynaptic activity
- APV is a specific inhibitor for NMDA channel that blocks the ion channel

## III. Learning in the Aplysia
### 1. Habituation
Experiment:
- before training: harmless stimulus -> defensive response
- training: present stimulus
- after training: stimulus -> diminished response

Mechanism:
- distributed change as several synapses participate
- **EPSPs caused by sensory neurons reduced** due to:
	- decreased number of presynaptic vesicles released into cleft
	- this is caused by reduced mobilisation to active zone
- this change is homosynaptic

Importance of training schedule:
- massed training -- 1 session of 10 stimuli separated by 10s of seconds
	- the effect lasts for minutes
- spaced training -- 4 sessions of 10 stimuli in each, separated by hours or days
	- the effect lasts three weeks
- different mechanism:  spaced training leads to **reduction in the number of synapses**

### 2. Sensitisation
Experiment:
- before training: harmless stimulus A (siphon touch) -> weak / no response
- training: noxious stimulus B (tail shock)
- after training: stimulus A -> enhanced response

Mechanism:
![[sensitisation.png | center | 500]]
- noxious stimulus causes **interneuron** to release serotonin (5-HT)
- 5-HT binds to metabotropic receptor and initiate biochemical processes mediated by G-proteins and cAMP (the second messenger)
- cAMP leads to 3 pathways
	1. K+ current decreases -> longer action potential
	2. more vesicles in the readily releasable pool (the active zone) -> more transmitters will be released
	3. more Ca2+ channels open so there is a larger Ca2+ current -> Ca2+ promote vesicle fusion and transmitter release
- the enhancement of synaptic strength between the sensory and motor neuron is faciliated by modulatory interneuron -> heterosynaptic
- long term sensitisation: more synapses between the sensory and motor neuron

### 3. Classical conditioning
Experiment:
- before training:
	- harmless stimulus A -> weak / no response
	- harmless stimulus B -> weak / no response
- training:
	- stimulus C **paired** with B -> strong response
	![[classical-conditioning-exp.png | center | 400]]
- after training:
	- stimulus B -> enhanced response
	- stimulus A -> unchanged response
- the effect is specific to CS+ -> CS+ and US get associated -- **associative learning**

Sensitisation vs classical conditioning:
- in sensitisation, all stimuli elicit vigorous response
- in classical conditioning, only on stimulus shows enhanced response
- classical conditioning leads to greater enhancements and the effect lasts longer

Mechanism:
![[conditioning.png | center | 500]]
Presynaptic:
- US causes interneuron to release 5-HT
- 5-HT bind with metabotropic receptors on the sensory neuron coupled with **adenylyl cyclase** enzyme
- adenylyl cyclase is a **coincidence detector** between CS and US:
	- CS activation causes an action potential which leads to Ca2+ influx
	- the Ca2+ influx boosts the effect of serotonin receptor activation on adenylyl cyclase
	- adenylyl cyclase produce **more cAMP** which activates 3 pathways that also appeared in sensitisation

Postsynaptic:
- on CS, sensory neuron release glutamate
- glutamate binds to glutamate receptors on the motor neuron, which includes NMDA receptors
- NMDA receptors act as a **coincidence detector** between the CS and the motor response:
	- on US, the motor neuron depolarises and the Mg2+ block in the NMDA receptor channel is removed
	- the NMDA receptors binds with glutamate released on CS by the sensory neuron
	- channel opens and lead to Ca2+ influx
- the Ca2+ influx causes **retrograde messenger** (NO, CO) to diffuse into the presynaptic sensory neuron
- retrograde messenger bind to enzymes in the cytoplasma of the sensory neuron and result in enhance neurotransmitter release

There isn't much sensitisation on CS- since:
- the effect of conditioning is much larger
- CS- is presented during training unlike training for sensitisation

## IV. Long-term potentiation
### 1. Hippocampus
- located in the medial temporal lobe
- an evolutionarily older part of cortex (archicortex with only three layers, cf. neocortex with six layers)
- main regions: the dentate gyrus, CA1, CA3, the subiculum
![[hippocampus.png | center | 500]]

Trisynaptic loop:
1. Perforant pathway: from the entorhinal cortex to the granule cells of the dentate gyrus
2. Mossy fibre pathway: from axons of the granule cells to the pyramidal cells of CA3
3. Schaffer collateral pathway: from axons of CA3 pyramidal cells to the pyramidal cells of CA1
- each pathway is very sensitive to the history of previous activity
![[hippocampus-loop.png | center | 500]]

Amnesia in H.M.
- bilateral temporal lobectomy: 2/3 of medial temporal lobes lesioned
- ![[case-of-HM.png | center | 500]]
### 2. In vivo and in vitro preparations
In vivo = "in the dish"

| Method         | Description                                    | Advantages                                                                | Disadvantages                                                                                       |
| :------------- | ---------------------------------------------- | ------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Slice          | remove neural circuit after sacrificing animal | - isolated<br>- stable electrodes<br>- accurate placement<br>- repeatable | - extration damage slices<br>- inputs, outputs and other connection pruned<br>- dies fairly quickly |
| Tissue culture | grow tissue separate from organism             | - as above<br>- die less quickly                                          | - different development to those in the brain<br>- no anatomical connection                         |

In vitro = "in the living animal"

| Method         | Description                           | Advantages                                                                                                          | Disadvantages                                                                                                          |
| -------------- | ------------------------------------- | ------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------- |
| Anaesthestised | put animal to sleep using anaesthetic | - intact preparation<br>- normal development<br>- normal anatomy                                                    | - anaesthetic affects neural functions<br>- intracellular recording very hard<br>- less controllable and repeatable    |
| Behaving       | record while animal free to behave    | - can link to behaviour<br>- no anaesthetic<br>- only direct link between neural processing and learning and memory | - can't record intracellularly<br>- multiple cells at once so could be hard to analyse<br>- hard to control and repeat |

Stimulation and recording techniques:
- intracellular:
	- individual cells
	- high signal to noise ratio
- extracellular:
	- many cells at once
	- low SNR
- possible combination:
	- extra stimulation, extra recording
	- extra stimulation, intra recording
	- intra stimulation, intra recording
- unfeasible:
	- intra stimulation, extra recording -- could hardly be detected
![[stimulation-recording.png | center | 300]]

- an excitatory synaptic event cause Na+ ions to flow into the dentrite -- negative current at 2
- inside the cell, the positive current moves toward the soma -- measured at 1
- at 3, a return current flows out of the neuron, generating a current source

### 3. Long-term potentiation (LTP)
Experimental results:
- only high frequency stimulation at 15/sec leads to LTP
	- NMDA channels in the postsynaptic membrane blocked by Mg2+
	- Mg2+ block removed when the postsynaptic membrane is sufficiently depolarised
	- individual EPSP leads to a depolarisation that decays to 0 on 10~10ms timescale
	- when EPSPs arrive with interval significantly larger than this, the successive EPSPs do not add up
	- when EPSPs arrive in rapid succession, they add up to create larger depolarisations which can remove the Mg2+ block
	- the entry of Ca2+ leads to LTP
- during high frequency stimulation:
	- larger EPSPs
	- population spike occurs earlier
	- slightly smaller population spike amplitude
- shortly after high frequency stimulation: rebound
	- smaller EPSPs
	- later population spike
	- not much change in population spike amplitude
- longer time after high frequency stimulation:
	- larger EPSPs
	- earlier population spike
	- lager population spike amplitude
- reason of change in the size of the population spike
	- more cells fire
	- more synchronicity in cell firing
![[effect-of-LTP.png | center | 400]]
![[LTP-experiment.png | center | 500]]


Induction of LTP: What's the signal to a synapse to undergo LTP?
1. presynaptic neuron spikes
2. calcium channel open, Ca2+ moves in
3. docking and fusion of vesicles
4. glutamate releases
5. glutamate diffuses across the synaptic cleft
6. glutamate binds to AMPA and NMDA receptors
7. AMPA channels opens
8. postsynaptic cell depolarises
9. NMDA channels open if glutamate still present
10. Ca2+ influx through NMDA channel -- end of induction

Note:
- NMDA acts as a coincidence detector
- intracellular calcium dynamics in postsynaptic neuron determine whether it is LTP (rapid and high) or LTD (slow and low)
![[induction-of-LTP.png | center | 400]]

Expression of LTP: How does the synapse undergo the efficacy change once it has been signalled?
- Early LTP:
	1. Ca2+ influx into the postsynaptic cell leads to retrograde messenger (possibly NO) release
	2. retrograde messenger casuses enhanced transmitter release
	3. in postsynaptic cell Ca2+ binds to calmodulin
	4. the binding catalyses other reactions, including enhancement on the AMPA receptors
		- Ca2+-calmodulin kinase adds phosphate group to AMPA
		- AMPA conductance increases -> larger EPSP
- Late LTP:
	1. Ca2+-calmodulin complex -> cAMP -> nucleus synthesis new receptors and other proteins
	2. proteins ('building blocks') are transported from soma to new synapse site
	3. new synapse is created
![[expression-of-LTP.png | center | 400]]

Suggestive properties that LTP/LTD are involved in memory:
- cooperativity -- need more than one input active
- associativity -- if a subset of the inputs fire and the postsynaptic cell fires, only that subset undergo LTP
	- synapse-specific -> higher memory capacity
	- associative -> suitable for associative learning
	- long-lasting -> memory retention

Note: 
- learning and memory involves BOTH synaptic plasticity dynamics and network dynamics
- example of behavioural effect that cannot be explained by synaptic plasticity alone
	- known forms of LTP require coincidences of order of milliseconds
	- associations can be made over seconds/minutes/hours

### 4. Experiments
Spatial navigation task:
- apparatus: the plus maze
- behaviour paradigm for training and testing:
	- starting from the same arm of the maze
	- rewarded for going another fixed arm of the maze
	- in test trials, the animal is started from a **novel** arm of the maze
- key behavioural measure of learning: measure whether the animal chooses
	- the originally trained arm -- the 'place' choice
	- or the arm that is in the same relative location as the originally trained arm was to the starting position -- the 'response' choice
- pharmacological interventions:
	- reversible inactivation of the **hippocampus** and the **striatum** (caudate nucleus) by **lidocaine**
	- as a control, inject saline the same brain area
	- inject lidocaine or saline on day 8 or day 16 of training
- result:
	- after short training, the 'place' choice dominates
	- after long training, the 'response' choice dominates
	- result reverted when hippocampus is inactivated after short training (day 8) -> hippocampus information predominantly used after short but not extending training -- spatial memory
	- result reverted when striatum is inactivated after long training (day 16) -> striatum information used after extended but not short training -- response based memory
![[spatial-navigation-task.png | center | 500]]

Spatial memory tasks:
- Barnes maze:
	- mouse placed in a well lit platform
	- hole around the rim of the platform
	- one hole leads to an escape tunnel
	- a set of contextual cues around the apparatus
	- mice can learn to associate the cues on the walls with the presence or absence of an escape route
- Morris water maze:
	- similar to the Barnes maze
	- cues on walls of the enclosure as before
	- the enclosure is filled with water which contains a raised platform in some location
	- mice can memorise where the platform is overtime
- start at a different local each time to see if the animal learns the position or action
- measure:
	- fraction of correct choices
	- escape latency
	- without the opportunity to escape, measure the time spent in goal area or goal quadrant
- lesion studies shows that **good performance requires intact hippocampus**
![[spatial-memory-tasks.png | center | 300]]



Correlational study: exploration and LTP
- implant electrode into rate and measure EPSPs continuously from awake behaving animals
- let animals explore a novel environment and measure the population EPSPs
- population EPSP amplitude and slop increases with exploration and declines slowly overtime after exploration stopped
- **actually**, these effects are due to changes in brain temperature as animals become more active and muscular effort raises brain temperature
- conclusion: correlation between EPSP and exploration DOESN'T mean causal relationship between LTP and place field formation

### 5. Perturbation with drugs
Agonist vs antagonists:
- agonist = chemical that binds to a receptor and causes same response by cell as normal
- antagonist = chemical that binds to a receptor but does not cause a biological response
![[agonist-antagonist.png | center | 400]]
Perturbation of experiments with drugs:
- AP5 is an NMDA receptor antagonist
- experiment paradigm:
	1. inject AP5 chronically, inject saline on control group
	2. train animal on spatial memory task (e.g. water maze task)
	3. perform transfer test: remove platform and see where rats search for it 
	4. test inducability of LTP
- result:
	- control and AP5 rates learn to escape in small number of trails but the AP5 rats appear to learn more slowly and inaccurately
	- AP5 rats did not search platform near its former location during the transfer test, whereas control rats did
	- AP5 blocks NMDA receptors so no LTP induced!
- the effect is specific to spatial learning (the control and AP5 rats would perform identically on visual discrimination task)
- storage of spatial memory is affected but not retrieval
![[perturbation-with-drugs.png | center | 300]]

## V. Reinforcement learning
### 1. The Rescorla-Wagner rule
Motivation: predict **rewards** depending on stimuli presented

Response:
$$
r = \sum_i s_i w_i
$$
- $r$: the response -- prediction of US
- $s_i$: conditional response CSi -- 0 = absent, 1 = present
- $w_i$: 'weight'i -- degree of association of CSi with US
- $u$: unconditional response US - 0 = absent, 1 = present

Error:
$$E = (u-r)^2 = \left(u - \sum_i s_i w_i\right)^2$$

Update direction: 'stochastic gradient descent' -- minimise error w.r.t. weights
$$-\frac{\partial E}{\partial w_i} \propto \underbrace{(u-r)}_{\delta}\,s_i$$
where $\delta$ is the **signed prediction error**.

Update rule:
$$
w_i \rightarrow w_i + \epsilon \delta s_i$$
where $\epsilon$ is the learning speed $\ll 1$.

**Pavlovian conditioning:**
![[pavlovian-conditioning.png | center | 300]]
- $w$ grows from 0 to 1
- curve is exponential decay with time constant $1/\epsilon$

**Pavlovian extinction:**
![[pavlocian-extinction.png | center | 300]]
- starts like classical conditioning
- then present CS in isolation
- conditioning stopped -- extinction
- weights decrease exponentially

**Partial reinforcement:**
![[partial-reinforcement.png | center | 400]]
- reward becomes stochastic
	- when US = 1 and CS = 1 -> exponential increase in $w$
	- when US = 0 and CS =1 -> exponential decrease in $w$
- $w$ converge to $\langle u\rangle$ -- the expectation of $u$
- weight represents probability of association of US and CS -- weaker response
- learning rate effects:
	- small -> small fluctuations but less adaptive
	- large -> large fluctuations but more adaptive (favourable in highly volatile environment)

**Overshadowing:**
![[overshadowing.png | center | 300]]
- get a weaker response when the CSs are presented in isolation at the end
- to adjust the association between the US and the two CS, modify the learning rate so different for each stimulus

**Blocking:**
![[blocking.png | center | 300]]
- CS2 is presented after CS1 has been conditioned
- prediction error already low, nothing to drive the learning with CS2

**Inhibitory conditioning:**
![[inhibitory-conditioning.png | center | 300]]
- $w_1$ converge to 1 and $w_2$ converge to -1
- negative prediction error means
	- third stimulus CS3 + CS2 -> reduced response
	- subsequent of a positive association between CS2 and US is slowed
- no response when CS1 and CS2 presented together

Can't explain secondary conditioning:
![[secondary-conditioning.png | center | 300]]

### 2. The temporal-difference learning rule

Rescorla-Wagner rule vs temporal-difference learning rule:
![[RW-vs-TD.png | center | 500]]

Motivation: predict **total future rewards** depending on stimuli presented and within trial time $t$

Response: prediction of total future rewards from time $t$ within the trial
$$r(t) = \sum_i \sum^t_{\tau=0}s_i (t-\tau) w_i (\tau)$$
Objective to predict:
$$\sum^T_{\tau=t} u(\tau)$$

Error:
$$E(t) = \left(\sum^T_{\tau=t}u(\tau) - r(t)\right)^2 = \left(\sum^T_{\tau=t}u(\tau) - \sum_i \sum^t_{\tau=0}s_i (t-\tau) w_i (\tau)\right)^2$$

Update direction:
$$\frac{\partial E(t)}{\partial w_i(\tau)} \propto \left(\sum^T_{\tau' = t}u(\tau') - r(t)\right)s_i(t-\tau)$$
Problem: the total future reward requires knowledge of reward beyond the current knowledge (need information until end of trail $t = T$)

Solution: use approximation
$$
\begin{aligned}
\sum^T_{\tau' = t}u(\tau') &= u(t) + \sum^T_{\tau' = t+1}u(\tau') \\
& \approx u(t) + r(t+1)
\end{aligned}
$$
this is known as **bootstrapping** as it if using $r$ itself to approximate the total error -- no external help.

This leads to:
$$\frac{\partial E(t)}{\partial w_i(\tau)} \stackrel{\approx}{\propto} \underbrace{\left(u(t) + \overbrace{r(t+1) - r(t)}^{\Delta r(t)}\right)}_{\delta} \,s_i(t-\tau)$$
where $\delta$ is the **temporal difference error**.

Time step update:
$$w_i(\tau) \rightarrow w_i(\tau) + \epsilon \delta(t) s_i(t-\tau)$$
where $\epsilon$ is the learning speed $\ll 1$.

### 3. Dopamine
- a neural substrate that acts on metabotropic receptors only
- drugs like cocaine and amphetamine leads to high dopamine levels
- extraverted, reward seeking people have high dopamine levels
- disorders related to dopamine disorder: schizophrenia (elevated levels of dopamine in pre-frontal cortex), Parkinson's (loss of dopamine secreting neurons), ADHD (associated with reduced activity)
- implicated in addiction and self-stimulation

**Dopamine = prediction error**
![[dopamine-effect.png | center | 500]]
- paradigm: monkeys trained to respond to stimuli like lights or sounds in order to obtain food and drink rewards
- cell respond vigorously to reward (US)
- before training cells do not respond to the light (CS)
- after training cell responds to light (CS), but not the reward (US)
- after training cell responds to absence of reward by suppressing baseline firing rate

### 4. Secondary conditioning
![[higher-order-conditioning.png | center | 600]]
- B and D unambiguously predict reinforcer (pain level)
- A and C provided uncertain information about reinforcer
- $\delta_i - \delta_j$ (where $i,j$ are trial types) are well explained in some regions of brain, e.g. ventral striatum






