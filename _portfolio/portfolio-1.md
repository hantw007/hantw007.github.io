---
title: "Evolving Finite State Machine (e-FSM)"
excerpt: "An online evolving method named evolving Finite State Machine (e-FSM) can determine unknown states (situations) and identify transitions. At the moment, it is similar to Markov Chain, but its structure evolves over time. This approach enables controllers to recognize unexpected situations and learn optimal decisions over time. Also, the e-FSM is fully explainable, while Deep Neural Network is not."
collection: portfolio
---

## Overview of an online evolving method: evolving Finite State Machine (e-FSM)

An online evolving method named evolving Finite State Machine (e-FSM) can determine unknown states (situations) and identify transitions. At the moment, it is similar to Markov Chain, but its structure evolves over time. This approach enables controllers to recognize unexpected situations and learn optimal controls (or decisions) over time. Also, the e-FSM is fully explainable, while Deep Neural Network is not.

## What is the optimal control?
The optimal controller requires to choose actions to satisfy the given criteria. If there are conflicted criteria (e.g., safety and speed), the appropriate trade-off is required. The recognition of latent factors (e.g., collision risk in the future) can be useful for the appropriate trade-off. Also, the determination of unexpected but experienced situations needs to recognize the latent factors in advance.

#### Table: Approaches for the optimal controls or decision-making
| Approached | Online optimal solutions learning<br> in unknown situations? |  Online recognition of <br> latent factors? | Prerequisites |
| :-------------------------: | :-----: | :----: | :--------------------------------:|
|           Rule-based        |    No   |   Yes  | Optimal rules for all situations  |
| Supervised <br> Learning    |    No   |   Yes  |    Labeled dataset / structure    |
| Reinforcement <br> Learning |   Yes   |    No  |           Reward-function         |

## What is the e-FSM?
The e-FSM is similar to the Finite State Machine (or Markov Chain), which consists of states and transitions. However, the total number of states is not initially defined but increased over time by determining new states. Transitions between determined states are identified in an iterative way and are represented by Transition Probability Matrices (TPMs).
