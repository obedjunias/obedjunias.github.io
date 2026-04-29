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

Likelihood and log-likelihood are foundational concepts in machine learning. Standard explanations often use the phrase "the probability of observing the data given the parameters," which can obscure what is being observed, what is random, and why probability is involved when the data already exists.

## The Setting: Supervised Learning

In <span class="tooltip-term">supervised learning<span class="tooltip-text">A type of machine learning where we train models using labeled data—pairs of inputs and their correct outputs. The model learns to map inputs to outputs by seeing examples.</span></span>, our training dataset consists of input-output pairs:

$$
D = \{(x_1, y_1), (x_2, y_2), \ldots, (x_N, y_N)\}
$$

The inputs $$x_i$$ and the labels $$y_i$$ are given and fixed. Nothing is uncertain in reality; the data already exists. This raises the question of why probability is necessary.

## What the Model Actually Represents

A supervised learning model does not directly predict labels. Instead, it defines a <span class="tooltip-term">conditional probability distribution<span class="tooltip-text">A probability distribution that depends on some condition. Here, it's the probability of different labels given a specific input. For example, p(y|x) means "the probability of label y, given that we observed input x."</span></span>:

$$
p(y \mid x; \theta)
$$

This distribution answers a specific question: "If this model, with <span class="tooltip-term">parameters<span class="tooltip-text">The weights and biases (θ) that the model learns during training. These are the knobs we adjust to make the model better at its task.</span></span> $$\theta$$, were responsible for assigning labels to input $$x$$, how likely would each possible label be?"

**Probability lives inside the model, not in the world**. The model treats labels as <span class="tooltip-term">random variables<span class="tooltip-text">A variable whose value is uncertain and determined by a probability distribution. Here, the model treats labels as random even though they're fixed in reality.</span></span>.

## What "Probability of the Data" Really Refers To

When referring to "the probability of observing the data given $$\theta$$," it does not mean:

- The probability that the dataset exists
- The probability that history happened this way
- The probability that we'll see these samples again

Instead, it means: **the <span class="tooltip-term">probability mass<span class="tooltip-text">The amount of probability assigned to a specific outcome. For discrete outcomes (like class labels), we use "probability mass" instead of "probability density."</span></span> the model assigns to the labels that actually occurred, conditioned on the inputs**.

This measures how well the model explains the observed data.

## Likelihood for One Training Example

Consider a single training example $$(x_i, y_i)$$. The model produces a <span class="tooltip-term">distribution over labels<span class="tooltip-text">A probability distribution that assigns probabilities to all possible labels. For example, in a 3-class problem, it might output: Class A: 0.7, Class B: 0.2, Class C: 0.1 (summing to 1.0).</span></span>:

$$
p(y \mid x_i; \theta)
$$

The likelihood contribution of this example is simply the probability assigned to the correct label $$y_i$$.

If the model assigns high probability to $$y_i$$, the model explains the example well. If it assigns low probability, the model does not explain the example well.

## Likelihood for the Full Dataset

Assuming examples are <span class="tooltip-term">independent (i.i.d.)<span class="tooltip-text">Independent and Identically Distributed: each training example is drawn from the same distribution and doesn't affect other examples. This means knowing one example tells us nothing about another.</span></span>, the standard assumption in supervised learning, the likelihood of the dataset is:

$$
p(D \mid \theta) = \prod_{i=1}^N p(y_i \mid x_i; \theta)
$$

This <span class="tooltip-term">product<span class="tooltip-text">The ∏ symbol means multiply all terms together. Here, we multiply the individual probabilities p(y₁|x₁) × p(y₂|x₂) × ... × p(yₙ|xₙ). This works because events are independent.</span></span> measures: "How well does this parameter setting $$\theta$$ explain all observed labels for their corresponding inputs?"

Likelihood is a function of the parameters, not a probability distribution over them.

## Why Likelihood Is Evaluated on Already-Seen Data

Evaluating likelihood on already-seen data is not about predicting the past; it is **<span class="tooltip-term">model evaluation<span class="tooltip-text">Assessing how well our model's predictions align with reality. We're measuring the model's quality, not making new predictions.</span></span>**.

The question being asked is: "If my model were the true <span class="tooltip-term">data-generating process<span class="tooltip-text">The underlying mechanism that produces our data. We assume there's some true process creating input-output pairs, and we're trying to approximate it with our model. This also means, we choose a probabilistic model that assigns probabilities to outputs given inputs, and we tune its parameters to agree with observed data.</span></span>, would it consider the observed labels plausible?"

Likelihood answers that question quantitatively.

High likelihood means the model assigns high probability to what happened. Low likelihood means the model strongly disagrees with the observed outcomes. Training aims to reduce this disagreement.

