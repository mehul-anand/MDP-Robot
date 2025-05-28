# MDP

This project simulates a robot navigating a 3x3 grid using a Markov Decision Process (MDP) and solves it with Q-learning, a reinforcement learning (RL) algorithm. The robot learns to reach a target while avoiding a wall, demonstrating foundational RL concepts applicable to robotics tasks.

- [MDP](#mdp)
  - [Diagram](#diagram)
  - [Basic Setup](#basic-setup)
  - [Implement Q-Learning to Solve the MDP](#implement-q-learning-to-solve-the-mdp)
  - [Analogy](#analogy)
  - [Run the Code](#run-the-code)
    - [Google Colab](#google-colab)

## Diagram
![robot-map](/images/robot.png)

## Basic Setup
**MDP Environment in Gymnasium**

We create a custom Gymnasium environment (`GridWorldMDP`) for a 3x3 grid MDP. The environment defines the following components (see `main.py` for the full implementation):

- **States**: Grid cells $({(0,0), (0,1), (0,2), (1,0), (1,2), (2,0), (2,1), (2,2)})$, excluding the wall at (1,1). Total states: 8.
- **Actions**: Up (0), Down (1), Left (2), Right (3).
- **Transition Probabilities**: 0.8 for the intended direction, 0.1 for each perpendicular direction (adjusted for walls/boundaries).
- **Rewards**: +10 for reaching the target at (2,2), -1 per move, -5 for hitting the wall at (1,1).
- **Termination**: Episode ends when the robot reaches (2,2).

## Implement Q-Learning to Solve the MDP
We use Q-learning, a model-free RL algorithm, to learn the optimal policy by estimating Q-values (expected cumulative rewards) for each state-action pair. Key details:
- **Hyperparameters**:
  - Learning rate $\alpha = 0.1$
  - Discount factor $\gamma = 0.9$ (balancing immediate vs. future rewards)
  - >  In the Q-learning implementation for the 3 x 3 grid MDP, we set $\gamma = 0.9$, meaning a reward received one step in the future is worth 90% of its value, a reward two steps in the future is worth $(0.9)^2 = 0.81$ , and so on.


  - Exploration rate $\epsilon = 0.1$ (epsilon-greedy strategy)
  - Number of episodes = $5000$
  - Maximum steps per episode = $100$
- **Process**: The agent explores the environment, updates Q-values, and learns a policy to navigate from $(0,0)$ to $(2,2)$ while avoiding the wall.


## Analogy
Below is a sample output showing the robot’s path during testing:

![output-ss](/images/output.png)

- `R`: Robot’s position.
- `W`: Wall at $(1,1)$.
- `T`: Target at $(2,2)$.

**MDP Components in the Code**:
- States and actions are defined in the environment.
- Transition probabilities $(0.8, 0.1, 0.1)$ are coded in the `step` method.
- Rewards $(+10, -1, -5)$.
- The discount factor $(\gamma = 0.9)$ is used in Q-learning.
- The policy is learned dynamically via Q-learning and stored in the Q-table.

## Run the Code
### Google Colab
- Copy the code into a Colab notebook and run it directly (plug-and-play).