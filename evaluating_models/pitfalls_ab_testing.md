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
