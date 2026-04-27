---
layout: post
title: "Conditional Probability, Priors, Likelihood, and Bayesian Updating: The Way It Finally Made Sense to Me"
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

## Moving Into ML Carefully

Now we can move into machine learning.

The first intuition I had was something like:

> Before training, maybe positive and negative have equal probability. Then the model sees a negative example. The update happens, and now the model becomes more negative and less positive. So it thinks there are more negative examples.

This intuition is mostly right, but one sentence needs to be corrected.

The model is not necessarily learning:

> There are more negatives in reality.

A better version is:

> Given the evidence it has seen, negative outcomes are now more plausible under the model.

That distinction matters.

The model does not see reality directly.

It sees data.

So after one negative example, a reasonable model should shift toward negative, but not become completely certain.

If one negative example makes it believe everything is negative, that is not learning. That is overfitting.

---

## A Small Supervised Learning Example

Let’s use a tiny spam classifier.

We will call:

* negative = spam
* positive = not spam

Suppose our training data has three examples:

| Example | Text            | Label             |
| ------- | --------------- | ----------------- |
| 1       | “free money”    | negative/spam     |
| 2       | “free prize”    | negative/spam     |
| 3       | “meeting today” | positive/not-spam |

The possible label hypotheses for a new email are:

$$
H_- = \text{the email is negative/spam}
$$

$$
H_+ = \text{the email is positive/not-spam}
$$

Before seeing any data, suppose the model has no reason to prefer one label over the other:

$$
P(H_-)=0.5
$$

$$
P(H_+)=0.5
$$

This is the initial prior over labels.

---

## Why We Do Not Jump to 100% After One Example

Now the first example is:

> “free money” → negative

If we were extremely naive, after seeing one negative example and zero positive examples, we might say:

$$
P(H_-)=1
$$

$$
P(H_+)=0
$$

But that would be too extreme.

One example is not enough to eliminate the other possibility.

So many simple probabilistic models use smoothing.

Smoothing means we start with small imaginary counts.

For example, before seeing real data, imagine we start with:

| Label    | Pseudo-count |
| -------- | -----------: |
| negative |            1 |
| positive |            1 |

This is like saying:

> Before data, keep both classes alive.

Now after seeing the first negative example, the counts become:

| Label    | Count |
| -------- | ----: |
| negative |     2 |
| positive |     1 |

So:

$$
P(H_-)=\frac{2}{3}
$$

$$
P(H_+)=\frac{1}{3}
$$

The model now leans negative.

But it is not certain.

That is exactly what we want.

---

## After the Second Negative Example

The second example is:

> “free prize” → negative

Now the counts become:

| Label    | Count |
| -------- | ----: |
| negative |     3 |
| positive |     1 |

So:

$$
P(H_-)=\frac{3}{4}
$$

$$
P(H_+)=\frac{1}{4}
$$

The model leans even more negative.

This makes sense because the evidence so far has been two negative examples and zero positive examples.

The second example did not reset the model.

It updated the already-updated belief.

---

## After the Positive Example

The third example is:

> “meeting today” → positive

Now the counts become:

| Label    | Count |
| -------- | ----: |
| negative |     3 |
| positive |     2 |

So:

$$
P(H_-)=\frac{3}{5}=0.6
$$

$$
P(H_+)=\frac{2}{5}=0.4
$$

The model still leans negative overall.

Why did it not go back to 50–50?

Because the positive example did not erase the two negative examples.

The full evidence is:

* negative
* negative
* positive

So the posterior reflects all three examples.

That is why sequential updating is cumulative.

---

## But Real Models Learn More Than Label Counts

If the model only learned that negatives are slightly more common, it would be a weak model.

A real classifier also learns features.

In this toy text example, the features are words.

From the negative examples:

* “free money”
* “free prize”

The model sees:

| Word  | Count in negative examples |
| ----- | -------------------------: |
| free  |                          2 |
| money |                          1 |
| prize |                          1 |

From the positive example:

* “meeting today”

The model sees:

| Word    | Count in positive examples |
| ------- | -------------------------: |
| meeting |                          1 |
| today   |                          1 |

So the model starts learning patterns like:

* “free” is more associated with spam
* “money” is more associated with spam
* “prize” is more associated with spam
* “meeting” is more associated with not-spam
* “today” is more associated with not-spam

This is where likelihood becomes useful.

The model learns things like:

$$
P(\text{“free”}\mid H_-)
$$

and:

$$
P(\text{“free”}\mid H_+)
$$

In words:

> If the email is spam, how expected is the word “free”?

and:

> If the email is not spam, how expected is the word “free”?

The word “free” has higher likelihood under the spam hypothesis because it appeared in the spam examples.

---

## The Training vs Inference Distinction

This was another subtle point.

I asked:

> But for likelihood, the model already knows that an example is positive or negative from the labels, right?

Yes.

During supervised training, the model knows the labels.

That is the point of supervised learning.

For the example:

> “free money” → spam

The model is not trying to guess whether this training example is spam.

