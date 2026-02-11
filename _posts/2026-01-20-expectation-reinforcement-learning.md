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
</style>

When I started learning reinforcement learning, one phrase kept appearing everywhere:

*"The goal of RL is to maximize the expected return."*

At first, I honestly didn't think much of it. I assumed "expected" just meant "average," and I moved on. But the deeper I went, the more that single word started bothering me.

Why expectation? Why not just say "maximize reward"? Why do value functions use expectation? Why does every Bellman equation have this averaging structure? And if the agent eventually learns the best action, why are we still talking about averages at all?

That one word, *expectation*, quietly turned out to be the backbone of everything.

## What I Thought Expectation Was (and Why That Was Incomplete)

My initial mental model was simple: "Expectation is just the mean or average of values that haven't happened yet."

That's not completely wrong, but it's dangerously incomplete.

The more precise idea is this: <span class="tooltip-term">Expectation<span class="tooltip-text">A weighted average of all possible outcomes, where each outcome is weighted by its probability. It represents what we'd get "on average" over infinitely many trials.</span></span> is a weighted average of all possible outcomes, where each outcome is weighted by how likely it is.

If a <span class="tooltip-term">random variable<span class="tooltip-text">A variable whose value is determined by a random process. It can take different values with different probabilities.</span></span> $$X$$ can take values $$x$$ with probabilities $$P(x)$$, then:

$$
E[X] = \sum_x P(x) \cdot x
$$

So yes, it's an average, but it's an average over possibilities, not over already observed samples.

That subtle distinction matters a lot in RL.

## The First Crack in My Intuition: "Is Expectation What I'll Get?"

I remember asking something like: "So if the expected reward is 5.2, does that mean the agent will at least get 5.2?"

The answer was no. And that was a turning point.

Expectation is not what we get in one run. It's what we get on average over many repetitions.

In one <span class="tooltip-term">episode<span class="tooltip-text">A complete sequence of interactions from start to end in an RL environment. For example, one game of chess from first move to checkmate.</span></span>, the agent might get 9. In another, it might get 2. Over many episodes, the average converges toward 5.2.

So expectation is not a guarantee. It's a long-run average under uncertainty.

That immediately explained why expectation even exists in the first place: because the future is uncertain.

## Why Expectation Even Shows Up in RL

This is where things clicked.

In <span class="tooltip-term">reinforcement learning<span class="tooltip-text">A type of machine learning where an agent learns to make decisions by interacting with an environment and receiving rewards. The goal is to learn a policy that maximizes cumulative reward.</span></span>, we're always facing uncertainty:

We don't know which action the <span class="tooltip-term">policy<span class="tooltip-text">A strategy that tells the agent what action to take in each state. It can be deterministic (always same action) or stochastic (probabilistic choice of actions).</span></span> will sample (if it's stochastic). We don't know exactly which next state the environment will produce. We don't know what long-term reward sequence will follow.

So if we ask: "How good is this state?"

There is no single answer. There are many possible futures.

Expectation is how we compress all those futures into one meaningful number.

It's our way of saying: "Given all the things that could happen, and how likely they are, what reward should we expect on average?"

## Where Expectation First Appears: The Value Function

This was the first formal place expectation stopped being abstract and became concrete.

The <span class="tooltip-term">state-value function<span class="tooltip-text">A function V(s) that tells us how good it is to be in state s. It represents the expected total future reward starting from that state and following a given policy.</span></span> is defined as:

$$
V^\pi(s) = E\left[\sum_{t=0}^{\infty} \gamma^t r_t \;\Big|\; s_0 = s, \pi\right]
$$

In words: the value of a state is the expected total future reward if we start in that state and follow policy $$\pi$$.

At first, I wondered: "Is this expectation just for the next step or for reaching the final goal?"

The answer was: both.

It includes immediate reward, plus all future rewards, compressed into a single expected number.

The <span class="tooltip-term">discount factor<span class="tooltip-text">A number γ (gamma) between 0 and 1 that reduces the value of future rewards. γ=0.9 means a reward next step is worth 90% of the same reward now. It makes closer rewards more valuable than distant ones.</span></span> $$\gamma$$ ensures that distant rewards matter less than immediate ones, making the infinite sum finite and well-behaved.

## The Line of Code That Forced Me to Understand Expectation

Then I saw this line during <span class="tooltip-term">value iteration<span class="tooltip-text">An algorithm that repeatedly updates value estimates for each state until they converge to the true values. It's a dynamic programming method for solving MDPs.</span></span> or policy evaluation:

```python
new_v += action_prob * (r + gamma * V[next_s])
```

I asked: "Is this expected value immediate?"

The clarification was subtle but crucial.

$$r$$ is the immediate reward. $$V(\text{next}_s)$$ already represents all future reward after that step. $$\gamma$$ discounts the future. `action_prob` means we're averaging over what action might be taken.

So that single line is literally:

