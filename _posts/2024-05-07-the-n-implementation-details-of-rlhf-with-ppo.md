---
layout: distill
title: The N Implementation Details of RLHF with PPO
description: Reinforcement Learning from Human Feedback (RLHF) is pivotal in the modern application of language modeling, as exemplified by ChatGPT. This blog post delves into an in-depth exploration of RLHF, attempting to reproduce the results from OpenAI's inaugural RLHF paper, published in 2019. Our detailed examination provides valuable insights into the implementation details of RLHF, which often go unnoticed.

date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
# authors:
#  - name: Anonymous


authors:
   - name: Shengyi Costa Huang
     affiliations: 
       name: Hugging Face
   - name: Tianlin Liu
     affiliations:
       name: University of Basel
   - name: Leandro von Werra
     affiliations:
       name: Hugging Face
       
       
# authors:
#   - name: Albert Einstein
#     url: "https://en.wikipedia.org/wiki/Albert_Einstein"
#     affiliations:
#       name: IAS, Princeton
#   - name: Boris Podolsky
#     url: "https://en.wikipedia.org/wiki/Boris_Podolsky"
#     affiliations:
#       name: IAS, Princeton
#   - name: Nathan Rosen
#     url: "https://en.wikipedia.org/wiki/Nathan_Rosen"
#     affiliations:
#       name: IAS, Princeton

# must be the exact same name as your blogpost
bibliography: 2024-05-07-the-n-implementation-details-of-rlhf-with-ppo.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Matching Learning Curves
  - name: General Implementation Details
  - name: Reward Model Implementation Details
  - name: Policy Training Implementation Details
  - name: PyTorch Adam optimizer numerical issues w.r.t RLHF
  - name: Limitations
  - name: Conclusion

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


**Reinforcement Learning from Human Feedback** (RLHF) has been an impactful technique for training modern language models such as ChatGPT. In our quest to research more on RLHF, this blog post closely examines OpenAI’s inaugural RLHF paper <d-cite key="Ziegler2019fine"></d-cite> published in 2019 together with its open-source codebase at available at [*openai/lm-human-preferences*](https://github.com/openai/lm-human-preferences). Despite being based on TensorFlow-1, the code base released by OpenAI is very well-evaluated and benchmarked, making it a good place to study RLHF implementation engineering details. 

