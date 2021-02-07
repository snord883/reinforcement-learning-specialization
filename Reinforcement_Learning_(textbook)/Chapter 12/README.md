# __Eligibility Traces__


## **Eligibility Traces**
- When TD methods are augmented with eligibility traces, they produce a family of methods spanning a spectrum that has Monte Carlo methods at one end ("=1) and one-step TD methods at the other ("=0). In between are intermediate methods that are often better than either extreme method.
- The mechanism is a short-term memory vector, the *eligibility trace* **z***t*, that parallels the long-term weight vector **w***t*. The rough idea is that when a component of wt participates in producing an estimated value, then the corresponding component of **z***t* is bumped up and then begins to fade away. Learning will then occur in that component of **w***t* if a nonzero TD error occurs before the trace falls back to zero. The trace-decay parameter λ => [0, 1] determines the rate at which the trace falls.
- Advantages over n-step methods:
    1. Only a single trace vector is required rather than a store of the last n feature vectors.
    2. Learning also occurs continually and uniformly in time rather than being delayed and then catching up at the end of the episode.
        - In addition learning can occur and affect behavior immediately after a state is encountered rather than being delayed n steps.

## **The λ-return**
- *Compound updates*: An update that averages simpler component updates.
    - A compound update can only be done when the longest of its component updates is complete.
    - Example: mixing half of a two-step return and half of a four-step return, has the diagram shown to the right.
    - *λ-return*: <br>
    ![alt_text](../images/lambda-return.JPG 'image')
    - The one-step return is given the largest weight, 1 − λ; the two-step return is given the next largest weight, (1−λ)λ; the three-step return is given the weight (1−λ)λ^2; and so on. The weight fades by λ with each additional step. After a terminal state has been reached, all subsequent n-step returns are equal to the conventional return, Gt.
    ![alt_text](../images/lambda-return-graph.JPG 'image')
    ![alt_text](../images/forward-view.JPG 'image')

## **TD(λ)**
- TD(λ) improves over the offline λ-return algorithm in three ways.
    1. It updates the weight vector on every step of an episode rather than only at the end.
    2. Its computations are equally distributed in time rather than all at the end of the episode.
    3. It can be applied to continuing problems rather than just to episodic problems.
- The eligibility trace vector is initialized to zero at the beginning of the episode, is incremented on each time step by the value gradient, and then fades away by
γλ <br>
![alt_text](../images/td-lambda.JPG 'image')
- The weight vector is a long-term memory, accumulating over the lifetime of the system.
- The eligibility trace is a short-term memory, typically lasting less time than the length of an episode.
    - Keeps track of which components of the weight vector have contributed, positively or negatively, to recent state valuations, where “recent” is defined in terms of γλ.
![alt_text](../images/backward-view.JPG 'image')
- At each moment we look at the current TD error and assign it backward to each prior state according to how much that state contributed to the current eligibility trace at that time.
    - Where the TD error and traces come together, we get the update given weight, changing the values of those past states for when they occur again in the future.
- Different values of **λ**
- λ = 0:
    - TD(0) => the one-step semi-gradient TD
        - The case in which only the one state preceding the current one is changed by the TD error.
- 0 < λ < 1:
    - More of the preceding states are changed, but each more temporally distant state is changed less because the corresponding eligibility trace is smaller.
        - Earlier states are given less *credit* for the TD error.
- λ = 1:
    - The algorithm is also known as TD(1).
    - Monte Carlo behavior
    - Then the credit given to earlier states falls only by γ per step.
        - If γ = 1, then the eligibility traces do not decay at all with time. (undiscounted)

## **n-step Truncated λ-return Methods**
- *Truncated TD(λ)* (aka **TDD(λ)**): Introduce n-step to terminate contining cases.

## **Redoing Updates: Online λ-return Algorithm**
- *n* should be large so that the method closely approximates the offine λ-return algorithm, but it should also be small so that the updates can be made sooner and can influence behavior sooner.
    - To get the best of both (albeit at the cost of computational complexity)
        - On each time step as you gather a new increment of data, you go back and redo all the updates since the beginning of the current episode.

## **True Online TD(λ)**
![alt_text](../images/triangle.JPG 'image')
- One row of this triangle is produced on each time step. It turns out that the weight vectors on the diagonal, the wtt, are the only ones really needed. The first, w00, is the initial weight vector of the episode, the last, wTT , is the final weight vector, and each weight vector along the way, wtt, plays a role in bootstrapping in the n-step returns of the updates. In the final algorithm the diagonal weight vectors are renamed without a superscript, wt .= wtt. The strategy then is to find a compact, efficient way of computing each wtt from the one before. If this is done, for the linear case in which ˆv(s,w) = w>x(s), then we arrive at the true online TD(") algorithm:
![alt_text](../images/online-td.JPG 'image')

## ***Dutch Traces in Monte Carlo Learning**

## **Sarsa (λ)**
![alt_text](../images/sarsa-lambda.JPG 'image')

## **Variable λ and γ**
- each time step will have a different λ and γ, denoted λt and γt.

## ***Off-policy Traces with Control Variates**

## **Watkins’s Q(λ) to Tree-Backup(λ)**
![alt_text](../images/watsons-q.JPG 'image')

## **Stable Off-policy Methods with Traces**
