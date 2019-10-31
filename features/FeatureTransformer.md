# FeatureTransformer

As stated before in the README. We use an Abstract, subclass hierarchy to handle the creation of new assets to be interpreted. The `FeatureTransformer` is an abstract of all columns.

## Properties and Setters

* Get the transformed output space for a given input space.
* Transform the data set and return a new data frame.


## Functions

Below are the functions that the `FeatureTransformer` uses to effectively operate. 

### Private

`None`

### Public

* `reset`
  * Optionally implementable method for resetting stateful transformers.
* `transform_space` 
  * Get the transformed output space for a given input space.
* `transform`
  * Transform the data set and return a new data frame.
