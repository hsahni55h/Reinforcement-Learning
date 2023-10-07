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

𝐺𝑡 ≐ 𝑅𝑡+1 + γ𝑅𝑡+2 + γ²𝑅𝑡+3 + …

∑𝑘=0∞ γᵏ𝑅𝑡+k+1

where 𝛾 ∈ [0, 1].

In particular, when we refer to "return," it is not necessarily the case that 𝛾 = 1; and when we refer to "discounted return," it is not necessarily true that 𝛾 < 1.
