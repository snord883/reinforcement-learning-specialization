
# __On-policy Prediction with Approxiation__


## **Value-function Approximation**
- *Functional approximation*: Supervised learning methods with numberical outputs.
    - Expect to receive examples of the desired input-output behaviour of the function.
    - Methods that cannot easily handle nonstationarity are less suitable for RL.
        - Most ANN and statistical methods all assume a static training set over which multiple passes are made. In RL, however, it is important that learning be able to occur online, while the agent is interacting with the environment (or model of the environment)

## **The Prediction Objective**
- In the tabular case a continuous measure of prediction quality was not necessary because the learned value function could come to equal the true value function exactly.
    - Values decoupled, update at one didn't impact another.
- By assumption we have far more states than weights, so making one state’s estimate more accurate invariably means making others’ less accurate.
    - Not possible to get exact values for all states
- Need to determine importance of each state by *Mean Squared Value Error* 
    - Often μ(s) is chosen to be the fraction of time spent in s<br>
![alt_text](../images/state-distribution.JPG 'image') <br>
![alt_text](../images/MSE.JPG 'image')

- Let h(s) denote the probability that an episode begins in each state s, and let n(s) denote the number of time steps spent
    1. Probability action *a* occurs, given in proceeding state |*s*
    2. Probability the agent ends up in state *s*, given in proceeding state |*s* and action *a* was taken <br> 
    - If there is discounting (γ < 1) it
should be treated as a form of termination, which can be done simply by including
a factor of γ in the second term
![alt_text](../images/on-policy-distribution.JPG 'image')<br>
![alt_text](../images/state-distribution-equation.JPG 'image')

## **Stochastic-gradient and Semi-gradient Methods**
- *Stocastic Gradient Descent (SGD)*: adjust the weight vector after each example by a small amount in the direction that would most reduce the error
    - Most widely used function approximation learning methods
    - Well suited for online RL
    - *Stocastic*: update is done on only one example <br>
![alt_text](../images/sgd-equation.JPG 'image')

- *Semi-gradient* methods: They include only a part of the gradient
    - One does not obtain the same guarantees if a bootstrapping estimate of v(St) is used as the target Ut if SGD is used
    - They take into account the effect of changing the weight vector wt on the estimate, but ignore its effect on the target

- *State Aggregation*: Is a generalizing function approximation in which states are grouped together, with one estimated value for each group
![alt_text](../images/state-aggregation-graph.JPG 'image')

## **Linear Methods**
- Feature vector **x**(*s*)
- Linear methods approximate state-value function: <br>
![alt_text](../images/linear-function.JPG 'image')

## **Feature Construction for Linear Methods**
- A limitation of the linear form is that it cannot take into account any interactions between features, such as the presence of feature i being good only in the absence of feature j.
    - **Polynomials**: Allow for the introduction of interactions between features
    - **Fourier Basis**: which expresses periodic functions as weighted sums of sine and cosine basis functions (features) of different frequencies
    ![alt_text](../images/poly-vs-fourier.JPG 'image')
    - **Coarse Coding**: Representing a state with features that overlap <br>
    ![alt_text](../images/coarse-coding.JPG 'image')
    ![alt_text](../images/coarse-coding-v2.JPG 'image')
    - **Tile Coding**: In tile coding the receptive fields of the features are grouped into partitions of the state space. Each such partition is called a *tiling*, and each element of the partition is called a *tile*.
        - With just one tiling, we would not have coarse coding but just a case of state aggregation.
        - To get true coarse coding with tile coding, multiple tilings are used, each o↵set by a fraction of a tile width.
        - Exactly one feature is present in each tiling, so the total number of features present is always the same as the number of tilings. (Same for any state)
        - Hyperparameters: number of tilings and shape of the tiles
    ![alt_text](../images/tile-coding.JPG 'image')
    ![alt_text](../images/generalizing-tile-coding.JPG 'image')
    - .
        - *Hashing*: a consistent pseudorandom collapsing of a large tiling into a much smaller set of tiles.
    - **Radial Basis Functions**: Rather than each feature being either 0 or 1, it can be anything in the interval [0, 1], reflecting various *degrees* to which the feature is present.
        - Typical RBF: Gaussian (bell-shaped) response xi(s) dependent only on the distance between the state, s, and the feature’s prototypical or center state, ci, and relative to the feature’s width, sigma
        -Advantage of RBFs over binary features is that they produce approximate functions that vary smoothly and are differentiable.
        ![alt_text](../images/rbf.JPG 'image')

