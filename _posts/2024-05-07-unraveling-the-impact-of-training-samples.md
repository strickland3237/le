---
layout: distill
title: Unraveling The Impact of Training Samples
description: How do we quantify the influence of datasets? Recent works on Data Attribution Methods shed light on this problem. In this blog post, we introduce Data Attribution Methods which leverage robust statistics and surrogate functions, and present their applications like distinguishing the feature selection difference of learning algorithms, detecting data leakage, and assessing model robustness.
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
authors:
  - name: Daiwei Chen
    url: 'https://chendaiwei-99.github.io'
    affiliations:
      name: UW-Madison

  - name: Jane Zhang
    url: 'https://openreview.net/profile?id=~Jane_Zhang2'
    affiliations:
      name: UW-Madison

  - name: Ramya Korlakai Vinayak
    url: 'https://ramyakv.github.io'
    affiliations:
      name: UW-Madison

# must be the exact same name as your blogpost
bibliography: 2024-05-07-unraveling-the-impact-of-training-samples.bib

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: Data Attribution Methods
    subsections:
      - name: Influence Functions
      - name: Data Models
      - name: TRAK
  - name: How do we use it?
    subsections:
      - name: Learning Algorithm Comparison
      - name: Data Leakage Detection
      - name: Prediction Brittleness Examination
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
  .details{
    border: 1px solid #000; /* Border style */
    padding: 10px; /* Optional padding for content inside the frame */
    background-color: #808080; /* light gray
    background color */
    color: #FFFFFF; /* Text color, change to contrast with the background */
  }
  .details summary{
    color: white;
    font-style: italic;
    font-weight: bold;
  }
  .details p{
    color:white;
  }
---

<!-- Note: please use the table of contents as defined in the front matter rather than the traditional markdown styling. -->

How do we quantify the true influence of datasets? What role does the influence score play in refining datasets and unraveling the intricacies of learning algorithms? Recent works on **Data Attribution Methods** give us an interesting answer to these problems.

