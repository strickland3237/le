---
layout: distill
title: Exploring Meta-learned Curiosity Algorithms
description: This blog post delves into Alet et al.'s ICLR 2020 paper, Meta-learning curiosity algorithms, which introduces a unique approach to meta-learning curiosity algorithms. Instead of meta-learning neural network weights, the focus is on meta-learning pieces of code, allowing it to be interpretable by humans. The post explores the two meta-learned algorithms, namely Fast Action Space Transition (FAST) and Cycle-Consistency Intrinsic Motivation (CCIM).
date: 2024-05-07
future: true
htmlwidgets: true

authors:
  - name: Batsirayi Mupamhi Ziki
    affiliations: 
      name: University of Cape Town

# must be the exact same name as your blogpost
bibliography: 2024-05-07-exploring-meta-learned-curiosity-algorithms.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Introduction
  - name: Background
    subsections:
    - name: Reinforcement Learning
    - name: Meta-learning and Meta-RL
    - name: Random Network Distillation
    - name: BYOL-Explore
  - name: Meta-learning curiosity algorithms
    subsections:
    - name: Meta-Learned Components and their DAGs
    - name: Method
    - name: FAST
    - name: CCIM
  - name: Experiments
    subsections:
    - name: Emperical Design
    - name: Empty grid-world
    - name: Deep sea
    - name: Results
  - name: Discussion
  - name: Conclusion
---

## Introduction

Dealing with environments with sparse rewards, i.e., feedback comes at a low frequency, in reinforcement learning (RL) requires meaningful exploration.
One way to encourage the RL agent to perform meaningful exploration is by instilling intrinsic motivation into the agents. This intrinsic motivation usually comes in the form of curiosity. As Schmidhuber <d-cite key="Schmidhuber1991APF"></d-cite> highlighted : One becomes curious as soon as one believes there's something about the world that one does not know. It is because of this that curiosity or intrinsic rewards are usually predictive errors. For instance, an RL agent equipped with a world model is given the current state of the environment, $$s_t$$, and attempts to predict the next state, $$s_{t+1}$$. The error in this prediction is the intrinsic reward. As the world model improves one should expect the intrinsic rewards to decrease as the agent's knowledge about environment increases. This is known as curiosity-driven exploration.

