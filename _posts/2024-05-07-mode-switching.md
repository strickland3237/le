---
layout: distill
title: Behavioral Differences in Mode-Switching Exploration for 
  Reinforcement Learning
description: In 2022, researchers from Google DeepMind presented an initial 
  study on  mode-switching exploration, by which an agent separates its 
  exploitation  and exploration actions more coarsely throughout an episode 
  by  intermittently and significantly changing its behavior policy. We 
  supplement their work in this blog  post by showcasing some observed 
  behavioral differences between  mode-switching and monolithic exploration 
  on the Atari suite and  presenting illustrative examples of its benefits. 
  This work aids  practitioners and researchers by providing practical 
  guidance and  eliciting future research directions in mode-switching 
  exploration.
date: 2024-05-07
future: true
htmlwidgets: true

# Anonymize when submitting
# authors:
#   - name: Anonymous

authors:
  - name: Loren J Anderson
    url: 
    affiliations: 
      name: USA Space Force

# must be the exact same name as your blogpost
bibliography: 2024-05-07-mode-switching.bib  

# Add a table of contents to your post.
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly. 
#   - please use this format rather than manually creating a markdown table of contents.
toc:
  - name: 1. Introduction
    subsections:
    - name: Mode-Switching Distinctions
    - name: Mode-Switching Basics
    - name: Blog Post Motivation
  - name: 2. Experiments
    subsections:
    - name: Concentrated Terminal States
    - name: Early Exploration
    - name: Concentrated Return
    - name: Post-Exploration Entropy
    - name: Top Exploitation Proportions
  - name: 3. Conclusion
    subsections:
    - name: Acknowledgements

# Below is an example of injecting additional post-specific styles.
# This is used in the 'Layouts' section of this post.
# If you use this post as a template, delete this _styles block.

---

## 1. Introduction

Imagine learning to ride a bicycle for the first time. This task 
requires the investigation of numerous actions such as steering the 
handlebars to change direction, shifting weight to maintain balance, and 
applying pedaling power to move forward. To achieve any satisfaction, a 
complex sequence of these actions must be taken for a substantial amount of 
time. However, a dilemma emerges: many other tasks such as eating, sleeping, and working may result in more immediate satisfaction (e.g. lowered hunger, better rest, bigger paycheck), which may tempt the learner to favor other tasks. Furthermore, if enough satisfaction is not quickly achieved, the learner may even abandon the task of learning to ride a bicycle altogether.

One frivolous strategy (Figure 1, Option 1) to overcome this dilemma is to 
interleave a few random actions on the bicycle throughout the remaining 
tasks of the day. This strategy neglects the sequential nature of bicycle 
riding and will achieve satisfaction very slowly, if at all. Furthermore, 
this strategy may interrupt and reduce the satisfaction of the other daily 
tasks. The more intuitive strategy (Figure 1, Option 2) is to dedicate 
significant portions of the day to explore the possible actions of bicycle 
riding. The benefits of this approach include testing the sequential 
relationships between actions, isolating different facets of the 
task for quick mastery, and providing an explicit cutoff point to shift 
focus and accomplish other daily tasks. Also -- let's face it -- who wants to wake up in the middle of the night to turn the bicycle handlebar twice 
before going back to bed? 