## Why We Maximize Likelihood by Changing the Weights

The data is fixed. The labels are fixed. The only component being modified is the parameter vector $$\theta$$.

Training involves adjusting $$\theta$$ so the model assigns as much probability as possible to the correct labels across the training set.

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

The <span class="tooltip-term">logarithm<span class="tooltip-text">A mathematical function that converts multiplication into addition. Log is monotonic, meaning if x > y, then log(x) > log(y), so maximizing likelihood is equivalent to maximizing log-likelihood.</span></span> is used because:

- Products of probabilities become sums
- Optimization becomes <span class="tooltip-term">numerically stable<span class="tooltip-text">Less prone to computational errors. Multiplying many small probabilities can lead to underflow (numbers too small to represent), but adding their logs avoids this problem.</span></span>
- The maximizer remains unchanged (log is monotonic)

The log-likelihood is:

$$
\log p(D \mid \theta) = \sum_{i=1}^N \log p(y_i \mid x_i; \theta)
$$

## Connection to Loss Functions

In practice, we minimize a loss instead of maximizing likelihood. The loss used in most classification models is:

$$
L(\theta) = -\frac{1}{N} \sum_{i=1}^N \log p(y_i \mid x_i; \theta)
$$

This is the <span class="tooltip-term">negative log-likelihood (NLL)<span class="tooltip-text">The negative of the log-likelihood. We minimize NLL instead of maximizing likelihood—they're equivalent, but minimization is the standard convention in optimization.</span></span>.

<span class="tooltip-term">Cross-entropy loss<span class="tooltip-text">A loss function that measures the difference between two probability distributions. In classification, it's identical to negative log-likelihood and measures how well predicted probabilities match true labels.</span></span>, binary cross-entropy, and softmax loss; all of these are just different parameterizations of NLL under different output distributions.

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

**Overthinking: "Is this the probability that the model could generate this exact dataset?"**

No. It is the amount of probability the model assigns to the correct labels. It acts as a scoring function for how well the model scores the actual answers, not an evaluation of whether the model could generate the dataset.

**Overthinking: "Are we assuming there's some true underlying probability distribution in nature?"**

Not necessarily. The model simply operates under the premise that *if* labels were random variables, this is how likely the observed outcomes would be. It is a modeling choice, not a claim about absolute reality.

**Overthinking: "Why is it called 'likelihood' if it's not really a probability?"**

It is a probability—specifically the probability of the observed labels computed using the model's current parameter values. The term "likelihood" indicates that it is viewed as a function of the parameters $$\theta$$ rather than the data.

**Overthinking: "Does maximizing likelihood mean the model will memorize the training data?"**

Not inherently. MLE finds parameters that agree with the training labels. Whether the model memorizes or generalizes depends on model capacity, regularization, and dataset size, not on the likelihood principle itself.

**Overthinking: "If likelihood measures 'surprise,' shouldn't we minimize it instead of maximize it?"**

High likelihood implies low surprise. The model assigns high probability to the observed outcomes, meaning the outcomes are expected. Maximizing likelihood ensures the model is unsurprised by the data.

</details>

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Common Misconceptions</h2></summary>

**Misconception 1: "We're computing the probability that the data is real"**

No. The data already exists. This computes how much probability the model assigns to the observed outcomes.

**Misconception 2: "Likelihood is a probability distribution over the data"**

No. Likelihood is a function of the parameters $$\theta$$, not the data. The data is fixed; $$\theta$$ is varied to find values that make the data most probable under the model.

**Misconception 3: "Maximizing likelihood means we're trying to predict the training data"**

No. It measures agreement. It answers: "Which parameter settings are most consistent with the observed data?"

**Misconception 4: "Log-likelihood is just a computational trick"**

Partially true, but it is conceptually important. Log-likelihood is additive across examples, making it interpretable as a sum of individual contributions. It is also the basis for information theory connections.

**Misconception 5: "Cross-entropy loss is different from likelihood"**

No. Cross-entropy loss is exactly negative log-likelihood. They are mathematically equivalent.

**Misconception 6: "We use likelihood because the data is random"**

No. The data already occurred. Likelihood is used because the **model** treats outcomes as random. The randomness is a property of the model's perspective.

</details>

## The Cleanest Mental Model

**Likelihood is the amount of probability the model assigns to the labels that actually occurred, given the inputs, under its current parameters**.

It represents the **agreement between the model and the data**.

## One-Sentence Takeaway

Training a supervised model means adjusting the weights so the model assigns maximal probability to the correct labels in the training data. Likelihood, log-likelihood, cross-entropy, and MLE are mathematically equivalent perspectives on this same objective.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.
