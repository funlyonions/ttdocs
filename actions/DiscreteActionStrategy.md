# DiscreteActionStrategy

Simple discrete strategy, which calculates the trade amount as a fraction of the total balance.

## Key Variables

* `instrument_symbols`
  * The exchange symbols of the instruments being traded.
* `actions_per_instrument`
  * The number of bins to divide the total balance by. Defaults to 20 (i.e. 1/20, 2/20, ..., 20/20).
* `max_allowed_slippage_percent`
  * The maximum amount above the current price the strategy will pay for an instrument. Defaults to 1.0 (i.e. 1%).


## Setters & Properties

Each property and property setter.

* `dtype`
  * A type or str corresponding to the dtype of the `action_space`.
* `exchange`
  * The exchange being used by the current trading environment.
  * This will be set by the trading environment upon initialization. Setting the exchange causes the strategy to reset.
* `action_space`
  * The shape of the actions produced by the strategy. This takes in a `gym.space` and is different for each given strategy.

## Functions

* `reset`
  * Optionally implementable method for resetting stateful strategies.
* `get_trade`
  * Get the trade to be executed on the exchange based on the action provided.
  * Usually this is the way we distill the information generated from the `action_space`.
  
## See `DiscreteActionStrategy` in Action

```py
from tensortrade.actions import DiscreteActionStrategy

action_strategy = DiscreteActionStrategy(n_actions=20,
                                         instrument_symbol='BTC')
```