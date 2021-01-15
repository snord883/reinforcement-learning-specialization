# __REINFORCEMENT LEARNING by Richard S. Sutton & Andrew G. Barto__

## __Elements of Reinforcement Learning__
- **Policy**: Is the mapping from preceived state of the environment to actions to be taken when in those states
    - Could be a simple function or lookup table
    - Could involve an extensive computation
- **Reward signal**: defines the goal of a RL problem.
    - *Reward*: a single number sent to the RL agent after each step
    - The agent's sole objective is to maximize the total *rewards* over the long run
    - defines what are good or bad events 
    - Primary basis for altering the **policy**
        - If an action selected by the policy is followed by a low reward, then the policy may be changed to select some other action in the same situation later.
- **Value function**: 
    - Specifies what is good in the long run (whereas the **reward signal** indicates what's good in the immediate sence)
    - *Value*: the total amount of *reward* an agent can expect to accumulate over the future, starting from that state (*reward* determines the immediate desirability of environmental states)
- **Model** (optional): Something that mimics how the environment will behave
    - *Planning* any means of deciding on a course of action based on possible future situations before they are actually experienced
    - *Model-based* method: RL methods that utilize models/planning
    - *Model-free* method: explicitly trail-and-error (opposite of *planning*)
- **State**: 
    - Formal definition: is given by the framework of the Markov decision process
    - Informal definition: is any data/information available to the agent about the environment 