# The pitfalls of AB testing

A/B testing is a widespread pratice today, but a lto can go wrong in setting up
and interpreting the results.

We will focus on *online* testing, when our models are deployed into production.

## What's A/B testing

We want to test questions like *is my new xxxxx better than the previous one?*. 
We split our traffic/data into two groups **control** (group A) 
and **experiment** (group B).

To decide if Group B performs better than Group A we use statistical hypothesis testing.
*Does my new XXXXX lead to a statistically significant change of my key metric?*

The overview of the process is:
1. Split into randomized control/experiement groups
1. Observe behavior of both groups on the proposed methods.
1. Compute test statistics
1. Compute p-value
1. Output decision

So what could go wrong? Let's see...

## Complete Separation of Experiences 

Are our users really well separated and only experimenting the version they should?

Are our users *permanently trained* by the old version ? There coulde be a
**carryover effect** that would influence the results.

We can do some A/A testing to make sure that the test framework is sane
(there should be no differences).

## Which Metric ?

Ultimately the right metric is the business metric, but this might not be measurable 
by the system.

Here are the basic 4 types of metrics:
* Business Metrics: LTV, CAC ...
* Measurable Live Metrics: Unique visitors, session length ...
* Offline Evaluation Metrics: Accuracy, RMSE ...
* Training Metrics: Loss function in the training

**The key is to make sure that the metric you are (can) use in your A/B testing is
aligned with what you want overall.**

## How Much Change Counts as Real Change? 

Even with everything set-up, when does a change means a real change? It's subjective 
but a good way to fight it is by setting up the value upfront and stick to it.

## One-Sided or Two-Sided

If your test is one-sided it only tests if the change is better without telling you
if it's worse. 
A two-sided test tells if you the change is either better or worse.

## False Positives

In this case a false positive is *rejecting the null hypothesis when
the null hypothesis is true*.

You have to be careful on how many false positives you can take, which depends
on the application. 

False positives are set by the significance level, 
and false negatives by the pwoer of the test.

Make sure they are Ok with the fundamentals of your test.

## How many observations do you need

Defined partially by the statistical power.

A common **anti-pattern** is to do the test until you get a change,
this is very **wrong**.

The power of a test is the ability to correctly identify the positives.
This can be written in a way that outputs a minimum number n of samples you need, upon
specification of power, signficance level and change.


## Is the distribution of the metric gaussian ? 

The vast majority of the A/B tests use the `t-test`.
This test assumes that both populations have a gaussian distribution.

But it could very well be that the distribution is *not* gaussian.

Although in most cases where,
1. The metric is an average,
1. The distribution has one mode,
1. The distribution is symmetric 

we could assume it's gaussian, in pratical terms it's quite possible that these conditions 
are **not** met.

Here are some empirical ways of mitigating the violation:

1. If the metric is nonnegative and has long tail (e.g. a count) take the log transform
1. Alternatively, the family of power transforms tends to stabilize the variance
1. The negative binomial is a better distribution for counts
1. If it's completely different (i.e the histogram) use a test that does not make the Gaussian assumption such as the Mann-Whitney test.

## Are the Variances Equal ? 

Even if both populations are gaussian, it can happen that the variances are not equal.
This could be a consequence of e.g. very different population sizes.

In this case, you should use another test like the **Welch's t-test**.


## What does the p-value mean ?

[read this](http://bactra.org/weblog/1111.html)

**A small p-value does not imply a significant result**

**A smaller p-value does not imply a more significant result**

In addition to running the hypothesis testing and computing the p-value we
**should compute the confidence interval of the two population mean estimates**.
If the distribution is close to being Gaussian the usual standard error estimation applies.
Otherwise, compute a bootstrap estimate.

Basically this should allows to differentiate between
* "There indeed a significant difference between the two populations"
* "I can't tell whether there is a difference because the variances of the estimates are too high"