## **Selecting Step-Size Parameters Manually**
- This method works best if the feature vectors do not vary greatly in length; ideally xTx is a constant.
![alt_text](../images/step-size.JPG 'image')

## **Nonlinear Function Approximation: Artificial Neural Networks**
- An ANN with no hidden layers can represent only a very small fraction of the possible input-output functions.
- nonlinearity is essential: if all the units in a multi-layer feedforward ANN have linear activation functions, the entire network is equivalent to a network with no hidden layers (because linear functions of linear functions are themselves linear).
- *Activation Function*: to produce the unit’s output, or activation. 
    - Different activation functions are used, but they are typically S-shaped, or sigmoid, functions such as the logistic function
![alt_text](../images/ann.JPG 'image')
- In reinforcement learning, ANNs can use TD errors to learn value functions, or they can aim to maximize expected reward as in a gradient bandit (Section 2.8) or a policy-gradient algorithm.
    - In the most common supervised learning case, the objective function is the expected error, or loss, over a set of labeled training examples
- *Backpropagation algorithm*: which consists of alternating forward and backward passes through the network.
    - Forward: computes the activation of each unit given the current activations of the network’s input units
    - Backward: efficiently computes a partial derivative for each weight
    - Note: can produce good results for shallow networks having 1 or 2 hidden layers, but it may not work well for deeper ANNs
        1. Overfitting
        2. a. the partial derivatives computed by its backward passes either decay rapidly toward the input side of the network, making learning by deep layers extremely slow
        2. b. the partial derivatives grow rapidly toward the input side of the network, making learning unstable
        - Less of a problem for online RL, with unlimited training data
    - Solutions:
        - *Cross Validation*: stopping training when performance begins to decrease on validation data different from the training data
        - *Regularizatoin*: modifying the objective function to discourage complexity of the approximation
        - *Weight Sharing*: introducing dependencies among the weights to reduce the number of degrees of freedom
        - *Dropout method*: During training, units are randomly removed from the network (dropped out) along with their connections.
        - *Batch Normalization*: adjusting each input variable to have zero mean and unit variance
        - *Deep Residual Learning*: 
        - *Deep Convolutional Networks*: 
        ![alt_text](../images/cnn.JPG 'image')

## **Least-Squares TD (LSTD)**

## **Memory-based Function Approximation**
- Memory-based function approximation methods are very different. They simply save training examples in memory as they arrive (or at least save a subset of the examples) without updating any parameters.
- *Lazy Learning*: Then, whenever a query state’s value estimate is needed, a set of examples is retrieved from memory and used to compute a value estimate for the query state
- Is an example of *nonparametric*: the approximating function’s form is not limited to a fixed parameterized class of functions, such as linear functions or polynomials, but is instead determined by the training examples themselves, together with some means for combining them to output estimated values for query states 
    - *local-learning*: methods that approximate a value function only locally in the neighborhood of the current query state
- Being nonparametric, memory-based methods have the advantage over parametric methods of not limiting approximations to pre-specified functional forms.
    - This allows accuracy to improve with more data accumulated.

## **Kernel-based Function Approximation**
- *Kernel function (aka kernel)*: assign weights to examples s0 and g in the database depending on the distance between s0 and a query states s
    - weights do not have to depend on distances; they can depend on some other measure of similarity between states

## **Looking Deeper at On-policy Learning: Interest and Emphasis**
- *Interest*: the degree to which we are interested in accurately valuing the state (or state–action pair) at time t.
- *Emphasis*: scalar multiplies the learning update and thus emphasizes or de-emphasizes the learning done at time t.

