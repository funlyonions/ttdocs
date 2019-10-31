# FeaturePipeline

The feature pipeline has a setup that resembles the keras library. The concept is simple. 

1. We have an observation of data
2. We take the observation and effectively run it through all declared ways of transforming that data and turn the result into a feature space.

## Class Parameters
* `steps` 
  * A list of feature transformations to apply to observations.
* `dtype`
  * The `dtype` elements in the pipeline should be cast to.

## Properties and Setters

* `steps`
  * A list of feature transformations to apply to observations.
* `dtype`
  * The `dtype` that elements in the pipeline should be input and output as.
* `reset`
  * Reset all transformers within the feature pipeline.




## Functions

Below are the functions that the `FeaturePipeline` uses to effectively operate. 

### Private
* `_transform`
  * Utility method for transforming observations via a list of `FeatureTransformer` objects.
  * In other words, it runs through all of the `steps` in a for loop, and casts the response. 

**The code from the transform function:**
As you see, it iterates through every step and adds the observation to the dataframe.
```py
for transformer in self._steps:
    observations = transformer.transform(observations, input_space)
```


### Public

* `reset`
  * Reset all transformers within the feature pipeline.
* `transform_space`
  * Apply the pipeline of feature transformations to an observation frame.

## Feature Pipeline In Action

```py
from tensortrade.features import FeaturePipeline
from tensortrade.features.scalers import MinMaxNormalizer
from tensortrade.features.stationarity import FractionalDifference
from tensortrade.features.indicators import SimpleMovingAverage

price_columns = ["open", "high", "low", "close"]
normalize_price = MinMaxNormalizer(price_columns)
moving_averages = SimpleMovingAverage(price_columns)
difference_all = FractionalDifference(difference_order=0.6)
feature_pipeline = FeaturePipeline(steps=[normalize_price,
                                          moving_averages,
                                          difference_all])

exchange.feature_pipeline = feature_pipeline
```