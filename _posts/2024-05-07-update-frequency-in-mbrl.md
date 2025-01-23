---
layout: distill
title: Fair Model-Based Reinforcement Learning Comparisons with Explicit and Consistent Update Frequency
# description: Model-based reinforcement learning has emerged as a promising approach to achieve both state-of-the-art performance and sample-efficiency.However, ensuring fair benchmark comparisons can be challenging due to the implicit design choices made by the different algorithms. This article focuses on one such choice, the update frequency of the model and the agent. While the update frequency can sometimes be optimized to improve performance, real-world applications often impose constraints, allowing updates only between deployments on the actual system. We emphasize the need for more evaluations using consistent update frequencies across different algorithms. This will provide researchers and practitioners with clearer comparisons under realistic constraints.
description: Implicit update frequencies can introduce ambiguity in the interpretation of model-based reinforcement learning benchmarks, obscuring the real objective of the evaluation. While the update frequency can sometimes be optimized to improve performance, real-world applications often impose constraints, allowing updates only between deployments on the actual system. This blog post emphasizes the need for evaluations using consistent update frequencies across different algorithms to provide researchers and practitioners with clearer comparisons under realistic constraints.
date: 2024-05-07
future: true
htmlwidgets: true

authors:
  - name: Albert Thomas
    url: https://albertcthomas.github.io/
    affiliations:
      name: Huawei Noah's Ark Lab
  - name: Abdelhakim Benechehab
    url: https://scholar.google.com/citations?user=JxgqOKwAAAAJ
    affiliations:
      name: Huawei Noah's Ark Lab - Department of Data Science, EURECOM, France
  - name: Giuseppe Paolo
    url: https://www.giupaolo.com
    affiliations:
      name: Huawei Noah's Ark Lab
  - name: Balázs Kégl
    url: https://twitter.com/balazskegl
    affiliations:
      name: Huawei Noah's Ark Lab

# must be the exact same name as your blogpost
bibliography: 2024-05-07-update-frequency-in-mbrl.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Introduction
  - name: Three popular model-based reinforcement learning algorithms
    subsections:
    - name: MBPO
    - name: PETS
    - name: BREMEN
  - name: Making the update frequency more accessible
  - name: Comparisons with fixed update frequency
  - name: Ablation studies
    subsections:
    - name: Varying the update frequency in MBPO
  - name: Conclusion
  - name: Appendix

# Below is an example of injecting additional post-specific styles.
# This is used in the 'Layouts' section of this post.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }
---

## Introduction

In reinforcement learning <d-cite key="Sutton1998"></d-cite>, an agent learns to make decisions by interacting with an environment, receiving a feedback, or reward, following each action it takes to move from a state of the environment to another. The objective is to learn a policy, a mapping from states to action, that maximizes the expected cumulative reward over successive interactions.

There are two main approaches when designing a reinforcement learning algorithm: model-based or model-free. Model-based reinforcement learning (MBRL) algorithms <d-cite key="Moerland2021"></d-cite> first learn a model of the environment dynamics which, given a state of the environment and an action, predicts the next state of the environment. This model can then be used in place of the real environment to learn or decide how to act. Model-free algorithms avoid this step and directly try to learn a policy. As MBRL algorithms can rely on the learned dynamics model instead of the real environment, they are known to be more sample efficient than model-free algorithms (see for instance <d-cite key="Chua2018"></d-cite> or <d-cite key="Janner2019"></d-cite>). MBRL is thus a good choice when interactions with the environment are limited, which is often the case for real applications such as controlling engineering systems.

