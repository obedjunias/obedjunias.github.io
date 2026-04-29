---
layout: post
title: "Expectation in Reinforcement Learning: The Way It Finally Made Sense to Me"
date: 2026-01-20 10:00:00-0400
description: A personal journey through understanding why expectation is everywhere in RL, from value functions to policy gradients, and why it's not just a math trick
tags: machine-learning reinforcement-learning probability
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

In reinforcement learning, a central phrase often appears:

*"The goal of RL is to maximize the expected return."*

Often, "expected" is casually interpreted as "average." However, this single word is the structural foundation of the entire framework.

Why rely on expectation rather than simply maximizing reward? Why do value functions use expectation? Why does every Bellman equation feature this averaging structure? Even when an agent learns an optimal policy, expectation remains central.

## Defining Expectation in Reinforcement Learning

A simplistic view defines expectation as merely the mean or average of future values.

This definition is incomplete.

The more precise idea is this: <span class="tooltip-term">Expectation<span class="tooltip-text">A weighted average of all possible outcomes, where each outcome is weighted by its probability. It represents what we'd get "on average" over infinitely many trials.</span></span> is a weighted average of all possible outcomes, where each outcome is weighted by how likely it is.

If a <span class="tooltip-term">random variable<span class="tooltip-text">A variable whose value is determined by a random process. It can take different values with different probabilities.</span></span> $$X$$ can take values $$x$$ with probabilities $$P(x)$$, then:

$$
E[X] = \sum_x P(x) \cdot x
$$

It is an average over possibilities, not over already observed samples.

That subtle distinction dictates the structure of reinforcement learning algorithms.

## Expectation vs. Guaranteed Return

If an expected reward is 5.2, it does not guarantee the agent will receive 5.2 in a given run.

Expectation is not a guarantee for a single execution. It is the theoretical mean over infinite repetitions.

In one <span class="tooltip-term">episode<span class="tooltip-text">A complete sequence of interactions from start to end in an RL environment. For example, one game of chess from first move to checkmate.</span></span>, the agent might get 9. In another, it might get 2. Over many episodes, the average converges toward 5.2.

Expectation evaluates a long-run average under uncertainty.

## The Role of Expectation in RL

In <span class="tooltip-term">reinforcement learning<span class="tooltip-text">A type of machine learning where an agent learns to make decisions by interacting with an environment and receiving rewards. The goal is to learn a policy that maximizes cumulative reward.</span></span>, an agent faces persistent uncertainty:

- The action the <span class="tooltip-term">policy<span class="tooltip-text">A strategy that tells the agent what action to take in each state. It can be deterministic (always same action) or stochastic (probabilistic choice of actions).</span></span> will sample (if it is stochastic) is uncertain.
- The next state the environment will produce is uncertain.
- The long-term reward sequence is uncertain.

So if evaluating: "How good is this state?"

There is no single deterministic answer. There are many possible futures.

Expectation compresses all those possible futures into one meaningful mathematical evaluation.

It answers: "Given all the things that could happen, and how likely they are, what reward should be expected on average?"

## Expectation in the Value Function

The <span class="tooltip-term">state-value function<span class="tooltip-text">A function V(s) that tells us how good it is to be in state s. It represents the expected total future reward starting from that state and following a given policy.</span></span> is defined as:

$$
V^\pi(s) = E\left[\sum_{t=0}^{\infty} \gamma^t r_t \;\Big|\; s_0 = s, \pi\right]
$$

In words: the value of a state is the expected total future reward if starting in that state and following policy $$\pi$$.

This expectation evaluates both the immediate step and reaching the final goal.

It includes the immediate reward, plus all future rewards, compressed into a single expected number.

The <span class="tooltip-term">discount factor<span class="tooltip-text">A number γ (gamma) between 0 and 1 that reduces the value of future rewards. γ=0.9 means a reward next step is worth 90% of the same reward now. It makes closer rewards more valuable than distant ones.</span></span> $$\gamma$$ ensures that distant rewards impact the calculation less than immediate ones, making the infinite sum finite and well-behaved.

## Expectation in the Bellman Equation

Consider this update line during <span class="tooltip-term">value iteration<span class="tooltip-text">An algorithm that repeatedly updates value estimates for each state until they converge to the true values. It's a dynamic programming method for solving MDPs.</span></span> or policy evaluation:

```python
new_v += action_prob * (r + gamma * V[next_s])
```

$$r$$ is the immediate reward. $$V(\text{next}_s)$$ already represents all expected future reward after that step. $$\gamma$$ discounts the future. `action_prob` averages the outcome over the possible actions.

This algorithm implements the standard evaluation:

