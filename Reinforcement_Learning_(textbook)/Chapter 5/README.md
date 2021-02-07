# __Monte Carlo Methods__

## **Monte Carlo Methods**
- *Monte Carlo Methods*:
    - Do not assume complete knowledge of the environment
    - Requires only *experience*
        - Sample sequences of states, actions, and rewards from actual or simulated interactions with an environment
    - Advantages:
        - Can be used to evaluate a single state without forming estimates for any other states.

## **Monte Carlo Prediction**
- *Visit* - each occurrence of state *s* in an episode
- *First-visit MC* - estimates value of state *s* under policy as the average of the return following the **first** visit to state (*s*)
- *Every-visit MC* - estimates value of state *s* under policy as the average of the return following the **every** visit to state (*s*)
![alt_text](../images/mc-example.JPG 'Example of first-visit monte carlo vs every-visit monte carlo')

## **Monte Carlo Estimation of Action Value**
- If a model is not available, then it is particularly useful to estimate *action values* (the values of state-action pairs)
- If a model is available, then *state values* alone are sufficient to determine the policy
- Essentially the same as for state values (presented above)
    - *Visit* - each occurrence of action *a* taken from state *s* 
    - Complication: 
        - Many *state-action* pairs may never be *visited*; other actions not taken from each state will not improve with experience
        - Solutions:
            - *Exploring starts*: Specifying that the episodes start in a state-action pair, and that every pair has a nonzero probability of being selected as the start

## **Monte Carlo Control**
- Overall idea is proceed according to the same patterns as in generalized policy interation (GPI) <br>
![alt_text](../images/mc-control-diagram.JPG 'image')
![alt_text](../images/mc-control-flow.JPG 'image')

## **Monte Carlo Control without Exploring Starts**
- *On-policy* methods: uses ε-greedy policies. Meaning select greedy action ![alt_text](../images/nonepsilon.JPG 'image') and nongreedy randomly ![alt_text](../images/epsilon.JPG 'image') probability
- *Off-policy* methods: discussed in next section

## **Off-Policy Prediction via Importance Sampling**
- One dilemma control methods face: They seek to learn the action value conditional of *optimal* behavior, but also need to act non-optimally to explore all actions.
- Solution: learn two policies.
    1. *Target Policy (π)* -  the policy being learned
    2. *Behavior Policy (b)* - the policy used to generate behavior (In this case we say that learning is "off" the target policy)
- *Coverage*: In order to use episodes from *b* to estimate values of *π*, it's required that every action taken under *π* is also taken, at least occasionally, under *b*.
- *Importance Sampling*: a general technique for estimating expected values under one distribution given samples of another.
- *Importance-Sampling Ratio*: The relative probability of their trajectories occurring under target and behavior policies.
    - This is applied to *off-policy* learning by weighting the returns according to the *importance-sampling ratio*
![alt_text](../images/importance-sampling-ratio.JPG 'image')
- 
    - 2 approaches for averages:
        1. *Oridinary importance sampling*: simple average
            - Unbound and vary volatile
        2. *Weighted importance sampling*: weighted average
            - produces a weighted average of only the returns consistent with the *target policy*

## **Incremental Implementation**
- For *on-policy* same as chapter 2, but average *returns*; rather than *rewards*
- For *off-policy*:
    - *Ordinary*: returns are scaled by the *importance sampling ratio* and the simply averaged
    - *Weighted*: form weighted average of the return, and slightly different incremental algorithm
        ![alt_text](../images/incremental-implementation-off-policy-weighted.JPG 'image')

## **Discounting-aware Importance Sampling**
- If the discount rate, *γ*, is 0. For an episode with 100 time steps, the return will be G0 = R1, but the importance sampling ratio will be scaled by the entire product. Realy just want the first factor and the other 99 are irrelevant. However they add enormously to its variance.
- *Flat partial returns*:
    - think of discounting as a degree of termination, or probability of termination (1-γ)
        - Step 2: (1-γ)γ
        - Step 3: (1-γ)γ**2 (γ is the probability that termination didn't occur in a previous step)
        - etc.
- *Horizon*: doesn't extend to termination, but instead stop at *h*

## **Pre-decision Importance Sampling**

