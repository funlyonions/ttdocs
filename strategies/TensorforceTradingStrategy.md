# TensorforceTradingStrategy

A trading strategy capable of self tuning, training, and evaluating with Tensorforce.


## See **`TensorforceTradingStrategy`** in Action

```py
from stable_baselines import PPO2
from tensortrade.strategies import TensorforceTradingStrategy


agent_spec = {
    "type": "ppo_agent",
    "step_optimizer": {
        "type": "adam",
        "learning_rate": 1e-4
    },
    "discount": 0.99,
    "likelihood_ratio_clipping": 0.2,
}

network_spec = [
    dict(type='dense', size=64, activation="tanh"),
    dict(type='dense', size=32, activation="tanh")
]

a_strategy = TensorforceTradingStrategy(environment=environment,
                                        agent_spec=agent_spec,
                                        network_spec=network_spec)
```