---
layout: post
title: "Bayesian Updating in Machine Learning: Making Sense of Training Data"
date: 2026-04-28 10:00:00-0400
description: A deep dive into conditional probability, priors, likelihood, and Bayesian updating in ML.
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

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

**Overthinking: “If the model sees a positive example after a negative example, shouldn’t it reset?”**

No. Evidence accumulates. The new positive example updates the current belief; it does not erase the previous negative example.

**Overthinking: “If labels are known during training, why do we need likelihood?”**

Because the known labels teach the model what each class looks like. Likelihood is learned from labeled data and then used when labels are unknown.


</details>



<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Common Misconceptions</h2></summary>

**Misconception 5: “One opposite example cancels the previous example.”**

Not automatically. Evidence has strength, and evidence accumulates. Exact cancellation only happens under special symmetry.

**Misconception 6: “In supervised learning, the model is guessing labels during training.”**

Not exactly. During training, labels are given. The model uses them to learn. During inference, labels are unknown, and the model predicts them.


</details>

---

## The Cleanest Mental Model

Here is what I would memorize for ML:

Machine learning version:

> Training adjusts the model so it assigns higher probability to the labels or outputs that actually occurred.

---

## One-Sentence Takeaway

Once Bayesian updating clicked, prior, likelihood, posterior, and even ML training started feeling like different versions of the same idea.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.