# __Sample-based Learning Methods__

## **Monte Carlo Methods**
- To use **Dynamic Programming**, the agent *must* know the environment's transition probabilities.
- **Monte Carlo**: estimate values by *averaging* over a large number of random samples
    - Learn directly from interactions.
    - These returns can only be observed at the end of an episode. <br>
    - Monte Carlo methods can estimate the value of an individual state independently of the values of any other states. In dynamic programming, the value of each state depends on the values of other states.
![alt_text](../images/monte-carlo1.JPG 'image')
![alt_text](../images/monte-carlo2.JPG 'image')
![alt_text](../images/monte-carlo3.JPG 'image')


## **Monte Carlo Control**

- To help guarantee state-actions are explored. We can utilize **exploring starts**: 
    - we must guarantee that episodes start in every state-action pair. 
![alt_text](../images/exploring-starts.JPG 'image')
- Problematic:
    - this algorithm must be able to start from every possible State action pair. Otherwise the agent may not explore enough and could converge to a suboptimal solution in many problems. It can be difficult to randomly sample an initial State action pair.
        - For example, how would you randomly sample the initial State action pair for a self-driving car?


## **Exploration Methods for Monte Carlo**
- **ε-soft policy**: 
    - Are always stochastic 
    - Disadvantage of Epsilon soft policies is that they are suboptimal for both acting and learning. Epsilon soft policies are neither optimal policies for obtaining reward nor are the optimal for exploring to find the best actions
![alt_text](../images/soft-greedy.JPG 'image')


## **Off-policy Learning for Prediction**
![alt_text](../images/on-policy.JPG 'image')
![alt_text](../images/off-policy.JPG 'image')
- One key rule of off policy learning is that the behavior policy must cover the target policy? In other words, if the target policy says the probability of selecting an action a given State s is greater than zero then the behavior policy must say the probability of selecting that action in that state is greater than 0
![alt_text](../images/off-policy-rule.JPG 'image')


## **Important Sampling**
![alt_text](../images/important-sampling.JPG 'image')
![alt_text](../images/important-sampling2.JPG 'image')
![alt_text](../images/important-sampling3.JPG 'image')