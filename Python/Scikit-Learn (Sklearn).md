# Install 
```python
pip install scikit-learn
```

# Metrics

With this function we can import the params that helps us to get the metrics in the models when we need to verify the accuracy

```python
from sklearn.metrics import ...
```

## Regression Metrics
The more basic metrics that we can use in regression are: **MAE, MSE, $R^2$**. These are metrics that helps to get the accuracy and measure the model through predictions.
### Mean Absolute Error (MAE)
```python
from sklearn.metrics import mean_absolute_error

measure_absolute_error(y_true,y_predict)
```
### Mean Square Error (MSE)
```python
from sklearn.metrics import mean_square_error

measure_square_error(y_true,y_predict) #Squared = False -> RMSE
```
### Coefficient of Determination ($R^2$)
```python
from sklearn.metrics import r2_score

r2_score(y_true,y_predict)
```

## Classification Metrics

In classifications problems, we have more variety to measure the accuracy and compare the values.

### Confusion Matrix 
```python
from sklearn.metrics import confusion_matrix

confusion_matrix(y_true,y_predict)
```

### Accuracy 
```python
from sklearn.metrics import accuracy_score

accuracy_score(y_true,y_predict)
```

### Precision 
```python
from sklearn.metrics import precision_score

precision_score(y_true,y_predict)
```

### Sensitivity/Recall 
```python
from sklearn.metrics import recall_score

recall_score(y_true,y_predict)
```

### F1 Score 
```python
from sklearn.metrics import f1_score

f1_score(y_true,y_predict)
```

### Summary Confusion Matrix
```python
from sklearn.metrics import classification_report

classification_report(y_true,y_predict)
```

## Clustering Metrics

In clustering problems, we have different functions to measure the accuracy and compare the values. This metrics are something similar because the rudimentary of this score is the longitude among points. 

### Adjusted Rand Index 
```python
from sklearn.metrics import adjusted_rand_score

adjusted_rand_score(labels_true,labels_predicted)
```

### Fowlkes Mallow Score 
```python
from sklearn.metrics import folwkes_mallow_score

folwkes_mallow_score(labels_true,labels_predicted)
```

### Silhouette 
```python
from sklearn.metrics import silhouette_score

silhouette_score(x,labels_predicted)
```

### Calinski Harabasz Index 
```python
from sklearn.metrics import calinski_harabasz_score

calinski_harabasz_score(x,labels_predicted)
```

# Regressions

## Linear Models:

### Simple:
To simple linear models, we should use:

```python
from sklearn.linear_model import LinearRegression
#First, we should do a instance of this method and add some params if we need to modify the values by default
Lr = LinearRegression(fit_intercept=True/False,...) #Fit intercept means b=0

Lr.fit(x_data,y_data) #Ajust the values and get the 'm' and 'b'
```

**Params:**
```python
Lr.coef_ # <-m
Lr.intercept_ # <-b
```
**Test & Accuracy:**
```python
Lr.score(x,y) # <-R^2
```
**Predict:**
It's helpful to do predictions with a model and compare with a true values
```python
Lr.predict(x)
```

### Multiple:
To Multiple Linear Models we can do the same step that in Simple Linear Model, however in **'X'**, it's **required** to have all the features to do the model.
This method fix to that and return all the params.

### Polinomial:
To this kind of models is required to get started with the values, it's necessary to transform the values.

```python
from sklearn.preprocessing import PolynomialFeatures

Poly = PolynomialFeautures(degree=#) #It's the polynomial grade
```

**Data Transform:**
```python
new_x = Poly.fit_transform(x) #This 'x' is the one we use to do the regression
```

We need to do the same steps than Simple Model after we transform the values. The first value of **Lr.coef_ = 0**. We don't take care about this value.

### Logistic Regression:
Allow us do regressions when there are 2 subsets.

```python
from sklearn.linear_model import LogisticRegression
#First, we instance the model with values by defauld or with a hyperaparams

logreg = LogisticRegression(
							C = ,#Allow to modify the regularization. Low values => Strong Regularization
							penalty = 'l1'|'l2'|'elasticnet'|'none', #specificate the penalty norm
							solver = 'newton-cg'|'lbfgs'|'sag'|'liblinear'|'saga'
							 
)

logreg.fit(x,y)
```

