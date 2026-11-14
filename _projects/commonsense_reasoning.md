---
layout: page
title: LOGICAL-COMMONSENSEQA
description: Commonsense QA where each option is a logical combo of two statements; strong on AND/OR, weak on negation. Published at ACL 2026 (short papers).
img: assets/img/proj_commonsense.jpg
importance: 1
category: nlp research, reasoning & llm safety
related_publications: true
---

Most commonsense benchmarks ask models to pick one plausible sentence. Real judgment is often about *combinations*: two facts can each sound fine alone while the pair is impossible, or one holds only when the other does not. **LOGICAL-COMMONSENSEQA** makes that explicit. Each question has two atomic statements, and each answer applies a plausibility-level operator (AND, OR, or NEITHER/NOR) to form a compound option.

With [Maria L. Pacheco](https://blast-cu.github.io/mlpacheco/) at the [BLAST Lab](https://blast-cu.github.io/), I built the benchmark and ran a broad model sweep (instruction-tuned, reasoning-focused, and fine-tuned models; zero-shot, few-shot, and chain-of-thought). Models were generally reasonable on conjunction and passable on disjunction. On negation-style questions, accuracy dropped quickly. Chain-of-thought often looked coherent but still landed on the wrong compound label.

That gap is what pulled me toward follow-up work on [structured compositional reasoning](https://arxiv.org/abs/2608.12836): helping models reason over these combinations instead of treating each option as a single fluent paragraph. I am also working on entailment-tree representations for the same failure modes.

**Timeline:** June 2025 – present  
**Paper:** [ACL 2026 short papers](https://aclanthology.org/2026.acl-short.61/) · [project page](/logical-csqa/) · [code](https://github.com/obedjunias19/logical-csqa) · [data](https://huggingface.co/datasets/ojayy/logical-csqa)