$$
V^\pi(s) = \sum_a \pi(a|s) \left[ r(s,a) + \gamma V^\pi(s') \right]
$$

Which is: "The value of this state is the expected value of immediate reward plus expected future value, averaged over all actions we might take."

That's the <span class="tooltip-term">Bellman equation<span class="tooltip-text">A recursive equation that expresses the value of a state in terms of immediate reward plus the discounted value of the next state. It's the foundation of most RL algorithms.</span></span>: expectation in code form.

## My Next Confusion: "But Where Do the Probabilities Come From?"

At this point, something else bothered me: "How do we even get these probabilities if we haven't observed the future?"

This turned out to split RL into two worlds.

**Model-based RL**

If we have or learn a model of the environment, then we explicitly estimate:

$$P(s'|s,a)$$, the <span class="tooltip-term">transition probability<span class="tooltip-text">The probability of ending up in state s' after taking action a in state s. This is part of the environment's dynamics.</span></span>

$$R(s,a)$$, the expected reward

Then expectation is literal: we multiply outcomes by probabilities.

**Model-free RL**

If we don't have a model, we don't know those probabilities.

So what do we do? We estimate expectations from samples.

Each experience is one draw from the unknown distribution. Over many samples, the average converges toward the true expectation.

So expectation never disappears. It just becomes <span class="tooltip-term">empirical<span class="tooltip-text">Based on observed data rather than theoretical calculation. Instead of computing E[X] analytically, we approximate it by averaging actual samples.</span></span> instead of analytic.

## The Big Mistake I Made About "Best Actions"

At some point I said something like: "But once the agent learns, it just takes the best action, right? So why do we still talk about expectation?"

This was mixing two different ideas.

Yes, after learning, the policy may become nearly deterministic.

But: the environment can still be <span class="tooltip-term">stochastic<span class="tooltip-text">Random or probabilistic. A stochastic environment means the same action in the same state can lead to different outcomes.</span></span>. Rewards can still vary. Returns can still fluctuate.

So even a deterministic policy still has a distribution over outcomes.

That means value is still an expectation.

So expectation isn't just for exploration. It's baked into how we define "how good something is."

## Q-Learning and the Phrase That Confused Me Most

This definition bothered me for a long time:

$$Q^*(s,a)$$ = expected return if we start in $$s$$, take action $$a$$, and then act optimally forever after.

I remember thinking: "How can it say 'act optimally thereafter' when we don't know the optimal policy yet?"

That felt circular.

The clarification that fixed it: that definition describes what $$Q^*$$ *means*, not how we compute it.

During learning, we don't actually act optimally afterward. We pretend we will by using:

$$
Q(s,a) \leftarrow r + \gamma \max_{a'} Q(s', a')
$$

That <span class="tooltip-term">max term<span class="tooltip-text">Taking the maximum Q-value over all possible next actions. This represents the assumption that we'll act optimally in the future.</span></span> is our current best guess of what optimal behavior looks like.

So <span class="tooltip-term">Q-learning<span class="tooltip-text">A model-free RL algorithm that learns the optimal action-value function Q* directly. It uses the max over next actions to bootstrap value estimates.</span></span> is still expectation-based, just bootstrapped through max instead of averaging over a policy.

## Expectation Shows Up Again in Policy Optimization

Then I moved from value-based methods to <span class="tooltip-term">policy gradients<span class="tooltip-text">A family of RL algorithms that directly optimize the policy by computing gradients of expected return with respect to policy parameters.</span></span>.

And expectation showed up again, in a new disguise.

The objective is:

$$
J(\theta) = E_{\tau \sim \pi_\theta}[R(\tau)]
$$

Which literally means: "Maximize the expected return over <span class="tooltip-term">trajectories<span class="tooltip-text">A sequence of states, actions, and rewards: (s₀, a₀, r₀, s₁, a₁, r₁, ...). It's one complete path through the environment.</span></span> generated by our policy."

We're no longer estimating values. We're directly optimizing expected return.

Same idea. Different object.

## How Likelihood Quietly Re-Entered the Picture

This part surprised me.

In supervised learning, we maximize <span class="tooltip-term">likelihood<span class="tooltip-text">The probability the model assigns to the observed data. Maximizing likelihood means finding parameters that make the observed outcomes most probable.</span></span>:

$$
\max_\theta \sum_i \log P_\theta(y_i | x_i)
$$

In policy gradients, we maximize expected return — but the gradient looks like:

$$
\nabla_\theta J(\theta) = E\left[\nabla_\theta \log \pi_\theta(a|s) \cdot \text{return}\right]
$$

So what are we really doing?

We're increasing the likelihood of actions that produced high returns — in expectation.

That connected likelihood, log-likelihood, and RL in a way I didn't expect.

## Advantage: Expectation as a Baseline

Another thing that finally made sense only after expectation clicked:

$$
A(s,a) = Q(s,a) - V(s)
$$

$$V(s)$$ is what we expect to get on average from this state. $$Q(s,a)$$ is what we got (on average) by taking this action.

So <span class="tooltip-term">advantage<span class="tooltip-text">How much better (or worse) a specific action is compared to the average action in that state. Positive advantage means the action is better than average.</span></span> is: "How much better was this action compared to what we normally expect from here?"

That's expectation again, now being used as a baseline to reduce variance in our estimates.

## Model-Based Planning and Expectation

Then I looked at <span class="tooltip-term">MPC (Model Predictive Control)<span class="tooltip-text">A planning method that uses a learned model to simulate future trajectories, then picks the action sequence with the best predicted outcome.</span></span>.

In MPC, we: simulate many possible futures, compute total rewards for each, and pick the action sequence with the best average outcome.

That is literally expectation over imagined rollouts.

And when MPC fails in the real world, it's usually because: the model's expectations are wrong, small errors compound, and the planner exploits model flaws.

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

## Where We Tend to Overthink

Sometimes the confusion comes from thinking too deeply about something that's actually straightforward. Here are places where I've overthought things (and you might too):

**Overthinking: "Is expectation some deep mathematical concept I need measure theory to understand?"**

The simple truth: For most of RL, it's just weighted averages. Sum up (probability × value) for each possible outcome. That's it. The fancy notation $$E[\cdot]$$ just means "average over possibilities."

**Overthinking: "If the environment is deterministic, does expectation disappear?"**

The simple truth: Not necessarily. Even with a deterministic environment, if our policy is stochastic, we still have uncertainty over which actions we'll take. Expectation handles that. And even with both deterministic, we might still use expectation over initial states or other sources of randomness.

**Overthinking: "Does the agent actually compute expectations during learning?"**

The simple truth: Usually no. The agent collects samples and updates estimates. The expectation is what those estimates *converge to* over time, not something explicitly calculated. It's the target, not the method.

**Overthinking: "Is the Bellman equation saying something profound about time?"**

The simple truth: It's just saying "value now = reward now + discounted value later." It's a recursive definition, not a philosophical statement. The profundity comes from how useful this decomposition is, not from hidden depth.

**Overthinking: "Why do we need both V(s) and Q(s,a)? Aren't they redundant?"**

The simple truth: They answer different questions. V asks "how good is this state?" Q asks "how good is this state-action pair?" They're related ($$V(s) = \sum_a \pi(a|s) Q(s,a)$$), but each is more convenient in different algorithms.

**Overthinking: "If Q-learning uses max instead of expectation, is it not really about expectation?"**

The simple truth: The max is just how we define "optimal." We're still computing the expected return — but under the assumption that future actions will be the best ones. Expectation is still there; we're just being optimistic about future behavior.

## Common Misconceptions

Let's address some frequent sources of confusion:

**Misconception 1: "Expected return means the return I should expect to get"**

Partially true, but misleading. Expected return is the long-run average. In any single episode, we might get much more or much less. It's a statistical property, not a guarantee.

**Misconception 2: "Value functions predict what will happen"**

No. Value functions predict what will happen *on average*. They compress many possible futures into one number. The actual future might be very different from the expected value.

**Misconception 3: "Model-free RL doesn't use expectations"**

Wrong. Model-free RL absolutely uses expectations — it just estimates them from samples instead of computing them analytically. The target is still the expected return; we're just approximating it empirically.

**Misconception 4: "Once we have the optimal policy, we don't need expectations anymore"**

No. Even the optimal value function is defined as an expectation. Optimality doesn't remove uncertainty from the environment; it just tells us how to act best given that uncertainty.

**Misconception 5: "The discount factor is just a trick to make the math work"**

Partially true, but it also has real meaning. It encodes how much we care about future vs. immediate rewards. $$\gamma = 0.99$$ means we're patient; $$\gamma = 0.9$$ means we're more short-sighted. It's a design choice with real consequences.

**Misconception 6: "Policy gradients are fundamentally different from value-based methods"**

Not as different as they seem. Both are ultimately about maximizing expected return. Value-based methods do it by estimating values and acting greedily. Policy gradients do it by directly adjusting action probabilities. Same goal, different paths.

## The Cleanest Mental Model

Here's what to memorize: **expectation in RL is how we summarize uncertain futures into actionable numbers**.

Every time we see $$E[\cdot]$$, we're saying: "We don't know exactly what will happen, but here's what we'd get on average across all possibilities."

Value functions, Q-functions, policy objectives, advantages — they're all built on this single idea.

## One-Sentence Takeaway

Expectation in reinforcement learning is not a math trick. It's the language we use to talk about long-term reward under uncertainty.

Once that clicked, the rest of RL stopped feeling like magic and started feeling inevitable.

---

**Note:** This blog post was written as a learning exercise. AI tools were used to help polish the writing and clarify explanations, but the concepts, questions, and understanding reflected here are my own. These posts document my learning journey through machine learning fundamentals.
