---
layout: distill
title: Understanding in-context learning in transformers
description: We propose a technical exploration of In-Context Learning (ICL) for linear regression tasks in transformer architectures. Focusing on the article <i>Transformers Learn In-Context by Gradient Descent</i> by J. von Oswald et al., published in ICML 2023 last year, we provide detailed explanations and illustrations of the mechanisms involved. We also contribute novel analyses on ICL, discuss recent developments and we point to open questions in this area of research.
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
# authors:
#   - name: Anonymous
#     affiliations:
#       name: Anonymous

authors:
 - name: Simone Rossi
   url: "https://scholar.google.com/citations?user=lTt86awAAAAJ&hl=en"
   affiliations:
     name: Stellantis, France
 - name: Rui Yuan
   url: "https://scholar.google.com/citations?hl=en&user=4QZgrj0AAAAJ"
   affiliations:
     name: Stellantis, France
 - name: Thomas Hannagan
   url: "https://scholar.google.com/citations?hl=en&user=u6OFo3YAAAAJ"
   affiliations:
     name: Stellantis, France

# must be the exact same name as your blogpost
bibliography: 2024-05-07-understanding-icl.bib

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: What is in-context learning?
    subsections:
      - name: From large language models to regression tasks
      - name: Objective of this blog post
  - name: Preliminaries and notations
    subsections:
      - name: Dataset construction and tokenization
      - name: A quick review of self-attention
      - name: Training details
  - name: Transformers can learn any linear function in-context
    subsections:
      - name: Linear self-attention is sufficient
  - name: What is special about linear self-attention?
    subsections:
      - name: Establishing a connection between gradient descent and data manipulation
      - name: Building a linear transformer that implements a gradient descent step
  - name: Experiments and analysis of the linear transformer
    subsections:
      - name: During training a linear transformer implements a gradient descent step
      - name: The effect of the GD learning rate
      - name: Analytical derivation of the best GD learning rate
      - name: If one layer is a GD step, what about multiple layers?
  - name: Is this just for transformers? What about LSTMs?
  - name: Concluding remarks
    subsections:
      - name: What now?

# Below is an example of injecting additional post-specific styles.
# This is used in the 'Layouts' section of this post.
# If you use this post as a template, delete this _styles block.
_styles: >
  
  .center {
      display: block;
      margin-left: auto;
      margin-right: auto;
  }

  .framed {
    border: 1px var(--global-text-color) dashed !important;
    padding: 20px;
  }

  d-article {
    overflow-x: visible;
  }

  .underline {
    text-decoration: underline;
  }

  .todo{
      display: block;
      margin: 12px 0;
      font-style: italic;
      color: red;
  }
  .todo:before {
      content: "TODO: ";
      font-weight: bold;
      font-style: normal;
  }
  summary {
    color: steelblue;
    font-weight: bold;
  }

  summary-math {
    text-align:center;
    color: black
  }

  [data-theme="dark"] summary-math {
    text-align:center;
    color: white
  }

  details[open] {
  --bg: #e2edfc;
  color: black;
  border-radius: 15px;
  padding-left: 8px;
  background: var(--bg);
  outline: 0.5rem solid var(--bg);
  margin: 0 0 2rem 0;
  font-size: 80%;
  line-height: 1.4;
  }

  [data-theme="dark"] details[open] {
  --bg: #112f4a;
  color: white;
  border-radius: 15px;
  padding-left: 8px;
  background: var(--bg);
  outline: 0.5rem solid var(--bg);
  margin: 0 0 2rem 0;
  font-size: 80%;
  }
  .box-note, .box-warning, .box-error, .box-important {
    padding: 15px 15px 15px 10px;
    margin: 20px 20px 20px 5px;
    border: 1px solid #eee;
    border-left-width: 5px;
    border-radius: 5px 3px 3px 5px;
  }
  d-article .box-note {
    background-color: #eee;
    border-left-color: #2980b9;
  }
  d-article .box-warning {
    background-color: #fdf5d4;
    border-left-color: #f1c40f;
  }
  d-article .box-error {
    background-color: #f4dddb;
    border-left-color: #c0392b;
  }
  d-article .box-important {
    background-color: #d4f4dd;
    border-left-color: #2bc039;
  }
  html[data-theme='dark'] d-article .box-note {
    background-color: #555555;
    border-left-color: #2980b9;
  }
  html[data-theme='dark'] d-article .box-warning {
    background-color: #7f7f00;
    border-left-color: #f1c40f;
  }
  html[data-theme='dark'] d-article .box-error {
    background-color: #800000;
    border-left-color: #c0392b;
  }
  html[data-theme='dark'] d-article .box-important {
    background-color: #006600;
    border-left-color: #2bc039;
  }
  d-article aside {
    border: 1px solid #aaa;
    border-radius: 4px;
    padding: .5em .5em 0;
    font-size: 90%;
  }
  .caption { 
    font-size: 80%;
    line-height: 1.2;
    text-align: left;
  }
---

