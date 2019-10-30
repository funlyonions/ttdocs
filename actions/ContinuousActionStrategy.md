# ContinuousActionStrategy

Simple continuous strategy, which calculates the trade amount as a fraction of the total balance.

instrument_symbol: The exchange symbol of the instrument being traded. Defaults to 'BTC'.
max_allowed_slippage: The maximum amount above the current price the strategy will pay for an instrument. Defaults to 1.0 (i.e. 1%).
dtype: A type or str corresponding to the dtype of the `action_space`. Defaults to `np.float16`