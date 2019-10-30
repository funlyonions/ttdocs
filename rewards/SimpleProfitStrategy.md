# Simple Profit Strategy

A reward strategy that rewards the agent for profitable trades and prioritizes trading over not trading.

## Class Parameters
None

## Functions
Below are the functions that the `SimpleProfitStrategy` uses to effectively operate. 

## Private

None

## Public

* `reset` - Reset variables
  * Necessary to reset the last purchase price and state of open positions
  * Variables it resets
    * `_purchase_price` - The price the bot purchased the asset
    * `_is_holding_instrument` - A boolean that shares with the get_reward function if we're currently holding onto a trade. 
* `get_reward` - Returns the reward for the given action
  * The `5^(log_10(profit))` function simply slows the growth of the reward as trades get large.

