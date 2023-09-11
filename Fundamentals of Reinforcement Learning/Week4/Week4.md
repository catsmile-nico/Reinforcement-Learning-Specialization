# Dynamic Programming
Involves using the Bellman equations and knowledge of the environment dynamics (denoted as p) to compute value functions and optimal policies. It does not require direct interaction with the environment and is based on a model of the Markov Decision Process (MDP).

## Policy Evaluation and Control
Reinforcement Learning involves two key tasks: policy evaluation and control.  
Control is the ultimate goal of reinforcement learning, but policy evaluation is often a necessary initial step to assess the quality of a policy.  
Policy evaluation assesses policy quality, control aims to improve policies, and dynamic programming methods are used to solve these tasks when the environment dynamics are known.

__Policy evaluation__  
Focuses on determining the value function for a specific policy, representing how good that policy is.  

__Control__  
Is the task of improving a policy(by producing a strictly better policy) to obtain as much reward as possible.   
We can try to improve policies to get better policies until it is no longer possible, in other words getting the optimal policy deems the control task complete.

## Iterative Policy Evaluation

Iterative policy evaluation is a fundamental technique in dynamic programming for solving Markov Decision Processes (MDPs) and is used to compute value functions that represent the expected number of steps until termination from a given state. It allows for the efficient estimation of state values under a specified policy.

__Key steps of iterative policy evaluation__

1. Initialize two arrays, V and V prime, with values typically set to zero.
2. Repeatedly perform sweeps through the state space, updating state values using the Bellman equation as an update rule.
3. Continue sweeping until the maximum change (delta) in the value function becomes smaller than a predefined threshold (theta).
4. Once the value function stops changing significantly (delta < theta), it has converged to the value function for the given policy.


## Policy Improvement

__Policy Improvement Theorem__  
states that if a new policy (Pi prime) selects actions with greater or equal values than the current policy (Pi) in every state, then Pi prime is at least as good as Pi. If Pi prime's actions have strictly greater values in at least one state, it is strictly better than Pi. This theorem allows us to construct better policies based on existing ones.

## Policy Iteration
Policy iteration alternates between two steps: policy evaluation and policy improvement. It starts with an initial policy (Pi 1) and iteratively evaluates it to obtain the state values (V Pi 1). Then, it uses the Policy Improvement Theorem to create a better policy (Pi 2) by acting greedily with respect to V Pi 1. This process continues, generating a sequence of improved policies, until the policy no longer changes, signifying the discovery of the optimal policy.


## Generalized Policy Iteration

### Flexibility of the Policy Iteration Framework
Generalized policy iteration provides flexibility while maintaining optimality guarantees. It allows for interleaving policy evaluation and policy improvement in various ways. One specific algorithm within this framework is value iteration. 

__Value iteration__  
involves sweeping over all states and improving the policy iteratively without completing policy evaluation. Instead, it updates the state value function directly based on the action that maximizes the current value estimate. This process continues until a termination condition, typically based on a small value change, is met. Value iteration converges to the optimal value function, which can then be used to derive the optimal policy.

__Synchronous and Asynchronous dynamic programming methods__  

__Synchronous methods__  
systematically sweep the entire state space in each iteration, which can be time-consuming for large state spaces. 
__Asynchronous methods__
in contrast update states in any order, potentially updating some states more frequently than others. 
To ensure convergence, asynchronous algorithms must continue to update all states, even though they update them in a non-systematic order. This flexibility allows them to propagate value information efficiently and can be advantageous in certain scenarios.

### Efficiency of Dynamic Programming
Dynamic programming's efficiency comes from its ability to use value estimates of successor states to improve the current estimate, known as bootstrapping. Policy iteration guarantees the discovery of optimal policies in polynomial time, making it exponentially faster than exhaustively searching through policy space. In practice, dynamic programming often converges quickly, as policy evaluations tend to change less with each iteration.

__Monte Carlo Sampling__  
An alternative method for policy evaluation. Involves gathering a large number of returns under a policy and taking their average to estimate state values. However, this approach can be computationally expensive and require many returns for each state due to the randomness inherent in actions and state transitions.

__Brute Force-Search__  
An alternative method for finding an optimal policy. This method evaluates every possible deterministic policy one at a time and selects the one with the highest value. However, the number of deterministic policies can be exponential in the number of states, making this approach impractical for complex problems.

__Advantages of Dynamic Programming and Bootstrapping__  
Dynamic programming allows for more efficient policy evaluation by leveraging value estimates of successor states to improve the current estimate. This process is known as bootstrapping and is more efficient than Monte Carlo methods that estimate each value independently. Policy iteration, a dynamic programming method, is guaranteed to find the optimal policy in polynomial time, making it exponentially faster than brute force-search.

### Use of approximate dynamic programming and reinforcement learning to address high-dimensional resource allocation problems

In this scenario, we have a single truck driver starting in Texas, and they are presented with four different loads of freight, each bound for different destinations. The main goal is to choose the most profitable load to transport. Here's a step-by-step breakdown of how the decision-making process unfolds:

1. __Initial State__: The truck driver begins in Texas and is brand new to the job. At this point, their estimate of the downstream value of all destinations is zero since they have no prior experience.

2. __Load Evaluation__: The driver evaluates each of the four available loads based on their respective payouts. For example, the load heading to New York offers a reward of $450.

3. __Load Selection__: The driver selects the load with the highest immediate payout. In this case, they choose the load going to New York because it offers the most significant reward.

3. __Updating Value Estimates__: Before moving, the driver updates their estimate of the value of being in Texas. This update reflects the payout they will receive for transporting the chosen load to New York. So, they update the value of being in Texas to $450.

4. __Repeat Process__: The driver repeats this process as they move to New York. They evaluate various loads available in New York, considering their payouts and the updated value of being in New York.

5. __Value Iteration__: The driver iteratively selects and transports loads, updating their value estimates at each location based on the rewards earned. This process continues until a termination condition is met or they reach a point where the most profitable load is in a different location.

6. __Optimal Load Selection__: Eventually, the driver arrives at a decision based on the updated value estimates. For example, they might choose a load bound for California over returning to Texas because it offers a higher payout.

7. __Updating Values Again__: The driver updates their value estimate for the current location (e.g., California) and repeats the process as they evaluate loads available there.

8. __Iterative Process__: This iterative process of evaluating loads, updating value estimates, and making decisions continues as the driver travels to various destinations.

9. __Smoothing Factor__: To update value estimates, the driver uses a smoothing factor (e.g., 0.1) and a learning rate step size. This ensures that the estimates gradually incorporate new information without drastic changes.

The key insight in this simplified scenario is that the driver uses their value estimates to make decisions at each step, taking into account the rewards they expect to receive. By iteratively updating these estimates and selecting the most promising loads, they aim to maximize their overall earnings.