---
title: Paper Review - Control as Inference
image: /assets/img/posts/control_inference.png
description: >
  Demonstrate how Reinforcement Learning can be modeled as a Probabilistic Inference problem
---

<!-- In the context of...
and after analyzing the different properties of ...
Probabilistic inference can be used in a lot of [...] explain why we chose to do this. -->

## Purpose
Reinforcement Learning (RL) is a method that aims to find an agent’s optimal course of actions given a set of possible actions, a set of possible states and an objective function representing the reward that awaits the agent. However, according to Sergey Levine, professor at UC Berkeley, reinforcement learning, or rather, optimal control problems are equivalent to a complete probabilistic inference problem as described by a probabilistic graphical model (PGM) with additional optimality variables modelling the reward function. This can prove to be useful with the powerful inference techniques of a PGM that can be used to solve various RL-related queries. Futhermore, it also allows for the modelling of sub-optimal behavior, useful for certain contexts, while standard RL methods only model the optimal behavior.

From there, my colleagues **Afuad-Abrar Hossain, Tony Brière and I** decided to dig deeper into this subject and reviewed the research paper from Dr. Levine which proposes this concept: [Reinforcement Learning and Control as Probabilistic Inference](https://arxiv.org/pdf/1805.00909.pdf). This paper shows how optimization in the context of decision-making and inference on probabilistic graphical models are equivalent. We demonstrated this idea in greater details by presenting this duality and implementing an application of this framework using the OpenAI Gym environment and building a game-playing agent in the *Frozen-Lake* game.

For the complete review, implementation, experiments and analysis of our findings see the full article below.

## Article

### Abstract

In recent years, formulating Reinforcement Learning as PGMs have gained considerable traction due to the availability of powerful inference techniques useful in solving various RL related queries. In this paper, we explore the *RL as Probabilistic Inference* framework and outline both an implementation of the traditional framework for RL and the PGM representation of RL, thereafter comparing their performances on the Frozen Lake game. We show that the the optimal policy retrieved via exact inference from the PGM framework is equivalent to the optimal policy derived from the traditional RL framework in the case of deterministic dynamics. Moreover, in the case of stochastic dynamics, we show that the policy retrieved via exact inference exhibits *optimistic (risk-seeking)* behavior, but is once again equivalent to the traditional RL optimal policy when retrieved via variational inference. 

<html>
<head>
  <meta charset="UTF-8">
  <title>PDF.js Example</title>
  <script src="/assets/js/pdfjs/build/pdf.js"></script>
  <script src="/assets/js/pdfjs/build/control_inference/simple.js"></script>
</head>
<body>
  <a target="_blank" href="/assets/js/pdfjs/web/viewer.html?file=/assets/js/pdfjs/build/control_inference/RL_Probabilistic_Inference.pdf">
    <canvas id="pdf"></canvas>
  </a>
</body>
</html>

[Link to the article](/assets/js/pdfjs/web/viewer.html?file=/assets/js/pdfjs/build/control_inference/RL_Probabilistic_Inference.pdf). 