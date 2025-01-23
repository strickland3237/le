---
layout: distill
title: RLHF without RL - Direct Preference Optimization
description: We discuss the RL part of RLHF and its recent displacement by direct preference optimization (DPO).
  With DPO, a language model can be aligned with
  human preferences without sampling from an LM, thereby significantly
  simplifying the training process. By now, DPO has been implemented in many projects and seems to be here to stay.
date: 2024-05-07
future: true
htmlwidgets: true

authors:
  - name: Michael Panchenko
    url: "https://transferlab.ai/authors/michael-panchenko"
    affiliations:
      name: appliedAI initiative GmbH

bibliography: 2024-05-07-rlhf-without-rl.bib

toc:
  - name: Background
    id: background
  - name: Is RLHF Reinforcement Learning?
    id: is-rlhf-reinforcement-learning
  - name: Direct Preference Optimization
    id: direct-preference-optimization
  - name: DPO in the Wild - Experiments, LLMs and Software
    id: dpo-in-the-wild-experiments-llms-and-software
  - name: Closing Remarks
    id: closing-remarks

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

## Background

Reinforcement learning from human feedback (RLHF) is an important technique for
aligning (large) language models (LM)
with human preferences. It was introduced by Christiano et al.<d-cite key="christiano2017deep"/> and then first 
applied to language models in the work by Ziegler et al.<d-cite key="ziegler2019fine"/>. 
Since then, RLHF has become a central building block of many LLM-based applications, 
including the first versions of ChatGPT.

