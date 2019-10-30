# TradingEnvironment
A trading environment made for use with Gym-compatible reinforcement learning algorithms.

It encapsulates everything related to the tensortrade library and runs it so that all parts of the tensortrade library can effectively work with each other. It expects interfaces such as the `ActionStrategy`, `InstrumentExchange`, `RewardStrategy` and `FeaturePipeline`. 

It steps through all of the interfaces in a consistent way, and should not change too often as all other parts of `tensortrade` changes. We're going to go through an overview of the Trading environment below.


## OpenAI Gym Primer

Usually the OpenAI gym runs in the following way:

```py
# Declare the environment
env = TrainingEnvironment()
# Declare and agent with an action_space, usually declared inside of the environment itself
agent = RandomAgent(env.action_space)
reward = 0
done = False

# Reset all of the variables
ob = env.reset() # Gets an observation as a response to resetting the variables
while True:
    # Get an observation, and input the previous reward, and indicator if the episode is complete or not (done). 
    action = agent.act(ob, reward, done)
    ob, reward, done, _ = env.step(action)
    if done:
        break
```

As such, the TradingEnvironment runs largely like this as well.


```py
from tensortrade.environments import TradingEnvironment
from tensortrade.strategies import StableBaselinesTradingStrategy


environment = TradingEnvironment(exchange=exchange,
                                 action_strategy=action_strategy,
                                 reward_strategy=reward_strategy,
                                 feature_pipeline=feature_pipeline)

strategy.environment = environment
test_performance = strategy.run(episodes=1, testing=True)
```


Here you may notice that we don't have the same training code we saw above:

```py
while True:
    # Get an observation, and input the previous reward, and indicator if the episode is complete or not (done). 
    action = agent.act(ob, reward, done)
    ob, reward, done, _ = env.step(action)
    if done:
        break
```

That's because the code to run that exist directly inside of the `TradingStrategy` codebase. The command `run`, has abstractions of that code. Please refer to the Strategies codebase.


## Key Functions:

To better understand what's inside of the `TradingEnvironment`, you should understand the notation. Everything that begins with an underscore `_` is a relatively private function. While everything that doesn't have the underscore is a public facing function. 

* `_take_action` - Determines a specific trade to be taken and executes it within the exchange.
* `_next_observation` - Returns the next observation from the exchange.
* `_get_reward` - Returns the reward for the current timestep.
* `_done` - Returns whether or not the environment is done and should be restarted. The two key conditions to determine if the environment is completed is if either `90% of the funds are lost` or if there are `no more observations left`. 
* `_info` - Returns any auxiliary, diagnostic, or debugging information for the current timestep.
* `step` - Run one timestep within the environment based on the specified action.
* `reset` - Resets the state of the environment and returns an initial observation.
* `render` - This sends an output of what's occuring in the gym enviornment for the user to keep track of.


Almost 100% of the private functions belong in the step function. 