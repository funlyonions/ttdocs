# Reward Strategy

A rewards are a means of determining how to tell the Agent if it's progressing and doing a good job, or doing a bad job. 

Ultimately the agent creates a sequence of actions to maximize its total reward over a given time. The RewardStrategy is an abstract class that encapsulates how to tell the trading bot in tensortrade if it's trading positively or negatively. The same methods will be called each time for each step, and we can directly swap out strategies. 


## Properties and Setters

* `exchange` - The central exchange for the strategy.
  * The exchange being used by the current trading environment. Setting the exchange causes the strategy to reset.

## Methods

* `get_reward` - Gets the reward for the RL agent.
  * Returns a float corresponding to the benefit earned by the action taken this timestep.
* `reset` - Resets the current state if the reward has a state.
  * Optionally implementable method for resetting stateful strategies.