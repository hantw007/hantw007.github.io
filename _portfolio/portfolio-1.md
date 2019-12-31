---
title: "Evolving Finite State Machine (e-FSM)"
excerpt: "An online evolving method named evolving Finite State Machine (e-FSM) can determine unknown states (situations) and identify transitions. At the moment, it is similar to Markov Chain, but its structure evolves over time. This approach enables controllers to recognize unexpected situations and learn optimal decisions over time. Also, the e-FSM is fully explainable, while Deep Neural Network is not."
collection: portfolio
---

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
<p>
  <img src="https://hantw007.github.io/images/MC_fig.png" width="300" height="200" align="center"><br>
  <em>Fig. 1: Markov Chain example</em>
</p>

The Markov-Chain's structure should be initially configured and fixed. In Fig. 1, the MC which consists of two states (s1 and s2) is presented. Transitions between states are represented by a matrix ![img](http://latex.codecogs.com/svg.latex?P_%7BMC%7D%0D%0A). Since the total number of states is two, the dimension of the transition probability matrix (TPM) is 2 by 2. 

On the other hand, the number of states in the e-FSM is niether initialized nor fixed. The states in the e-FSM are determined over time as needed. Instead of a single TPM, mutiple TPMs are implemented in the e-FSM, where each TPM is corelated with possible actions. Therefore, the dimension of all TPMs is varied based on the determination of states. The below fig.2 shows an example of the e-FSM's evolving sequence.

<p>
  <img src="https://hantw007.github.io/images/eFSM_evolve_fig.png" width="800" height="300" align="center"><br>
  <img src="https://hantw007.github.io/images/trMat_fig.png" width="800" height="80" align="center"><br>
  <em>Fig. 2: Evolving example of the e-FSM</em>
</p>

In the example, there was a single state (s1) by t=2. Based on a chosen action at time t, ![img](http://latex.codecogs.com/svg.latex?a%28r%29), all TPMs, ![img](http://latex.codecogs.com/svg.latex?%5Cmathbb%7BP%7D_t%5E%7Ba%28r%29%7D)![img](http://latex.codecogs.com/svg.latex?%5Cforall)r, are 1 by 1 dimensional matrices. Until a new state (s2) is determined at t=3, the TPMs are identified. Once s2 is newly determined, dimension of all TPMs is expanded to 2 by 2, and they are identified by t=11 until s3 is determined.

Continue updating...
