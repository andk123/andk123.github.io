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
Reinforcement Learning is a method that aims to find an agent’s optimal course of actions given a set of possible actions, a set of possible states and an objective function representing the reward that awaits the agent. However, according to Sergey Levine, professor at UC Berkeley, reinforcement learning, or rather, optimal control problems are equivalent to a complete probabilistic inference problem as described by a probabilistic graphical model (PGM) with additional optimality variables modelling the reward function.

From there, my colleagues Afuad-Abrar Hossain, Tony Brière and I decided to dig deeper into this subject and reviewed the research paper from Dr. Levine which proposes this concept: [Reinforcement Learning and Control as Probabilistic Inference](https://arxiv.org/pdf/1805.00909.pdf). This paper shows how optimization in the context of decision-making and inference on probabilistic graphical models are equivalent, and we demonstrated this idea in greater details by presenting this duality and implementing an application of this framework using the OpenAI Gym environment by building a game-playing agent in the *Frozen-Lake* game.

## Article

For the complete review, implementation, experiment and analysis of our findings see the full article below.

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

[Link to the review](/assets/js/pdfjs/web/viewer.html?file=/assets/js/pdfjs/build/control_inference/RL_Probabilistic_Inference.pdf). 