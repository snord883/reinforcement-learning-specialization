# __FINITE MARKOV DECISION PROCESS (MDP)__

## **The Agent-Environment Interface**
- *Agent* - The learner or decision maker
- *Environment* - The thing the *agent* interacts with (everything outside the *agent*)
- *Markov Property* - The state must include information about all aspects for the past agent-environment interaction that make a difference for the future
    - The probablity of each possible value S*t* and R*t* depends only on the immediately proceeding state and action, S*t-1* and A*t-1*, and not at all on earlier states/actions<br>
![alt_text](../images/agent-env.JPG 'Image of the relationship between the agent and its environment')

## **Goals and Rewards**
- Rewards are a way of communicating to the agent *what* you want to achieve, **not** *how* you want to achieve it 
- Examples:
    - Maze:
        - -1 for every time step that passes prior to escaping; encourages the agent to escape ASAP
    - Recycle robot:
        - +1 for every item gathered
        - -1 for running into person or object
        - -3 for running out of battery
    - Chess:
        - +1 for winning
        - -1 for losing
        - 0 for draw
            - Note: Should not do +1 for capturing opponent's pieces, because the agent could learn to capture more piece yet lose the game

## **Returns and Episodes**
- *Episodes* - A nature notion of final time step, that is, the agent-environment interaction breaks naturally into sequences
    - Ends with a special state called *terminal state*
    - The next episodes begins independently of how the previous one ended
    - *Episodic tasks* - tasks of this kind
    - Examples:
        - plays of a game
        - trips through a maze
- *Continuing tasks* - the agent-environment without a natural break into identifiable episodes
    - Problem: reward the agent is trying to maximize could be infinity
    - Solution:
        - *Discounting* - the agent tries to maximize the expected *discounted return*
            - Agent is "myoptic" if discount rate=0, only cares about immediate reward
![alt_text](../images/discount-return.JPG 'Image of the discounted return function')

## **Unified Notation for Episodic and Continuing Tasks**
- *Absorbing state* - the transition only to itself and that generates only reward of zero. (This is used to have episodic task to mimic continuing tacks)
![alt_text](../images/absorbing-state.JPG 'Image of the absorbing state')