**Params:**
```python
logreg.coef_ # <-m
logreg.intercept_ # <-b
```
**Test & Accuracy:**
```python
logreg.score(x,y) # <-R^2
```
**Predict:**
It's helpful to do predictions with a model and compare with a true values
```python
logreg.predict(x)
logreg.predict_proba(x) # Return the probability
```
**Target Classes:**
```python
logreg.classes_ 
```

### Ridge:

```python
from sklearn.linear_model import Ridge
#We start with a alpha value
ridge = Ridge(alpha= # -> It's a regularization value. More biggest = high regularization
			 )

ridge.fit(x,y)
```

**Params:**
```python
ridge.coef_ # <-m
ridge.intercept_ # <-b
```
**Test & Accuracy:**
```python
ridge.score(x,y) # <-R^2
```
**Predict:**
```python
ridge.predict(x)
```

### Lasso:

```python
from sklearn.linear_model import Lasso
#We start with a alpha value >0, if it's 0, is a Normal Linear Regression 
lasso = Lasso(alpha= # -> It's a regularization value.
			 )
lasso.fit(x,y)
```

**Params:**
```python
lasso.coef_ # <-m
lasso.intercept_ # <-b
```
**Test & Accuracy:**
```python
lasso.score(x,y) # <-R^2
```
**Predict:**
```python
lasso.predict(x)
```

### Elastic Net:
This model follow the same steps that Ridge and Lasso. But this included the **L1 RATIO**, this help to get a better relation. Ridge (0) - Lasso (1)
```python
from sklearn.linear_model import ElasticNet
```

### Decision Tree

```python
from sklearn.tree import DecisionTreeRegressor

tree = DecisionTreeRegressor(
		max_depth # -> Maximum depth that tree can reach
		min_samples_split # -> Minimum number of observations for a nodo can split
		min_samples_leaf # -> Minimum number of observations that should have a children Nodo to split. 
		max_leaf_nodes # -> Maximum number of terminal Nodo
		ccp_alpha # -> It's the value to Prunning
) 

tree.fit(x,y)
```

**Params:**
```python
tree.feature_importances_ # -> Give the value. More bigger, more important
```
**Test & Accuracy:**
```python
tree.score(x,y) # <-R^2
```
**Predict:**
```python
tree.predict(x)
```

### Random Forest

```python
from sklearn.ensemble import RandomForestRegressor

rf = RandomForestRegressor(
		n_estimators # -> Number of tree in the model
		max_depth # -> Depth of each tree
		min_samples_split,min_samples_leaf,min_leaf_nodes,ccp_alpha # -> same that Decision Tree Regressor
		max_features # -> Maximum number of predictors in each split
		oob_score # -> Calculate OUT-OF-BAG R^2. Increase Train Time
		n_jobs # -> Cores number used to train. -1 = All cores
) 

rf.fit(x,y)
```

**Test & Accuracy:**
```python
rf.score(x,y) # <-R^2
```
**Predict:**
```python
rf.predict(x)
```

###  SVR
There are 3 types of SVM that we can use with this library

```python
from sklearn.svm import SVR,NuSVR,LinearSVR
```

- SVR => Regularization with C param
- NuSVR => Regularization with the maximum number of Support Vectors allowed
- LinearSVR => K Lineal model but more faster than SVR

```python
svr = SVR(
		  kernel = 'lineal'|'poly'|'rbf'|'sigmoid'|'precomputed'
		  degree # -> Just when 'poly' is actived. Set the polynomial grade
		  gamma # ->  'poly'|'rbf'|'sigmoid', value or auto
		  C # -> Margin regularization
)

svr.fit(x,y)
```

**Params:**
```python
svr.coef_ # <-m
svr.intercept_ # <-b
```
**Test & Accuracy:**
```python
svr.score(x,y) # <-R^2
```
**Predict:**
```python
svr.predict(x)
```