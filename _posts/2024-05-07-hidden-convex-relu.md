---
layout: distill
title: The Hidden Convex Optimization Landscape of Two-Layer ReLU Networks
description: In this article, we delve into the research paper titled 'The Hidden Convex Optimization Landscape of Regularized Two-Layer ReLU Networks'. We put our focus on the significance of this study and evaluate its relevance in the current landscape of the theory of machine learning. This paper describes how solving a convex problem can directly give the solution to the highly non-convex problem that is optimizing a two-layer ReLU Network. After giving some intuition on the proof through a few examples, we will observe the limits of this model as we might not yet be able to throw away the non-convex problem.
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
authors:
  - name: Victor Mercklé
    url: "https://victormerckle.fr/"
    affiliations:
      name: LabHC, LJK - France
  - name: Franck Iutzeler
    url: "https://iutzeler.org/"
    affiliations:
      name: Institut de Mathématiques de Toulouse, Université de Toulouse, CNRS
  - name: Ievgen Redko
    url: "https://ievred.github.io/"
    affiliations:
      name: Paris Noah's Ark lab

#authors:
#  - name: Albert Einstein
#    url: "https://en.wikipedia.org/wiki/Albert_Einstein"
#    affiliations:
#      name: IAS, Princeton

# must be the exact same name as your blogpost
bibliography: 2024-05-07-hidden-convex-relu.bib  

#TODO make sure that TOC names match the actual section names - they do
toc:
  - name: I. Overview and Motivation
    subsections:
    - name: Problem and notation
    - name: Research context
  - name: II. Convex Reformulation
    subsections:
    - name: Small example walkthrough
    - name: Specifics about equivalence
    - name: Activation patterns
    - name: Extensions of the convex reformulation to other settings
  - name: III. Can we Forget the Non-Convex Problem?
    subsections:
    - name: Solving the convex problem efficiently is hard
    - name: Activation patterns are not a constant in the non-convex problem
    - name: On large initialization scale
    - name: On very small initialization
  - name: Conclusion

_styles: >

  .remark {
    display: block;
    margin: 12px 0;
    font-style: italic;
  }
  .remark:before {
    content: "Remark.";
    font-weight: bold;
    font-style: normal;
  }
  .remark[text]:before {
    content: "Remark (" attr(text) ") ";
  }

  .center {
      display: block;
      margin-left: auto;
      margin-right: auto;
  }

  .legend {
      display: block;
      margin-left: 50px;
      margin-right: 50px;
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

---

