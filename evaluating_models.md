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

*Precision: Out of the items the ranker/classifier predicted to be relevant, how many are truly relevant?

*Recall: Out of the items the ranker/classifier predicted to be relevant, how many were found?


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
*NDCG: Divides the DCG by the perfect DCG






`
