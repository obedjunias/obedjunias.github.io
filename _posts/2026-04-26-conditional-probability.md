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

When I started learning conditional probability, the formula itself did not look that bad:

$$
P(E \mid F)=\frac{P(E\cap F)}{P(F)}
$$

But the intuition behind it bothered me.

The part that felt strange was this:

> If event $$F$$ has already happened, why do we suddenly enter $$F$$ and treat it like the new sample space?

Because there are still outcomes outside $$F$$, right?

They are still inside the original sample space $$S$$. They did not magically disappear. So why are we allowed to ignore them?

This was the first place where conditional probability stopped feeling like a formula and started feeling like a change in perspective.

The key idea is this:

> Conditioning does not change reality. It changes what is still possible given what we now know.

That sentence is the backbone of this whole topic.

The original sample space still exists. But once we are told that $$F$$ happened, outcomes outside $$F$$ are no longer compatible with our information. So for the question we are asking now, $$F$$ becomes the relevant world.

Not because the rest of $$S$$ vanished.

But because our uncertainty has been restricted.

---

## The Dice Example That Makes the Whole Thing Concrete

Suppose we roll a fair six-sided die.

The sample space is:

$$
S={1,2,3,4,5,6}
$$

Now define two events:

$$
E = \text{the number is greater than 3}
$$

So:

$$
E={4,5,6}
$$

And:

$$
F = \text{the number is even}
$$

So:

$$
F={2,4,6}
$$

Before we know anything else, the probability that the number is greater than 3 is:

$$
P(E)=\frac{3}{6}=\frac{1}{2}
$$

That is because, out of all six possible die outcomes, three are greater than 3.

So far, nothing is conditional.

We are living in the full sample space:

$$
S={1,2,3,4,5,6}
$$

Now suppose someone tells us:

> The number is even.

That means $$F$$ happened.

Now the possible outcomes are no longer all six outcomes. They are only:

$$
F={2,4,6}
$$

This is where I initially got stuck.

Because outcomes 1, 3, and 5 still exist in the original sample space. But they are incompatible with the information we just received.

If I know the number is even, then 1 is impossible. 3 is impossible. 5 is impossible.

Not impossible in the original game.

Impossible given the information I now have.

So when I ask:

$$
P(E \mid F)
$$

I am not asking:

> Out of all six die outcomes, how many are greater than 3?

I am asking:

> Out of the outcomes that are even, how many are greater than 3?

Inside $$F$$, the possible outcomes are:

$$
{2,4,6}
$$

Among those, the outcomes greater than 3 are:

$$
{4,6}
$$

So:

$$
P(E\mid F)=\frac{2}{3}
$$

That is the whole idea.

The denominator changed because the relevant world changed.

Before evidence, the relevant world was $$S$$.

After evidence, the relevant world is $$F$$.

---

## The First Mental Model That Helped

Here is the way I started thinking about it:

> Conditional probability is probability after information has filtered the world.

Before the information:

$$
S={1,2,3,4,5,6}
$$

After the information “the number is even”:

$$
F={2,4,6}
$$

The event $$F$$ acts like a filter.

Everything incompatible with $$F$$ gets removed from consideration.

Again, this does not mean the removed outcomes never existed. It means they are no longer possible under the condition.

This distinction matters a lot:

* The original sample space is the full set of possible outcomes before extra information.
* The conditioned sample space is the set of possible outcomes after the information is known.

So when we condition on $$F$$, we are saying:

> Assume $$F$$ happened. Now reason only inside that assumption.

That is why $$F$$ becomes the new reference set.

---

## Prior: What I Believed Before the Information

Once conditional probability started making sense, the next words were:

* prior
* update
* posterior
* likelihood

At first, these sounded like extra terminology. But they are actually just names for different parts of belief revision.

A prior is what we believe before seeing the new information.

The word “prior” literally means before.

In the die example, before being told the number is even, the probability that the number is greater than 3 is:

$$
P(E)=\frac{1}{2}
$$

This is the prior probability of $$E$$.

It is what we believed before the evidence arrived.

So prior does not mean “random guess.”

It means:

> the belief state before this new piece of information is incorporated.

In this example, the prior is simple because the die is fair and all six outcomes are equally likely.

Before knowing anything else, three outcomes are greater than 3:

$$
{4,5,6}
$$

and three are not:

$$
{1,2,3}
$$

So the prior belief is exactly 50–50.

---

## Evidence: The Thing That Changes the Question

The evidence is the new information we receive.

In our example, the evidence is:

$$
F=\text{the number is even}
$$

Once we hear this, the question changes.

We are no longer asking:

> How likely is $$E$$ in the full sample space?

We are asking:

> How likely is $$E$$ among the worlds where $$F$$ is true?

That shift is the core of conditioning.

The evidence does not directly tell us whether $$E$$ happened.

It does not say “the number is greater than 3.”

It only says “the number is even.”

But that information still changes how plausible $$E$$ is.

Before hearing “even,” $$E$$ had probability:

$$
\frac{1}{2}
$$

After hearing “even,” $$E$$ has probability:

$$
\frac{2}{3}
$$

