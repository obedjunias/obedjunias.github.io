---
layout: page
title: S-LoRAA - Scalable Multi-Agent LLM System
description: Dynamic LoRA adapter orchestration for efficient multi-agent inference pipelines
img:
importance: 1
category: agentic ai & systems
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [System Architecture](#system-architecture) • [Experimental Results](#experimental-results) • [Technical Contributions](#technical-contributions) • [Impact & Insights](#impact-and-insights) • [Conclusion](#conclusion)

---

## overview

Designed and implemented S-LoRAA, a scalable system for dynamically orchestrating multiple LoRA adapters as independent agents over a shared frozen base model, enabling efficient multi-agent LLM pipelines under resource constraints.

**Timeline:** August 2025 – Present
**Course:** Systems for Machine Learning, University of Colorado Boulder
**Status:** Completed

## System Architecture

S-LoRAA treats each agent as a lightweight LoRA module that can be loaded, executed, and evicted on demand, providing a systems-oriented solution to multi-agent LLM deployment.

### Core Components

**LoRA-Based Agents**
- Each agent represented as a low-rank update (A_i, B_i) on a frozen base model
- Independent, task-specific adapters for specialized behaviors
- Dramatically reduced memory footprint compared to full models

**Adapter Manager**
- Handles all GPU memory interactions and adapter lifecycle
- Maintains registry of available adapters
- Performs dynamic loading/unloading with latency optimization
- Manages memory pressure through intelligent caching

**Orchestration System**
- Coordinates agent execution across multi-step pipelines
- Implements three scheduling policies:
  - **LRU (Least Recently Used)**: Evicts least recently used adapters
  - **Lookahead**: Uses future task information to minimize reloads
  - **Round-Robin**: Cycles through agents in fixed order
- Routes inference calls and manages adapter transitions

**Execution Pipeline**
- Multi-stage processing: environment → orchestrator → adapter manager → model
- Fine-grained system-level logging of metrics
- Precise measurement of load/unload overhead and GPU transitions

### Evaluation Environments

Three controlled settings to isolate ordering effects:

1. **Global Random Shuffle**: Maximal entropy, unpredictable adapter transitions
2. **Per-Topic Block**: Questions grouped by subject, minimal switching
3. **Round-Robin Interleaving**: Deterministic high-frequency switching

## Experimental Results

### Performance Across Memory Tiers

Evaluated system behavior at 5 GB, 7.5 GB, and 15 GB memory budgets:

**LoRA Adapters:**
- Robust across all environments and memory constraints
- Stable accuracy regardless of switching frequency
- Load time < 1 second per adapter
- Nearly scheduler-agnostic behavior

**Full Fine-Tuned Models:**
- Higher accuracy but extreme memory requirements
- Infeasible at 5 GB, unstable at 7.5 GB
- Load time tens of seconds (20-90× slower than LoRA)
- Highly sensitive to switching patterns

### Key Findings

**Systems-ML Trade-offs**
- LoRA enables multi-agent operation where full models are infeasible
- Memory constraints create hard feasibility boundaries
- Cumulative switching overhead dominates full-model pipelines

**Scheduler Influence**
- LoRA: Minimal variance across scheduling policies
- Full models: Dramatic differences between LRU, Lookahead, and Round-Robin
- Lookahead reduces unnecessary loads in high-entropy workloads

**Ordering Impact**
- Block evaluation minimizes transitions but differences persist at systems level
- Shuffle and round-robin environments amplify switching costs
- LoRA maintains efficiency across all ordering patterns

## Technical Contributions

1. **Dynamic Multi-Agent Framework**: Complete lifecycle management for LoRA adapters including loading, execution, eviction, and scheduling under GPU memory constraints

2. **Controlled Evaluation Methodology**: Three execution environments isolating different sources of variation in multi-task performance

3. **Comparative Systems Study**: Comprehensive measurement of accuracy, latency, memory usage, throughput, and runtime for LoRA vs. full models

4. **Fine-Grained Metrics**: System-level logging of load/unload counts, GPU memory transitions, and inference latency

## Impact and Insights

**Systems Design Perspective:**
- Parameter-efficient adaptation is a systems design decision, not just a modeling choice
- Lightweight adapters enable scalable execution of specialized behaviors
- Multi-agent LLM pipelines can be efficient even on modest hardware

**Practical Implications:**
- LoRA-based agents practical for real-world deployment under resource constraints
- Scheduler choice critical for full models but not for LoRA
- Switching overhead often determines pipeline feasibility, not model accuracy

**Future Directions:**
- Hybrid model-sharing strategies
- Advanced scheduling policies with predictive loading
- Multi-GPU and distributed execution
- Application to complex agentic workflows

## Conclusion

S-LoRAA demonstrates that multi-agent LLM systems can be made practical through parameter-efficient adaptation. The system provides a foundation for understanding how model specialization and systems behavior interact, showing that lightweight LoRA adapters enable scalable multi-agent operation where traditional full-model pipelines fail or become prohibitively expensive.

---

*This project was completed as part of the Systems for Machine Learning course at the University of Colorado Boulder.*
