---
layout: post
title: "Conditional Probability, Priors, Likelihood, and Bayes' Rule: The Foundations"
date: 2026-04-26 10:00:00-0400
description: A deep dive into conditional probability, priors, likelihood, and Bayesian updating.
tags: machine-learning probability math-for-ml
categories: machine-learning
giscus_comments: true
related_posts: false
toc:
  beginning: true
---

<style>
.tooltip-term {
  position: relative;
  color: #2698ba;
  border-bottom: 1px dotted #2698ba;
  cursor: help;
  font-weight: 500;
}

.tooltip-term .tooltip-text {
  visibility: hidden;
  width: 300px;
  background-color: #555;
  color: #fff;
  text-align: left;
  border-radius: 6px;
  padding: 10px;
  position: absolute;
  z-index: 1;
  bottom: 125%;
  left: 50%;
  margin-left: -150px;
  opacity: 0;
  transition: opacity 0.3s;
  font-size: 0.9rem;
  font-weight: normal;
  line-height: 1.4;
  box-shadow: 0 2px 8px rgba(0,0,0,0.2);
}

.tooltip-term .tooltip-text::after {
  content: "";
  position: absolute;
  top: 100%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
}

.tooltip-term:hover .tooltip-text {
  visibility: visible;
  opacity: 1;
}

@media (max-width: 768px) {
  .tooltip-term .tooltip-text {
    width: 250px;
    margin-left: -125px;
  }
}
details summary {
  list-style: none;
}
details summary::-webkit-details-marker {
  display: none;
}
details summary h2::after {
  content: ' ▼';
  display: inline-block;
  margin-left: 8px;
  font-size: 0.7em;
  transition: transform 0.2s ease-in-out;
  transform: rotate(-90deg);
}
details[open] summary h2::after {
  transform: rotate(0deg);
}
</style>

The formula for conditional probability is mathematically straightforward:

$$
P(E \mid F)=\frac{P(E\cap F)}{P(F)}
$$

While the formula is simple, the intuition behind the denominator is often counterintuitive. If event $$F$$ has already occurred, treating $$F$$ as the entirely new sample space can feel mathematically abrupt. The outcomes outside $$F$$ still exist in the original sample space $$S$$; they have not disappeared. The shift here is not about altering the physical reality of the sample space, but about restricting the scope of possibility based on new information.

Conditional probability represents a fundamental change in perspective. Conditioning does not change reality; it changes what is possible given the current information. The original sample space still exists, but once $$F$$ occurs, outcomes outside $$F$$ are no longer compatible with the available information. $$F$$ becomes the relevant world. Our uncertainty has been restricted.

---

## A Concrete Dice Example

Suppose we roll a fair six-sided die. The original sample space is:

$$
S=\{1,2,3,4,5,6\}
$$

Now define two events. Let's say $$E$$ is the event that the number is greater than 3, and $$F$$ is the event that the number is even:

$$
E=\{4,5,6\}
$$

$$
F=\{2,4,6\}
$$

Before we know anything else, the probability that the number is greater than 3 is exactly half, because three out of the six possible outcomes satisfy the condition:

$$
P(E)=\frac{3}{6}=\frac{1}{2}
$$

So far, nothing is conditional. We are living in the full sample space. But now, suppose someone tells us that the number is even. That means event $$F$$ has happened. Now the possible outcomes are no longer all six outcomes; they are restricted to just the even numbers:

$$
F=\{2,4,6\}
$$

This is a common point of confusion. Outcomes 1, 3, and 5 still exist in the original sample space, but they are incompatible with the information we just received. If we know the number is even, then rolling a 1, 3, or 5 is impossible given the new information. So when we ask for the conditional probability $$P(E \mid F)$$, we are not asking how many of all six die outcomes are greater than 3. Instead, we are asking: out of the outcomes that are even, how many are greater than 3? 

Inside $$F$$, our possible outcomes are restricted to $$\{2,4,6\}$$. Among those, the outcomes greater than 3 are $$\{4,6\}$$. Therefore, our updated probability is:

$$
P(E\mid F)=\frac{2}{3}
$$

The denominator changed because the relevant world changed. Before the evidence, the relevant world was $$S$$. After the evidence, the relevant world is $$F$$.

---

## Conditioning as a Filter

A useful mental model is to view conditional probability as probability after information has filtered the world. 

Before the information, our world was $$S=\{1,2,3,4,5,6\}$$. After the information "the number is even", our world is filtered down to $$F=\{2,4,6\}$$. The event $$F$$ acts like a filter, and everything incompatible with $$F$$ gets removed from consideration. Again, this does not mean the removed outcomes never existed; it just means they are no longer possible under the new condition.

This distinction matters heavily. The original sample space is the full set of possible outcomes before extra information, whereas the conditioned sample space is the set of possible outcomes after the information is known. When we condition on $$F$$, we are simply saying: assume $$F$$ happened, and now reason exclusively inside that assumption. That is exactly why $$F$$ becomes the new reference set.

---

## Prior: Belief Before Evidence

The next major concepts are the prior, update, posterior, and likelihood. These terms are precise names for different parts of belief revision.

A **prior** is simply what we believe before seeing the new information. In our die example, before being told the number is even, the probability that the number is greater than 3 is:

$$
P(E)=\frac{1}{2}
$$

This is the prior probability of $$E$$. It is what we believed before the evidence arrived. Prior does not mean a "random guess." Instead, it represents the belief state before this new piece of information is incorporated. In this specific example, the prior is straightforward because the die is fair and all six outcomes are equally likely, leaving us with an exact 50–50 split.

---

## Evidence: The Thing That Changes the Question

The **evidence** is the new information we receive. In our example, the evidence is the revelation that the number is even ($$F$$). Once we hear this, the question fundamentally changes. We are no longer asking how likely $$E$$ is in the full sample space; we are asking how likely $$E$$ is among the worlds where $$F$$ is true. 

That shift is the core of conditioning. The evidence does not directly tell us whether $$E$$ happened—it doesn't explicitly say "the number is greater than 3." It only says "the number is even." But that information still drastically changes how plausible $$E$$ is. Before hearing "even," $$E$$ had a probability of $$1/2$$. After hearing "even," $$E$$ has a probability of $$2/3$$. 

Evidence can completely change the probability of another event even if it does not directly state that event.

---

## Posterior: Belief After Evidence

The **posterior** is our final belief after incorporating the evidence. So in our example, our posterior probability of $$E$$ after learning $$F$$ is:

$$
P(E\mid F)=\frac{2}{3}
$$

We moved from a prior of $$1/2$$ to a posterior of $$2/3$$. That is the prior-to-posterior movement. The event itself did not change, the die roll did not change, and reality did not change. What changed was our information. Therefore, posterior simply means the probability after updating on the evidence. It is just our newly updated belief given what we currently know.

## Update: The Movement from Prior to Posterior

The term "update" should not be confused with the likelihood. The update is not a single probability term; it is the entire revision process of changing from the prior to the posterior.

In our die example, we started with a prior probability of $$P(E)=\frac{1}{2}$$. We then received the evidence that $$F$$ (the number being even) had occurred. Our posterior belief became $$P(E\mid F)=\frac{2}{3}$$. The update is simply the movement from $$\frac{1}{2}$$ to $$\frac{2}{3}$$ caused by the arrival of the new evidence. This distinction matters because the likelihood is only one ingredient used in a Bayesian update, not the update itself.

---

## Evidence Accumulates Over Time

When dealing with multiple pieces of evidence, it is important to understand how they interact. Suppose a model starts with a 50–50 belief. It sees one negative example, so the belief moves toward the negative hypothesis. Then, it sees one positive example. Why does it not just revert to the original 50–50 belief? 

The answer is that evidence accumulates. A new piece of evidence does not erase the old evidence. If we see one negative example and then one positive example, our belief should reflect both observations together, not only the most recent one. 

