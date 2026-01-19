---
layout: post
title: What Does "Likelihood of the Training Data" Actually Mean?
date: 2026-01-19 10:00:00-0400
description: An explanation of likelihood and log-likelihood in machine learning detailing what's really being measured and why probability matters for data that already exists
tags: machine-learning probability likelihood
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
</style>

Likelihood and log-likelihood are everywhere in machine learning, yet they're also among the most misunderstood concepts. Many explanations repeat the phrase "the probability of observing the data given the parameters" and move on, leaving us confused about what is being observed, what is random, and why probability is involved at all when the data already exists.

Let's clear that confusion carefully and precisely.

## The Setting: Supervised Learning

In <span class="tooltip-term">supervised learning<span class="tooltip-text">A type of machine learning where we train models using labeled data—pairs of inputs and their correct outputs. The model learns to map inputs to outputs by seeing examples.</span></span>, our training dataset consists of input-output pairs:

$$
D = \{(x_1, y_1), (x_2, y_2), \ldots, (x_N, y_N)\}
$$

Here's what we know:

The inputs $$x_i$$ are given and fixed. The labels $$y_i$$ are given and fixed. Nothing here is uncertain in reality. The data already exists.

So why are we talking about probability at all?

## What the Model Actually Represents

Here's something we need to understand: a supervised learning model does not directly predict labels. Instead, it defines a <span class="tooltip-term">conditional probability distribution<span class="tooltip-text">A probability distribution that depends on some condition. Here, it's the probability of different labels given a specific input. For example, p(y|x) means "the probability of label y, given that we observed input x."</span></span>:

$$
p(y \mid x; \theta)
$$

This distribution answers a very specific question: "If this model, with <span class="tooltip-term">parameters<span class="tooltip-text">The weights and biases (θ) that the model learns during training. These are the knobs we adjust to make the model better at its task.</span></span> $$\theta$$, were responsible for assigning labels to input $$x$$, how likely would each possible label be?"

The key point here is that **probability lives inside the model, not in the world**. From the model's perspective, labels are treated as <span class="tooltip-term">random variables<span class="tooltip-text">A variable whose value is uncertain and determined by a probability distribution. Here, the model treats labels as random even though they're fixed in reality.</span></span>.

## What "Probability of the Data" Really Refers To

When we say "the probability of observing the data given $$\theta$$," we're not talking about:

- The probability that the dataset exists
- The probability that history happened this way
- The probability that we'll see these samples again

Instead, it means: **the <span class="tooltip-term">probability mass<span class="tooltip-text">The amount of probability assigned to a specific outcome. For discrete outcomes (like class labels), we use "probability mass" instead of "probability density."</span></span> the model assigns to the labels that actually occurred, conditioned on the inputs**.

This is the single most important clarification. We're measuring how well our model explains what we already observed.

## Likelihood for One Training Example

Let's take a single training example $$(x_i, y_i)$$. The model produces a <span class="tooltip-term">distribution over labels<span class="tooltip-text">A probability distribution that assigns probabilities to all possible labels. For example, in a 3-class problem, it might output: Class A: 0.7, Class B: 0.2, Class C: 0.1 (summing to 1.0).</span></span>:

$$
p(y \mid x_i; \theta)
$$

The likelihood contribution of this example is simply the probability assigned to the correct label $$y_i$$.

If the model assigns high probability to $$y_i$$, the model explains this example well. If the model assigns low probability to $$y_i$$, the model finds this example surprising.

That's it. Nothing more exotic is happening.

## Likelihood for the Full Dataset

Assuming examples are <span class="tooltip-term">independent (i.i.d.)<span class="tooltip-text">Independent and Identically Distributed: each training example is drawn from the same distribution and doesn't affect other examples. This means knowing one example tells us nothing about another.</span></span>, the standard assumption in supervised learning, the likelihood of the dataset is:

$$
p(D \mid \theta) = \prod_{i=1}^N p(y_i \mid x_i; \theta)
$$

This <span class="tooltip-term">product<span class="tooltip-text">The ∏ symbol means multiply all terms together. Here, we multiply the individual probabilities p(y₁|x₁) × p(y₂|x₂) × ... × p(yₙ|xₙ). This works because events are independent.</span></span> measures: "How well does this parameter setting $$\theta$$ explain all observed labels for their corresponding inputs?"

Likelihood is therefore a function of the parameters, not a probability distribution over them.

## Why Likelihood Is Evaluated on Already-Seen Data

This is the conceptual sticking point for many of us. We're not predicting the past. We're doing **<span class="tooltip-term">model evaluation<span class="tooltip-text">Assessing how well our model's predictions align with reality. We're measuring the model's quality, not making new predictions.</span></span>**.

The question being asked is: "If my model were the true <span class="tooltip-term">data-generating process<span class="tooltip-text">The underlying mechanism that produces our data. We assume there's some true process creating input-output pairs, and we're trying to approximate it with our model. This also means, we choose a probabilistic model that assigns probabilities to outputs given inputs, and we tune its parameters to agree with observed data.</span></span>, would it consider the observed labels plausible?"

Likelihood answers that question quantitatively.

High likelihood means the model is not surprised by what happened. Low likelihood means the model strongly disagrees with the observed outcomes. Training aims to reduce this disagreement.

## Why We Maximize Likelihood by Changing the Weights

The data is fixed. The labels are fixed. The only thing we're allowed to change is the parameter vector $$\theta$$.

So training becomes: **adjust $$\theta$$ so the model assigns as much probability as possible to the correct labels across the training set**.

