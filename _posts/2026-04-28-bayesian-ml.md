---
layout: post
title: "Bayesian Updating in Machine Learning: Making Sense of Training Data"
date: 2026-04-28 10:00:00-0400
description: A deep dive into conditional probability, priors, likelihood, and Bayesian updating in ML.
tags: machine-learning probability math-for-ml
categories: machine-learning
featured: true
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

## Applying Probability to Machine Learning

These probabilistic concepts apply directly to machine learning. A common initial intuition is: *Before training, positive and negative labels have equal probability. Then the model sees a negative example. An update occurs, and the model assigns higher probability to the negative class. It concludes there are more negative examples in the world.*

This intuition requires refinement. The model is not learning that there are absolutely more negative examples in reality. More precisely: *given the observed evidence, negative outcomes are now more plausible under the model.*

The model does not observe reality directly; it only observes the provided data. After observing one negative example, the model shifts its distribution toward the negative label, but it should not become completely certain. If one single negative example causes a model to assign 100% probability to the negative class, that is overfitting.

---

## A Small Supervised Learning Example

Let’s use a tiny, intuitive spam classifier to demonstrate this. We will call the negative class "spam" and the positive class "not spam". Suppose our training data consists of just three examples:

| Example | Text            | Label             |
| ------- | --------------- | ----------------- |
| 1       | “free money”    | negative/spam     |
| 2       | “free prize”    | negative/spam     |
| 3       | “meeting today” | positive/not-spam |

The possible label hypotheses for any new, unseen email are:

$$
H_- = \text{the email is negative/spam}
$$

$$
H_+ = \text{the email is positive/not-spam}
$$

Before seeing any of the training data, suppose the model has absolutely no reason to prefer one label over the other. We would represent this as an equal split:

$$
P(H_-)=0.5
$$

$$
P(H_+)=0.5
$$

This initial 50–50 split is our model's prior over the labels.

---

## Why We Do Not Jump to 100% After One Example

The model encounters the first training example: "free money" → negative. An extremely naive system might look at this single negative example and instantly conclude:

$$
P(H_-)=1
$$

$$
P(H_+)=0
$$

Jumping to 100% certainty is extreme. One example is insufficient evidence to permanently eliminate the other possibility. To prevent this, many probabilistic models use a technique called smoothing. Smoothing initializes the model with small pseudo-counts for all classes. For example, before observing data, the model behaves as if it has already seen one instance of each class:

| Label    | Pseudo-count |
| -------- | -----------: |
| negative |            1 |
| positive |            1 |

This acts as a mathematical safeguard, keeping all classes alive as possibilities before data is observed. Now, after seeing the first actual negative example, our counts become:

| Label    | Count |
| -------- | ----: |
| negative |     2 |
| positive |     1 |

Which means our probabilities update to:

$$
P(H_-)=\frac{2}{3}
$$

$$
P(H_+)=\frac{1}{3}
$$

The model now appropriately leans negative based on the evidence, but it is not completely certain. That is exactly the behavior we want.

---

## After the Second Negative Example

The model then processes the second training example: "free prize" → negative. Our running counts update again:

| Label    | Count |
| -------- | ----: |
| negative |     3 |
| positive |     1 |

And our probabilities shift:

$$
P(H_-)=\frac{3}{4}
$$

$$
P(H_+)=\frac{1}{4}
$$

The model leans even more strongly negative now. This makes perfect sense because the evidence so far consists of two real negative examples and zero real positive examples. Notice that the second example did not reset the model; instead, it updated the already-updated belief.

---

## After the Positive Example

Finally, the model sees the third example: "meeting today" → positive. Our final counts become:

| Label    | Count |
| -------- | ----: |
| negative |     3 |
| positive |     2 |

Yielding our final probabilities for this tiny dataset:

$$
P(H_-)=\frac{3}{5}=0.6
$$

$$
P(H_+)=\frac{2}{5}=0.4
$$

