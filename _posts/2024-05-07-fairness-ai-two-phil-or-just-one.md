---
layout: distill
title: "Fairness in AI: two philosophies or just one?"
description: The topic of fairness in AI has garnered more attention over the last year, recently with the arrival of the EU's AI Act. This goal of achieving fairness in AI is often done in one of two ways, namely through counterfactual fairness or through group fairness. These research strands originate from two vastly differing ideologies. However, with the use of causal graphs, it is possible to show that they are related and even that satisfying a fairness group measure means satisfying counterfactual fairness. 
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
# authors:
#   - name: Anonymous

authors:
  - name: MaryBeth Defrance
    url: https://orcid.org/my-orcid?orcid=0000-0002-6570-8857
    affiliations:
      name: University of Ghent

# must be the exact same name as your blogpost
bibliography: 2024-05-07-fairness-ai-two-phil-or-just-one.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Why fairness?
  - name: What is fairness?
    subsections: 
    - name: Explainable AI
    - name: Group fairness
  - name:  Unifying these philosophies
    subsections:
    - name: Measurement error - Demographic parity
    - name: Selection on label - Equalized odds
    - name: Selection on predictor - conditional use accuracy equality
    - name: Confirmation with experiments
  - name: What can we take away? 

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

This blog post is based on the paper of Anthis and Veitch<d-cite key="Causal_context"></d-cite>. The original paper is enriched with a wide overview of fairness concepts used in research and visuals aiding the readers in gaining a deeper understanding. The blog post aims to raise questions about the dichotomy between procedural and outcome fairness, that they perhaps should not be treated as separate research fields as is currently often the case. 

## Why fairness? 
The spread of AI exposed some of the dark patterns that are present in society. Some well known examples are the COMPAS case<d-cite key="COMPAS_article"></d-cite> which showed discrimination against black defendants and the Amazon hiring tool<d-cite key="Reuters_Dastin_2018"></d-cite> which showed a preference towards men compared to women. However, these AI system were most likely not the source of this disparate treatment. This behavior stems from the data that was used to train the system, thus this behavior comes from people who were behind the creation of that data. 

Fairness in AI is a research strain which aims to remove the biases in the AI models that result in that disparate treatment. The goal of these models is that people are treated more fairly, perhaps even more than a human decision. 

