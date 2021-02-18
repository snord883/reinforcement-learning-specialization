# __FOUNDATIONALS OF REINFORCEMENT LEARNING__

## **Policy**
- **Policy**: How an agent selects these actions.
    - *Deterministic Policy*: a policy maps each state to a single action
    - *Stochastic Policy*: is one where multiple actions may be selected with non-zero probability.
        1. The sum over all action probabilities must be 1 for each state
        2. Each action probability must be non-negative. <br>
    ![alt_text](./images/policy-types.JPG 'image')
    - Set of actions can be different for each state
    - It's important that policies **depend only on the current state**, not on other things like time or previous states.
        - The state defines all the information used to select the current action.

    Example:
    -  We might also want to define a policy that chooses the opposite of what it did last, alternating between left and right actions. However, that would not be a valid policy because this is conditional on the last action.
        - Better approach: the last action should be included in the state. <br>
    ![alt_text](./images/policy-rules.JPG 'image')

## **Value Functions**
![alt_text](./images/value-function-graph.JPG 'image')
- **State-value Function**: represents the expected return from a given state under a specific policy. <br>
![alt_text](./images/state-value-function.JPG 'image')
- **Action-value Function**: represents the expected return from a given state after taking a specific action, later following a specific policy.<br>
![alt_text](./images/action-value-function.JPG 'image')

## **Bellman Equations**
![alt_text](./images/state-value-function-bellman.JPG 'image') 

![alt_text](./images/action-value-function-bellman.JPG 'image')

<hr>

## **Optimal Policy**
![alt_text](./images/optimal-policy.JPG 'image')

- Policies can be combined to for another policy (optimal policy) <br>
![alt_text](./images/optimal-policy-combined.JPG 'image')


![alt_text](./images/optimal-policy-example.JPG 'image')


<hr>

## **Bellman Optimality Equations**

- Deterministic optimal policy will assign Probability 1, for an action that achieves the highest value and Probability 0, for all other actions. We can express this another way by replacing the sum over Pi star with a max over a.

State Value Bellman Optimality Equation: <br>
![alt_text](./images/optimal-policy-bellman.JPG 'image')


Action Value Bellman Optimality Equation: <br>
![alt_text](./images/optimal-policy-bellman-action.JPG 'image')

![alt_text](./images/bellman-equations-compared.JPG 'image')

<hr>

## **Using Optimal Value Functions to Get Optimal Policies**
- Choose the next state with the high reward plus discounted next state-value
![alt_text](./images/optimal-policy-exercise1.JPG 'image')
![alt_text](./images/optimal-policy-exercise.JPG 'image')

<hr>

## **Policy Evaluation vs. Control**
- **Policy Evaluation**: is the task of determining the value function for a specific policy.
- **Control**:  is the task of finding a policy to obtain as much reward as possible. In other words, finding a policy which maximizes the value function.

## **Iterative Policy Evaluation**
- Each iteration applies this updates to every state, S, in the state space, which we call a sweep. Applying this update repeatedly leads to a better and better approximation to the state value function v Pi. If this update leaves the value function approximation unchanged, that is, if v_k plus 1 equals v_k for all states, then v_k equals v Pi, and we have found the value function.
![alt_text](./images/policy-evaluation.JPG 'image')

- Two methods for updating the policy:
    1. Using two arrays and making a *sweep* through all of the states to update the *V'*
    2. Using one array, some updates will themselves use new values instead of old. 
        - This single array version is still guaranteed to converge, and in fact, will usually converge faster. (Because it gets to use the updated values sooner.) 
![alt_text](./images/iterative-policy-evaluation2.JPG 'image')
![alt_text](./images/iterative-policy-evaluation.JPG 'image')

<hr>

## **Policy Improvement**
![alt_text](./images/policy-improvement-theorem.JPG 'image')

## **Policy Interation**
![alt_text](./images/policy-iteration.JPG 'image')
![alt_text](./images/policy-iteration2.JPG 'image')

<hr>

## **Generalized Policy Interation**
- *Value iteration*: Sweeps over all the states and greedify with respect to the current value function. However, we do not run policy evaluation to completion. We perform just one sweep over all the states. After that, we greedify again. 
![alt_text](./images/generalized-policy-iteration.JPG 'image')