# Introduction to Sequential Decision-Making

## k-armed Bandit Problem
We have an agent who chooses between "k" actions and receives a reward based on the action it chooses.

[2:42] Action-Values function

__Decision making under uncertainty__
Agents, like doctors in medical trials, face choices with unknown rewards (e.g., different treatments). Their goal is to maximize cumulative rewards despite limited information.

__Action selection__
Involves picking actions (e.g., treatments) that lead to various outcomes (e.g., patient health improvement). Agents aim to select actions that maximize long-term expected rewards.

__Estimating Value of an Action__
"Value" represents an action's expected reward.
This involves determining which action is likely to provide the highest long-term reward.

__Trade-off between exploration and exploitation__
The agent needs to balance between exploring actions to gather more information about their rewards (exploration) while also exploiting the actions that appear to yield the highest rewards based on current knowledge (exploitation).

__Maximizing Reward through Optimization__
The ultimate objective in the k-armed bandit problem is to find an optimal strategy or policy that maximizes the expected cumulative reward over time. This involves repeatedly selecting actions, observing their outcomes, updating value estimates, and adapting the decision-making strategy.

---

## Fundamental concepts of rewards, time steps and values.
Rewards: provide feedback on the desirability of outcomes
Time step: represents the sequential nature of interaction
Value: guide agent's decision-making by estimated the expected cumulative rewards associated with different action

---

## Estimating Action Values

__Estimating action values using the sample-average method__
Action values are initially unknown to the agent.
The sample-average method calculates an average of the rewards received for a particular action providing a way for the agent to approximate the true action values based on collected data.

__Greedy action selection__
A decision-making strategy where the agent chooses the action that currently has the largest estimated value, maximizing immediate rewards by exploiting current knowledge.
In the case of the doctor in the medical trial, this means selecting the treatment that the doctor believes to be the most effective based on the current estimate of treatment values.

__Exploration-exploitation dilemma__
The agent must decide when to explore for potential long-term benefits and when to exploit for immediate rewards, as it cannot do both simultaneously.
Finding the right balance between exploration and exploitation can significantly impact the agent's long-term performance.

__Incremental Implementation to the sample-average method__

[0:50] Incremental update function



$$
Q(A+1) \leftarrow Q(A) + \frac{1}{N(A)} \cdot \left[R(t) - Q(A)\right]
$$

NewEstimate ← OldEstimate + StepSize[Target - OldEstimate]

    Q(A) is the estimated action value for action 'A'.
    N(A) is the number of times action 'A' has been taken.
    R(t) is the reward received at time 't'.

---

## Exploration vs Exploitation Tradeoff

__epsilon greedy__
A simple method to balance exploration and exploitation.
- Parameter ε (positive value between 0 and 1) controls the exploration-exploitation trade-off.
- At each step generate a random number. If number lesser than ε, explore, otherwise exploit.

__how it works__
ε=0, agent performs no exploration steps
ε=0.01, agent occasionally explores new actions, even though it strongly favors exploiting its current knowledge.
ε=0.1, agent explores a broader range of actions more frequently, which can be useful in situations where the environment is complex or uncertain

---

## Optimistic Initial Values
By assuming actions or states are better than they actually are, the agent explores to confirm these optimistic estimates. As it interacts with the environment and receives rewards, it updates its estimates based on real experiences. Over time, as the agent gains more accurate knowledge, the influence of the optimistic initial values diminishes.

__How it encourage early exploration__
This technique is beneficial when there's limited prior knowledge about the environment, ensuring the agent explores sufficiently to discover valuable actions or states early on.

__Limitations__
- Crucial to strike a balance with the degree of optimism to avoid inefficient exploration or convergence issues.
- not well-suited for non-stationary problems
- May not know what the optimistic initial value should be because we don't know the maximum reward

---

## Upper-Confidence Bound (UCB) Action Selection
They choose actions deterministically but promote exploration by favoring actions with fewer samples.

__Driving exploration using uncertainty in estimates__
Calculate the UCB for each action based on two components:

- Expected Value: The agent maintains an estimate of the expected reward or value for each action. It uses this estimate to prioritize actions that seem promising based on past experiences.

- Uncertainty: UCB considers the uncertainty or variance in the estimated values. Actions with higher uncertainty are given a higher UCB, as they are more likely to lead to valuable discoveries.

By selecting the action with the highest UCB, it chooses the action that has the potential to offer the best trade-off between high expected rewards and reducing uncertainty as the process repeats.

As the agent's estimates become more accurate, it shifts towards exploiting the best-known actions while still exploring to gather valuable information.

---

