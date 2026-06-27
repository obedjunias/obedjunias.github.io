---
layout: page
title: "LOGICAL-COMMONSENSEQA"
description: "A Benchmark for Logical Commonsense Reasoning"
permalink: /logical-csqa/
nav: false
---

<style>
  @import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;500;600;700;800;900&display=swap');

  /* ── Design tokens (poster theme) ──────────────────────────────────── */
  .lcsqa { font-family: "Inter", system-ui, sans-serif; color: #4A4A4A; }

  /* ── Hero ─────────────────────────────────────────────────────────── */
  .lcsqa-hero {
    background: #fff;
    border-radius: 12px;
    border: 1.5px solid #D6DAE2;
    overflow: hidden;
    margin-bottom: 1.5rem;
    box-shadow: 0 2px 12px rgba(27,42,74,0.08);
  }
  .hero-accent {
    height: 6px;
    background: #1B2A4A;
  }
  .hero-body { padding: 1.75rem 2rem 1.6rem; }
  .hero-title {
    font-family: Georgia, "Times New Roman", serif;
    font-size: 2rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    color: #1B2A4A;
    margin: 0 0 0.2rem;
    line-height: 1.1;
  }
  .hero-subtitle {
    font-size: 1rem;
    font-weight: 600;
    color: #1B2A4A;
    margin: 0 0 1rem;
  }
  .thesis-pill {
    display: inline-block;
    padding: 0.45rem 1rem;
    background: #EBF3FD;
    border: 2px solid #C2D9F0;
    border-radius: 10px;
    font-size: 0.88rem;
    font-weight: 700;
    color: #1B2A4A;
    margin-bottom: 1rem;
    line-height: 1.35;
  }
  .hero-authors {
    font-size: 0.88rem;
    color: #4A4A4A;
    margin-bottom: 1rem;
    line-height: 1.6;
  }
  .hero-authors a { color: #378ADD; text-decoration: none; }
  .hero-authors a:hover { text-decoration: underline; }

  /* ── Badges ───────────────────────────────────────────────────────── */
  .badge-row {
    display: flex;
    flex-wrap: wrap;
    gap: 0.4rem;
    margin-bottom: 1rem;
  }
  .lcsqa-badge {
    display: inline-flex;
    align-items: center;
    padding: 0.22rem 0.65rem;
    border-radius: 999px;
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.03em;
    text-transform: uppercase;
  }
  .badge-acl { background: rgba(55,138,221,0.12); color: #1B2A4A; border: 1px solid rgba(55,138,221,0.35); }
  .badge-nlp { background: rgba(42,157,143,0.10); color: #1B5E57; border: 1px solid rgba(42,157,143,0.30); }
  .badge-cu  { background: rgba(27,42,74,0.07);   color: #1B2A4A; border: 1px solid rgba(27,42,74,0.20); }

  /* ── Link buttons ─────────────────────────────────────────────────── */
  .link-buttons { display: flex; flex-wrap: wrap; gap: 0.45rem; }
  .link-btn {
    display: inline-flex;
    align-items: center;
    gap: 0.3rem;
    padding: 0.38rem 0.85rem;
    border-radius: 8px;
    font-size: 0.8rem;
    font-weight: 700;
    text-decoration: none !important;
    transition: opacity 0.15s, transform 0.15s;
    font-family: "Inter", system-ui, sans-serif;
  }
  .link-btn:hover { opacity: 0.82; transform: translateY(-1px); }
  .btn-paper   { background: #1B2A4A; color: #fff !important; }
  .btn-arxiv   { background: #374151; color: #fff !important; }
  .btn-slides  { background: #374151; color: #fff !important; }
  .btn-code    { background: #374151; color: #fff !important; }
  .btn-dataset { background: #2A7A6F; color: #fff !important; }

  /* ── Section block ────────────────────────────────────────────────── */
  .sec-block {
    border: 1.5px solid #D6DAE2;
    border-radius: 12px;
    overflow: hidden;
    margin-bottom: 1.5rem;
    box-shadow: 0 2px 12px rgba(27,42,74,0.06);
  }
  .sec-header {
    background: #1B2A4A;
    padding: 0.9rem 1.5rem;
  }
  .sec-header-title {
    font-family: Georgia, serif;
    font-size: 1.2rem;
    font-weight: 700;
    color: #fff;
    margin: 0 0 0.15rem;
    letter-spacing: 0.02em;
  }
  .sec-header-desc {
    font-size: 0.82rem;
    color: rgba(255,255,255,0.75);
    margin: 0;
  }
  .sec-body {
    padding: 1.2rem 1.5rem;
    background: #F8F9FB;
  }

  /* ── Abstract ─────────────────────────────────────────────────────── */
  .abstract-box {
    border-left: 4px solid #378ADD;
    background: #fff;
    border-radius: 0 8px 8px 0;
    padding: 1rem 1.2rem;
    font-size: 0.91rem;
    line-height: 1.75;
    color: #4A4A4A;
  }

  /* ── Motivation ───────────────────────────────────────────────────── */
  .motivation-text {
    font-size: 0.91rem;
    line-height: 1.75;
    color: #4A4A4A;
    margin: 0 0 0.75rem;
  }
  .logic-questions {
    display: flex;
    flex-direction: column;
    gap: 0.45rem;
    margin: 0.75rem 0 0.9rem;
  }
  .logic-q {
    display: flex;
    align-items: center;
    gap: 0.55rem;
    padding: 0.45rem 0.8rem;
    border-radius: 8px;
    font-size: 0.87rem;
    font-weight: 600;
    background: #fff;
    border: 1.5px solid #D6DAE2;
    color: #1B2A4A;
  }
  .lq-dot { width: 9px; height: 9px; border-radius: 50%; flex-shrink: 0; }

  /* ── Research gap ─────────────────────────────────────────────────── */
  .gap-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(190px, 1fr));
    gap: 0.7rem;
    margin-bottom: 0.75rem;
  }
  .gap-card {
    background: #fff;
    border: 1.5px solid #D6DAE2;
    border-radius: 10px;
    padding: 0.85rem 1rem;
  }
  .gap-card-title {
    font-family: Georgia, serif;
    font-weight: 700;
    color: #1B2A4A;
    font-size: 0.88rem;
    margin-bottom: 0.2rem;
  }
  .gap-card-examples {
    font-size: 0.76rem;
    color: #6B7280;
    margin-bottom: 0.35rem;
    font-style: italic;
  }
  .gap-card-limit { font-size: 0.81rem; color: #4A4A4A; line-height: 1.5; }
  .gap-lcsqa-box {
    background: #EBF3FD;
    border: 1.5px solid #C2D9F0;
    border-radius: 10px;
    padding: 0.7rem 1rem;
    font-size: 0.87rem;
    font-weight: 600;
    color: #1B2A4A;
    text-align: center;
  }

  /* ── Operators ────────────────────────────────────────────────────── */
  .operator-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(150px, 1fr));
    gap: 0.7rem;
    margin-bottom: 1rem;
  }
  .op-card {
    border-radius: 10px;
    padding: 0.9rem 0.85rem;
    text-align: center;
    border: 1.5px solid;
  }
  .op-and { background: #EBF3FD; border-color: #378ADD; }
  .op-or  { background: #E6F5F3; border-color: #2A9D8F; }
  .op-nor { background: #FCE9E6; border-color: #D9544D; }
  .op-mix { background: #F3EFF9; border-color: #8A6FB7; }
  .op-label {
    font-family: monospace;
    font-size: 1.1rem;
    font-weight: 800;
    margin-bottom: 0.25rem;
  }
  .op-and .op-label { color: #1B4F8A; }
  .op-or  .op-label { color: #1A6B5A; }
  .op-nor .op-label { color: #9D2B22; }
  .op-mix .op-label { color: #5B3D8A; }
  .op-desc { font-size: 0.79rem; color: #4A4A4A; line-height: 1.45; }

  .example-box {
    background: #fff;
    border: 1.5px solid #C2D9F0;
    border-radius: 10px;
    padding: 0.95rem 1.2rem;
    font-size: 0.87rem;
    line-height: 1.7;
  }
  .ex-q { font-weight: 700; color: #1B2A4A; margin-bottom: 0.5rem; }
  .ex-op-and { font-family: monospace; font-weight: 800; color: #1B4F8A; }
  .ex-op-or  { font-family: monospace; font-weight: 800; color: #1A6B5A; }
  .ex-op-nor { font-family: monospace; font-weight: 800; color: #9D2B22; }
  .ex-correct { color: #3D7F2C; font-weight: 600; font-size: 0.82rem; }
  .ex-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.84rem;
  }
  .ex-table td { padding: 0.28rem 0.4rem; vertical-align: middle; }
  .ex-table td:first-child { width: 110px; }
  .ex-table td:last-child  { width: 130px; }

  /* ── Pipeline ─────────────────────────────────────────────────────── */
  .pipeline-steps {
    display: flex;
    flex-direction: column;
    gap: 0.6rem;
    margin-bottom: 0.85rem;
  }
  .pipeline-step {
    display: grid;
    grid-template-columns: 2rem 1fr;
    gap: 0.75rem;
    align-items: flex-start;
    background: #fff;
    border: 1.5px solid #D6DAE2;
    border-radius: 10px;
    padding: 0.8rem 1rem;
  }
  .step-num {
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    background: #1B2A4A;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.78rem;
    font-weight: 800;
    flex-shrink: 0;
    margin-top: 0.1rem;
  }
  .step-title {
    font-family: Georgia, serif;
    font-weight: 700;
    color: #1B2A4A;
    font-size: 0.88rem;
    margin-bottom: 0.2rem;
  }
  .step-desc { font-size: 0.83rem; color: #4A4A4A; line-height: 1.5; }
  .validation-badge {
    display: inline-flex;
    align-items: center;
    gap: 0.35rem;
    background: #EAF5F0;
    border: 1.5px solid #3D7F2C;
    border-radius: 8px;
    padding: 0.45rem 0.85rem;
    font-size: 0.82rem;
    font-weight: 600;
    color: #2E5B23;
    margin-bottom: 0.75rem;
  }
  .dataset-stats {
    display: flex;
    gap: 0.65rem;
    flex-wrap: wrap;
  }
  .dataset-stat {
    flex: 1;
    min-width: 100px;
    background: #fff;
    border: 1.5px solid #D6DAE2;
    border-radius: 8px;
    padding: 0.55rem 0.75rem;
    text-align: center;
  }
  .dataset-stat-num {
    font-family: Georgia, serif;
    font-size: 1.15rem;
    font-weight: 700;
    color: #1B2A4A;
  }
  .dataset-stat-label { font-size: 0.73rem; color: #6B7280; margin-top: 0.05rem; }

  /* ── Eval table ───────────────────────────────────────────────────── */
  .eval-table {
    width: 100%;
    border-collapse: collapse;
    font-size: 0.85rem;
  }
  .eval-table th {
    background: #1B2A4A;
    color: #fff;
    padding: 0.5rem 0.75rem;
    text-align: left;
    font-weight: 600;
  }
  .eval-table td {
    padding: 0.48rem 0.75rem;
    border-bottom: 1px solid #D6DAE2;
    color: #4A4A4A;
    line-height: 1.5;
  }
  .eval-table tr:nth-child(even) td { background: #fff; }
  .eval-table tr:nth-child(odd)  td { background: #F8F9FB; }

  /* ── Results ──────────────────────────────────────────────────────── */
  .stat-cards-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(170px, 1fr));
    gap: 0.7rem;
    margin-bottom: 0.85rem;
  }
  .stat-card {
    border-radius: 12px;
    padding: 0.9rem 1rem;
    border: 1.5px solid;
    display: flex;
    flex-direction: column;
  }
  .stat-card-red   { background: #FCE9E6; border-color: #D9544D; }
  .stat-card-green { background: #EAF5F0; border-color: #3D7F2C; }
  .stat-num {
    font-family: Georgia, serif;
    font-size: 1.9rem;
    font-weight: 800;
    line-height: 1;
    margin-bottom: 0.25rem;
  }
  .stat-card-red   .stat-num { color: #D9544D; }
  .stat-card-green .stat-num { color: #3D7F2C; }
  .stat-model { font-size: 0.8rem; font-weight: 700; color: #1B2A4A; margin-bottom: 0.15rem; }
  .stat-caption { font-size: 0.76rem; color: #4A4A4A; line-height: 1.4; }

  .csqa-comparison {
    background: #FFF4BF;
    border: 1.5px solid #E0B100;
    border-radius: 10px;
    padding: 0.9rem 1.2rem;
    font-size: 0.88rem;
    line-height: 1.65;
    color: #4A4A4A;
    margin-bottom: 0.75rem;
  }
  .csqa-comparison strong { color: #1B2A4A; }

  .results-notes {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 0.7rem;
  }
  .results-note {
    background: #fff;
    border: 1.5px solid #D6DAE2;
    border-radius: 10px;
    padding: 0.8rem 1rem;
    font-size: 0.83rem;
    line-height: 1.5;
    color: #4A4A4A;
  }
  .results-note-title {
    font-family: Georgia, serif;
    font-weight: 700;
    color: #1B2A4A;
    font-size: 0.87rem;
    margin-bottom: 0.25rem;
  }

  /* ── Analysis ─────────────────────────────────────────────────────── */
  .analysis-intro { font-size: 0.89rem; color: #4A4A4A; line-height: 1.7; margin-bottom: 0.9rem; }
  .decomposition-cascade {
    display: flex;
    flex-direction: column;
    gap: 0.2rem;
    margin-bottom: 1rem;
  }
  .decomp-step {
    display: grid;
    grid-template-columns: 88px 1fr;
    gap: 0.75rem;
    align-items: center;
    background: #fff;
    border: 1.5px solid;
    border-radius: 10px;
    padding: 0.8rem 1rem;
  }
  .ds-blue   { border-color: #378ADD; }
  .ds-purple { border-color: #8A6FB7; }
  .ds-red    { border-color: #D9544D; }
  .decomp-num {
    font-family: Georgia, serif;
    font-size: 1.5rem;
    font-weight: 800;
    line-height: 1;
    text-align: center;
  }
  .ds-blue   .decomp-num { color: #378ADD; }
  .ds-purple .decomp-num { color: #8A6FB7; }
  .ds-red    .decomp-num { color: #D9544D; }
  .decomp-title {
    font-family: Georgia, serif;
    font-weight: 700;
    color: #1B2A4A;
    font-size: 0.87rem;
    margin-bottom: 0.15rem;
  }
  .decomp-desc { font-size: 0.81rem; color: #4A4A4A; line-height: 1.45; }
  .cascade-arrow {
    text-align: left;
    color: #1B2A4A;
    font-size: 0.85rem;
    opacity: 0.45;
    padding-left: 40px;
  }

  .error-patterns { display: flex; flex-direction: column; gap: 0.55rem; margin-bottom: 1rem; }
  .error-pattern {
    background: #fff;
    border: 1px solid #D6DAE2;
    border-left: 4px solid;
    border-radius: 0 8px 8px 0;
    padding: 0.7rem 1rem;
    font-size: 0.84rem;
    line-height: 1.55;
    color: #4A4A4A;
  }
  .ep-and { border-left-color: #378ADD; }
  .ep-or  { border-left-color: #2A9D8F; }
  .ep-nor { border-left-color: #D9544D; }
  .ep-op-label {
    font-family: monospace;
    font-weight: 800;
    font-size: 0.88rem;
    margin-right: 0.45rem;
  }
  .ep-and .ep-op-label { color: #1B4F8A; }
  .ep-or  .ep-op-label { color: #1A6B5A; }
  .ep-nor .ep-op-label { color: #9D2B22; }
  .ep-name { font-weight: 700; color: #1B2A4A; margin-right: 0.3rem; }

  .analysis-conclusion {
    background: #1B2A4A;
    color: #fff;
    border-radius: 10px;
    padding: 0.9rem 1.2rem;
    font-size: 0.88rem;
    font-weight: 600;
    line-height: 1.55;
  }

  /* ── Takeaways ────────────────────────────────────────────────────── */
  .takeaway-cards {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(195px, 1fr));
    gap: 0.7rem;
    margin-bottom: 0.75rem;
  }
  .takeaway-card {
    border-radius: 12px;
    border: 1.5px solid;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    background: #fff;
  }
  .tc-blue  { border-color: #378ADD; }
  .tc-red   { border-color: #D9544D; }
  .tc-green { border-color: #3D7F2C; }
  .tc-header {
    display: flex;
    align-items: center;
    gap: 0.55rem;
    padding: 0.65rem 0.85rem;
    border-bottom: 2px solid;
  }
  .tc-blue  .tc-header { background: #EBF3FD; border-bottom-color: #378ADD; }
  .tc-red   .tc-header { background: #FCE9E6; border-bottom-color: #D9544D; }
  .tc-green .tc-header { background: #EAF5F0; border-bottom-color: #3D7F2C; }
  .tc-num-badge {
    width: 26px;
    height: 26px;
    border-radius: 50%;
    color: #fff;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 0.78rem;
    font-weight: 900;
    flex-shrink: 0;
  }
  .tc-blue  .tc-num-badge { background: #378ADD; }
  .tc-red   .tc-num-badge { background: #D9544D; }
  .tc-green .tc-num-badge { background: #3D7F2C; }
  .tc-header-title { font-size: 0.81rem; font-weight: 800; color: #1B2A4A; line-height: 1.2; }
  .tc-body {
    padding: 0.85rem;
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 0.5rem;
  }
  .tc-stat {
    font-family: Georgia, serif;
    font-size: 1.55rem;
    font-weight: 800;
    line-height: 1;
    text-align: center;
  }
  .tc-blue  .tc-stat { color: #378ADD; }
  .tc-red   .tc-stat { color: #D9544D; }
  .tc-green .tc-stat { color: #3D7F2C; }
  .tc-caption { font-size: 0.78rem; color: #4A4A4A; text-align: center; line-height: 1.4; }
  .tc-implication {
    font-size: 0.76rem;
    padding: 0.45rem 0.65rem;
    border-radius: 8px;
    border: 1.5px solid;
    text-align: center;
    line-height: 1.35;
    width: 100%;
    box-sizing: border-box;
    color: #1B2A4A;
  }
  .tc-blue  .tc-implication { background: #EBF3FD; border-color: #378ADD; }
  .tc-red   .tc-implication { background: #FCE9E6; border-color: #D9544D; }
  .tc-green .tc-implication { background: #EAF5F0; border-color: #3D7F2C; }

  .core-message {
    background: #1B2A4A;
    color: #fff;
    border-radius: 12px;
    padding: 1rem 1.4rem;
    font-size: 0.9rem;
    font-weight: 600;
    line-height: 1.6;
  }
  .core-message-title {
    font-family: Georgia, serif;
    font-size: 0.95rem;
    font-weight: 700;
    margin-bottom: 0.35rem;
    color: #fff;
  }

  /* ── Venue / Presentation ─────────────────────────────────────────── */
  .venue-row {
    display: flex;
    align-items: center;
    gap: 0.7rem;
    flex-wrap: wrap;
    margin-bottom: 0.75rem;
  }
  .venue-pill {
    display: inline-block;
    padding: 0.22rem 0.65rem;
    background: #1B2A4A;
    color: #fff;
    border-radius: 999px;
    font-size: 0.72rem;
    font-weight: 700;
    letter-spacing: 0.04em;
    text-transform: uppercase;
  }
  .venue-name { font-size: 0.88rem; color: #4A4A4A; }

  /* ── Citation ─────────────────────────────────────────────────────── */
  .citation-box {
    background: #1e293b;
    color: #e2e8f0;
    border-radius: 10px;
    padding: 1rem 1.3rem;
    font-family: monospace;
    font-size: 0.77rem;
    line-height: 1.75;
    overflow-x: auto;
    margin: 0.75rem 0 0.5rem;
  }

  /* ── PhD notice ───────────────────────────────────────────────────── */
  .phd-notice {
    display: flex;
    align-items: center;
    gap: 0.6rem;
    background: #F0F7FF;
    border: 1.5px solid #C2D9F0;
    border-radius: 10px;
    padding: 0.65rem 1rem;
    font-size: 0.84rem;
    color: #1B2A4A;
    margin-bottom: 1rem;
    line-height: 1.5;
  }
  .phd-notice-dot {
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background: #2A9D8F;
    flex-shrink: 0;
    box-shadow: 0 0 0 3px rgba(42,157,143,0.2);
  }
  .phd-notice a { color: #378ADD; text-decoration: none; font-weight: 600; }
  .phd-notice a:hover { text-decoration: underline; }
  html[data-theme="dark"] .phd-notice { background: rgba(55,138,221,0.08); border-color: rgba(55,138,221,0.25); color: #cbd5e1; }

  /* ── Responsive ───────────────────────────────────────────────────── */
  @media (max-width: 580px) {
    .results-notes { grid-template-columns: 1fr; }
    .stat-cards-grid { grid-template-columns: 1fr 1fr; }
    .takeaway-cards { grid-template-columns: 1fr; }
  }

  /* ── Dark Mode ────────────────────────────────────────────────────── */
  html[data-theme="dark"] .lcsqa { color: #cbd5e1; }

  /* Hero */
  html[data-theme="dark"] .lcsqa-hero { background: #1e293b; border-color: #334155; }
  html[data-theme="dark"] .hero-title  { color: #e2e8f0; }
  html[data-theme="dark"] .hero-subtitle { color: #cbd5e1; }
  html[data-theme="dark"] .hero-authors  { color: #94a3b8; }
  html[data-theme="dark"] .thesis-pill   { background: rgba(55,138,221,0.15); border-color: rgba(55,138,221,0.4); color: #93c5fd; }

  /* Badges */
  html[data-theme="dark"] .badge-acl { background: rgba(55,138,221,0.18); color: #93c5fd; border-color: rgba(55,138,221,0.4); }
  html[data-theme="dark"] .badge-nlp { background: rgba(42,157,143,0.15); color: #5eead4; border-color: rgba(42,157,143,0.4); }
  html[data-theme="dark"] .badge-cu  { background: rgba(100,130,180,0.15); color: #93c5fd; border-color: rgba(100,130,180,0.35); }

  /* Sections */
  html[data-theme="dark"] .sec-block { border-color: #334155; }
  html[data-theme="dark"] .sec-body  { background: #0f172a; }

  /* White-background cards */
  html[data-theme="dark"] .abstract-box,
  html[data-theme="dark"] .gap-card,
  html[data-theme="dark"] .logic-q,
  html[data-theme="dark"] .pipeline-step,
  html[data-theme="dark"] .dataset-stat,
  html[data-theme="dark"] .example-box,
  html[data-theme="dark"] .results-note,
  html[data-theme="dark"] .decomp-step,
  html[data-theme="dark"] .error-pattern { background: #1e293b; border-color: #334155; }

  /* Text in white cards */
  html[data-theme="dark"] .abstract-box   { color: #cbd5e1; }
  html[data-theme="dark"] .motivation-text { color: #cbd5e1; }
  html[data-theme="dark"] .logic-q         { color: #e2e8f0; }
  html[data-theme="dark"] .gap-card-title  { color: #e2e8f0; }
  html[data-theme="dark"] .gap-card-limit  { color: #cbd5e1; }
  html[data-theme="dark"] .gap-card-examples { color: #64748b; }
  html[data-theme="dark"] .step-title      { color: #e2e8f0; }
  html[data-theme="dark"] .step-desc       { color: #cbd5e1; }
  html[data-theme="dark"] .dataset-stat-num   { color: #e2e8f0; }
  html[data-theme="dark"] .dataset-stat-label { color: #64748b; }
  html[data-theme="dark"] .decomp-title    { color: #e2e8f0; }
  html[data-theme="dark"] .decomp-desc     { color: #cbd5e1; }
  html[data-theme="dark"] .ep-name         { color: #e2e8f0; }
  html[data-theme="dark"] .error-pattern   { color: #cbd5e1; }
  html[data-theme="dark"] .op-desc         { color: #cbd5e1; }
  html[data-theme="dark"] .ex-q            { color: #e2e8f0; }
  html[data-theme="dark"] .ex-correct      { color: #86efac; }
  html[data-theme="dark"] .stat-model      { color: #e2e8f0; }
  html[data-theme="dark"] .stat-caption    { color: #cbd5e1; }
  html[data-theme="dark"] .results-note    { color: #cbd5e1; }
  html[data-theme="dark"] .results-note-title { color: #e2e8f0; }
  html[data-theme="dark"] .analysis-intro  { color: #cbd5e1; }
  html[data-theme="dark"] .tc-header-title { color: #e2e8f0; }
  html[data-theme="dark"] .tc-caption      { color: #cbd5e1; }
  html[data-theme="dark"] .venue-name      { color: #94a3b8; }

  /* Operator cards */
  html[data-theme="dark"] .op-and { background: rgba(55,138,221,0.12); border-color: rgba(55,138,221,0.4); }
  html[data-theme="dark"] .op-or  { background: rgba(42,157,143,0.12); border-color: rgba(42,157,143,0.4); }
  html[data-theme="dark"] .op-nor { background: rgba(217,84,77,0.12);  border-color: rgba(217,84,77,0.4); }
  html[data-theme="dark"] .op-mix { background: rgba(138,111,183,0.12); border-color: rgba(138,111,183,0.4); }

  /* Stat cards */
  html[data-theme="dark"] .stat-card-red   { background: rgba(217,84,77,0.12); border-color: rgba(217,84,77,0.4); }
  html[data-theme="dark"] .stat-card-green { background: rgba(61,127,44,0.12); border-color: rgba(61,127,44,0.4); }

  /* Special boxes */
  html[data-theme="dark"] .gap-lcsqa-box    { background: rgba(55,138,221,0.10); border-color: rgba(55,138,221,0.35); color: #93c5fd; }
  html[data-theme="dark"] .csqa-comparison  { background: rgba(224,177,0,0.08); border-color: rgba(224,177,0,0.4); color: #cbd5e1; }
  html[data-theme="dark"] .csqa-comparison strong { color: #e2e8f0; }
  html[data-theme="dark"] .validation-badge { background: rgba(61,127,44,0.12); border-color: rgba(61,127,44,0.4); color: #86efac; }

  /* Takeaway cards */
  html[data-theme="dark"] .takeaway-card           { background: #1e293b; }
  html[data-theme="dark"] .tc-blue  .tc-header     { background: rgba(55,138,221,0.12); }
  html[data-theme="dark"] .tc-red   .tc-header     { background: rgba(217,84,77,0.12); }
  html[data-theme="dark"] .tc-green .tc-header     { background: rgba(61,127,44,0.12); }
  html[data-theme="dark"] .tc-blue  .tc-implication { background: rgba(55,138,221,0.12); color: #93c5fd; }
  html[data-theme="dark"] .tc-red   .tc-implication { background: rgba(217,84,77,0.12); color: #fca5a5; }
  html[data-theme="dark"] .tc-green .tc-implication { background: rgba(61,127,44,0.12); color: #86efac; }

  /* Eval table */
  html[data-theme="dark"] .eval-table td { color: #cbd5e1; border-bottom-color: #334155; }
  html[data-theme="dark"] .eval-table tr:nth-child(even) td { background: #1e293b; }
  html[data-theme="dark"] .eval-table tr:nth-child(odd)  td { background: #0f172a; }
</style>

<div class="lcsqa">

<!-- ══════════════════════════════════════════════════════ PHD NOTICE -->
<div class="phd-notice">
  <span class="phd-notice-dot"></span>
  Open to PhD research conversations in AI/NLP, reasoning, and trustworthy language systems for Spring/Fall 2027 — <a href="https://obedjunias.com/#contact">get in touch</a>.
</div>

<!-- ═══════════════════════════════════════════════════════════ HERO -->
<div class="lcsqa-hero">
  <div class="hero-accent"></div>
  <div class="hero-body">
    <h1 class="hero-title">LOGICAL-COMMONSENSEQA</h1>
    <p class="hero-subtitle">A Benchmark for Logical Commonsense Reasoning</p>
    <div class="thesis-pill">High CommonsenseQA accuracy does not imply logical commonsense reasoning.</div>
    <p class="hero-authors">
      <a href="https://obedjunias.com">Obed Junias</a><sup>1</sup>&ensp;·&ensp;
      <a href="https://blast-cu.github.io/">Maria Leonor Pacheco</a><sup>1</sup><br>
      <sup>1</sup>University of Colorado Boulder
    </p>
    <div class="badge-row">
      <span class="lcsqa-badge badge-acl">ACL 2026 Short Papers</span>
      <span class="lcsqa-badge badge-nlp">Commonsense Reasoning</span>
      <span class="lcsqa-badge badge-cu">BLAST Lab · CU Boulder</span>
    </div>
    <div class="link-buttons">
      <a class="link-btn btn-paper"   href="https://aclanthology.org/2026.acl-short.61/" target="_blank">&#x1F4C4; Paper</a>
      <a class="link-btn btn-arxiv"   href="https://aclanthology.org/2026.acl-short.61.pdf" target="_blank">&#x2B07; PDF</a>
      <a class="link-btn btn-slides"  href="/logical-csqa/slides/"             target="_blank">&#x1F5A5; Slides</a>
      <a class="link-btn btn-code"    href="https://github.com/obedjunias19/logical-csqa"              target="_blank">&#x2795; Code</a>
      <a class="link-btn btn-dataset" href="https://huggingface.co/datasets/ojayy/logical-csqa"        target="_blank">&#x1F4CA; Dataset</a>
    </div>
  </div>
</div>

<!-- ═══════════════════════════════════════════════════════ ABSTRACT -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Abstract</div>
  </div>
  <div class="sec-body">
    <div class="abstract-box">
      Commonsense reasoning often involves evaluating multiple plausible interpretations rather than selecting a single atomic answer, yet most benchmarks rely on single-label evaluation, obscuring whether statements are jointly plausible, mutually exclusive, or jointly implausible. We introduce <strong>LOGICAL-COMMONSENSEQA</strong>, a benchmark that reframes commonsense reasoning as <em>logical composition</em> over pairs of atomic statements using plausibility-level operators (<strong>AND</strong>, <strong>OR</strong>, and <strong>NEITHER/NOR</strong>). Evaluating instruction-tuned, reasoning-specialized, and fine-tuned models under zero-shot, few-shot, and chain-of-thought prompting, we find that while models perform reasonably on conjunctive and moderately on disjunctive reasoning, performance degrades sharply on negation-based questions. LOGICAL-COMMONSENSEQA exposes fundamental reasoning limitations and provides a controlled framework for advancing compositional commonsense reasoning.
    </div>
  </div>
</div>

<!-- ═════════════════════════════════════════════════════ MOTIVATION -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Motivation</div>
    <div class="sec-header-desc">From single-answer ranking to logical commonsense composition</div>
  </div>
  <div class="sec-body">
    <p class="motivation-text">
      When we say a model is good at commonsense reasoning, we usually mean it can pick a plausible answer from a set of choices. For example, asked what someone driving a car might have seen, the model picks "automobile accidents" — and we count that as correct.
    </p>
    <p class="motivation-text">
      But when humans reason through a question, we rarely stop at one answer. A situation can have multiple plausible interpretations. And when we evaluate those possibilities, we naturally ask:
    </p>
    <div class="logic-questions">
      <div class="logic-q"><div class="lq-dot" style="background:#378ADD;"></div>Can both of these be true at the same time?</div>
      <div class="logic-q"><div class="lq-dot" style="background:#2A9D8F;"></div>Can at least one of them be true?</div>
      <div class="logic-q"><div class="lq-dot" style="background:#D9544D;"></div>Can neither of them be true?</div>
    </div>
    <p class="motivation-text">
      That is the motivation behind this benchmark. We ask: can models <strong>compose commonsense plausibility</strong> using logical operators — AND, OR, and NEITHER/NOR? The task format stays multiple-choice, so any model that can take a standard QA benchmark can take this one.
    </p>
  </div>
</div>

<!-- ═══════════════════════════════════════════════════ RESEARCH GAP -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Research Gap</div>
    <div class="sec-header-desc">Existing benchmarks test parts of the problem, but not all three together</div>
  </div>
  <div class="sec-body">
    <div class="gap-cards">
      <div class="gap-card">
        <div class="gap-card-title">Commonsense QA</div>
        <div class="gap-card-examples">CommonsenseQA, SocialIQA, PIQA</div>
        <div class="gap-card-limit">Tests everyday plausibility but in a single-answer format. Ambiguity is erased, and logical relationships between answer choices are never evaluated.</div>
      </div>
      <div class="gap-card">
        <div class="gap-card-title">Ambiguity-Aware</div>
        <div class="gap-card-examples">AmbigQA, ProtoQA</div>
        <div class="gap-card-limit">Recognizes that questions can have multiple valid answers, but does not evaluate explicit logical composition over those alternatives.</div>
      </div>
      <div class="gap-card">
        <div class="gap-card-title">Logical Reasoning</div>
        <div class="gap-card-examples">LogiQA, ReClor, COM2</div>
        <div class="gap-card-limit">Tests structured inference with logical operators, but the focus is formal validity — not everyday commonsense plausibility.</div>
      </div>
    </div>
    <div class="gap-lcsqa-box">
      LOGICAL-COMMONSENSEQA sits at the intersection: commonsense plausibility + ambiguity + explicit logical composition.
    </div>
  </div>
</div>

<!-- ════════════════════════════════════════════ LOGICAL OPERATORS -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Logical Operators</div>
    <div class="sec-header-desc">Each answer option pairs two atomic statements under one of three plausibility-level operators</div>
  </div>
  <div class="sec-body">
    <div class="operator-grid">
      <div class="op-card op-and">
        <div class="op-label">AND</div>
        <div class="op-desc">Both statements are independently plausible given the question context</div>
      </div>
      <div class="op-card op-or">
        <div class="op-label">OR</div>
        <div class="op-desc">At least one statement is plausible — they are not mutually exclusive</div>
      </div>
      <div class="op-card op-nor">
        <div class="op-label">NEITHER/NOR</div>
        <div class="op-desc">Neither statement is plausible — both are jointly implausible</div>
      </div>
      <div class="op-card op-mix">
        <div class="op-label">MIXED</div>
        <div class="op-desc">Different operators across answer choices within the same question — prevents shortcut exploitation</div>
      </div>
    </div>

    <div class="example-box">
      <div class="ex-q">Q: Sammy wanted to go to where the people were. Where might he go?</div>
      <table class="ex-table">
        <tr>
          <td><span class="ex-op-and">AND</span></td>
          <td style="color:#4A4A4A;">local events <strong>AND</strong> social venues</td>
          <td><span class="ex-correct">&#x2714; both plausible</span></td>
        </tr>
        <tr>
          <td><span class="ex-op-or">OR</span></td>
          <td style="color:#4A4A4A;">local events <strong>OR</strong> empty parks</td>
          <td><span class="ex-correct">&#x2714; at least one plausible</span></td>
        </tr>
        <tr>
          <td><span class="ex-op-nor">NEITHER/NOR</span></td>
          <td style="color:#4A4A4A;">NEITHER quiet retreats <strong>NOR</strong> empty parks</td>
          <td><span class="ex-correct">&#x2714; neither is plausible</span></td>
        </tr>
      </table>
    </div>
  </div>
</div>

<!-- ════════════════════════════════════ BENCHMARK CONSTRUCTION -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Benchmark Construction</div>
    <div class="sec-header-desc">Neural generation with deterministic symbolic composition — no model in the composition loop</div>
  </div>
  <div class="sec-body">
    <div class="pipeline-steps">
      <div class="pipeline-step">
        <div class="step-num">1</div>
        <div>
          <div class="step-title">Candidate Generation</div>
          <div class="step-desc">Starting from 5,000 CommonsenseQA questions, GPT-4o-mini over-generates 4–6 plausible and 4–6 implausible atomic answer candidates per question, specifically prompted for multi-step causal and situational reasoning rather than shallow lexical cues.</div>
        </div>
      </div>
      <div class="pipeline-step">
        <div class="step-num">2</div>
        <div>
          <div class="step-title">Refinement and Pruning</div>
          <div class="step-desc">Options are filtered to remove trivial answers solvable by keyword matching. <em>Near-miss distractors</em> are deliberately preserved — options that satisfy most contextual constraints but fail on one subtle commonsense violation. Result: 3 correct and 4 incorrect atomic options per question.</div>
        </div>
      </div>
      <div class="pipeline-step">
        <div class="step-num">3</div>
        <div>
          <div class="step-title">Deterministic Symbolic Composition</div>
          <div class="step-desc">A symbolic program pairs refined atomic options and assigns operator labels (AND, OR, NEITHER/NOR). This step is fully deterministic — no language model is involved in composition or labeling. We also construct a MIXED setting where different operators appear across choices within the same question, yielding 4,999 additional instances.</div>
        </div>
      </div>
    </div>
    <div class="validation-badge">
      Human validation &nbsp;&#xB7;&nbsp; Gwet's AC2 = <strong>0.84</strong> (awareness) &nbsp;/&nbsp; <strong>0.91</strong> (consensus) &nbsp;&#xB7;&nbsp; 250 test questions, two independent annotators
    </div>
    <div class="dataset-stats">
      <div class="dataset-stat">
        <div class="dataset-stat-num">19,996</div>
        <div class="dataset-stat-label">Total instances</div>
      </div>
      <div class="dataset-stat">
        <div class="dataset-stat-num">4,999</div>
        <div class="dataset-stat-label">Per operator (AND / OR / NEITHER / MIXED)</div>
      </div>
      <div class="dataset-stat">
        <div class="dataset-stat-num">11,996 / 6K / 2K</div>
        <div class="dataset-stat-label">Train / Dev / Test</div>
      </div>
    </div>
  </div>
</div>

<!-- ════════════════════════════════════════ EVALUATION SETUP -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Evaluation Setup</div>
    <div class="sec-header-desc">Instruction-tuned, reasoning-specialized, and fine-tuned models across multiple prompting regimes</div>
  </div>
  <div class="sec-body">
    <table class="eval-table">
      <thead>
        <tr>
          <th style="width:130px;">Paradigm</th>
          <th>Models</th>
          <th style="width:200px;">Prompting</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td><strong>Prompted</strong></td>
          <td>LLaMA-3.1-8B, LLaMA-3.3-70B, Qwen2.5-7B, Gemini-2.5-Flash, Gemini-3-Flash-Preview</td>
          <td>Zero-shot, 1/2/3-shot, CoT</td>
        </tr>
        <tr>
          <td><strong>Fine-tuned</strong></td>
          <td>Flan-T5-base (seq2seq), DeBERTa-v3-base (encoder), LLaMA-3.1-8B (QLoRA)</td>
          <td>Supervised fine-tuning</td>
        </tr>
      </tbody>
    </table>
  </div>
</div>

<!-- ═══════════════════════════════════════════════════ KEY RESULTS -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Key Results</div>
    <div class="sec-header-desc">Models collapse on NEITHER/NOR — near or below random chance across model families and prompting strategies</div>
  </div>
  <div class="sec-body">
    <div class="stat-cards-grid">
      <div class="stat-card stat-card-red">
        <div class="stat-num">13.1%</div>
        <div class="stat-model">LLaMA-3.1-8B · 0-shot</div>
        <div class="stat-caption">NEITHER/NOR Macro-F1 — below random chance (25%)</div>
      </div>
      <div class="stat-card stat-card-red">
        <div class="stat-num">13.4%</div>
        <div class="stat-model">LLaMA-3.3-70B · 0-shot</div>
        <div class="stat-caption">9× more parameters, essentially no gain over the 8B model</div>
      </div>
      <div class="stat-card stat-card-red">
        <div class="stat-num">23.5%</div>
        <div class="stat-model">Gemini-2.5-Flash · 0-shot</div>
        <div class="stat-caption">Frontier proprietary model — still near random chance</div>
      </div>
      <div class="stat-card stat-card-green">
        <div class="stat-num">89.5%</div>
        <div class="stat-model">LLaMA-3.1-8B · fine-tuned</div>
        <div class="stat-caption">Supervision recovers the gap — the failure is learnable</div>
      </div>
    </div>

    <div class="csqa-comparison">
      <strong>The same model, 59 points lower.</strong> LLaMA-3.1-8B scores <strong>72.2%</strong> on CommonsenseQA. On LOGICAL-COMMONSENSEQA, the same model drops to <strong>13.1%</strong> on NEITHER/NOR — a 59-point fall on the same underlying commonsense knowledge. Single-answer benchmarks were giving us a flattering picture.
    </div>

    <div class="results-notes">
      <div class="results-note">
        <div class="results-note-title">Humans vs. Models</div>
        Human evaluation on NEITHER/NOR scores <strong>0.70</strong>, while zero-shot LLMs score ~0.13. The task is clearly solvable — the collapse is specific to models at inference time.
      </div>
      <div class="results-note">
        <div class="results-note-title">Few-shot prompting hurts</div>
        With 3 in-context examples, LLaMA-3.1-8B drops from 13.1% to ~6% on NEITHER/NOR. Chain-of-thought provides no rescue either, reaching only 8.2%.
      </div>
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════════ ANALYSIS -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Analysis</div>
    <div class="sec-header-desc">The failure is compositional, not atomic — models know the facts but cannot compose them under operators</div>
  </div>
  <div class="sec-body">
    <p class="analysis-intro">
      To pinpoint where failures arise, we decomposed the task into three components and evaluated each in isolation with LLaMA-3.1-8B. The results show that knowledge is largely present — the breakdown is in composition.
    </p>
    <div class="decomposition-cascade">
      <div class="decomp-step ds-blue">
        <div class="decomp-num">79%</div>
        <div>
          <div class="decomp-title">Atomic Plausibility</div>
          <div class="decomp-desc">Classifying individual statements as plausible or implausible, in isolation. The commonsense knowledge is largely intact.</div>
        </div>
      </div>
      <div class="cascade-arrow">&#x2193;</div>
      <div class="decomp-step ds-purple">
        <div class="decomp-num">52–69%</div>
        <div>
          <div class="decomp-title">Operator Verification</div>
          <div class="decomp-desc">Given gold plausibility labels, does the model determine whether they satisfy the target operator? Even with correct atomic facts, applying the logical relation is already imperfect.</div>
        </div>
      </div>
      <div class="cascade-arrow">&#x2193;</div>
      <div class="decomp-step ds-red">
        <div class="decomp-num">46.8%</div>
        <div>
          <div class="decomp-title">NEITHER/NOR + Distractors</div>
          <div class="decomp-desc">Full task with competing composite answer options. Distractor competition causes the sharpest additional drop. The difficulty arises from the interaction of all three components, not any one alone.</div>
        </div>
      </div>
    </div>

    <p style="font-family:Georgia,serif;font-weight:700;color:#1B2A4A;font-size:0.9rem;margin:0.9rem 0 0.5rem;">Error Patterns</p>
    <div class="error-patterns">
      <div class="error-pattern ep-and">
        <span class="ep-op-label">AND</span><span class="ep-name">Single-statement dominance —</span>
        The model anchors on one plausible clause and treats the full option as correct, ignoring whether the second clause is also plausible.
      </div>
      <div class="error-pattern ep-or">
        <span class="ep-op-label">OR</span><span class="ep-name">Thematic similarity —</span>
        Rather than verifying that at least one clause is plausible, the model selects options whose two clauses are thematically related but individually implausible.
      </div>
      <div class="error-pattern ep-nor">
        <span class="ep-op-label">NEITHER/NOR</span><span class="ep-name">Negation inversion and plausibility dominance —</span>
        The model selects the most plausible pair of statements despite the operator requiring both to be implausible. Highly plausible content survives even when it should be rejected.
      </div>
    </div>

    <div class="analysis-conclusion">
      LCSQA separates knowing commonsense facts from composing them under logical constraints. Models are not simply missing knowledge — they fail when negation, operator scope, and distractor competition interact simultaneously.
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════════ TAKEAWAYS -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Takeaways</div>
    <div class="sec-header-desc">High CommonsenseQA accuracy does not imply logical commonsense reasoning</div>
  </div>
  <div class="sec-body">
    <div class="takeaway-cards">
      <div class="takeaway-card tc-blue">
        <div class="tc-header">
          <div class="tc-num-badge">1</div>
          <div class="tc-header-title">Benchmarks can overestimate reasoning</div>
        </div>
        <div class="tc-body">
          <div class="tc-stat">72.2% → 13.1%</div>
          <div class="tc-caption">Same model, same commonsense knowledge — different question format.</div>
          <div class="tc-implication"><strong>Implication:</strong> Single-answer accuracy tells a flattering story about model reasoning ability.</div>
        </div>
      </div>
      <div class="takeaway-card tc-red">
        <div class="tc-header">
          <div class="tc-num-badge">2</div>
          <div class="tc-header-title">Negation reveals hidden failure</div>
        </div>
        <div class="tc-body">
          <div class="tc-stat">13–23%</div>
          <div class="tc-caption">All zero-shot models land near or below random chance (25%) on NEITHER/NOR.</div>
          <div class="tc-implication"><strong>Implication:</strong> Scaling from 8B to 70B parameters does not fix the problem.</div>
        </div>
      </div>
      <div class="takeaway-card tc-green">
        <div class="tc-header">
          <div class="tc-num-badge">3</div>
          <div class="tc-header-title">The gap is learnable</div>
        </div>
        <div class="tc-body">
          <div class="tc-stat">89.5%</div>
          <div class="tc-caption">NEITHER/NOR Macro-F1 after fine-tuning LLaMA-3.1-8B with QLoRA.</div>
          <div class="tc-implication"><strong>Implication:</strong> The failure is an inference-time limitation, not a dataset artifact.</div>
        </div>
      </div>
    </div>
    <div class="core-message">
      <div class="core-message-title">Core message</div>
      Logical commonsense reasoning requires more than selecting a plausible answer. It requires composing plausibility under explicit operators and resisting distractors that are individually plausible but logically incorrect.
    </div>
  </div>
</div>

<!-- ══════════════════════════════════════════════ PRESENTATION -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Presentation</div>
  </div>
  <div class="sec-body">
    <div class="venue-row">
      <span class="venue-pill">ACL 2026</span>
      <span class="venue-name"><strong>64th Annual Meeting of the Association for Computational Linguistics (Volume 2: Short Papers)</strong></span>
    </div>
    <p style="font-size:0.88rem;color:#4A4A4A;margin-bottom:0.5rem;line-height:1.6;">
      San Diego, California, United States &nbsp;·&nbsp; <strong>Poster: July 6, 2026</strong>. If you are attending ACL and would like to discuss the paper, feel free to <a href="https://obedjunias.com/#contact" style="color:#378ADD;">reach out</a>.
    </p>
    <p style="font-size:0.88rem;color:#4A4A4A;margin:0;">
      <a href="/logical-csqa/slides/" target="_blank" style="color:#378ADD;font-weight:700;">View the conference slides &#x2192;</a>
    </p>
  </div>
</div>

<!-- ════════════════════════════════════════════════════ CITATION -->
<div class="sec-block">
  <div class="sec-header">
    <div class="sec-header-title">Citation</div>
  </div>
  <div class="sec-body">
    <div class="citation-box">
@inproceedings{junias-pacheco-2026-logical,<br>
&nbsp;&nbsp;title&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = &#x7B;&#x7B;LOGICAL&#x7D;-&#x7B;COMMONSENSEQA&#x7D;: A Benchmark for Logical Commonsense Reasoning&#x7D;,<br>
&nbsp;&nbsp;author&nbsp;&nbsp;&nbsp;&nbsp; = "Junias, Obed and Pacheco, Maria Leonor",<br>
&nbsp;&nbsp;booktitle = "Proceedings of the 64th Annual Meeting of the &#x7B;A&#x7D;ssociation for &#x7B;C&#x7D;omputational &#x7B;L&#x7D;inguistics (Volume 2: Short Papers)",<br>
&nbsp;&nbsp;month&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = jul,<br>
&nbsp;&nbsp;year&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = "2026",<br>
&nbsp;&nbsp;address&nbsp;&nbsp;&nbsp; = "San Diego, California, United States",<br>
&nbsp;&nbsp;publisher = "Association for Computational Linguistics",<br>
&nbsp;&nbsp;url&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = "https://aclanthology.org/2026.acl-short.61/",<br>
&nbsp;&nbsp;pages&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = "746--758",<br>
&nbsp;&nbsp;ISBN&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; = "979-8-89176-391-3"<br>
}
    </div>
    <p style="font-size:0.8rem;color:#6B7280;margin:0;line-height:1.5;">
      <em>This research is conducted at the <a href="https://blast-cu.github.io/" style="color:#378ADD;">BLAST Lab</a> at the University of Colorado Boulder under the supervision of Dr. Maria Leonor Pacheco.</em>
    </p>
  </div>
</div>

</div><!-- /.lcsqa -->
