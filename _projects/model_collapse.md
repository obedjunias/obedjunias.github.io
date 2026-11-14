---
layout: page
title: mechanistic analysis of synthetic-data-induced model collapse
description: Training on synthetic data in a loop; reading collapse from activations, then ablation and patching to see what's broken and whether steering can bring it back.
img: assets/img/proj_model_collapse.jpg
importance: 1
category: nlp research, reasoning & llm safety
related_publications: false
---

When models are trained again and again on their own outputs, quality drifts. A lot of work measures that drift by perplexity or benchmark scores. I want to know what changes **inside** the model: whether a “collapsed” capability is actually gone from the weights, or still there but not reachable at inference time.

With [Maria L. Pacheco](https://blast-cu.github.io/mlpacheco/) at the [BLAST Lab](https://blast-cu.github.io/), I set up recursive training on synthetic data and compare regimes so we can separate pure distribution shift from compounding parameter change. One early result: generations from a recursively trained model are nearly linearly decodable from internal activations, which suggests collapse leaves a strong trace in representation space even when outputs look worse.

The rest of the project is causal. I use neuron ablation and activation patching to find where collapse-related information concentrates, and I test activation steering to see whether steering can recover behavior that looks lost on the surface. If steering works, the capability may still be in the network; if it does not, we are closer to real erasure.

**Timeline:** August 2026 – present  
**Status:** in progress