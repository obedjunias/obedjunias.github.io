---
layout: page
title: "measuring model collapse under recursive summarization training"
description: investigating the fundamental limits of recursive training and synthetic data proliferation in foundation model ecosystems
img:
importance: 1
category: nlp, reasoning & llm safety
related_publications: false
---

**quick navigation:** [research motivation](#research-motivation) • [experimental framework](#experimental-framework) • [measurement & detection](#measurement--detection) • [advisor](#advisor)

---

## research motivation

as the web becomes increasingly saturated with model-generated content, the risk of **model collapse**—a degenerative process where future generations of models lose their ability to represent the diversity and fidelity of the original human data distribution—becomes a critical bottleneck for ai sustainability. 

this research focuses on the **theoretical and empirical foundations** of this failure mode. specifically, we investigate the **autophagous (self-consuming) loops** that occur when recursive training cycles progressively replace human-written golden corpora with synthetic summaries, leading to irreversible loss of knowledge fidelity.

**status:** work in progress (active research)  
**advisor:** [maria leonor pacheco](https://blast-cu.github.io/mlpacheco/), [blast lab](https://blast-cu.github.io)

## experimental framework

### controlled recursive pipelines
designing and orchestrating a recursive training environment to isolate the causal drivers of distributional shift:
- **synthetic-human hybrid corpora**: modeling the gradual transition from human-centric to synthetic-dominant data regimes.
- **recursive feedback loops**: simulating multiple generations of model training where each generation is conditioned on the outputs of its predecessor.
- **compression-collapse dynamics**: specifically analyzing how summarization—a task involving inherent information loss—accelerates or catalyzes token-level and semantic-level collapse.

## measurement & detection

### early warning signals & indicators
a core goal of this research is developing a **robust measurement framework** to detect the onset of collapse before major downstream failures occur. we are currently investigating:
- **entropy decay analysis**: tracking the reduction in model output entropy as a proxy for distributional narrowing.
- **lexical & semantic diversity**: developing metrics to quantify the "bleaching" of linguistic variety across generations.

---

*this research represents a core interest in the sustainability and groundedness of large-scale reasoning systems, serving as a foundation for future inquiries into robust foundation model training.*
