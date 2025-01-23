---
layout: distill
title: Understanding gradient inversion attacks from the prior knowledge perspective
description: In this blogpost, we mention multiple works in gradient inversion attacks, point out the chanllenges we need to solve in GIAs, and provide a perspective from the prior knowledge to understand the logic behind recent papers.
date: 2024-05-07
future: true
htmlwidgets: true

#Anonymize when submitting
authors:
  - name: Yanbo Wang
    affiliations:
      name: School of AI, UCAS $\n$ CRIPAC & MAIS, CASIA
  - name: Jian Liang
    affiliations:
      name: School of AI, UCAS $\n$ CRIPAC & MAIS, CASIA
  - name: Ran He
    affiliations:
      name: School of AI, UCAS $\n$ CRIPAC & MAIS, CASIA
      


# must be the exact same name as your blogpost
bibliography: 2024-05-07-understanding-gradient-inversion-attacks-from-the-prior-knowledge-perspective.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Fundamental pipeline of GIAs 
  - name: The tough challenge in GIAs
  - subsections:
    - name: A simple example of information discards 
  - name: Understanding GIAs from the prior knowledge perspective
  - subsections:
    - name: Unparameterized regularization terms
    - name: Generative models
    - name: End-to-end networks 
  - name: Limitation and future directions 
  - name: Conclusions


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
Federated learning, as a way to collaboratively train a deep model, was originally developed to enhance training efficiency and protect data privacy. In a federated learning paradigm, no matter whether it is horizontal or vertical, data could be processed locally, and the central server could only get access to the processed information, such as trained model weights or intermediate gradients<d-cite key="zhangsurvey"></d-cite>. Avoiding direct access to private local data, federated learning is believed to successfully protect clients' data privacy, for the central server could only make use of uploaded information to train a global model but it does not know exactly what the training dataset really contains. However, in horizontal federated learning, researchers found that with training gradients, the central server could still recover input data, which may be a threat to training data privacy. Such privacy attack is then named gradient inversion attack (or gradient leakage attack).

