---
layout: page
title: algorithmic bias in llm-based depression detection
description: evaluating and mitigating fairness issues in language-based mental health classification
img: assets/img/proj_bias_depression.jpg
importance: 1
category: responsible ai
related_publications: true
---

**Quick Navigation:** [Overview](#overview) • [Publication](#publication) • [Research Contributions](#research-contributions) • [Key Findings](#key-findings) • [Impact](#impact)

---

## overview

Investigated algorithmic bias in language-based models for automated depression detection, with a focus on socio-demographic disparities across gender and race/ethnicity.

**Timeline:** January 2025 – November 2025
**Position:** Responsible AI Researcher, Institute of Cognitive Science, CU Boulder
**Advisor:** Dr. Theodora Chaspari, HUBBS Lab
**Status:** Published at IEEE-EMBS 2025

## publication

**Junias, Obed**, Prajakta Kini, and Theodora Chaspari. "Assessing Algorithmic Bias in Language-Based Depression Detection: A Comparison of DNN and LLM Approaches." *2025 IEEE EMBS International Conference on Biomedical and Health Informatics (BHI)*. IEEE, 2025.

**Links:** [IEEE Xplore](https://ieeexplore.ieee.org/abstract/document/11269509) | [arXiv:2509.25795](https://arxiv.org/abs/2509.25795)

## research contributions

### Large-Scale Fairness Evaluation

Led comprehensive fairness evaluation comparing different model architectures:

- **Deep Neural Networks (DNNs)**: Evaluated bias in traditional DNN-based embedding approaches
- **Large Language Models**: Assessed LLaMA, GPT-4, and other state-of-the-art LLMs
- **Dataset**: Clinical interview transcripts from DAIC-WOZ (Distress Analysis Interview Corpus)
- **Fairness Dimensions**: Gender and race/ethnicity disparities

### Bias Mitigation Strategies

Implemented and evaluated multiple approaches to reduce algorithmic bias:

**For DNN-Based Models:**
- **Fairness-Aware Loss Functions**: Applied specialized loss functions to address demographic disparities
- **Worst-Group Loss**: Optimized for the worst-performing demographic group, achieving better balance between performance and fairness
- **Fairness-Regularized Loss**: Minimized loss across all groups (less effective than worst-group loss)

**For Large Language Models:**
- **In-Context Learning**: Varied prompt framing and shot counts in few-shot learning
- **Guided Prompting**: Applied ethical framing to mitigate bias
- **Low-Resource Settings**: Explored bias mitigation in resource-constrained scenarios

### Diagnostic Tools

Developed quantitative methods for bias assessment:

- **Diagnostic Probes**: Tools to detect and measure bias in model outputs
- **Fairness Metrics**: Quantified disparities across demographic groups
- **Model Selection Criteria**: Informed model selection based on fairness considerations

## key findings

**Model Performance:**
- LLMs outperform DNN-based models in depression classification
- LLMs show particularly strong performance for underrepresented groups (e.g., Hispanic participants)
- LLMs exhibit reduced gender bias compared to DNN-based embeddings

**Bias Mitigation Results:**
- Worst-group loss achieves best balance between performance and fairness for DNNs
- Guided prompting with ethical framing mitigates gender bias in 1-shot LLM settings
- Increasing shot count (N-shot learning) does not further reduce disparities
- Race/ethnicity disparities persist across both model types and mitigation strategies

**Persistent Challenges:**
- Racial disparities remain difficult to mitigate with current techniques
- Neither prompting strategies nor increased shots effectively reduce race/ethnicity disparities
- Highlights need for continued research in fairness-aware mental health AI

## impact

This work advances responsible AI in mental health applications by:

1. Providing empirical evidence of bias in depression detection systems
2. Demonstrating the importance of fairness evaluation in clinical AI
3. Offering practical mitigation strategies for reducing demographic disparities
4. Informing model selection and deployment decisions for mental health tools

---

*This research is conducted at the HUBBS Lab at CU Boulder's Institute of Cognitive Science under the supervision of Dr. Theodora Chaspari.*
