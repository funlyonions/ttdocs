# FractionalDifference

A transformer for differencing values within a feature pipeline by a fractional order.




## Class Parameters
* `columns`
  *  A list of column names to difference.
* `difference_order`
  * The fractional difference order. Defaults to 0.5.
* `difference_threshold`
  * A type or str corresponding to the dtype of the `observation_space`.
* `inplace`
  * If `False`, a new column will be added to the output for each input column.

## Functions

Below are the functions that the `InstrumentExchange` uses to effectively operate. 

### Private

* `_difference_weights`
  * Gets the weights for ...
* `_fractional_difference`
  * Computes fractionally differenced series, with an increasing window width.

### Public

* `transform_space`
  * Get the transformed output space for a given input space.
* `transform`
  * Apply the pipeline of feature transformations to an observation frame.
* `reset`
  * Resets the history of the standard scaler.


See `FractionalDifference` in action:

```py
from tensortrade.features import FeaturePipeline
from tensortrade.features.stationarity import FractionalDifference
price_columns = ["open", "high", "low", "close"]
difference_all = FractionalDifference(difference_order=0.6) # fractional difference is seen here
feature_pipeline = FeaturePipeline(steps=[difference_all]) 
exchange.feature_pipeline = feature_pipeline
```