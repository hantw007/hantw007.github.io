---
title: "Evolving Finite State Machine (e-FSM)"
excerpt: "An online evolving method named evolving Finite State Machine (e-FSM) can determine unknown states (situations) and identify transitions. At the moment, it is similar to Markov Chain, but its structure evolves over time. This approach enables controllers to recognize unexpected situations and learn optimal decisions over time. Also, the e-FSM is fully explainable, while Deep Neural Network is not."
collection: portfolio
---

## Design of evolving methodology: evolving Finite State Machine (e-FSM) for constructing a stochastic model from scratch without human intervensions.
<p>
  <img src="https://hantw007.github.io/images/eFSM.png" width="800" height="300" align="center">
</p>

-	Instead of designing a model by hand, evolving Finite State Machine constructs a stochastic model from scratch by determining states and identifying state-transitions.
-	State Determination: the observations are clustered by the online clustering method (e.g., evolving Takagi-Sugeno) and each cluster-center is considered as a state.
-	State-transition Identification: Observed consecutive variation of probability distributions at t-1 and t are used to identify state-transitions in an online way.
-	Project is sponsored by Ford Motor Company.
-	Publication(s): https://arxiv.org/abs/1908.10823


<!--
## Overview of an online evolving method: evolving Finite State Machine (e-FSM)

An online evolving method named evolving Finite State Machine (e-FSM) can determine unknown states (situations) and identify transitions. At the moment, it is similar to Markov Chain, but its structure evolves over time. This approach enables controllers to recognize unexpected situations and learn optimal controls (or decisions) over time. Also, the e-FSM is fully explainable, while Deep Neural Network is not.

## What is the optimal control?
The optimal controller requires to choose actions to satisfy the given criteria. If there are conflicted criteria (e.g., safety and speed), the appropriate trade-off is required. The recognition of latent factors (e.g., collision risk in the future) can be useful for the appropriate trade-off. Also, the determination of unexpected but experienced situations needs to recognize the latent factors in advance.


### Table: Approaches for the optimal controls or decision-making

| Approached | Online optimal solutions learning<br> in unknown situations? |  Online recognition of <br> latent factors? | Prerequisites |
| :-------------------------: | :-----: | :----: | :--------------------------------:|
|           Rule-based        |    No   |   Yes  | Optimal rules for all situations  |
| Supervised <br> Learning    |    No   |   Yes  |    Labeled dataset / structure    |
| Reinforcement <br> Learning |   Yes   |    No  |           Reward-function         |


## What is the e-FSM?
The e-FSM is similar to the Finite State Machine (or Markov Chain), which consists of states and transitions. However, the total number of states is not initially defined but increased over time by determining new states. Transitions between determined states are identified in an iterative way and are represented by Transition Probability Matrices (TPMs).

### Comparison between Markov-Chain (MC) and e-FSM  
The Markov-Chain's structure should be initially configured and fixed. In Fig. 1, the MC which consists of two states (s1 and s2) is presented. Transitions between states are represented by a matrix ![img](http://latex.codecogs.com/svg.latex?P_%7BMC%7D%0D%0A). Since the total number of states is two, the dimension of the transition probability matrix (TPM) is 2 by 2. 
<p>
  <img src="https://hantw007.github.io/images/MC_fig.png" width="300" height="200" align="center"><br>
  <em>Fig. 1: Markov Chain example</em>
</p>

On the other hand, the number of states in the e-FSM is niether initialized nor fixed. The states in the e-FSM are determined over time as needed. Instead of a single TPM, mutiple TPMs are implemented in the e-FSM, where each TPM is corelated with possible actions. Therefore, the dimension of all TPMs is varied based on the determination of states. The below fig.2 shows an example of the e-FSM's evolving sequence.

<p>
  <img src="https://hantw007.github.io/images/eFSM_evolve_fig.png" width="800" height="300" align="center"><br>
  <img src="https://hantw007.github.io/images/trMat_fig.png" width="800" height="80" align="center"><br>
  <em>Fig. 2: Evolving example of the e-FSM</em>
</p>

In the example, there was a single state (s1) by t=2. Based on a chosen action at time t, ![img](http://latex.codecogs.com/svg.latex?a%28r%29), all TPMs, ![img](http://latex.codecogs.com/svg.latex?%5Cmathbb%7BP%7D_t%5E%7Ba%28r%29%7D)![img](http://latex.codecogs.com/svg.latex?%5Cforall)r, are 1 by 1 dimensional matrices. Until a new state (s2) is determined at t=3, the TPMs are identified. Once s2 is newly determined, dimension of all TPMs is expanded to 2 by 2, and they are identified by t=11 until s3 is determined.

## Specific Features of the e-FSM
As briefly described, the e-FSM has two main features: online determination of states and online identification of transition probability matrices. Therefore, initially unexpected situations can be recognized, and future states could be predicted in advance.
<p>
  <img src="https://hantw007.github.io/images/eFSM_framework.png" width="800" height="300" align="center"><br>
  <em>Fig. 3: The e-FSM's framework</em>
</p>


### Online determination of states in the e-FSM
The online determination can be possible by using one of the online clustering methods, evolving Takage Sugeno. At every time-step <i>t</i>, a set of observations in a vector form (![img](http://latex.codecogs.com/svg.latex?z_t)) is implemented to update existing cluster centers or creating a new cluster. Each cluster-center is considered as a state in the e-FSM; the eTS is described in "Filev, D. et al., Markov chain modeling approaches for on board applications, ACC 2010".

When a new cluster is created, dimension of transtion probability matrices are expanded. Otherwise, similarities between a set of observations and existing states are calculated and normalized to use them as probability distributions of states. Since cluster-centers are represented as states in the e-FSM, the euclidean distance between a set of observation and existing cluster-centers is implemented for obtaining the similarities.

* State set in the e-FSM: ![img](http://latex.codecogs.com/svg.latex?S_t)={![img](http://latex.codecogs.com/svg.latex?s_t)(1), ![img](http://latex.codecogs.com/svg.latex?s_t)(2), ..., ![img](http://latex.codecogs.com/svg.latex?s_t)(![img](http://latex.codecogs.com/svg.latex?n_t))}, where ![img](http://latex.codecogs.com/svg.latex?n_t) is the total number of determined states by timestep <i>t</i>.
* Probability distributions of states at timestep <i>t</i> are <i>Prob</i>(![img](http://latex.codecogs.com/svg.latex?S_t)) =[![img](http://latex.codecogs.com/svg.latex?%5Cgamma_t%5E1%28z_t%29), ![img](http://latex.codecogs.com/svg.latex?%5Cgamma_t%5E2%28z_t%29), ..., ![img](http://latex.codecogs.com/svg.latex?%5Cgamma_t%5E%7Bn_t%7D%28z_t%29)]
  * ![img](http://latex.codecogs.com/svg.latex?%5Cgamma_t%5Ei%28z_t%29) is similarity between ![img](http://latex.codecogs.com/svg.latex?z_t) and ![img](http://latex.codecogs.com/svg.latex?z_t%5E%7B%2Ai%7D), where ![img](http://latex.codecogs.com/svg.latex?z_t%5E%7B%2Ai%7D) is ![img](http://latex.codecogs.com/svg.latex?i%5E%7Bth%7D) cluster-center.(<i>i</i>=1, ..., ![img](http://latex.codecogs.com/svg.latex?n_t)).
  

Continue updating...
-->