The label tells it that.

Instead, the model uses this labeled example to learn what spam looks like.

So during training, labels help the model estimate likelihoods.

For example:

$$
P(\text{words}\mid \text{spam})
$$

and:

$$
P(\text{words}\mid \text{not spam})
$$

Then, during inference, the label is not known.

Suppose a new email arrives:

> “free meeting”

Now the model must infer the label.

It compares:

$$
P(\text{“free meeting”}\mid H_-)
$$

with:

$$
P(\text{“free meeting”}\mid H_+)
$$

Then it combines those likelihoods with the class priors:

$$
P(H_-\mid x)\propto P(H_-)P(x\mid H_-)
$$

$$
P(H_+\mid x)\propto P(H_+)P(x\mid H_+)
$$

That gives the posterior probability of each label.

So the labels are known during training.

But they are unknown during inference.

Training uses labels to learn the relationship between features and classes.

Inference uses that learned relationship to predict labels for new examples.

---

## A Concrete New Email Example

Suppose the new email is:

> “free meeting”

This email has one word that looks spammy:

* free

and one word that looks not-spammy:

* meeting

So the model has mixed evidence.

It does not simply say:

> I saw more negative examples during training, so this must be negative.

A better model says:

> Negative is slightly more common in my training data, but I also need to see which label better explains these particular words.

That means it uses both:

1. Class prior
2. Feature likelihood

The class prior says:

$$
P(H_-)=0.6
$$

$$
P(H_+)=0.4
$$

The likelihood asks:

$$
P(\text{“free meeting”}\mid H_-)
$$

and:

$$
P(\text{“free meeting”}\mid H_+)
$$

If “free” is very strong evidence for spam, the model may predict spam.

If “meeting” is very strong evidence for not-spam, the model may predict not-spam.

The final answer depends on how these forces balance.

That is the whole Bayesian structure:

$$
\text{posterior} \propto \text{prior} \times \text{likelihood}
$$

---

## Generative vs Discriminative Models

The spam example above is closest to a generative classifier like Naive Bayes.

A generative classifier models:

$$
P(x\mid y)
$$

and:

$$
P(y)
$$

Then it uses Bayes’ rule to compute:

$$
P(y\mid x)
$$

A discriminative classifier directly models:

$$
P(y\mid x)
$$

For example, logistic regression or a neural network classifier directly predicts a distribution over labels given the input.

But the intuition still carries over.

Even if the model is not explicitly Bayesian, training still changes the model so that it assigns higher probability to the correct labels and lower probability to incorrect labels.

The data is fixed.

The labels are fixed.

The thing we change is the model.

That is why the Bayesian language is useful even when the actual optimization procedure is gradient descent.

---

## How This Connects to “Likelihood of the Training Data”

In supervised learning, we often write:

$$
D={(x_1,y_1),(x_2,y_2),\ldots,(x_N,y_N)}
$$

The inputs are known.

The labels are known.

The data already exists.

So why talk about probability?

The answer is:

> Probability lives inside the model.

The model assigns probabilities to labels.

For one training example ($$x_i,y_i$$), the model gives:

$$
p(y\mid x_i;\theta)
$$

The likelihood contribution of that example is the probability assigned to the correct label:

$$
p(y_i\mid x_i;\theta)
$$

If this number is high, the model explains the example well.

If this number is low, the model is surprised by the correct label.

For the whole dataset, assuming examples are independent, the likelihood is:

$$
p(D\mid \theta)=\prod_{i=1}^N p(y_i\mid x_i;\theta)
$$

The model is asking:

> Under these parameters $$\theta$$, how much probability do I assign to the labels that actually occurred?

Training then adjusts $$\theta$$ to make this likelihood high.

Usually we maximize log-likelihood instead:

$$
\log p(D\mid \theta)=\sum_{i=1}^N \log p(y_i\mid x_i;\theta)
$$

And in practice, we minimize negative log-likelihood:

$$
L(\theta)=-\frac{1}{N}\sum_{i=1}^N \log p(y_i\mid x_i;\theta)
$$

This is the same idea behind cross-entropy loss.

So likelihood in ML is not asking:

> What is the probability that the dataset exists?

It is asking:

> How well does this model, with these parameters, explain the observed labels?

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

**Misconception 5: “One opposite example cancels the previous example.”**

Not automatically. Evidence has strength, and evidence accumulates. Exact cancellation only happens under special symmetry.

**Misconception 6: “In supervised learning, the model is guessing labels during training.”**

Not exactly. During training, labels are given. The model uses them to learn. During inference, labels are unknown, and the model predicts them.

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

Machine learning version:

> Training adjusts the model so it assigns higher probability to the labels or outputs that actually occurred.

---

## One-Sentence Takeaway

Conditional probability and Bayesian updating are not tricks with formulas; they are the language of changing uncertainty when new information rules out or reweights possible worlds.

Once that clicked, prior, likelihood, posterior, and even ML training started feeling like different versions of the same idea.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.