Formally, this is <span class="tooltip-term">Maximum Likelihood Estimation (MLE)<span class="tooltip-text">A method for finding the parameter values that make the observed data most probable under the model. We search for the θ that maximizes the likelihood function.</span></span>:

$$
\hat{\theta} = \underset{\theta}{\arg\max} \, p(D \mid \theta)
$$

<span class="tooltip-term">arg max<span class="tooltip-text">"Argument of the maximum"—the input value (here, θ) that produces the maximum output. We're not finding the maximum value itself, but which θ gives us that maximum.</span></span>

Or, equivalently:

$$
\hat{\theta} = \underset{\theta}{\arg\max} \sum_{i=1}^N \log p(y_i \mid x_i; \theta)
$$

## Why We Use Log-Likelihood

We take the <span class="tooltip-term">logarithm<span class="tooltip-text">A mathematical function that converts multiplication into addition. Log is monotonic, meaning if x > y, then log(x) > log(y), so maximizing likelihood is equivalent to maximizing log-likelihood.</span></span> because:

- Products of probabilities become sums
- Optimization becomes <span class="tooltip-term">numerically stable<span class="tooltip-text">Less prone to computational errors. Multiplying many small probabilities can lead to underflow (numbers too small to represent), but adding their logs avoids this problem.</span></span>
- The maximizer remains unchanged (log is monotonic)

The log-likelihood is:

$$
\log p(D \mid \theta) = \sum_{i=1}^N \log p(y_i \mid x_i; \theta)
$$

## Connection to Loss Functions

In practice, we minimize a loss instead of maximizing likelihood. The loss used in most models is:

$$
L(\theta) = -\frac{1}{N} \sum_{i=1}^N \log p(y_i \mid x_i; \theta)
$$

This is the <span class="tooltip-term">negative log-likelihood (NLL)<span class="tooltip-text">The negative of the log-likelihood. We minimize NLL instead of maximizing likelihood—they're equivalent, but minimization is the standard convention in optimization.</span></span>.

<span class="tooltip-term">Cross-entropy loss<span class="tooltip-text">A loss function that measures the difference between two probability distributions. In classification, it's identical to negative log-likelihood and measures how well predicted probabilities match true labels.</span></span>, binary cross-entropy, and softmax loss; all of these are just different parameterizations of NLL under different output distributions.

---

**That's the core explanation!** If you've made it this far and the main concepts are clear, you're done. What follows are supplementary sections addressing common confusions and mental traps—useful for solidifying understanding, but not essential for grasping the fundamentals.

---

## Where We Tend to Overthink

Sometimes the confusion comes from thinking too deeply about something that's actually straightforward. Here are places where I've overthought things (and you might too):

**Overthinking: "Is this the probability that the model could generate this exact dataset?"**

The simple truth: No. It's just how much probability the model assigns to the correct labels. Think of it like a scoring function: "How well does the model score the actual answers?" Not "Could the model have created this test?"

**Overthinking: "Are we assuming there's some true underlying probability distribution in nature?"**

The simple truth: Not really. We're just saying "IF labels were random variables from our model's perspective, here's how likely it would consider the observed outcomes." It's a modeling choice, not a claim about reality.

**Overthinking: "Why is it called 'likelihood' if it's not really a probability?"**

The simple truth: It is a probability—just not a probability over data or parameters. It's the probability of the observed labels, computed using the model's current parameter values. The name "likelihood" helps us remember we're viewing it as a function of $$\theta$$.

**Overthinking: "Does maximizing likelihood mean the model will memorize the training data?"**

The simple truth: Not inherently. MLE just finds parameters that agree with the training labels. Whether the model memorizes or generalizes depends on the model's capacity, regularization, and how much data you have; not on the likelihood principle itself.

**Overthinking: "If likelihood measures 'surprise,' shouldn't we minimize it instead of maximize it?"**

The simple truth: High likelihood = low surprise = good. The model assigns high probability to what actually happened, meaning it's not surprised. We maximize likelihood because we want the model to be unsurprised by reality.


## Common Misconceptions

Let's address some frequent sources of confusion:

**Misconception 1: "We're computing the probability that the data is real"**

No. The data already exists. We're computing how much probability our model assigns to the observed outcomes.

**Misconception 2: "Likelihood is a probability distribution over the data"**

No. Likelihood is a function of the parameters $$\theta$$, not the data. The data is fixed; we vary $$\theta$$ to see which values make the data most probable under the model.

**Misconception 3: "Maximizing likelihood means we're trying to predict the training data"**

No. We're not predicting anything. We're measuring agreement. We're asking: "Which parameter settings would have been most consistent with what we observed?"

**Misconception 4: "Log-likelihood is just a computational trick"**

Partially true, but it's also conceptually important. Log-likelihood is additive across examples, which makes it interpretable as a sum of individual contributions. It's also the basis for information theory connections.

**Misconception 5: "Cross-entropy loss is different from likelihood"**

No. Cross-entropy loss is exactly negative log-likelihood. They're the same thing with different names, used in different communities.

**Misconception 6: "We use likelihood because the data is random"**

No. The data isn't random—it already happened. We use likelihood because our **model** treats outcomes as random. The randomness is in the model's perspective, not in reality.

## The Cleanest Mental Model

Here's what to memorize: **likelihood is the amount of probability the model assigns to the labels that actually occurred, given the inputs, under its current parameters**.

Not the probability that the data exists. Not the probability of re-observing history. But the **agreement between the model and reality**.

## One-Sentence Takeaway

Training a supervised model means adjusting the weights so the model assigns maximal probability to the correct labels in the training data.

Once this sentence is clear, likelihood, log-likelihood, cross-entropy, and MLE all become the same idea seen from different angles.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.
