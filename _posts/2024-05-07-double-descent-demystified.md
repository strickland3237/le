---
layout: distill
title: Double Descent Demystified
description: Identifying, Interpreting & Ablating the Sources of a Deep Learning Puzzle
date: 2024-05-07
future: true
htmlwidgets: true

authors:
  - name: Rylan Schaeffer
    url: "https://scholar.google.com/citations?user=6tMEGz8AAAAJ&hl=en"
    affiliations:
      name: Stanford University
  - name: Zachary Robertson
    url: "https://scholar.google.com/citations?user=769PIisAAAAJ&hl=en&oi=ao"
    affiliations:
      name: Stanford University
  - name: Akhilan Boopathy
    url: "https://scholar.google.com/citations?user=21alU7EAAAAJ&hl=en"
    affiliations:
      name: MIT
  - name: Mikail Khona
    url: "https://scholar.google.com/citations?user=K5f0SYQAAAAJ&hl=en&oi=ao"
    affiliations:
      name: MIT
  - name: Kateryna Pistunova
    url: "https://scholar.google.com/citations?user=V7QY5j0AAAAJ&hl=en"
    affiliations:
      name: Stanford University
  - name: Jason W. Rocks
    url: "https://scholar.google.com/citations?user=rFHAzMUAAAAJ"
    affiliations:
      name: Boston University
  - name: Ila R. Fiete
    url: "https://scholar.google.com/citations?user=uE-CihIAAAAJ&hl=en&oi=ao"
    affiliations:
      name: MIT
  - name: Andrey Gromov
    url: "https://scholar.google.com/citations?user=D056qfMAAAAJ&hl=en&oi=ao"
    affiliations:
      name: UMD & Meta AI FAIR
  - name: Sanmi Koyejo
    url: "https://scholar.google.com/citations?user=EaaOeJwAAAAJ&hl=en&oi=ao"
    affiliations:
      name: Stanford University

# must be the exact same name as your blogpost
bibliography: 2024-05-07-double-descent-demystified.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Introduction
  - name: Double Descent in Ordinary Linear Regression
    subsections:
    - name: Empirical Evidence
    - name: Notation and Terminology
    - name: Mathematical Analysis
    - name: Factor 1 - Low Variance in Training Features
    - name: Factor 2 - Test Features in Training Feature Subspace
    - name: Factor 3 - Errors from Best Possible Model
    - name: Divergence at the Interpolation Threshold
    - name: Generalization in Overparameterized Linear Regression  
  - name: Adversarial Data
    subsections:
    - name: Adversarial Test Examples
    - name: Adversarial Training Data
  - name: Intuition for Nonlinear Models

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

