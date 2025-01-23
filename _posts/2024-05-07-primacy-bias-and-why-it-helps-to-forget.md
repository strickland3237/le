---
layout: distill
title: "It's Time to Move On: Primacy Bias and Why It Helps to Forget"
description: "'The Primacy Bias in Deep Reinforcement Learning' demonstrates how the first experiences of a deep learning model can cause catastrophic memorization and how this can be prevented. In this post we describe primacy bias, summarize the authors' key findings, and present a simple environment to experiment with primacy bias."
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
# authors:
#   - name: Anonymous

authors:
  - name: Matthew Kielo
    url: https://mkiel.org/
    affiliations:
      name: Georgia Institute of Technology
  - name: Vladimir Lukin
    url: https://github.com/divannyteoretik
    affiliations:
      name: Georgia Institute of Technology

# must be the exact same name as your blogpost
bibliography: 2024-05-07-primacy-bias-and-why-it-helps-to-forget.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Introduction to Primacy Bias
  - name: Off Policy Deep Reinforcement Learning
    subsections:
    - name: Are we Overcomplicating?  
  - name: Selecting a Replay Ratio
    subsections:
    - name: Heavy Priming 
  - name: Weight Resets
    subsections:
    - name: Do Resets Work?
    - name: "What’s The Catch?" 
  - name: Implementing Primacy Bias
    subsections:
    - name: 2x2 Switching Frozen Lake
    - name: Results
  - name: Conclusions

# Below is an example of injecting additional post-specific styles.
# This is used in the 'Layouts' section of this post.
# If you use this post as a template, delete this _styles block.
# This is a test??


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

## Introduction to Primacy Bias

Primacy bias occurs when a model's training is damaged by overfitting to its first experiences. This can be caused by poor hyperparameter selection, the underlying dynamics of the system being studied, or simply bad luck. 

