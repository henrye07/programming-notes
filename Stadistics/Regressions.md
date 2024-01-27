# Lineal

$$ Y = a + bX $$

```chart
type: line
labels: [1,2,3,4,5]
series:
  - title: 
    data: [1,2,3,4,5]
tension: 0.2
width: 80%
labelColors: false
fill: false
```

$$
	b= {\sum(x-\bar{x})(y-\bar{y}) \over \sum(x-\bar{x})^2}
$$

$$
 a = \bar{Y} - b \bar{X}
$$

$$
 R^2 = {\sum (Y_p - \bar{Y})^2 \over \sum (Y - \bar{Y})^2}
$$
# Parabolic
$$
 Y = a+bX+cX^2
$$
```chart
type: line
labels: [1,2,3,4,5]
series:
  - title: 
    data: [5,3,1,3,5]
tension: 0.2
width: 60%
labelColors: false
fill: false
```

# Exponential
$$
 Y = a e^{bX}
$$
```chart
type: line
labels: [1,2,3,4,5]
series:
  - title: 
    data: [1,10,20,50,100]
tension: 0.2
width: 60%
labelColors: false
fill: false
```
$$
 ln{Y} = ln{a} + bX 
$$
$$
Y' = a' + bX
$$
$$
b= {n \sum{XY'}-\sum{X}\sum{Y'} \over n \sum{X^2}-(\sum{X})^2}
$$
$$
a = \bar{Y}'-b\bar{X}
$$
# Potential
$$
Y = aX^b
$$
$$
log{Y} = log{a} + b log{X}
$$
$$
Y' = a' + bX'
$$
$$
b= {n \sum{X'Y'}-\sum{X'}\sum{Y'} \over n \sum{X'^2}-(\sum{X'})^2}
$$
$$
a' = \bar{Y}'-b\bar{X}'
$$

# Creciente

$$
Y = {aX \over X+b}
$$
$$
1/Y = {X+b \over aX}
$$
$$
Y' = {{1\over a} + {{b\over a}X'}}
$$

# Logistic Regressions

It’s another kind of regression, it’s more conventional when we want to split the data in 2 subsets

This algorithm is based in the Sigmoid equation:

Where Z= a+bm

It’s based in the logarithmic of the probability in function of the event.

We can implement regulations through the hyperparam C, if this is more smaller, more strong is the regulation

Support simple linear model and multiple linear models, although the target can be binary or multiple

## Regularization

There are models which allow to correction of the errors where the values of the coefficients are too big, pretty features are participating or there are data that do overfitting

### Ridge (reduce the multicolionity)

Add a term for improve the performance of the equation and decrease the variance.

This method penalty the sum of coefficient square root, searching for decrease the variance and increase the bias

If lambda increase, this remove feature

### Lasso

This add the same term of Ridge but penalty the sum of the absolute value of the coefficients

This method allow for some coefficient reach zero.

It’s unstable if there are multicolineality

### Elastic Net

It’s the mixture of Ridge and Lasso, for control the regularity and penalty add the term delta (0-Ridge,1-Lasso)

# Decision Tree

It’s a algorithm which can be used as regressions as classifications.

Consistent in create predictively models which are do with binary rules (Yes/No)

For regressions we have accounted Residual Sum of Square (RSS), which this is possible identify the divisions

How we can’t identify all the possibles partitions of the predictors, we implement the Recursive Binary Splitting

For classification we applied the Classification Error Rate ->

Gino Index quantify the total variance of set

Cross Entropy = Information Gain

It’s the way for quantity the disorder in the system. Less entropy more homogeneous

## Chi-Square

Identify if there are difference between the child nodos and parent nodos

A big value is a big homogeneity in the nodos

If we want to control the size of the tree we can implement methods as: Greedy and Prunning

Prunning: it’s a method to avoid overfitting. One time is create the tree, this is pruning and hold the structure with the less error test.

Some alternatives more complex are: Cost Complex Pruning(penalty the model with ridge or lasso) and Weakest Link Pruning