$$
V^\pi(s) = \sum_a \pi(a|s) \left[ r(s,a) + \gamma V^\pi(s') \right]
$$

This states: "The value of this state is the expected value of immediate reward plus expected future value, averaged over all actions that might be taken."

That is the <span class="tooltip-term">Bellman equation<span class="tooltip-text">A recursive equation that expresses the value of a state in terms of immediate reward plus the discounted value of the next state. It's the foundation of most RL algorithms.</span></span>: expectation applied recursively.

## Where Do the Probabilities Come From?

A common question is: "How are these probabilities obtained if the future has not been observed?"

This divides RL into two primary paradigms.

**Model-based RL**

If a model of the environment is available or learned, the process explicitly estimates:

$$P(s'|s,a)$$, the <span class="tooltip-term">transition probability<span class="tooltip-text">The probability of ending up in state s' after taking action a in state s. This is part of the environment's dynamics.</span></span>

$$R(s,a)$$, the expected reward

Then expectation is literal: we multiply outcomes by probabilities.

**Model-free RL**

If we don't have a model, we don't know those probabilities.

So what do we do? We estimate expectations from samples.

Each experience is one draw from the unknown distribution. Over many samples, the average converges toward the true expectation.

So expectation never disappears. It just becomes <span class="tooltip-term">empirical<span class="tooltip-text">Based on observed data rather than theoretical calculation. Instead of computing E[X] analytically, we approximate it by averaging actual samples.</span></span> instead of analytic.

## Optimal Actions and Expectation

A common misconception assumes that once an optimal policy is learned, expectation is no longer relevant because the agent simply takes the "best" action.

This conflates two different concepts.

Yes, after learning, the policy may become nearly deterministic.

However, the environment can still be <span class="tooltip-term">stochastic<span class="tooltip-text">Random or probabilistic. A stochastic environment means the same action in the same state can lead to different outcomes.</span></span>. Rewards can still vary. Returns can still fluctuate.

Even a deterministic policy operates over a distribution of possible outcomes.

Therefore, value remains an expectation. Expectation is not merely a tool for exploration; it is mathematically baked into the definition of value.

## Q-Learning and the Assumption of Optimality

Consider the standard definition of the optimal action-value function:

$$Q^*(s,a)$$ = expected return if we start in $$s$$, take action $$a$$, and then act optimally forever after.

A frequent point of confusion is how the definition assumes optimal future actions before the optimal policy is actually known.

This definition establishes the theoretical target for $$Q^*$$, not the computational mechanism.

During learning, Q-learning approximates this future optimality using the max operator:

$$
Q(s,a) \leftarrow r + \gamma \max_{a'} Q(s', a')
$$

That <span class="tooltip-term">max term<span class="tooltip-text">Taking the maximum Q-value over all possible next actions. This represents the assumption that we'll act optimally in the future.</span></span> is the current best estimate of optimal future behavior.

So <span class="tooltip-term">Q-learning<span class="tooltip-text">A model-free RL algorithm that learns the optimal action-value function Q* directly. It uses the max over next actions to bootstrap value estimates.</span></span> is still expectation-based, but it bootstraps through the max operator instead of averaging over an explicit policy distribution.

## Expectation in Policy Optimization

In policy optimization methods like <span class="tooltip-term">policy gradients<span class="tooltip-text">A family of RL algorithms that directly optimize the policy by computing gradients of expected return with respect to policy parameters.</span></span>, the objective is defined directly in terms of expectation:

$$
J(\theta) = E_{\tau \sim \pi_\theta}[R(\tau)]
$$

This translates to: "Maximize the expected return over <span class="tooltip-term">trajectories<span class="tooltip-text">A sequence of states, actions, and rewards: (s₀, a₀, r₀, s₁, a₁, r₁, ...). It's one complete path through the environment.</span></span> generated by the current policy."

The focus shifts from estimating value functions to directly optimizing expected return.

## Connecting Expectation and Likelihood

In supervised learning, models are trained to maximize <span class="tooltip-term">likelihood<span class="tooltip-text">The probability the model assigns to the observed data. Maximizing likelihood means finding parameters that make the observed outcomes most probable.</span></span>:

$$
\max_\theta \sum_i \log P_\theta(y_i | x_i)
$$

In policy gradients, the goal is to maximize expected return, resulting in a gradient that looks like this:

$$
\nabla_\theta J(\theta) = E\left[\nabla_\theta \log \pi_\theta(a|s) \cdot \text{return}\right]
$$

This formulation structurally ties RL to supervised learning: the algorithm increases the likelihood of actions that produced high returns, evaluated in expectation.

## Advantage as an Expectation Baseline

Expectation also serves as a baseline in Advantage calculations:

$$
A(s,a) = Q(s,a) - V(s)
$$

$$V(s)$$ is the expected return from the current state. $$Q(s,a)$$ is the expected return after taking a specific action.

The <span class="tooltip-term">advantage<span class="tooltip-text">How much better (or worse) a specific action is compared to the average action in that state. Positive advantage means the action is better than average.</span></span> evaluates: "How much better is this specific action compared to the general expectation for this state?"

Expectation acts as a critical baseline to reduce variance in gradient estimates.

## Model-Based Planning

In <span class="tooltip-term">MPC (Model Predictive Control)<span class="tooltip-text">A planning method that uses a learned model to simulate future trajectories, then picks the action sequence with the best predicted outcome.</span></span>, the algorithm simulates many possible futures, computes total rewards for each trajectory, and selects the action sequence yielding the highest average outcome.

This is an explicit calculation of expectation over simulated rollouts.

When MPC fails in deployment, it is often because the model's computed expectations are inaccurate, causing compounding errors that the planner exploits.

So again: expectation is powerful, but only as good as the model behind it.

## The Final Mental Model That Stuck

This is the single sentence that made everything feel coherent:

**Expectation is how an agent reasons about the future when it cannot know exactly what will happen.**

Whenever we see $$E[\cdot]$$ in RL, we can read it as: "Average over all the things that could happen, weighted by how likely they are."

And that single idea explains: value functions, Bellman equations, Q-learning, policy gradients, advantage, likelihood, planning, and model-based vs model-free RL.

Everything.

---

**That's the core explanation!** If you've made it this far and the main concepts are clear, you're done. What follows are supplementary sections addressing common confusions and mental traps. Useful for solidifying understanding, but not essential for grasping the fundamentals.

---

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Where We Tend to Overthink</h2></summary>

**Overthinking: "Is expectation some deep mathematical concept I need measure theory to understand?"**

For most of RL, expectation is simply a weighted average: sum up (probability × value) for each possible outcome. The notation $$E[\cdot]$$ designates this average over probabilities.

**Overthinking: "If the environment is deterministic, does expectation disappear?"**

Not necessarily. In a deterministic environment, a stochastic policy still introduces uncertainty over actions. Expectation handles this variation. Even if both are deterministic, expectation might still be applied over initial states or other sources of randomness.

**Overthinking: "Does the agent actually compute expectations during learning?"**

Usually, no. In model-free RL, the agent collects samples and updates estimates. The expectation is the theoretical target those estimates *converge to* over time, rather than a value explicitly calculated during each step.

**Overthinking: "Is the Bellman equation saying something profound about time?"**

The Bellman equation provides a recursive decomposition: value now equals reward now plus discounted expected value later.

**Overthinking: "Why do we need both V(s) and Q(s,a)? Aren't they redundant?"**

They answer different questions. V evaluates the state; Q evaluates the state-action pair. They are related via $$V(s) = \sum_a \pi(a|s) Q(s,a)$$, but each is utilized differently depending on the algorithm.

**Overthinking: "If Q-learning uses max instead of expectation, is it not really about expectation?"**

The max operator defines "optimal" behavior. The algorithm still computes the expected return, but under the assumption that future actions will be optimal.

</details>

<details markdown="1">
<summary><h2 style="display: inline-block; vertical-align: middle;">Common Misconceptions</h2></summary>

**Misconception 1: "Expected return means the return I should expect to get"**

Expected return is the long-run theoretical average. In any single episode, the actual return fluctuates. It is a statistical property, not a guarantee.

**Misconception 2: "Value functions predict what will happen"**

Value functions predict what will occur *in expectation*. They compress many possible futures into a single metric. A single trajectory may deviate significantly from the expected value.

**Misconception 3: "Model-free RL doesn't use expectations"**

Model-free RL fundamentally relies on expectations, estimating them empirically from samples rather than computing them analytically.

**Misconception 4: "Once we have the optimal policy, we don't need expectations anymore"**

The optimal value function is still defined as an expectation. Optimality dictates the best actions given environmental uncertainty; it does not eliminate that uncertainty.

**Misconception 5: "The discount factor is just a trick to make the math work"**

The discount factor encodes the relative importance of future versus immediate rewards. A value closer to 1 prioritizes long-term returns, while a lower value prioritizes immediate rewards.

**Misconception 6: "Policy gradients are fundamentally different from value-based methods"**

Both frameworks ultimately maximize expected return. Value-based methods estimate values and act greedily upon them. Policy gradients directly adjust action probabilities to increase expected return.

</details>

## The Cleanest Mental Model

**Expectation in RL is the mathematical mechanism for summarizing uncertain futures into actionable evaluations.**

The notation $$E[\cdot]$$ designates the average outcome across all probabilistic possibilities.

Value functions, Q-functions, policy objectives, and advantages are all constructed upon this foundation.

## One-Sentence Takeaway

Expectation in reinforcement learning provides the mathematical language to evaluate long-term reward under uncertainty.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.
