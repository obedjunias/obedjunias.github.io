---
layout: page
title: "measuring model collapse under recursive summarization training"
description: investigating the fundamental limits of recursive training and synthetic data proliferation in foundation model ecosystems
img:
importance: 1
category: nlp research ,reasoning & llm safety
related_publications: false
---

**quick navigation:** [research motivation](#research-motivation) • [experimental framework](#experimental-framework) • [measurement & detection](#measurement--detection) • [advisor](#advisor)

---

## research motivation

As the web becomes increasingly saturated with model-generated content, the risk of **model collapse**—a degenerative process where future generations of models lose their ability to represent the diversity and fidelity of the original human data distribution—becomes a critical bottleneck for AI sustainability. 

This research focuses on the **theoretical and empirical foundations** of this failure mode. Specifically, we investigate the **autophagous (self-consuming) loops** that occur when recursive training cycles progressively replace human-written golden corpora with synthetic summaries, leading to irreversible loss of knowledge fidelity.

**Status:** Work in progress (active research)  
**Advisor:** [Dr. Maria Leonor Pacheco](https://blast-cu.github.io/mlpacheco/), [BLAST Lab](https://blast-cu.github.io)

## experimental framework

### controlled recursive pipelines
Designing and orchestrating a recursive training environment to isolate the causal drivers of distributional shift:
- **Synthetic-Human Hybrid Corpora**: Modeling the gradual transition from human-centric to synthetic-dominant data regimes.
- **Recursive Feedback Loops**: Simulating multiple generations of model training where each generation is conditioned on the outputs of its predecessor.
- **Compression-Collapse Dynamics**: Specifically analyzing how summarization—a task involving inherent information loss—accelerates or catalyzes token-level and semantic-level collapse.

## measurement & detection

### early warning signals & indicators
A core goal of this research is developing a **robust measurement framework** to detect the onset of collapse before major downstream failures occur. We are currently investigating:
- **Entropy Decay Analysis**: Tracking the reduction in model output entropy as a proxy for distributional narrowing.
- **Lexical & Semantic Diversity**: Developing metrics to quantify the "bleaching" of linguistic variety across generations.

---

*This research represents a core interest in the sustainability and groundedness of large-scale reasoning systems, serving as a foundation for future inquiries into robust foundation model training.*