This is the core idea behind sequential updating. After the first data point $$D_1$$, our belief becomes our posterior:

$$
P(H\mid D_1)
$$

After observing the second data point $$D_2$$, we do not go back to the original prior and compute $$P(H\mid D_2)$$ in isolation. Instead, we compute the joint posterior:

$$
P(H\mid D_1,D_2)
$$

The old posterior becomes the new prior. Learning is an accumulation of knowledge, not a replacement. If every new observation reset the process, stable learning would be impossible.

---

## Understanding Likelihood

While prior (*belief before evidence*) and posterior (*belief after evidence*) are relatively straightforward, likelihood can be harder to grasp.

The phrase people often use is that likelihood is $$P(\text{data}\mid \text{hypothesis})$$. While technically correct, it can feel empty until the direction of the equation really clicks. Likelihood asks: *if this hypothesis were true, how expected would this evidence be?* 

That is the entire idea. It is not asking how likely the hypothesis is—that would be the posterior. Likelihood keeps the hypothesis fixed and asks whether the observed data fits it. So likelihood is represented by:

$$
P(D\mid H)
$$

Whereas the posterior is represented by:

$$
P(H\mid D)
$$

These are not the same thing, and the direction absolutely matters.

---

## A Coin Example for Likelihood

Suppose we have two hypotheses about a coin. The first hypothesis ($$H_1$$) is that the coin is fair, and the second hypothesis ($$H_2$$) is that the coin is biased toward heads:

$$
H_1=\text{the coin is fair}
$$

$$
H_2=\text{the coin is biased toward heads}
$$

Before flipping, suppose we find both hypotheses equally plausible, giving us equal priors:

$$
P(H_1)=0.5
$$

$$
P(H_2)=0.5
$$

Now we flip the coin once and observe heads. The likelihood under the fair-coin hypothesis is simply $$P(\text{heads}\mid H_1)=0.5$$. However, the likelihood under the biased-coin hypothesis might be much higher, perhaps:

$$
P(\text{heads}\mid H_2)=0.9
$$

This does not mean that $$P(H_2\mid \text{heads})=0.9$$. That would be a completely different statement (the posterior). The likelihood only tells us that if the coin were indeed biased toward heads, then seeing a heads would be very expected. Therefore, the evidence fits $$H_2$$ much better than it fits $$H_1$$. 

To find out which hypothesis is actually more probable (the posterior), we still need to mathematically combine this likelihood with our prior. That is exactly why likelihood is not our final belief in the hypothesis; likelihood is just a measure of how well the hypothesis explains the evidence.

---

## Likelihood in the Dice Example

Let's return to the die to solidify this. We define our hypothesis $$H$$ as the event that the number is greater than 3, and our evidence $$F$$ as the event that the number is even:

$$
H=\{4,5,6\}
$$

$$
F=\{2,4,6\}
$$

The likelihood is represented by $$P(F\mid H)$$. In plain English, we are asking: *if the number were greater than 3, how likely would it be even?*

Inside our hypothesis $$H$$, the possible outcomes are $$\{4,5,6\}$$. Out of those three outcomes, the even ones are $$\{4,6\}$$. Therefore, our likelihood is:

$$
P(F\mid H)=\frac{2}{3}
$$

This is the likelihood. On the other hand, the posterior is $$P(H\mid F)$$. In words, the posterior asks: *given that the number is even, how likely is it that the number is greater than 3?*

This numerical coincidence can sometimes obscure the conceptual difference. The likelihood $$P(F\mid H)$$ and the posterior $$P(H\mid F)$$ measure probability in completely opposite directions. Relying purely on simple examples with symmetric probabilities can accidentally hide these important distinctions.

---

## Defining Likelihood Properly

A common misinterpretation of likelihood is phrasing it as: *given this hypothesis, how good is this data for it to be true?* This phrasing is misleading.

The correct formulation is: *given this hypothesis, how expected is the observed data?* Alternatively, *if this hypothesis were true, how well would it explain the data?*

