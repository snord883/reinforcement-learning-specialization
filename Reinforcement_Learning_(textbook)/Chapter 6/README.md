# __Temporal-Difference Learning__

## **Temporal-Difference (TD) Learning**
- Central and novel to reinforcement learning (RL)
- Combination of Monte Carlo and Dynamic Programming ideas
    - MC: Can learn directly learn from raw experience without a model of the environment
    - DP: Updates estimates based in part on other learned estimates, withing waiting for a final outcome (bootstrap)

## **TD Prediction**
- TD: waits only until the end of the next time step and use the observed *reward* to update the estimate
    - Because its update in part is based on an existing estimate, we say it's a *bootstrapping* method, like DP
- TD formula <br>
![alt_text](../images/td-prediction.JPG 'image')
- MC formula   
    - MC: waits until the end of the episode to determine the *return* (only then is G*t* known) <br>
![alt_text](../images/mc-prediction.JPG 'image')


![alt_text](../images/td-vs-mc-example.JPG 'image')
![alt_text](../images/td-vs-mc-graph.JPG 'image')

## **SARSA**

## **Q-Learning**

## **Expected Sarsa**