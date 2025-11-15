---
layout: about
title: about
permalink: /
# subtitle: <a href='#'>Affiliations</a>. Address. Contacts. Motto. Etc.

profile:
  align: right
  image: obed_junias_pfp.jpg
  image_circular: false

# selected_papers: true
social: true

announcements:
  enabled: true
  scrollable: true
  limit: 5

# latest_posts:
#   enabled: true
#   scrollable: true
#   limit: 3
---

<style>
.about-content {
  display: flex;
  flex-wrap: wrap;
  align-items: flex-start;
}

.about-text {
  flex: 1 1 100%;
  text-align: justify;
  order: 2;
}

.profile {
  flex: 0 0 200px;
  order: 1;
  margin-bottom: 20px;
}

/* Desktop view: add spacing between image and text */
@media (min-width: 769px) {
  .profile {
    margin-left: 5px;
  }
}

/* Mobile view: stack vertically and remove margins */
@media (max-width: 768px) {
  .about-content {
    flex-direction: column;
  }

  .profile {
    order: 0;
    align-self: center;
    float: none !important;
    margin-left: 0;
  }

  .about-text {
    order: 1;
  }
}

/* Resize and evenly space social icons */
.author__urls-wrapper {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 15px;
  margin-top: 10px;
}

.author__urls-wrapper li {
  list-style: none;
}

.author__urls-wrapper svg {
  width: 40px;
  height: 40px;
}

</style>

<div class="about-content">
  <div class="about-text" markdown="1">
I'm a second-year Master's student in Computer Science at the [University of Colorado Boulder](https://www.colorado.edu/cs/), advised by [Dr. Maria L. Pacheco](https://blast-cu.github.io/mlpacheco/) in the [BLAST Lab](https://blast-cu.github.io/). My work sits at the intersection of interpretable reasoning and responsible AI.

My current research focuses on developing **interpretable reasoning systems and benchmarks** for **commonsense and logical inference** in natural language processing. I am exploring **entailment tree-based frameworks** as a way to make machine reasoning more transparent, structured, and logically grounded. In parallel, I work with [Dr. Theodora Chaspari](https://www.colorado.edu/cs/theodora-chaspari) on **bias detection and fairness evaluation** in LLMs, particularly within the **mental health domain**—work that reflects my broader commitment to building AI systems that remain trustworthy and equitable across diverse populations.

**Looking ahead**, I am interested in exploring how **structured reasoning** and **social or moral alignment** can be incorporated into **foundation model pretraining**, and how models internalize, perceive, and compare these signals during **inference and generation**. I also aim to investigate **reflective post-training frameworks**, including **reinforcement learning (RL)-based approaches**, that encourage models to reflect, revise, and align with human values.

From a **systems perspective**, I am interested in how these mechanisms can be implemented and evaluated at scale in **open, transparent, and sustainable model ecosystems**.

## Research Interests

- **Natural Language Processing, Understanding, and Reasoning:** Commonsense reasoning, neuro-symbolic methods for interpretable NLP  
- **Responsible and Interpretable AI for Social Good:** Fairness and bias mitigation, social and moral alignment in LLMs, ethical and equitable development of AI 
- **Agentic and Reflective Systems:** Self-reflective and introspective agents, multi-agent collaboration
- **MLSys and Reinforcement Learning:** Open, transparent, and sustainable model ecosystems, reasoning-aware pretraining, reflective post-training, and reinforcement learning for alignment

**I’m actively seeking opportunities in NLP and related areas.**  
Feel free to reach out for research collaborations or other opportunities.

  </div>
</div>
