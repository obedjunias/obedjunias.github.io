---
layout: page
title: "ScoutR: Agentic Football Transfer Intelligence Platform"
description: Agentic AI transfer intelligence platform for club tactical and financial constraints
img:
importance: 1
category: agentic ai & systems
related_publications: false
---

**Quick Navigation:** [Overview](#overview) • [System Architecture](#system-architecture) • [Key Features](#key-features) • [Technical Stack](#technical-stack)

---

## overview

Designed and shipped **ScoutR**, an **agentic AI transfer intelligence platform** that monitors player data across leagues and surfaces candidates aligned to club tactical and financial constraints. 

ScoutR transforms how football clubs identify talent by leveraging autonomous agents to reason over complex statistical and financial data, providing grounded recommendations that reduce manual scouting overhead and optimize recruitment.

**Status:** Completed  
**Tech Stack:** LangGraph, Gemini, Claude, Pydantic, ChromaDB, RAG, SSE, Prompt Engineering

## system architecture

### Multi-Agent Pipeline

Built a robust **LangGraph-based multi-agent orchestration layer** where agents collaborate to fulfill complex scouting requests:

- **Parsing Agent**: Uses Gemini to parse natural language scouting queries into structured **Pydantic schemas**, enabling precise tool calling, typed intermediate states, and complex downstream reasoning.
- **Analysis Agent**: Produces tactical-fit analysis and valuation summaries based on retrieved data.
- **Fault-Tolerant Inference Layer**: Designed a **3-tier multi-model inference layer** (Gemini → Claude → fallback) to handle API rate limits and outages while maintaining uninterrupted agent workflows for mission-critical recruitment.

## key features

### RAG over StatsBomb Event Data
Implemented a **Retrieval-Augmented Generation (RAG)** pipeline using **ChromaDB** to index StatsBomb event data. This allows the agents to:
- Ground all recommendations in granular statistical evidence.
- Dramatically reduce hallucinated comparisons during player evaluation.
- Provide direct citations to specific match events or performance metrics.

### Real-Time Streaming UX
Engineered a modern, transparent interface using **Server-Sent Events (SSE)**:
- **Streaming Execution**: Exposes intermediate reasoning steps in real-time as the agent executes **long-horizon tasks**.
- **Interactive Interface**: Supports complex decision workflows in a single interactive view, revealing the decision process that previously was a "black box".

## impact

ScoutR provides professional-grade analytics to clubs without large dedicated data teams, democratizing access to agentic AI in sports technology. By automating the initial "filtering" and "analysis" phases of recruitment, it allows human scouts to focus on final validation and qualitative assessment.

---

*This project highlights the intersection of Agentic NLP, RAG, and high-stakes decision support systems.*
