---
layout: about
title: about
permalink: /
# subtitle: <a href='#'>Affiliations</a>. Address. Contacts. Motto. Etc.

profile:
  align: right
  image: obed_junias2.jpg
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
    margin-left: 5 px;
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
I'm a second-year Master's student at the [University of Colorado Boulder](https://www.colorado.edu/cs/) advised by Professor [Maria L. Pacheco](https://blast-cu.github.io/mlpacheco/) in the [BLAST Lab](https://blast-cu.github.io/). I'm broadly interested in Natural Language Processing, with a focus on interpretable AI and structured reasoning systems. My current research involves developing interpretable and explainable AI systems using entailment trees to make machine reasoning more transparent and understandable.

In parallel, I'm working under Professor [Theodora Chaspari](https://www.colorado.edu/cs/theodora-chaspari) on detecting and mitigating bias and fairness issues in Large Language Models within the mental health domain. This work reflects my broader interest in responsible AI and my commitment to building systems that are equitable and beneficial across diverse populations.

## Research Interests

- **Natural Language Understanding and Reasoning:** Natural Language Understanding (NLU) and Reasoning (NLR), Agentic and Neuro-Symbolic reasoning systems  
- **Interpretability and Responsible AI:** Interpretable and explainable NLP models, Responsible and ethical development of AI systems  
- **Interdisciplinary Applications of NLP:** NLP for mental health and AI for social good


**I’m actively seeking opportunities in NLP and related areas.**  
Feel free to reach out for research collaborations or other opportunities.

  </div>
</div>
