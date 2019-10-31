# StableBaselinesTradingStrategy

A trading strategy capable of self tuning, training, and evaluating with stable-baselines.

## See **`StableBaselinesTradingStrategy`** in Action

```py
from stable_baselines import PPO2

from tensortrade.strategies import StableBaselinesTradingStrategy

b_strategy = StableBaselinesTradingStrategy(environment=environment,
                                            model=PPO2,
                                            policy='MlpLnLSTMPolicy')
```