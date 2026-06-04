---
layout: page
title: "LOGICAL-COMMONSENSEQA"
description: "A Benchmark for Logical Commonsense Reasoning"
permalink: /logical-csqa/
nav: false
---

<style>
  .project-hero {
    background: linear-gradient(135deg, #1a1a2e 0%, #16213e 50%, #0f3460 100%);
    border-radius: 12px;
    padding: 2.5rem 2rem;
    margin-bottom: 2rem;
    color: #fff;
    position: relative;
    overflow: hidden;
  }
  .project-hero::before {
    content: '';
    position: absolute;
    top: -40%;
    right: -10%;
    width: 350px;
    height: 350px;
    background: radial-gradient(circle, rgba(99,179,237,0.12) 0%, transparent 70%);
    pointer-events: none;
  }
  .project-hero h1 {
    font-size: 2rem;
    font-weight: 800;
    letter-spacing: -0.5px;
    margin-bottom: 0.4rem;
    color: #fff;
  }
  .project-hero .subtitle {
    font-size: 1.1rem;
    color: #a0c4ff;
    margin-bottom: 1.2rem;
  }
  .badge-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.5rem;
    margin-bottom: 1.4rem;
  }
  .badge {
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
    padding: 0.3rem 0.75rem;
    border-radius: 999px;
    font-size: 0.78rem;
    font-weight: 600;
    letter-spacing: 0.02em;
    text-transform: uppercase;
  }
  .badge-acl    { background: rgba(52,211,153,0.18); color: #6ee7b7; border: 1px solid rgba(52,211,153,0.35); }
  .badge-nlp    { background: rgba(99,179,237,0.18); color: #93c5fd; border: 1px solid rgba(99,179,237,0.35); }
  .badge-cu     { background: rgba(250,200,80,0.15);  color: #fcd34d; border: 1px solid rgba(250,200,80,0.3); }
  .authors-line {
    font-size: 0.95rem;
    color: #cbd5e1;
    margin-bottom: 1.2rem;
  }
  .authors-line a { color: #93c5fd; text-decoration: none; }
  .authors-line a:hover { text-decoration: underline; }
  .link-buttons {
    display: flex;
    flex-wrap: wrap;
    gap: 0.6rem;
  }
  .link-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.4rem;
    padding: 0.45rem 1rem;
    border-radius: 8px;
    font-size: 0.85rem;
    font-weight: 600;
    text-decoration: none !important;
    transition: opacity 0.18s, transform 0.18s;
  }
  .link-btn:hover { opacity: 0.85; transform: translateY(-1px); }
  .btn-paper  { background: #3b82f6; color: #fff !important; }
  .btn-arxiv  { background: #b91c1c; color: #fff !important; }
  .btn-code   { background: #374151; color: #fff !important; }
  .btn-poster { background: #6d28d9; color: #fff !important; }

  .abstract-box {
    border-left: 4px solid #3b82f6;
    background: var(--global-code-bg-color, #f8fafc);
    border-radius: 0 8px 8px 0;
    padding: 1.2rem 1.5rem;
    margin: 1.5rem 0;
    font-size: 0.95rem;
    line-height: 1.7;
  }

  .section-title {
    font-size: 1.25rem;
    font-weight: 700;
    margin-top: 2rem;
    margin-bottom: 0.8rem;
    padding-bottom: 0.4rem;
    border-bottom: 2px solid #e2e8f0;
  }
  
  .operator-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 1rem;
    margin: 1rem 0 1.5rem;
  }
  .operator-card {
    border-radius: 10px;
    padding: 1.1rem 1rem;
    text-align: center;
  }
  .op-and  { background: linear-gradient(135deg, #d1fae5, #a7f3d0); border: 1px solid #6ee7b7; }
  .op-or   { background: linear-gradient(135deg, #dbeafe, #bfdbfe); border: 1px solid #93c5fd; }
  .op-nor  { background: linear-gradient(135deg, #fce7f3, #fbcfe8); border: 1px solid #f9a8d4; }
  .operator-card .op-label {
    font-size: 1.4rem;
    font-weight: 800;
    font-family: monospace;
    margin-bottom: 0.3rem;
  }
  .op-and .op-label  { color: #065f46; }
  .op-or  .op-label  { color: #1e40af; }
  .op-nor .op-label  { color: #9d174d; }
  .operator-card .op-desc {
    font-size: 0.82rem;
    color: #374151;
  }

  .results-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.88rem;
    margin: 1rem 0 1.5rem;
  }
  .results-table th {
    background: #1e3a5f;
    color: #fff;
    padding: 0.6rem 0.8rem;
    text-align: left;
    font-weight: 600;
  }
  .results-table td {
    padding: 0.55rem 0.8rem;
    border-bottom: 1px solid #e2e8f0;
  }
  .results-table tr:nth-child(even) td { background: #f8fafc; }
  .results-table .best { font-weight: 700; color: #1d4ed8; }
  .results-table .worst { color: #b91c1c; }

  .finding-list {
    list-style: none;
    padding: 0;
    margin: 0.5rem 0 1.5rem;
  }
  .finding-list li {
    display: flex;
    gap: 0.75rem;
    align-items: flex-start;
    margin-bottom: 0.8rem;
    font-size: 0.95rem;
    line-height: 1.6;
  }
  .finding-list li::before {
    content: attr(data-icon);
    font-size: 1.1rem;
    flex-shrink: 0;
    margin-top: 0.05rem;
  }

  .example-box {
    background: #f0f4ff;
    border: 1px solid #c7d7fd;
    border-radius: 10px;
    padding: 1.2rem 1.4rem;
    margin: 1rem 0 1.5rem;
    font-size: 0.9rem;
    line-height: 1.7;
  }
  .example-box .ex-question { font-weight: 600; color: #1e3a5f; margin-bottom: 0.4rem; }
  .example-box .ex-statements { color: #374151; margin-bottom: 0.4rem; }
  .example-box .ex-op { font-weight: 700; color: #3b82f6; font-family: monospace; }
  .example-box .ex-answer { color: #065f46; font-weight: 600; }

  .citation-box {
    background: #1e293b;
    color: #e2e8f0;
    border-radius: 10px;
    padding: 1.2rem 1.5rem;
    font-family: monospace;
    font-size: 0.8rem;
    line-height: 1.7;
    overflow-x: auto;
    margin: 1rem 0;
  }

  .venue-pill {
    display: inline-block;
    padding: 0.25rem 0.7rem;
    background: linear-gradient(90deg, #7c3aed, #3b82f6);
    color: #fff;
    border-radius: 999px;
    font-size: 0.78rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }
</style>

<!-- ═══════════════════════════════════════════════════ HERO -->
<div class="project-hero">
  <h1>LOGICAL-COMMONSENSEQA</h1>
  <p class="subtitle">A Benchmark for Logical Commonsense Reasoning</p>

  <div class="badge-row">
    <span class="badge badge-acl">🏆 ACL 2026 Main Conference</span>
    <span class="badge badge-nlp">📖 Commonsense Reasoning</span>
    <span class="badge badge-cu">🏔 CU Boulder · BLAST Lab</span>
  </div>

  <p class="authors-line">
    <a href="https://obedjunias.com">Obed Junias</a><sup>1</sup>&ensp;·&ensp;
    <a href="https://blast-cu.github.io/">Maria Leonor Pacheco</a><sup>1</sup><br>
    <sup>1</sup>University of Colorado Boulder
  </p>

  <div class="link-buttons">
    <a class="link-btn btn-paper" href="https://arxiv.org/abs/2601.16504" target="_blank">📄 Paper</a>
    <a class="link-btn btn-arxiv" href="https://arxiv.org/pdf/2601.16504" target="_blank">⬇ PDF</a>
    <a class="link-btn btn-poster" href="/logical-csqa/slides/" target="_blank">🖥 Slides</a>
  </div>
</div>

<!-- ═══════════════════════════════════════════════════ ABSTRACT -->
<div class="abstract-box">
  <strong>Abstract.</strong>
  Commonsense reasoning often involves evaluating multiple plausible interpretations rather than selecting a single atomic answer, yet most benchmarks rely on single-label evaluation, obscuring whether statements are jointly plausible, mutually exclusive, or jointly implausible. We introduce <strong>LOGICAL-COMMONSENSEQA</strong>, a benchmark that reframes commonsense reasoning as <em>logical composition</em> over pairs of atomic statements using plausibility-level operators (<strong>AND</strong>, <strong>OR</strong>, and <strong>NEITHER/NOR</strong>). Evaluating instruction-tuned, reasoning-specialized, and fine-tuned models under zero-shot, few-shot, and chain-of-thought prompting, we find that while models perform reasonably on conjunctive and moderately on disjunctive reasoning, performance degrades sharply on negation-based questions. LOGICAL-COMMONSENSEQA exposes fundamental reasoning limitations and provides a controlled framework for advancing compositional commonsense reasoning.
</div>

---

<!-- ═══════════════════════════════════════════════════ MOTIVATION -->
<div class="section-title">Motivation</div>

Standard commonsense QA benchmarks ask models to pick a single correct answer. But everyday reasoning rarely works this way — understanding that *"it can rain AND be sunny"* or *"you cannot be in two cities at once"* requires **logical composition**, not just plausibility scoring over singletons.

Existing benchmarks obscure this distinction. LOGICAL-COMMONSENSEQA makes it explicit by encoding the logical relationship between pairs of commonsense statements as a first-class reasoning target.

<!-- ═══════════════════════════════════════════════════ OPERATORS -->
<div class="section-title">Logical Operators</div>

<div class="operator-grid">
  <div class="operator-card op-and">
    <div class="op-label">AND</div>
    <div class="op-desc">Both statements are jointly plausible given the question context</div>
  </div>
  <div class="operator-card op-or">
    <div class="op-label">OR</div>
    <div class="op-desc">At least one statement is plausible — they are not mutually exclusive</div>
  </div>
  <div class="operator-card op-nor">
    <div class="op-label">NEITHER / NOR</div>
    <div class="op-desc">Neither statement is plausible — both are jointly implausible</div>
  </div>
</div>

**Example question:**

<div class="example-box">
  <div class="ex-question">Q: What would you do if you were hungry?</div>
  <div class="ex-statements">
    S₁: <em>You would eat food.</em><br>
    S₂: <em>You would drink water.</em>
  </div>
  <div>Logical operator: <span class="ex-op">AND</span></div>
  <div class="ex-answer">✓ Both are jointly plausible responses to hunger.</div>
</div>

<!-- ═══════════════════════════════════════════════════ METHODOLOGY -->
<div class="section-title">Benchmark Construction</div>

The benchmark is built on top of **CommonsenseQA** and its underlying **ConceptNet** knowledge graph:

1. **Pair Sampling** — For each question, pairs of answer candidates are sampled and labeled with AND / OR / NEITHER based on their joint plausibility under the original question context.
2. **Annotation Protocol** — Labels are derived from the structure of human-annotated ConceptNet triples combined with crowdsourced plausibility judgments.
3. **Compositional Test Set** — Items span all three operator types, enabling fine-grained evaluation of conjunction, disjunction, and negation-based commonsense reasoning.

<!-- ═══════════════════════════════════════════════════ EVALUATION -->
<div class="section-title">Evaluation Setup</div>

We evaluate a diverse set of model families and prompting strategies:

| Category | Models |
|---|---|
| Instruction-tuned | GPT-4o, Claude 3 Sonnet, Llama-3 Instruct |
| Reasoning-specialized | o1-mini, DeepSeek-R1 |
| Fine-tuned | RoBERTa-large, DeBERTa-v3 |

**Prompting conditions:** Zero-shot · Few-shot · Chain-of-Thought (CoT)

<!-- ═══════════════════════════════════════════════════ KEY FINDINGS -->
<div class="section-title">Key Findings</div>

<ul class="finding-list">
  <li data-icon="✅">Models perform <strong>reasonably on AND (conjunctive) reasoning</strong> — the easiest operator — especially under chain-of-thought prompting.</li>
  <li data-icon="⚠️">Performance is <strong>moderate on OR (disjunctive) reasoning</strong>, with notable variance across model families.</li>
  <li data-icon="❌">Performance <strong>degrades sharply on NEITHER/NOR (negation-based) questions</strong> — the hardest operator — across all model types and prompting conditions.</li>
  <li data-icon="🔍">Chain-of-thought prompting helps for AND and OR but provides <strong>limited benefit for negation</strong>, suggesting structural reasoning gaps rather than insufficient context.</li>
  <li data-icon="📊">Fine-tuned discriminative models exhibit different failure modes compared to large generative instruction-tuned models.</li>
</ul>

<!-- ═══════════════════════════════════════════════════ CONTRIBUTIONS -->
<div class="section-title">Contributions</div>

1. **LOGICAL-COMMONSENSEQA benchmark** — A novel evaluation dataset that reframes commonsense QA as logical composition over statement pairs, enabling controlled assessment of AND, OR, and NEITHER/NOR reasoning.

2. **Systematic evaluation** — Comprehensive benchmarking of instruction-tuned, reasoning-specialized, and fine-tuned models across multiple prompting regimes (zero-shot, few-shot, CoT).

3. **Diagnostic insight** — A detailed error analysis revealing that negation-based commonsense reasoning is a persistent, cross-model bottleneck not resolved by scaling or improved prompting.

4. **Foundation for future work** — A controlled compositional framework that enables targeted research on advancing logical commonsense reasoning beyond single-label benchmarks.

<!-- ═══════════════════════════════════════════════════ PRESENTATION -->
<div class="section-title">Presentation</div>

<span class="venue-pill">ACL 2026</span> &ensp; **63rd Annual Meeting of the Association for Computational Linguistics**

This work is presented at the main conference. If you are attending ACL 2026 and would like to discuss the paper, feel free to [reach out](https://obedjunias.com/#contact).

**[🖥 View the conference slides →](/logical-csqa/slides/){:target="_blank"}**

<!-- ═══════════════════════════════════════════════════ CITATION -->
<div class="section-title">Citation</div>

<div class="citation-box">
@article{junias2026logical,<br>
&nbsp;&nbsp;title     = {LOGICAL-COMMONSENSEQA: A Benchmark for Logical Commonsense Reasoning},<br>
&nbsp;&nbsp;author    = {Junias, Obed and Pacheco, Maria Leonor},<br>
&nbsp;&nbsp;journal   = {arXiv preprint arXiv:2601.16504},<br>
&nbsp;&nbsp;year      = {2026},<br>
&nbsp;&nbsp;url       = {https://arxiv.org/abs/2601.16504}<br>
}
</div>

---

*This research is conducted at the [BLAST Lab](https://blast-cu.github.io/) at the University of Colorado Boulder under the supervision of Dr. Maria Leonor Pacheco.*
