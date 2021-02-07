# __Dynamic Programming__

- *Dynamic Programming* - refers to the collection of algorithms that can be used to compute optimal policies given a perfect model of the environment

## **Policy Evaluation (Prediction)**
- *Policy evaluation* - how to compute the state-value function for an arbitrary policy.

## **Policy Improvement**
- The process of making a new policy that improves on an original policy, by making it greedy with respect to the value function of the original policy.

## **Policy Iteration**
![alt_text](../images/policy-iteration.JPG 'Paragraph about policy iteration')
![alt_text](../images/policy-evaluation-function.JPG 'policy evaluation')

## **Value Iteration**
- *Value Iteration* - Is when *policy evaluation* is stopped after one sweep <br>
![alt_text](../images/value-evaluation-function.JPG 'policy evaluation')
- Drawback to *policy interation*, requires multiple sweeps through the state set. Figure 4.1, suggests that it may be possible to truncate *policy evaluation* to the first three iterations
![alt_text](../images/policy-evaluation.JPG 'policy evaluation')
- Like *policy evaluation*, *value interation* formally requires infinite number of iterations to converge to v*. In practice, we stop once the value function changes by only a small amount in a sweep.

## **Asynchronous Dynamic Programming**
- Drawback to the DP methods is they involve operations over the entire state set of the MDP.
    - Backgammon has over 10^20 states. At a million/second it would still take over 1,000 years for a single sweep
- *Asynchronous Dynamic Programming* - update values of states in any order whatsoever, using whatever values of other states happen to be available.

## **Generalized Policy Iteration**
- *Policy Interation*
    - *Policy Evaluation*: Making the value function consistent with the current policy
    - *Policy Improvement*: Making the policy greedy with respect to the current value function <br>
![alt_text](../images/gpi.JPG 'generalized policy interation')
- If both, the evaluation process and improvement process stabilize, no longer produce change, then the value function and policy must be optimal
    - Making the policy greedy with respect to the value functions makes the value function inconsistent with the changed policy
    - Making the value function consistent with the policy typically makes it that the policy is no longer greedy
![alt_text](../images/gpi-compete.JPG 'generalized policy interation')