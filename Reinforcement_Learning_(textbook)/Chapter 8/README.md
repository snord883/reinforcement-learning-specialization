# __Planning and Learning with Tabular Methods__

## **Planning and Learning with Tabular Methods**
- *Model-based methods*: 
    - Dynamic programming and Heuristic search
    - Rely on *planning* as their main component
        - *Planning*: Any computational process that takes a model as input and produces or improves a policy for interacting with the modeled environment
- *Model-free methods*:
    - Monte Carlo and Temporal-difference
    - Rely on *learning*  as their main component

## **Models and Planning**
- *Model*:
    - *Environment*: Anything that an agent can use to predict how the environment will respond to its actions.
        - Given a state and action, a model produces a prediction of the resultant next state and next rewards (each with some probability of occuring)
    - *Distribution models*: Produce a description of all possibilities and their probabilities
    - *Sample models*: produce just one of the possibilities, sampled according to their probabilities 

## **Dyna: Intergrated Planning, Acting, and Learning**
- Planning agent roles for real experience
    1. improve the model to make it more accurately match the real environment (*model-learning* or *indirect reinforcement learning*)
        - Often achieve a better policy with fewer environmental interactions
    2. Direcly improve the value function and policy (*direct reinforcement learning*)
        - Much simpler and not affected by biases in the design of the model<br>

![alt_text](..\images\direct-rl.JPG 'image')

- *Dyna*
    - Includes all methods:
        - Planning: random-sample one-step tabular Q-planning
            - Only samples from state-action pairs that have been previously experienced; model is never queried with a pair with no information
        - Acting: 
        - Model-learning: Table-based and assumes the model is deterministic (meaning no randomness is involved in the determining of future states)
        - Direct RL: one-step tabluar Q-learning
    - n=0 is a nonplanning agent ==> uses only *direct RL*

![alt_text](..\images\dyna-Q.JPG 'image')
![alt_text](..\images\dyna-q-example.JPG 'image')
![alt_text](..\images\dyna-q-example-explained.JPG 'image')

## **When the Model Is Wrong**
- We want the agent to explore to find changes to the environment, but not so much that the performance is greatly degraded.
- Dyna-Q+ agent:
    - Keeps track for each state-action pair of how many time steps have elapsed since the pair was last tried in a real interaction with the environment.
        - The more time that has elapsed, the greater (we presume) that the dynamics of this pair has changed and the model is incorrect
    - "Bonus reward" - to encourage behavior that tests long-untried actions
    ![alt_text](..\images\bonus-reward.JPG 'image')

- Maze shifts. Model takes some time to learn new path
![alt_text](..\images\change-in-env.JPG 'image')

- Maze introduces a shortcut, but the model has already learned the previous path. It'll either take a long time to learn the new path or may never recognize it.
![alt_text](..\images\change-in-env-shortcut.JPG 'image')


## **Prioritized Sweeping**
- In the previous Dyna agents, simulated transitions are started in state-action pairs selected uniformily randomly from all previously experienced pairs.
    - Uniformily is not usually the best approach,
        - this means a lot of pointless actions are considered since they take the agent from one zero-value state to another
    - Search focusing on working *backward* from "goal-state"
        - "goal-state": is just a special. In general we want to work backward not just from goal-state, but from any state whose value has changed. (As in the maze examples)
    - *Backward focusing* is the term for this general idea
- *Prioritized Sweeping*: is a reinforcement learning technique for model-based algorithms that prioritizes updates according to a measure of urgency, and performs these updates first. A queue is maintained of every state-action pair whose estimated value would change nontrivially if updated, prioritized by the size of the change. When the top pair in the queue is updated, the effect on each of its predecessor pairs is computed. If the effect is greater than some threshold, then the pair is inserted in the queue with the new priority.
    - Limitation: Uses *expected* updates

## **Expected vs Sample Updates**
- *Expected*: Considering all possible events that might happen
    - Better estimate, because they are uncorrupted by sampling error
    - More computationally expensive
- *Sample*: Considering single sample of what might happen
- In practice, the computation required by update opertations is usually dominated by the number of state-action pairs at which *Q* is evaluated.
    - *Branching Factor*: the number of possible next states, *s'*
    - Then *expected* update requires roughly *b* time the computation as *sample* update <br>
    ![alt_text](..\images\expected-vs-sample.JPG 'image')

## **Trajectory Sampling**
- Exhaustive sweeps: implicitly devote equal time to all parts of the state space rather than focusing where it is needed (Used most often in practice)
- *Trajectory sampling*: to distribute updates according to the on-policy distribution (the current policy being observed)
    - Focusing on the on-policy distribution could be beneficial because it cast vast, uninteresting parts of the space to be ignored
    - Or it could be detrimental because it causes the same old parts to be updated over and over <br>
    ![alt_text](..\images\on-policy-vs-uniform.JPG 'image')
    ![alt_text](..\images\on-policy-vs-uniform-v2.JPG 'image')

## **Real-time Dynamic Programming (RTDP)**
- *RTDP*: The on-policy trajectory sampling version of the value-iteration algorithm of DP.
- Is an example of *asynchronous* DP algorithm
    - Algorithms not organized in terms of systematic sweeps of the state set; they update state values in any order whatsoever, using whatever values of other states that happen to be available.
- RTDP converges with a probability one to a policy that is optimal for all relevant states provided:
    1. the initial value of every goal state is zero
    2. there exists at least one policy guarantees that a goal state will be reached with probability one from any start state
    3. all rewards for transactions from non-goal states are strictly negative
    4. all initial values are equal to or greater than their optimal values
- Known as *stocastic optimal path problems*: usually stated in terms of cost minimization (rather than reward maximimization)

## **Planning at Decision Time**
- Planning can be used in 2 ways
    1. *Background planning*: Using planning to gradually improve a policy or value function on the basis of simulated experience obtained by a model
    2. *Decision-time planning*: Here planning focuses on a particular state

## **Heuristic Search**
- *Heuristic Search*: For each state encountered, a large tree of possible continuations is considered. The approxiamate value function is applied to the leaf node and back up the current state. Once the backed-up values of the nodes are computed, the best of them is chosen as the current action, and then all backed-up values are discarded.
    - High computation if many branches
    - To resolve, simply reduce the number of steps ahead it looks (obviously the more the steps ahead the closer to optimal it'll chose) <br>
    ![alt_text](..\images\heuristic-search.JPG 'image')

## **Rollout Algorithm**
- *Rollout Algorithms*: Decision-time planning based on Monte Carlo applied to simulated trajectory that all begin at the currect environment state.
    - Estimate action values for a given policy by averaging the returns of many trajectories that start with each possible action

## **Monte Carlo Tree Search**
- Is executed after encountering each new state to select the agent's action for that state; it is executed again to select the action for the next state; and so on.
- Continues to repeat these 4 steps until no time is left or computational resources exhausted:
    1. Selection: Starting from the root node, traverse the tree to select a leaf node.
    2. Expansion: On some of the iterations (depending on details of the application), the tree is expanded from the selected leaf node by adding one or more child nodes reached from the selected node via unexplored actions.
    3. Simulation: From the selected node (or newly-added child nodes), simulation of a complete episode is run with actions selected by the rollout policy. (Result is a MC trail with actions selected from first tree policy and then beyond the tree rollout policy)
    4. Backup: The return is used to update the action values. (No values of the states or the actions saved beyond the tree)
- Moves to the selected state and starts again. <br>
![alt_text](..\images\mc-tree-search.JPG 'image')


## **PART 1 ENDS:**

![alt_text](..\images\part-1-diagram.JPG 'image')