So evidence can change the probability of another event even if it does not directly state that event.

That was an important click for me.

---

## Posterior: What I Believe After the Information

The posterior is the belief after incorporating the evidence.

The word “posterior” means after.

So in our example:

$$
P(E\mid F)=\frac{2}{3}
$$

is the posterior probability of $$E$$ after learning $$F$$.

Before evidence:

$$
P(E)=\frac{1}{2}
$$

After evidence:

$$
P(E\mid F)=\frac{2}{3}
$$

That is the prior-to-posterior movement.

The event itself did not change. The die roll did not change. Reality did not change.

What changed was our information.

So posterior means:

> the probability after updating on the evidence.

Not the true answer.

Not the final truth of the universe.

Just the updated belief given what we currently know.

---

## Update: The Movement from Prior to Posterior

This was another word I initially wanted to collapse into the others.

I wondered:

> Is update the same thing as likelihood?

No.

The update is the whole process of changing from prior to posterior.

In the die example:

Prior:

$$
P(E)=\frac{1}{2}
$$

Evidence:

$$
F=\text{even}
$$

Posterior:

$$
P(E\mid F)=\frac{2}{3}
$$

The update is the movement:

$$
\frac{1}{2} \rightarrow \frac{2}{3}
$$

caused by the evidence.

So update is not a single probability term.

It is the revision process.

That matters because likelihood is only one ingredient used in a Bayesian update.

---

## Why a New Piece of Evidence Does Not Reset Everything

Another confusion I had was something like this:

> Suppose I start 50–50. Then I see one negative example, so I move toward negative. Then I see one positive example. Why do I not just go back to 50–50?

The answer is:

> Because evidence accumulates.

A new piece of evidence does not erase the old evidence.

If we see one negative example and then one positive example, our belief should reflect both observations, not only the most recent one.

This is the idea behind sequential updating.

After the first data point $$D_1$$, we have:

$$
P(H\mid D_1)
$$

After the second data point $$D_2$$, we do not go back to the original prior and compute only:

$$
P(H\mid D_2)
$$

Instead, we compute:

$$
P(H\mid D_1,D_2)
$$

The old posterior becomes the new prior.

That is the cleanest way to say it.

Learning is not replacement.

Learning is accumulation.

If every new observation reset us back to the beginning, we would never learn anything stable.

---

## Likelihood: The Concept I Had to Slow Down For

Prior made sense:

> What did I believe before the evidence?

Posterior made sense:

> What do I believe after the evidence?

But likelihood was harder.

The phrase people often use is:

> likelihood is (P$$\text{data}\mid \text{hypothesis}$$)

That is technically correct, but it can feel empty until the direction really clicks.

Likelihood asks:

> If this hypothesis were true, how expected would this evidence be?

That is the whole idea.

Not:

> How likely is the hypothesis?

That would be posterior.

Likelihood keeps the hypothesis fixed and asks whether the observed data fits it.

So likelihood is:

$$
P(D\mid H)
$$

Posterior is:

$$
P(H\mid D)
$$

These are not the same thing.

The direction matters.

---

## A Coin Example for Likelihood

Suppose we have two hypotheses about a coin:

$$
H_1=\text{the coin is fair}
$$

$$
H_2=\text{the coin is biased toward heads}
$$

Before flipping, suppose both hypotheses are equally plausible:

$$
P(H_1)=0.5
$$

$$
P(H_2)=0.5
$$

Now we flip once and observe heads.

The likelihood under the fair-coin hypothesis is:

$$
P(\text{heads}\mid H_1)=0.5
$$

The likelihood under the biased-coin hypothesis might be:

$$
P(\text{heads}\mid H_2)=0.9
$$

This does not mean:

$$
P(H_2\mid \text{heads})=0.9
$$

That would be a different statement.

The likelihood only says:

> If the coin were biased toward heads, then seeing heads would be very expected.

So the evidence fits $$H_2$$ better than $$H_1$$.

But to get the posterior, we still need to combine this likelihood with the prior.

That is why likelihood is not belief in the hypothesis.

Likelihood is how well the hypothesis explains the evidence.

---

## Likelihood in the Dice Example

Now return to the die.

Let:

$$
H = \text{the number is greater than 3}
$$

So:

$$
H={4,5,6}
$$

Let the evidence be:

$$
F=\text{the number is even}
$$

The likelihood is:

$$
P(F\mid H)
$$

In words:

> If the number were greater than 3, how likely would it be even?

Inside the hypothesis $$H$$, the possible outcomes are:

$$
{4,5,6}
$$

The even ones are:

$$
{4,6}
$$

So:

$$
P(F\mid H)=\frac{2}{3}
$$

This is likelihood.

But the posterior is:

$$
P(H\mid F)
$$

In words:

> Given that the number is even, how likely is it that the number is greater than 3?

That also equals $$2/3$$ in this particular example, but conceptually the two questions are different.

Likelihood:

$$
P(F\mid H)
$$

Posterior:

$$
P(H\mid F)
$$

The fact that they can sometimes have the same numerical value does not mean they are the same idea.

That is one of those places where examples can accidentally hide the distinction.

