---
layout: distill
title: 'Towards Robust Foundation Models: Adversarial Contrastive Learning'
description: Foundation models pre-trained on large-scale unlabelled datasets using self-supervision can be generalizable to a wide range of downstream tasks. Existing work has shown that adversarial attacks can effectively fool any downstream models fine-tuned from a pre-trained foundation model. The existence of such adversarial attacks necessitates the development of robust foundation models which can yield both standard generalization and adversarial robustness to safety-critical downstream tasks. Currently, adversarial contrastive learning (ACL) is one of the most effective methods for outputting a robust foundation model. ACL incorporates contrastive learning with adversarial data to effectively output a robust representation without requiring costly annotations. In this blog, we introduced two NeurIPS 2023 publications that can enhance ACL's efficacy and efficiency, respectively. (1) This blog introduces Adversarial Invariant Regularization (AIR) which is a state-of-the-art ACL algorithm. A causal theoretical framework is built to interpret ACL, and then the AIR algorithm is derived from the causal framework to regulate and improve the ACL. (2) This blog also introduces a Robustness-aware Coreset Selection (RCS) method to speed up ACL. RCS does not require label information and searches for an informative training subset that can maintain the adversarial robustness. For the first time, RCS enables the application of ACL on the large-scale ImageNet-1K dataset. 
# Your blog post's abstract. 
  # Please add your abstract or summary here and not in the main body of your text. 
  # Do not include math/latex or hyperlinks.
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
# authors:
#   - name: Anonymous

authors:
  - name: Jingfeng Zhang
    url: https://zjfheart.github.io/
    affiliations:
      name: The University of Auckland & RIKEN Center for Advanced Intelligence Project
  - name: Xilie Xu
    url: https://godxuxilie.github.io/
    affiliations:
      name: National University of Singapore

# must be the exact same name as your blogpost
bibliography: 2024-05-07-robust-foundation-model.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Foundation Models  
    subsections:
    - name: Contrastive Learning (CL)
  - name: Robust Foundation Models
    subsections:
    - name: Adversarial Contrastive Learning (ACL)
  #   subsections:
  #   - name: Interactive Figures
  - name: Enhancing ACL via Adversarial Invariant Regularization (AIR)
    subsections:
      - name: Causal View of ACL
      - name: the Methodology of AIR
      - name: Empirical Results
      - name: Robust Self-Supervised Learning (RobustSSL) Benchmark
  - name: Efficient ACL via Robustness-Aware Coreset Selection (RCS)
    subsections:
      - name: Motivation---ACL is Inefficient
      - name: the Methodology of RCS
      - name: Experimental Results
  

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

<!-- Note: please use the table of contents as defined in the front matter rather than the traditional markdown styling. -->

## Foundation Models
<!-- In this section, we introduct foundation models and robust foundation models. -->

