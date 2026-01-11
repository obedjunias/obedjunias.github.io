---
layout: page
title: Medical Ethics Assessment of Large Language Models
description: Evaluating ethical reasoning capabilities of LLMs in clinical contexts
img:
importance: 2
category: work
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [Research Objective](#research-objective) • [Methodology](#methodology) • [Key Findings](#key-findings) • [Impact & Implications](#impact-and-implications) • [Technical Contributions](#technical-contributions) • [Conclusion](#conclusion)

---

## Overview

Assessed the ethical reasoning capabilities of large language models in clinical contexts, an underexplored dimension of Responsible AI, revealing critical limitations in their reliability and depth for ethically sensitive healthcare tasks.

**Course:** Deep Natural Language Understanding, University of Colorado Boulder
**Status:** Completed

## Research Objective

As LLMs are increasingly applied in clinical contexts for documentation and decision support, their ability to understand and reason about medical ethics remains an open question. This study systematically evaluates whether current models can navigate ethical trade-offs that arise in day-to-day medical practice.

## Methodology

### Model Evaluation

Evaluated four representative LLMs across different model types and training focuses:

- **Mistral-7B**: General-purpose baseline model
- **BioMistral-7B**: Domain-adapted version fine-tuned on biomedical data
- **DeepSeek-R1-Distill-Qwen-1.5B**: Instruction-tuned open-source model
- **ChatGPT-4o-mini**: State-of-the-art proprietary model

**Key Comparisons:**
1. Domain adaptation effects (Mistral vs. BioMistral)
2. Open-source vs. proprietary model capabilities
3. Answer accuracy vs. reasoning quality

### Evaluation Framework

**Question Set**: Curated 100 multiple-choice questions spanning high-stakes ethical categories:
- Informed consent
- Surrogate decision-making
- Disclosure and confidentiality
- Reproductive rights
- Public health obligations
- Professional impairment
- End-of-life care

**Prompting Strategies:**
- **Zero-shot**: Direct answer selection
- **Few-shot**: 3-5 examples with gold-standard rationales
- **RAG-enhanced**: Retrieval-Augmented Generation using AMA Code of Medical Ethics

### Retrieval-Augmented Generation Pipeline

Implemented RAG using the AMA Code of Medical Ethics as external knowledge source:

- **Embedding Model**: PubMedBERT MS MARCO for biomedical text retrieval
- **Retrieval Process**: Top-10 similar chunks using cosine similarity
- **Re-ranking**: MiniLM cross-encoder for semantic relevance
- **Integration**: Top-ranked sections prepended to model prompts

### Behavioral Probing Techniques

**Confidence Probing (Open-Source Models)**
- Extracted token-level logits and computed softmax probabilities
- Measured confidence in each answer choice, including incorrect selections
- Identified cases of confidently wrong predictions

**Reasoning Probing (ChatGPT & DeepSeek)**
- Collected natural language rationales via "letter + reason" prompts
- Two-step verification:
  1. **Answer Match**: Consistency between stated choice and generated answer
  2. **Reasoning Match**: Alignment with gold-standard ethical principles and clinical logic

## Key Findings

### Performance Results

**Model Accuracy:**
- BioMistral outperformed Mistral, demonstrating benefit of domain adaptation
- ChatGPT-4o-mini achieved highest overall accuracy and reasoning quality
- Even best model failed on nearly 1 in 5 cases, often with high confidence

**RAG Impact:**
- Minimal performance gains from external ethics guidelines
- Retrieved content either already known or too general to be useful
- Suggests context alone insufficient without application capability

**Few-Shot Learning:**
- Mixed results: improved Mistral accuracy
- Slightly reduced BioMistral performance (possible interference with domain training)
- Limited overall effectiveness

### Critical Limitations Identified

**Reliability Issues:**
- Models made serious errors on ethically complex scenarios
- High-confidence incorrect answers pose safety risks
- Failures particularly common with conflicting ethical principles

**Reasoning Depth:**
- Partial knowledge of medical ethics principles
- Inability to reliably apply principles to novel situations
- Surface-level pattern matching vs. true ethical understanding

**Contextual Application:**
- Models struggle to navigate trade-offs between competing ethical values
- Difficulty with nuanced, real-world clinical scenarios
- External knowledge integration insufficient without reasoning capability

## Research Questions Addressed

1. **How well do current LLMs identify the most ethical course of action in clinical settings?**
   - Partial competence with significant failures, especially on complex cases

2. **Does domain adaptation or external knowledge retrieval improve ethical performance?**
   - Domain adaptation helps modestly; RAG provides minimal benefit

3. **Do model confidence scores and natural language rationales provide reliable signals of ethical soundness?**
   - No—models can be confidently wrong; rationales often miss critical reasoning

## Impact and Implications

### Societal Impact

**Early Warning Signal**: Systematic evidence of LLM failures in medical-ethical reasoning enables development of safer clinical decision-support tools

**Clinical Safety**: Highlights dangers of over-reliance on LLMs in high-stakes settings, prompting:
- Rigorous human oversight requirements
- Additional safety checks before deployment
- Domain-specific alignment investments

### Broader Implications

1. **Current State**: LLMs exhibit partial understanding of medical ethics but lack reliability for clinical use
2. **Deployment Risk**: Ethically flawed suggestions could jeopardize patient safety and erode public trust
3. **Research Needs**: Better training methods, stronger grounding in ethical principles, and more thoughtful evaluation required

## Technical Contributions

1. **Curated Evaluation Benchmark**: 100-question dataset covering diverse high-stakes ethical scenarios
2. **Dual Probing Framework**: Combined confidence analysis and reasoning evaluation for comprehensive assessment
3. **RAG Pipeline for Ethics**: Retrieval system using professional medical ethics guidance
4. **Systematic Comparison**: Domain adaptation, few-shot learning, and external knowledge effects

## Conclusion

This study demonstrates that current language models show partial understanding of medical ethics principles but are not yet reliable for clinical applications. Simply adding more context through retrieval or examples is insufficient—models need fundamental improvements in how they reason about and apply ethical principles in complex situations.

The findings serve as a critical foundation for future work on trustworthy medical AI, emphasizing the need for human oversight, specialized training, and robust safety mechanisms before LLMs can be responsibly deployed in healthcare settings.

---

*This research contributes to the responsible development of AI systems in healthcare by identifying specific limitations and risks in current LLM approaches to medical ethics.*
