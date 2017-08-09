# Offline Evaluation Mechanisms


Consider we are still in the prototype phase, where we're 
tweaking everything, from features to types of model and training methods.

## Prototyping Phase: Training, Validation, Model Selection

For every tweak we get a new model.
From all the available models we chose the *right* one, 
by looking at the **validation results** (and not the *training results*).

We split the dataset into:

* **Training dataset**: used to train, find the parameters, of our model
* **Validation dataset**: used to validate how good our model is

As an **output of the validation dataset** we can tune the **hyperparameters** 
of our model and repeat the process.

**Why splitting the dataset?** To essentially avoid overfitting, we want the
2 datasets to be statistically independent.

The error coming from the validation is a proxy of the *generalization error*.

### How to split the datasets

* **Hold-out validation**: First chunk of data is training, second is training
* **K-fold cross validatiom**: We split in K chinks.
* **Bootstrap resampling**: We take small chunks at distincts parts of the 
dataset and create a new one.


#### Hold-out Validation

It's straightforward to implement computationally.
Usually the validation results come from a smaller set of data, which gives a 
less reliable estimate of the generalization error.

**Not good for small datasets**


#### Cross-Validation

Note that this is not the same as hyperparameter tunning.
This validation technique is more expensive than the hold-out validation.
There are different ways of doing cross-validation, the most commont on is k-fold
cross-validation:

* For a given set of hyperparameters each of the `k` datasets takes turns in being
the validation dataset. **the overall performance is the average** of the k individual 
performances.

A specific case (and extreme one ) is the *leave-one-out cross validation*, 
where k is equal to the number of points of the data set.

**Costly but good for very small datasets**

#### Bootstrap and Jackknife

We create multiple datsets by sampling from a single dataset.
With multiple datasets we will have multiple estimates for the parameters
we can use things like the variance and confidence interval for the estimate.

As opposed to cross validation Boostrap *allows for replacement*, this is essentially 
to make sure that we're sampling from the **same empirical distribution**.

The usage is similar to the cross-validation

### Difference between Validation and Testing

Validation is a part of the **prototyping phase**, once a model is picked we
have the *last part of prototpying* which is to train a new model with the
**best hyperparameters** on the  **whole dataset**. 

**After** we have this best model training we go into **evaluation** where 
the model is **actually tested** againts *test* or *real* data in production (on-line).










