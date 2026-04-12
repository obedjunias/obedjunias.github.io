---
layout: page
title: lost in plot - contrastive learning for movie retrieval
description: dense retrieval system for tip-of-the-tongue movie search from vague descriptions
img:
importance: 2
category: nlp research ,reasoning & llm safety
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [Problem Statement](#problem-statement) • [Approach](#approach) • [Results](#results) • [Technical Contributions](#technical-contributions) • [Insights & Future Directions](#insights-and-future-directions) • [Impact](#impact)

---

## overview

Developed a dense retrieval system for "tip-of-the-tongue" movie search, enabling users to find films from vague, fragmentary natural language descriptions using contrastive learning.

**Course:** Natural Language Processing, University of Colorado Boulder
**Status:** Completed

## problem statement

Humans naturally recall movies through fragments—bits of plot, emotion, or striking visuals—rather than exact titles. We remember "that comic-horror about a haunted house at Christmas" or "the one where Brad Pitt plays Death," not precise keywords. This creates a fundamental gap:

**The Challenge:**
- Traditional keyword-based search fails with vague queries
- Generative models (LLMs) hallucinate plausible but incorrect titles
- Need semantic understanding to bridge natural descriptions and movie metadata

**Research Questions:**
1. How effective is contrastive learning-based dense retrieval for retrieving movies from vague user descriptions?
2. How does a fine-tuned model compare to few-shot prompting (GPT-4) and vanilla BERT encoder?

## approach

### System Architecture

**Base Model:** Pre-trained BERT encoder with contrastive multi-task learning

**Components:**
1. **Encoder:** BERT produces contextualized embeddings with mean pooling
2. **Projection Layer:** Linear projection to lower-dimensional retrieval space with ℓ2-normalization
3. **Classification Heads:** Three auxiliary tasks for genre, decade, and theme prediction

**Mathematical Formulation:**
```
h = MeanPool(BERT(text, mask)) ∈ R^H
ẑ = normalize(W_proj · h)  // retrieval embedding
```

### Data Preparation

**Movie Metadata (TMDb/IMDb):**
- Combined plot summaries, titles, and keywords
- Multi-hot encoding for genres
- Decade mapping for release years
- Latent themes extracted via BERTopic clustering

**Synthetic Dataset:**
- Created 3,000 vague movie descriptions using GPT-4 few-shot prompting
- Indexed 100K+ movies in FAISS for efficient retrieval
- Evaluation queries mimic real "tip-of-the-tongue" scenarios

### Anchor-Positive Sampling

Training pairs (aᵢ, pᵢ) where:
- **Anchor (aᵢ):** Movie metadata (plot, title, keywords) from a specific theme
- **Positive (pᵢ):** Different movie sharing same BERTopic theme
- **Implicit Negatives:** All other examples in the batch

### Multi-Task Loss Function

**InfoNCE Contrastive Loss:**
```
L_retr = -1/N Σᵢ log[exp(ẑᵃᵢ · ẑᵖᵢ/τ) / Σⱼ exp(ẑᵃᵢ · ẑᵖⱼ/τ)]
```

**Auxiliary Classification Losses:**
- Genre prediction (multi-label binary cross-entropy)
- Decade prediction (cross-entropy)
- Theme prediction (cross-entropy)

**Combined Objective:**
```
L = w_retr·L_retr + w_genre·L_genre + w_year·L_year + w_theme·L_theme
```

### Training Details

- **Optimizer:** AdamW with weight decay
- **Batch size:** 16
- **Learning rate:** 2×10⁻⁵
- **Scheduler:** Cosine decay with 10% warm-up
- **Epochs:** 8 (early stopping on MRR)
- **Evaluation:** FAISS index of 100K movies, measured Recall@1/5/10/25 and MRR

## results

### Performance Comparison

**Key Findings:**
- **vs. GPT-4 Few-Shot:** Contrastive model significantly outperformed on Recall@K and MRR
- **vs. Vanilla BERT:** Fine-tuned model fell slightly short of base encoder performance

**Metrics:** Recall@1, Recall@5, Recall@10, Recall@25, Mean Reciprocal Rank (MRR)

### Why It Beats GPT-4 Few-Shot

**Reliability Advantage:**
- GPT-4 frequently hallucinates plausible but incorrect titles
- Dense retrieval grounds answers in pre-computed embeddings
- Cosine similarity over indexed movies ensures factual retrieval
- No generation means no fabrication

### Why It Lags Behind Vanilla BERT

**Analysis of Performance Gap:**

1. **Large Theme Space:**
   - Too many themes introduced noisy positives
   - Some themes had only handful of movies (under-represented)

2. **Coarse Theme Granularity:**
   - Movies sharing high-level topics still semantically distant
   - Example: Two "sci-fi" films with very different plots treated as similar

3. **Weak Positive Sampling:**
   - Relied only on shared themes
   - Ignored stronger signals: overlapping keywords, cast, directors

4. **Competing Classification Heads:**
   - Multiple auxiliary objectives pulled model in different directions
   - Genre, decade, and theme heads potentially overwhelmed core retrieval signal
   - Balancing multi-task losses proved delicate

## technical contributions

1. **Dense Retrieval Framework:** Contrastive learning system aligning vague descriptions with movie metadata in shared semantic space

2. **Synthetic Evaluation Dataset:** 3,000+ "tip-of-the-tongue" queries mimicking real user search patterns

3. **Multi-Task Architecture:** Combined retrieval and classification objectives for semantic understanding

4. **Large-Scale Indexing:** FAISS-based system for efficient retrieval over 100K+ movies

5. **Comparative Analysis:** Systematic evaluation against strong baselines (GPT-4, vanilla BERT)

## insights and future directions

### Key Takeaways

**Contrastive Learning Promise:**
- Modest fine-tuning yields practical benefits over generative approaches
- Reliable retrieval without hallucination risk
- Scalable to large movie databases

**Challenges Identified:**
- Theme-based positives insufficient for strong semantic signal
- Multi-task loss balancing critical but difficult
- Need for harder negative mining strategies

### Future Work

**Methodological Improvements:**
- **Hard Negative Mining:** More challenging negatives during training
- **Partial Fine-Tuning:** Only tune top transformer layers to preserve general knowledge
- **Richer Metadata Signals:** Incorporate cast, directors, cinematographer into contrastive objective
- **Adaptive Loss Weighting:** Dynamic balancing of multi-task objectives

**Evaluation Enhancements:**
- Test on real user queries (not just synthetic descriptions)
- User studies measuring practical search effectiveness
- Cross-dataset generalization evaluation

**Broader Applications:**
- Extend to music retrieval ("that song about flying and loss")
- Photo search from vague descriptions ("waterfall at sunrise")
- General "tip-of-the-tongue" information retrieval

## impact

This work demonstrates that contrastive learning can bridge the gap between natural human descriptions and structured metadata, enabling more intuitive search systems. While challenges remain, the approach shows clear advantages over generative methods in factual grounding and retrieval reliability.

The system addresses a common real-world problem—finding content from imperfect memory—and provides a foundation for semantic retrieval in domains where vague queries are the norm.

---

*This project was completed as part of the Natural Language Processing course at the University of Colorado Boulder.*