The model still leans negative overall. It does not revert to 50–50 after seeing a positive example because the new positive example does not erase the previous two negative examples. The accumulated evidence is two negatives and one positive; the posterior probability mathematically reflects all three examples. Sequential updating is cumulative.

---

## But Real Models Learn More Than Label Counts

If a model only learned that negative labels were slightly more common in the dataset, it would be a very weak model. A real classifier also learns the relationship between the labels and the *features*. In our toy text example, the features are the individual words.

From the two negative examples ("free money" and "free prize"), the model observes the word "free" twice, "money" once, and "prize" once. From the positive example ("meeting today"), the model observes the words "meeting" and "today" once each. 

By tracking these feature counts, the model learns valuable patterns. It learns that "free", "money", and "prize" are strongly associated with spam, while "meeting" and "today" are associated with non-spam. This is precisely where likelihood becomes mathematically useful. The model calculates feature likelihoods like:

$$
P(\text{“free”}\mid H_-)
$$

and:

$$
P(\text{“free”}\mid H_+)
$$

The model is essentially asking: *if the email is spam, how expected is the word “free”?* And conversely, *if the email is not spam, how expected is the word “free”?* In this dataset, the word "free" has a much higher likelihood under the spam hypothesis because it appeared exclusively in the spam examples.

---

## The Training vs Inference Distinction

A common point of confusion is the role of labels during likelihood estimation: *the model already knows whether an example is positive or negative from the labels, right?*

During supervised training, the model is provided the true labels. When the model processes the training example `"free money" → spam`, it is not guessing whether the example is spam. The provided label serves as the ground truth. 

Instead, the model uses this labeled example to learn the fundamental characteristics of what spam looks like. During training, these known labels help the model estimate the likelihoods:

$$
P(\text{words}\mid \text{spam})
$$

and:

$$
P(\text{words}\mid \text{not spam})
$$

Then, during inference (when the model is deployed), the label is entirely unknown. Suppose a brand new email arrives that says "free meeting". Now the model must infer the hidden label. It compares the likelihood of those words under the negative hypothesis:

$$
P(\text{“free meeting”}\mid H_-)
$$

with the likelihood under the positive hypothesis:

$$
P(\text{“free meeting”}\mid H_+)
$$

It then mathematically combines those calculated likelihoods with the class priors it learned:

$$
P(H_-\mid x)\propto P(H_-)P(x\mid H_-)
$$

$$
P(H_+\mid x)\propto P(H_+)P(x\mid H_+)
$$

That combination gives the final posterior probability for each label. Labels are known during training, but they are unknown during inference. Training uses the known labels to learn the probabilistic relationship between features and classes. Inference uses that learned relationship to predict labels for new examples.

---

## A Concrete New Email Example

Suppose the new email is exactly that phrase: "free meeting". This email contains mixed evidence. It has one word that looks incredibly spammy ("free") and one word that looks very not-spammy ("meeting"). 

Because of this mixed evidence, the model does not simply assume the email is negative just because negative examples were more common during training. A probabilistic model actively weighs the overall class prevalence against how well each label explains these particular words.

The model actively balances two components: the **class prior** and the **feature likelihood**.

The class prior is the baseline probability of each class based on the overall dataset counts:

$$
P(H_-)=0.6
$$

$$
P(H_+)=0.4
$$

The feature likelihood asks how well each hypothesis explains the specific words in this email:

$$
P(\text{“free meeting”}\mid H_-)
$$

and:

$$
P(\text{“free meeting”}\mid H_+)
$$

If "free" is incredibly strong evidence for spam, the model may ultimately predict spam. However, if "meeting" is overwhelmingly strong evidence for not-spam, the model may confidently predict not-spam. The final classification depends entirely on how these opposing forces balance out mathematically. That exact balancing act is the structural core of Bayesian reasoning:

$$
\text{posterior} \propto \text{prior} \times \text{likelihood}
$$

---

## Generative vs Discriminative Models

