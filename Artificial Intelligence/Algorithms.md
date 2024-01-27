# Regressions

Generally we use the regression for predicted **Continuous Values**

# Classification

Generally we use the classification for predicted **Categorical Values**

## Binary Classification
### Logistic Regression

	-LG is one of the basic and popular algorithms for solving binary classification problems
	-For each input, logistic regression outputs a probability that this input belongs to the two classes
		* Set a probability threshold boundary that determines which calss the input belongs to
	-Examples:
		*Emails (Spam / Not Spam)
		*Credit Card Transactions (Fraudulent / Not Fraudulent)
		* Loan Default (Yes / No)

This algorithm is based in the Sigmoid equation:

Where:
$$ Z = {1 \over{1+e^{-z}}} $$
Transformation of the linear regression to a logistic regression curve:
$$ Y = {1 \over{1+e^{-(mx+b)}}} $$
the idea of **Sigmoid function** is gives an output probability between 0 and 1. The default probability threshold is set at 0.5 typically. 
	- Class 0 -> Below 0.5
	- Class 1 -> Above 0.5

It’s based in the logarithmic of the probability in function of the event.

We can implement regulations through the hyperparam C, if this is more smaller, more strong is the regulation.

Support simple linear model and multiple linear models, although the target can be binary or multiple.


## Multiclass Classification
