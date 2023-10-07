# Introduction

Deep Reinforcement Learning for Robotics is a paradigm shift. 
The basic idea is to start with raw sensor input, define a goal for the robot, and let it figure out, through trial and error, the best way to achieve the goal.
In this paradigm, perception, internal state, planning, control, and even sensor and measurement uncertainty, are not explicitly defined. 
All of those traditional steps between observations (the sensory input) and actionable output are learned by a neural network.

![Intro Reinforcement Learning](images/intro_reinforcement%20learning.png)


# Sparse Rewards in Reinforcement Learning
Say you are an agent, and your goal is to play chess. At every time step, you choose any action from the set of possible moves in the game. Your opponent is part of the environment; she responds with her own move, and the state you receive at the next time step is the configuration of the board, when it’s your turn to choose a move again. The reward is only delivered at the end of the game, and, let’s say, is +1 if you win, and -1 if you lose.

This is an episodic task, where an episode finishes when the game ends. The idea is that by playing the game many times, or by interacting with the environment in many episodes, you can learn to play chess better and better.

It's important to note that this problem is exceptionally difficult, because the feedback is only delivered at the very end of the game. So, if you lose a game (and get a reward of -1 at the end of the episode), it’s unclear when exactly you went wrong: maybe you were so bad at playing that every move was horrible, or maybe instead … you played beautifully for the majority of the game, and then made only a small mistake at the end.

When the reward signal is largely uninformative in this way, we say that the task suffers the problem of sparse rewards. 

- A task is an instance of the reinforcement learning (RL) problem.
- Continuing tasks are tasks that continue forever, without end.
- Episodic tasks are tasks with a well-defined starting and ending point.
  - In this case, we refer to a complete sequence of interaction, from start to finish, as an episode.
  - Episodic tasks come to an end whenever the agent reaches a terminal state.

- Reward hypothesis: All goals can be framed as the maximization of the expected cummulative reward.

- Discounted Return
For an arbitrary time step 𝑡, both refer to:

𝐺𝑡 ≐ 𝑅ₜ₊₁ + γ𝑅ₜ₊₂ + γ²𝑅ₜ₊₃ + …

$$
\sum_{k=0}^{\infty} \gamma^k R_{t+k+1}, \text{ where } \gamma \in [0,1]
$$

In particular, when we refer to "return," it is not necessarily the case that 𝛾 = 1; and when we refer to "discounted return," it is not necessarily true that 𝛾 < 1.

# Markov Decision Process (MDP).

In general, the state space S is the set of all nonterminal states.

In continuing tasks, this is equivalent to the set of all states.

In episodic tasks, we use S⁺ to refer to the set of all states, including terminal states.

The action space A is the set of possible actions available to the agent.

In the event that there are some states where only a subset of the actions are available, we can also use A(s) to refer to the set of actions available in state s ∈ S.


At an arbitrary time step 𝑡, the agent-environment interaction has evolved as a sequence of states, actions, and rewards:

(S₀, A₀, R₁, S₁, A₁, …, Rₜ₋₁, Sₜ₋₁, Aₜ₋₁, Rₜ, Sₜ, Aₜ)

When the environment responds to the agent at time step t+1, it considers only the state and action at the previous time step (Sₜ, Aₜ).

In particular, it does not care what state was presented to the agent more than one step prior. (In other words, the environment does not consider any of S₀, …, Sₜ₋₁.)

And, it does not look at the actions that the agent took prior to the last one. (In other words, the environment does not consider any of A₀, …, Aₜ₋₁.)

Furthermore, how well the agent is doing or how much reward it is collecting has no effect on how the environment chooses to respond to the agent. (In other words, the environment does not consider any of R₀, …, Rₜ.)

Because of this, we can completely define how the environment decides the state and reward by specifying

𝑝(s′, r∣s, a) ≐ 𝑃(Sₜ₊₁ = s′, Rₜ₊₁ = r∣Sₜ = s, Aₜ = a)

for each possible s′, r, s, and a. These conditional probabilities are said to specify the one-step dynamics of the environment.


A Markov decision Process is defined by:
- a (finite) set of states S
- a (finite) set of actions A
- a (finite) set of rewards R
- the one step dynamics of the environment 
    𝑝(s′, r∣s, a) ≐ 𝑃(Sₜ₊₁ = s′, Rₜ₊₁ = r∣Sₜ = s, Aₜ = a) for each possible s′, r, s, and a.
- a discount rate  $$\gamma \in [0,1]$$