---

## The Wording That Finally Helped

I asked something like:

> Is likelihood: given this hypothesis, how good is this data for it to be true?

That was close, but slightly off.

The better wording is:

> Given this hypothesis, how expected is the observed data?

or:

> If this hypothesis were true, how well would it explain what I saw?

The small wording difference matters.

“How good is this data for the hypothesis to be true?” can sound like we are asking whether the data makes the hypothesis true.

That leans toward posterior thinking.

Likelihood is more like:

> Pretend the hypothesis is true. Would the data be surprising or unsurprising?

High likelihood means the data is unsurprising under the hypothesis.

Low likelihood means the data is surprising under the hypothesis.

That is it.

Nothing more mystical is happening.

---

## Bayes’ Rule as the Whole Story

Now the pieces fit into Bayes’ rule:

$$
P(H\mid D)=\frac{P(D\mid H)P(H)}{P(D)}
$$

Each part has a role:

$$
P(H)=\text{prior}
$$

$$
P(D\mid H)=\text{likelihood}
$$

$$
P(H\mid D)=\text{posterior}
$$

$$
P(D)=\text{normalizer/evidence probability}
$$

The informal version is:

$$
\text{posterior} \propto \text{likelihood} \times \text{prior}
$$

This is the cleanest mental model:

> Start with what you believed before. Then reweight each hypothesis by how well it explains the evidence. Normalize. The result is your posterior.

So likelihood does not replace the prior.

It modifies it.

A hypothesis with a strong prior but weak likelihood may lose probability.

A hypothesis with a weak prior but very strong likelihood may gain probability.

The posterior is the balance between both.

---

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

Sometimes the confusion comes from thinking too deeply about something that is actually straightforward.

**Overthinking: “Why does $$F$$ become the new sample space?”**

The simple truth: because we are now assuming $$F$$ happened. Outcomes outside $$F$$ are incompatible with the information we have. They still exist in the original sample space, but not in the conditioned world.

**Overthinking: “Did the probability change because reality changed?”**

No. Reality did not change. Our information changed. Conditional probability is about updating uncertainty, not changing the past.

**Overthinking: “Is posterior the true answer?”**

Not necessarily. Posterior is the updated belief given the evidence and the model. If the evidence is incomplete or the model is wrong, the posterior can still be wrong.

**Overthinking: “Is likelihood the same as posterior?”**

No. Likelihood is (P$$D\mid H$$). Posterior is (P$$H\mid D$$). Same symbols, opposite direction, completely different meaning.


</details>

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

Sometimes the confusion comes from thinking too deeply about something that is actually straightforward.

**Overthinking: “Why does $$F$$ become the new sample space?”**

The simple truth: because we are now assuming $$F$$ happened. Outcomes outside $$F$$ are incompatible with the information we have. They still exist in the original sample space, but not in the conditioned world.

**Overthinking: “Did the probability change because reality changed?”**

No. Reality did not change. Our information changed. Conditional probability is about updating uncertainty, not changing the past.

**Overthinking: “Is posterior the true answer?”**

Not necessarily. Posterior is the updated belief given the evidence and the model. If the evidence is incomplete or the model is wrong, the posterior can still be wrong.

**Overthinking: “Is likelihood the same as posterior?”**

No. Likelihood is (P$$D\mid H$$). Posterior is (P$$H\mid D$$). Same symbols, opposite direction, completely different meaning.

**Overthinking: “If the model sees a positive example after a negative example, shouldn’t it reset?”**

No. Evidence accumulates. The new positive example updates the current belief; it does not erase the previous negative example.

**Overthinking: “If labels are known during training, why do we need likelihood?”**

Because the known labels teach the model what each class looks like. Likelihood is learned from labeled data and then used when labels are unknown.

</details>

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Common Misconceptions</h2></summary>

**Misconception 1: “Conditioning deletes the rest of the sample space.”**

No. The rest of the sample space still exists. Conditioning only says that, given the information we have, those outcomes are no longer possible for the current question.

**Misconception 2: “Prior means random guess.”**

No. Prior means belief before the current evidence. Sometimes it is uniform because we have no reason to prefer one hypothesis. But priors can also encode strong previous knowledge.

**Misconception 3: “Likelihood tells us how likely the hypothesis is.”**

No. Likelihood tells us how likely the evidence is under the hypothesis.

The posterior tells us how likely the hypothesis is after seeing the evidence.

**Misconception 4: “Update equals likelihood.”**

No. The update uses likelihood, but it is not the likelihood itself. The update is the full movement from prior to posterior.


</details>

---

## The Cleanest Mental Model

Here is what I would memorize.

Conditional probability:

> Reason inside the world where the condition is true.

Prior:

> What I believed before this evidence.

Likelihood:

> If this hypothesis were true, how expected would this evidence be?

Update:

> Reweight beliefs based on how well each hypothesis explains the evidence.

Posterior:

> What I believe after incorporating the evidence.

---

## One-Sentence Takeaway

Conditional probability and Bayesian updating are not tricks with formulas; they are the language of changing uncertainty when new information rules out or reweights possible worlds.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.