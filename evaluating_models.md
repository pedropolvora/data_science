# Evaluating Machine learning models

Notes based on the free OReilly report

* Evaluation metrics are tied to machine learning tasks
  * Classification
  * Regression
  * Ranking


## Classification Metrics 

Classification is about predicting class labels given input data.  We can of course have binary or multi class scenarios. 

#### Accuracy 

``` 
Total = Correct + Incorrect
Accuracy = Correct /Total
```

*Pitfalls*: Accuracy makes no distinctions between classes,  so a correct 1 or a correct 0 is all bundled up.

#### Confusion Matrix 

Yields all the information

``` 
P1 = Predicted as Positive
P0 = Predicted as Negative 
L1 = Labeled as Positive
L0 = Labeled as Negative 

  | P1 | P0
L1| 80 | 20
L0|  5 | 195
``` 
#### Average Per-Class Accuracy 

We can look at the average accuracy per class to have a more detailed info of accuracy. 

Accuracy will be very biased if we have very imbalanced classes. Here , the using the average per-class accuracy is much more useful.

*Pitfalls*:  If one of the classes has very few elements, then the test statistics will have very high variance.


#### Log-Loss

Can be used if the output of the classifier is a probability. It’s a ‘soft’ measurement of accuracy that incorporates the idea of a probabilistic confidence.

```
Log-loss = -1/N Sum(y log p + (1-y) log(1-p) 

p = probability of the point belonging to class 1 
y = observed class ( 0 or 1) 

```
This is also the cross entropy between the distance of the true labels and predictions.

We want to minimise this quantity 


#### AUC

Area under the curve, Receiver Operating Characteristic (ROC) curve.
Plots the rate of true positives to the rate of true negatives.  

Show you how many correct positive classifications can be gained as you allow for more and more false positives. 

## Ranking Metrics 

Ranking is related to binary classification. 

Examples: Search or recommendation engines. 


#### Precision-Recall

* Precision: Out of the items the ranker/classifier predicted to be relevant, how many are truly relevant?

* Recall: Out of the items the ranker/classifier predicted to be relevant, how many were found?


``` 
Precision = #relevant_answers_returned / #total_answers_returned


Recall = #total_correct_answers / #relevant_answers_returned

``` 

We can do precision@k recall@k by considering only the first k items returned.

We can build a precision-recall curve by varying the k 

##### F1 Score

We can combine precision and recall by ther *harmonic mean*:

``` 
F1 = 2 precision*recall/(precision + recall)
``` 

This will tend to smaller of the two elements.  

We want to maximise this variable 

#### NDCG

Normalized Discounted Cumulative Gain. 

* Cumulative Gain:  Sums up the relevance of the top k items 
* Discounted CG: Discounts the items further down the List 
* NDCG: Divides the DCG by the perfect DCG

## Regression Metrics

Predicting numerical values/scores.


#### RMSE 

Root-Mean-Square-Error

```
RMSE = Sqrt(Sum (y_i - y^_i)^2 )/n)
``` 
Where `y_i` denotes the real value and `y^_i` denotes the observed value, 
and we have `n` the number of observations.

*Pitfalls* : Not robust to outliers, note the quadratic term.

#### Quantiles of Errors

Quantiles are much more robust that the mean of a distribution.
They can be used for robust estimatores of performance,

``` 
MAPE = median(|y_i - y^_i) / y_i|)
``` 

We could also use the 90th percentil has a worst case scenario behavior.

#### Almost Correct Predictions 

We can also define the percent of estimates that differ from the true value by `X%`.


#### Training vs Evalutation Metrics

We can use a different loss function  in the training procedure
than for evaluation. This usually happens when you're using a model
for something it was not designed to do.

*It's always better to train a method using the same metric as you'll use for evaluation*


#### Skewed Datasets

Always be on the look out for data skew, i.e., where one kind of data 
is much more rare than others, or when very large or very samll outliers 
could drastically change the metric.

E.g. if we have 99% of data of NOT_SPAM type, then a trivial classifier
that simply puts all the points to NOT_SPAM will have 99% accuracy and a
great ROC.

Note that data skew affects both training and evaluation.

In case of outlies, we should use robust evaluaters (for the evaluation phase).
Effective solutions for large outlies would include reformulating the task.


`
