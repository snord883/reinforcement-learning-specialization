# __MULTI-ARMED BANDITS__

## **A *k*-armed Bandit Problem**
- Faced with a choice amoung *k* different options, or actions
- After each action, numerical reward depending on the action selected
    - *Greedy* actions: the action(s) with the highest estimated *value*
        - This is also know as *exploiting* your current knowledge of the values of the actions
    - *Nongreedy* actions: the actions that are not the highest *value*
        - This is also know as *exploring*, because this enables you to improve your estimate of the nongreedy action's *value*
    - Since it is not possible to *exploit* and *explore* with any one action selection, often referred to as the "conflict" between *exploiting and exploring*
![alt_text](..\images\bandit.JPG 'Image of the simple bandit problem, implemented with an incremental method')

## **Action-value Method**:
- Methods for estimating the values of actions and for using the estimates to make action selection decisions
    - One method for estimating the value is taking the average of rewards actually received:
![alt_text](..\images\action-value-function.JPG 'Image of the action-value function')

## **Incremental Implementation**
- Incremental methods address the issue with action-value methods having to store all rewards
- To save on memory (not having to save each time-step):<br>
![alt_text](..\images\incremental.JPG 'Image of the incremental function')

## **Tracking a Nonstationary Problem**
- The averaging methods discussed so far are appropriate for stationary bandit problems, that is, for bandit problems in which the reward probablities do not change over time.
- Give more weight to recent rewards than long-past rewards.
    - Popular: using a constant step-size parameter (α)<br>
    ![alt_text](..\images\incremental_nonstationary.JPG 'Image of the incremental function for nonstationary problems')

## **Optimistic Initial Values**
- Set the initial Q (estimate value) higher than the actual value, so it encourages initial exploration since the reward from each selected action will be less than the *optimistic inital value*. Eventually converging to actual values.
- Not well suited for nonstationary problems
    - If the task changes, created a need for additional exploration, this method cannot help.

## **Upper-Confidence-Bound (UCB) Action Selection**
- Exploration is needed:
    - greedy action selection ignore exploration
    - ε-greedy action selection with no regard to how likely they are to even produce an optimal reward
- 
![alt_text](..\images\ucb-selection.JPG 'Image of the upper-confidence-bound function selection')
- Upper-Confidence-Bound Selection function:
    - N*t*(*a*) - denotes the number of times that action (*a*) has been selected prior to *t*
        - if =0, then *a* is considered to be a maximizing action
    - *c* > 0: controls the degree of exploration
    - square-root term: measure of the uncertainty or variance in the estimate of *a*'s value
- Explanation:
    - Each time *a* is selected: the uncertainty decreases, because N*t*(*a*) increases in the denominator
    - Eacth time *a* is NOT selected: the uncertainty increase, because *t* increase in the numerator
        - The use of the natural log means the increase gets smaller over time

## **Gradient Bandit Algorithm**
- H*t*(*a*): numerical *preference* for each action *a*
    - *preference*: has no interpretation of the *reward* or *value*
    - the larger the *preference*, the more often that actions is taken
    - Initially all 0, so all actions have the same probability of being selected<br>
    - Increment prefernce:
        - ![alt_text](..\images\preference-baseline.JPG 'preference baseline symbol'): the baseline which the reward is compared
        - reward > baseline: probability of selecting A*t* in the future increases
        - reward < baseline: probability of selecting A*t* in the future decreases
        - Non-selected actions move opposite directions
![alt_text](..\images\softmax-function.JPG 'Image of the function to increment preference')
- π*t*(*a*): probability of taking action (*a*) at time (*t*)<br>
![alt_text](..\images\softmax-function.JPG 'Image of the soft-max function selection')