This distinction is crucial. The phrasing "how good is this data for the hypothesis to be true?" subtly implies an evaluation of whether the data *makes* the hypothesis true. That is posterior thinking. 

Likelihood simply evaluates whether the data is surprising under the assumption that the hypothesis is true. High likelihood means the data is expected under the hypothesis, while low likelihood means the data is highly surprising.

## The Cricket Example That Puts It All Together

Let’s tie all of these concepts together with a concrete example: a cricket match.

Suppose today’s match is between Royal Challengers Bengaluru (RCB) and Delhi Capitals (DC). In the first innings, Delhi Capitals collapses and gets bowled out for a mere 75 runs. 

When asking, "What is the probability that RCB wins?", the natural process of answering aligns with Bayesian updating.

### Before the Innings: The Prior

Before the match begins, there is an initial expectation based on historical data. Taking into account factors like overall team strength, pitch conditions, recent player form, and the venue, RCB might be considered the slight favorite. 

This initial belief is the prior. Mathematically, it looks like this:

$$
P(\text{RCB wins})=0.55
$$

$$
P(\text{DC wins})=0.45
$$

This prior establishes that before seeing a single ball bowled, RCB is expected to win 55% of the time.

---

### New Evidence Arrives

As the game progresses, new information arrives. In this case, the evidence is extreme:

$$
D = \text{DC scored only 75}
$$

To update the beliefs, the compatibility of this evidence with each possible hypothesis must be evaluated.

---

**Hypothesis 1: RCB Wins**

Assume the first hypothesis is true:

$$
H_1 = \text{RCB wins}
$$

Evaluate the likelihood of seeing the evidence under this assumption:

$$
P(D \mid H_1)
$$

This evaluates: *If it was certain that RCB was going to win the match, how expected is it that DC would only score 75 runs?*

It is highly expected. A team being bowled out for 75 usually results in a loss, making this evidence very compatible with an RCB victory. This yields a high likelihood, perhaps:

$$
P(D \mid H_1)=0.8
$$

---

**Hypothesis 2: DC Wins**

Now assume the alternative hypothesis is true:

$$
H_2 = \text{DC wins}
$$

Evaluate the likelihood of the evidence under this new assumption:

$$
P(D \mid H_2)
$$

This evaluates: *If it was certain that DC was going to win the match, how expected is it that they would only score 75 runs?*

It is highly unlikely for a team to win a T20 match after scoring only 75 runs. Because this scenario is so rare, the evidence has a very low likelihood under this hypothesis. Perhaps:

$$
P(D \mid H_2)=0.1
$$

---

### The Update and The Posterior

The initial beliefs are now combined with the new evidence. The posterior probability represents the updated belief after factoring in the innings:

$$
P(\text{RCB wins} \mid \text{DC}=75)
$$

Because the evidence (DC scoring 75) is overwhelmingly more likely under the hypothesis that RCB wins, confidence in an RCB victory skyrockets. The posterior probability might jump to:

$$
P(\text{RCB wins} \mid \text{DC}=75) = 0.95
$$

---

### Summarizing the Shift

The updating process follows four steps:

1. **Prior:** Before the innings, RCB was a slight favorite based on historical factors.
2. **Evidence:** DC suffered a massive batting collapse, scoring only 75 runs.
3. **Likelihood:** The probability of that collapse occurring was evaluated under each possible winner, showing it strongly supported the hypothesis of an RCB victory.
4. **Posterior:** After combining the prior with the likelihood of the evidence, RCB became the overwhelming favorite.

The prior is the belief *before* the innings, the evidence is the *75 all out*, the likelihood measures *how expected* that 75 is under each possible winner, and the posterior is the final updated belief *after* the innings.

---

### Alternative Scenario

Suppose the match went differently. Suppose DC batted first and scored a massive 240 runs. 

The prior remains the exact same (RCB 55%, DC 45%). However, the new evidence is entirely different. The likelihood of a team scoring 240 runs must be evaluated:

$$
P(240 \mid \text{DC wins})
$$

