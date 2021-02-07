# __Off-policy Methods with Approximation__


## **Off-policy Methods with Approximation**
- *Off-policy*: we seek to learn a value function for a *target policy*, given data due to a different *behavior policy b*.

## **Semi-gradient Methods**
- per-step importance sampling ratio: <br>
![alt_text](../images/sampling-ratio.JPG 'image')

## **Examples of Off-policy Divergence**
- Note that the importance sampling ratio, p*t*, is 1 on this transition because there is only one action available from the first state, so its probabilities of being taken under the target and behavior policies must both be 1. In the final update above, the new parameter is the old parameter times a scalar constant, 1 + α(2γ − 1). If this constant is greater than 1, then the system is unstable and w will go to positive or negative infinity depending on its initial value. Here this constant is greater than 1 whenever γ > 0.5. Note that stability does not depend on the specific step size, as long as α > 0. Smaller or larger step sizes would a↵ect the rate at which *w* goes to infinity, but not whether it goes there or not.
- Each time there is a transition from the w state to the 2w state, increasing w, there would also have to be a transition out of the 2w state. That transition would reduce *w*, unless it were to a state whose value was higher (because γ < 1) than 2w, and then that state would have to be followed by a state of even higher value, or else again *w* would be reduced.

## **The Deadly Triad**
- *The Deadly Triad*:
    - If any two elements of the deadly triad are present, but not all three, then instability can be avoided.
    1. **Function approximation**: A powerful, scalable way of generalizing from a state space much larger than the memory and computational resources (e.g., linear function
        approximation or ANNs).
        - Most clearly cannot be given up.
    2. **Bootstrapping**: Update targets that include existing estimates (as in dynamic programming or TD methods) rather than relying exclusively on actual rewards and
        complete returns (as in MC methods).
        - Doing without bootstrapping is possible, at the cost of computational and data efficiency
    3. **Off-policy training**: Training on a distribution of transitions other than that produced by the target policy. Sweeping through the state space and updating all states uniformly, as in dynamic programming, does not respect the target policy and is an example of off-policy training.
        - On-policy methods are often adequate.
            - Except: The agent learns not just a single value function and single policy, but large numbers of them in parallel.

## **Linear Value-function Geometry**
- We assume that its true value function, v, is too complex to be represented exactly as an approximation.
    - If v cannot be represented exactly, what representable value function is closest to it?
        - we need a measure of the distance between two value functions.
            - *Bellman error*: If an approximate value function v*w* were substituted for v*π*, the difference between the right and left sides of the modified equation could be used as a measure of how far o↵ vw is from v*π*
                - The Bellman error is the expectation of the TD error. <br>
            ![alt_text](../images/bellman-error.JPG 'image') <br>
            - **μ**: the degree to which we care about di↵erent states being accurately valued <br>
            ![alt_text](../images/geometry-distance-formula.JPG 'image') <br>
            ![alt_text](../images/geometry-distance-graph.JPG 'image')

## **Gradient Descent in the Bellman Error**
- *naive residual-gradient*: 
    - converges robustly, it does not necessarily converge to a desirable place <br>
    ![alt_text](../images/naive-residual-gd.JPG 'image')
- *Residual-gradient*: 
    - the equation below involves the next state, S*t+1*, appearing in two expectations that are multiplied together. To get an unbiased sample of the product, two independent samples of the next state are required, but during normal interaction with an external environment only one is obtained. One expectation or the other can be sampled, but not both.
    ![alt_text](../images/residual-gd.JPG 'image')
- Three (3) convergence of the residual-gradient method is unsatisfactory
    1. Slow
    2. Converge to the wrong values
    3. Next section

## **The Bellman Error is Not Learnable**
- Bellman error objective (BE) is not learnable
- The VE is not learnable, but the parameter that optimizes it is!
    - One error that is always observable is that between the value estimate at each time and the return from that time
        - *Mean Square Return Error*: denoted RE, is the expectation, under μ, of the square of this error <br>
        ![alt_text](../images/msre.JPG 'image')


![alt_text](../images/learnable.JPG 'image')


## **Gradient-TD Methods**

## **Emphatic-TD Methods**

## **Reducing Variance**