The spam example is closest to a **generative classifier** (like Naive Bayes). A generative classifier models the joint distribution by explicitly learning both the likelihood of the features given the class ($$P(x\mid y)$$) and the prior probability of the class itself ($$P(y)$$). It then uses Bayes' rule to compute the final posterior prediction:

$$
P(y\mid x)
$$

On the other hand, a **discriminative classifier** (like logistic regression or a neural network classifier) directly models the boundary between classes. It skips modeling the prior and likelihood separately and directly predicts a distribution over labels given the input:

$$
P(y\mid x)
$$

The fundamental intuition still carries over. Even if a model is not explicitly framed in Bayesian terms, the training process still inherently changes the model so that it assigns higher probability to the correct labels and lower probability to incorrect labels. During training, the data is fixed and the labels are fixed. The only thing that changes is the internal state of the model. The language of Bayesian updating is extremely useful for building intuition, even when the actual mathematical optimization procedure is gradient descent.

---

## How This Connects to “Likelihood of the Training Data”

In supervised learning literature, the dataset is often written mathematically as a collection of inputs and known labels:

$$
D=\{(x_1,y_1),(x_2,y_2),\ldots,(x_N,y_N)\}
$$

Since the inputs and labels are known, and the data already exists, the role of probability might seem unclear. The key is that *probability lives inside the model.*

The model assigns probabilities to labels. For one single training example ($$x_i, y_i$$), the model produces a probability for the correct label:

$$
p(y_i\mid x_i;\theta)
$$

The likelihood contribution of that specific example is simply the probability the model assigned to the correct label. If this number is high, the model currently explains the example very well. If this number is low, the model does not explain the correct label well.

For the entire dataset (assuming the examples are independent), the total likelihood is the product of all those individual probabilities:

$$
p(D\mid \theta)=\prod_{i=1}^N p(y_i\mid x_i;\theta)
$$

Through this equation, the model evaluates how much total probability it assigns to the observed labels under its current internal parameters ($$\theta$$).

The goal of training is to adjust $$\theta$$ to make this likelihood as high as possible. Usually, for mathematical stability, the log-likelihood is maximized instead:

$$
\log p(D\mid \theta)=\sum_{i=1}^N \log p(y_i\mid x_i;\theta)
$$

In practical frameworks like PyTorch or TensorFlow, optimizers are designed to minimize values rather than maximize them, so the **negative log-likelihood** is minimized:

$$
L(\theta)=-\frac{1}{N}\sum_{i=1}^N \log p(y_i\mid x_i;\theta)
$$

This exact formulation is the core mathematical idea behind the standard cross-entropy loss function used to train almost all modern neural networks. 

Likelihood in machine learning is not an evaluation of the probability that the dataset exists. It is an evaluation of how well the specific model, given its current parameters, explains the observed labels.

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

**Overthinking: “If the model sees a positive example after a negative example, shouldn’t it reset?”**  
Evidence accumulates mathematically. The new positive example updates the current belief state; it does not simply erase the previous negative example.

**Overthinking: “If labels are known during training, why do we need likelihood?”**  
The known labels are exactly what teach the model the feature distributions for each class. The likelihood is learned from the labeled data during training, and then it is utilized during inference when the labels are unknown.

</details>

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Common Misconceptions</h2></summary>

**Misconception 5: “One opposite example cancels the previous example.”**  
Evidence has different strengths, and evidence accumulates over time. Exact cancellation only happens under very special symmetry conditions.

**Misconception 6: “In supervised learning, the model is guessing labels during training.”**  
During training, the ground-truth labels are given, and the model uses them to learn its internal parameters. It is only during inference that the labels are unknown and the model must actively predict them.

</details>

---

## The Cleanest Mental Model

This is the core concept for machine learning training:

> Training adjusts the model's internal parameters so that it assigns the highest possible probability to the labels or outputs that actually occurred in the dataset.

---

## One-Sentence Takeaway

Once Bayesian updating truly clicks, you realize that the prior, the likelihood, the posterior, and even the supervised machine learning training process itself are all just different mathematical expressions of the exact same underlying idea.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.