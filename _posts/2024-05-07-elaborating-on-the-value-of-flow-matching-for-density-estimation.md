---
layout: distill
title: Elaborating on the Value of Flow Matching for Density Estimation
description:  The transfer of matching-based training from Diffusion Models to Normalizing
              Flows allows to fit expressive continuous normalizing flows 
              efficiently and therefore enables their usage for different kinds 
              of density estimation tasks. One particularly interesting task is 
              Simulation-Based Inference, where Flow Matching enabled several 
              improvements. The post shall focus on the discussion of Flow 
              Matching for Continuous Normalizing Flows. To highlight the 
              relevance and the practicality of the method, their use and 
              advantages for Simulation-Based Inference is elaborated. 
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
authors:
  - name: Maternus Herold
    affiliations: 
      name: BMW Group, appliedAI Institute for Europe gGmbH & University of the Bundeswehr Munich
  - name: Faried Abu Zaid
    affiliations:
      name: appliedAI Institute for Europe gGmbH

# must be the exact same name as your blogpost
bibliography: 2024-05-07-elaborating-on-the-value-of-flow-matching-for-density-estimation.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Motivation
  - name: Continuous Normalizing Flows
  - name: Flow Matching
    subsections:
    - name: Gaussian conditional probability paths
    # - name: Generalized Flow-Based Models
  - name: Empirical Results
  - name: Application of Flow Matching in Simulation-Based Inference 
    subsections:
    - name: Primer on Simulation-Based Inference
    - name: Flow Matching for Simulation-Based Inference 
  - name: A Personal Note 

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

# Motivation 

Normalizing Flows (NF) enable the construction of complex probability
distributions by transforming a simple, known distribution into a more complex
one. They do so by leveraging the change of variables formula, defining a
bijection from the simple distribution to the complex one. 

For most of the time, flows were based on chaining several differentiable and
invertible transformations. However, these diffeomorphic transformations limit
the flows in their complexity as such have to be simple. Furthermore, this leads
to trade-off sampling speed and evaluation performance <d-cite
key="papamakarios_normalizing_2019"></d-cite>. Their continuous counterpart,
Continuous Normalizing Flows (CNFs) have been held back by limitations in their
Simulation-Based maximum likelihood training <d-cite
key="tong_improving_2023"></d-cite>. By utilizing Flow Matching, this limitation
has been overcome and CNFs have been shown to be a powerful tool for density
estimation. 

In the following sections, CNFs and Flow Matching are explained. Following the
explanation, the empirical results of Flow Matching are presented. Finally, the
application of Flow Matching in Simulation-Based Inference is discussed, which
shall highlight their wide applicability and consistent improvement.

