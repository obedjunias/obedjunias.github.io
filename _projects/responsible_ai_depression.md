---
layout: page
title: algorithmic bias in llm-based depression detection
description: Same depression-detection task with classical DNNs vs. LLMs; measured fairness gaps across demographics. IEEE-BHI 2025.
img: assets/img/proj_bias_depression.jpg
importance: 1
category: responsible ai
related_publications: true
---

Automated depression screening from interview text is increasingly realistic, but clinical NLP systems can track demographics in ways clinicians might not intend. With [Theodora Chaspari](https://www.colorado.edu/cs/theodora-chaspari) at the HUBBS Lab (Institute of Cognitive Science, CU Boulder), I compared classical DNN embeddings and modern LLMs on the DAIC-WOZ interview corpus and measured disparities by gender and race/ethnicity alongside standard classification metrics.

LLMs beat the DNN baselines overall and did relatively better on some underrepresented groups (for example Hispanic participants). Gender gaps were often smaller with LLMs than with the embedding-based pipeline. Race and ethnicity disparities were stubborn: they showed up across architectures and did not go away just by adding more few-shot examples or ethics-framed prompts. For DNNs, a worst-group loss helped trade off accuracy and fairness more sensibly than a plain fairness regularizer.

The takeaway for me was not “LLMs are safer by default” but that **you have to measure fairness on the same footing as accuracy** before these tools get anywhere near deployment. The full write-up is in our BHI paper below.

**Timeline:** January – November 2025  
**Paper:** [IEEE BHI 2025](https://ieeexplore.ieee.org/abstract/document/11269509) · [arXiv:2509.25795](https://arxiv.org/abs/2509.25795)

Junias, Obed; Kini, Prajakta; Chaspari, Theodora. *Assessing Algorithmic Bias in Language-Based Depression Detection: A Comparison of DNN and LLM Approaches.* IEEE-EMBS International Conference on Biomedical and Health Informatics (BHI), 2025.