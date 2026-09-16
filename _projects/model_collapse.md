---
layout: page
title: mechanistic analysis of synthetic-data-induced model collapse
description: investigating how model collapse manifests inside language model internals and whether lost capabilities are gone or merely inaccessible
img: assets/img/proj_model_collapse.jpg
importance: 1
category: nlp research, reasoning & llm safety
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [Research Progress](#research-progress)

---

## overview

Investigating how model collapse manifests inside language model internals — tracing where degradation originates, what drives it, and whether collapsed capabilities are destroyed or merely unreachable.

**Timeline:** August 2026 – Present  
**Advisor:** [Dr. Maria Leonor Pacheco](https://blast-cu.github.io/mlpacheco/), [BLAST Lab](https://blast-cu.github.io)  
**Status:** In progress

## research progress

- Investigating how model collapse manifests inside language model internals, showing recursively trained model generations are linearly decodable from activations with near-perfect accuracy.
- Comparing different training regimes to disentangle pure data drift from compounding parameter drift.
- Using neuron ablation and activation patching to causally localize where collapse-related information concentrates in the network.
- Testing whether activation steering can repair collapsed behavior, probing whether lost capabilities are gone or merely inaccessible.
