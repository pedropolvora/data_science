# Hyperparameter Tuning 

Details on how to perform hyperparameter tuning


## Model Parameters Vs Hyperparameters

Given a mathematical expression of a module with certain undefined quantities besides
the experimental data, those undefined quantities are the parameters. E.g `y = ax +b `
if we observe `y` and `x` then `a` and `b` are the model parameters.

*These are the parameters finding with training*

In other advanced models, we might have other parameters which are required for the
computation of the model but are *not* found during the training phase.
These are the **hyperparameters** e.g. the number of clusters (k) in a k-means clustering.

#### What do hyperparameters do ? 

They control the capacity, or degrees of freedom, of a model.
This is very important to get right *to avoid overfitting*.

When you are training a ML model, you're essentially using optimization techniques 
over a loss function. The way you do this optimization might *itself require
hyperparameters*.


## Hyperparameter Tuning Mechanism

Remember that these settings can have a *very large impact* on the overall 
quality of the model.

Different datasets might require different hyperparameters.

Hyperparameter tuning is a meta-optimization task.
This is essentially done by running each model coming from each set of hyperparameters
and compare the performance of the model.

## Hyperparameter Tuning Algorithms

The tuning algorithm for hyperparameters is not the outcome of s closed formula 
as in the case of the optimizaztion of the parameters (think e.g. OLS). We are
optimizing a response surface.

There are, however, algorithms to allows us to do hyperparameter tuning.

#### Grid Search

Picks out a *grid* of hyperparameter values and evaluates every one of them.
It can be exponential or linear or any other scale.

It's simple to set-up and trivial to parallelize. But it's expensive in terms of 
*total* computational time.

#### Random Search

Variation over grid search. Search over random subset points of the entire grid.
It can be shown that with 60 observations you get within 5% of the maximum with 95% 
probability in most conditions.

It's equally simple and easy to parallelize, less precise but cheaper than grid search.

#### Smart Hyperparameter Tuning

From each hyperparameter setting, you choose where to go.
There are different algos for this, and they have even their own parameters.
They might was well differ according with the different type of model we're using.

Some of the most recent optimization methods like these are :

* Derivative-free optimization: employ heuristics e.g. genetic algos, Nelder-Mead method.
* Baysian optimization: modelling the response with another function and sample from there
* Random forest smart tuning: modelling the response with another function and sample from there


## Nested Cross-validation

Model selection can include not only choosing among the best hyperparameters
but also among different *families* of models. But tuning hyperparameters should be 
restricted to only model families.

In the case we're considering different families, we should have a validation set for 
the hyperparameter tuner as well.

So what we do is first look for the best hyperparameters of each family and then compare 
the resulting set of optimal models against each other.