This likelihood is extremely high. If DC wins the match, it is very expected that they batted incredibly well. Conversely:

$$
P(240 \mid \text{RCB wins})
$$

This likelihood is much lower. If RCB were to win, it is highly unusual that they would allow the opposition to score 240 runs first. Because the evidence strongly favors the DC-winning hypothesis, the posterior probability drastically shifts toward DC.

The exact same framework and updating process is used, but different evidence leads to a different conclusion. This demonstrates Bayesian reasoning: start with initial beliefs, observe data, and reweight beliefs based on how well the hypotheses explain the data.

---

## Bayes’ Rule

These pieces assemble formally into Bayes' rule:

$$
P(H\mid D)=\frac{P(D\mid H)P(H)}{P(D)}
$$

Each component of Bayes' rule plays a distinct role. Multiply the **prior** ($$P(H)$$) by the **likelihood** ($$P(D \mid H)$$), which evaluates how well the hypothesis explains the evidence. This results in the updated **posterior** ($$P(H \mid D)$$), after dividing by the **normalizer** ($$P(D)$$) to ensure the probabilities sum to 1.

The simplified structure of this equation is:

$$
\text{posterior} \propto \text{likelihood} \times \text{prior}
$$

This provides the cleanest framework: start with prior beliefs, reweight each hypothesis by how well it explains the new evidence, and normalize. The result is the posterior.

The likelihood does not replace the prior; it modifies it. A hypothesis with a strong prior but a weak likelihood may lose probability overall. Conversely, a hypothesis with a weak prior but a very strong likelihood may gain probability. The posterior is the logical balance of both forces.

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

**Overthinking: “Why does $$F$$ become the new sample space?”**  
Because we are now assuming $$F$$ happened. Outcomes outside $$F$$ are incompatible with the information we currently have. They still exist in the original sample space, but they do not exist in the conditioned world.

**Overthinking: “Did the probability change because reality changed?”**  
Reality did not change; our information changed. Conditional probability is purely about updating uncertainty, not about altering the past or changing reality.

**Overthinking: “Is posterior the true answer?”**  
Not necessarily. The posterior is simply the updated belief given the current evidence and the model. If the evidence is incomplete or if the starting model is flawed, the posterior can still be incorrect.

**Overthinking: “Is likelihood the same as posterior?”**  
Likelihood is $$P(D\mid H)$$, while posterior is $$P(H\mid D)$$. They use the same symbols but in the opposite direction, and they have completely different mathematical meanings.

</details>

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Common Misconceptions</h2></summary>

**Misconception 1: “Conditioning deletes the rest of the sample space.”**  
The rest of the sample space still physically exists. Conditioning only establishes that, given the new information, those alternative outcomes are no longer possible for the specific question being asked.

**Misconception 2: “Prior means random guess.”**  
Prior means the state of belief before the current evidence. Sometimes it is uniform because there is no reason to prefer one hypothesis over another, but priors can also encode very strong previous knowledge.

**Misconception 3: “Likelihood tells us how likely the hypothesis is.”**  
Likelihood evaluates how likely the evidence is under the assumption of the hypothesis. It is the posterior that evaluates how likely the hypothesis is after seeing the evidence.

**Misconception 4: “Update equals likelihood.”**  
The update uses the likelihood, but it is not the likelihood itself. The update is the full mathematical movement from the prior to the posterior.

</details>

---

## The Cleanest Mental Model

These core definitions form the foundation of the framework:

* **Conditional probability:** Reasoning exclusively inside the world where the condition is true.
* **Prior:** The belief state before receiving the new evidence.
* **Likelihood:** If a given hypothesis were true, how expected would this new evidence be?
* **Update:** The process of reweighting beliefs based on how well each hypothesis explains the evidence.
* **Posterior:** The final belief state after incorporating the new evidence.

---

## One-Sentence Takeaway

Conditional probability and Bayesian updating form the fundamental language of changing uncertainty when new information rules out or reweights possible worlds.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.