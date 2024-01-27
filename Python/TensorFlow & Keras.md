# Setting up TF
- We need to import the library always, if we don't have installed in our system, we need to install first.
```python
import tensorflow as tf
```
## Tensor
* A tensor is a multidimensional arrays (nd-array) with a uniform type. 
* All the tensors are immutable.

[Introduction to Tensorflow](https://github.com/aiplanethub/Deep_Learning_Bootcamp/blob/master/Tensor_Operations/DL_Day3.ipynb)

# Keras

We can use keras, importing the library from **TensorFlow**

```python
from tensorflow import keras
```

## Layers

We have different types of layers in Tensorflow, that are within the submodule called **layers**, that we can import as follows:
```python
from tensorflow.keras import layers
```

### Dense Layer
	- A Dense Layer is just a regular layer of neurons in a neural network. 
	- It is the most common and frequently used layer.
	- In a normal Neural Network, in the hidden layers, each neuron recices input from all the neurons in the previous layer and is thus called densely connected or dense.
	- Each output of a dense layer is computed using every input to the layer.
	- Dense layers expect one-dimensinal input.

```python
from tensorflow.keras.layers import Dense
```

### Flatten
	- Flatten Layers is used to flatten the input, it means to reshape the input data into a one-dimensional array. 

```python
from tensorflow.keras.layers import Flatten
```
## Creating models with Layers

There are two ways to create a model using the Layers API.
	1- Sequential Model: The most common model type is the sequential model, a linear stack of layers. In short, it allows you to build a model layer by layer.
	Each layer has weights that correspond to the layer that follows it.
	2- Functional Model: Unlike the stack of layers in Sequential API, the functional API is a way to build graphs of layers.

[Building a Model](https://github.com/aiplanethub/Deep_Learning_Bootcamp/blob/master/DL%20For%20Classification/%20DL_Day6_Building_a_DL_Model.ipynb)

## Linear Regression
There are five steps which we can understand the life-cycle in the LR with keras.
	- Define the model
	- Compile the model
	- Fit the model
	- Make predictions on the test data
	- Evaluate the model

## 1- Define the model
	 First we need to select the type of model that can work and then choose the architecture of network topology.
	 This means, defining the layers of the model, configuring each layer (Number of nodes and activation function), and connecting the layers togeteher into a cohesive model.
	 There are two options which we can defined the model:
	 - Sequential API
	 - Functinal API
### Sequential API
	It's the simplest API to get started with Deep Learning.
	It's called Sequential, because we defining a Sequential class and later we add the layers to the model, one by one in a linear manner, since input to output.
	It's no recommeded to use this class when:
		- The model has multiple inputs or multiple outputs
		- Any of your layers has multiple inputs or multiple outpus
		- You need to do layer sharing
		- You want non-linear topology
	
```python
from tensorflow.keras import Sequential
```
We have other class within the keras library for add the kind of layers for the model, this class is:

```python
from tensorflow.keras.layers import Dense
```

Now, we can create the model.

```python
model = Sequential() #Initializing the model
model.add(Dense(10, #units => Dimensionality of the output space
				activation='', #default is linear but this have softmax,softplus,softsign,relu,tanh,sigmoid and grad_sigmoid
				input_shape=(number_features,) #We need to specifying the input shape in adavance, because we need to know the shape of their inputs to create their weights. This expects a vector of n_features
				name="" # Name of the layer
				)
		)
model.add(Dense(8,activation=''))
model.add(Dense(1))
```
Always the first layer needs to be assign the input shape because we need to know the shape of the inlet data.
The activation function decide, whether a neuron should be activated or not.

## 2- Compile the model
	Before we compiling the model, first we need to select a loss function that we want to optimize (Mean Square Error or Cross Entropy). 
	It also requires that we select an algorithm to perform the optimization procedure.
```python
from tensorflow.keras.optimizers import RMSprop
```
**RMSprop**: This measn Root Mean Square Propagation. It's one of the most popular gradient descent optimization algortihms for deep learning networks. It's reliable and fast.
```python
optimizer = RMSprop(0.01) # This number represents the learning rate
```
The learining rate must be thiscovered via trial and error. This is in a range of 1 to 10^-6

Now, we can compile the model.
```python
model.compile(loss='', # Here we need to assinged the loss function, that can be 'mean_squared_error', 'binary_crossentropy', 'sparce_categorical_crossentropy' 
			  optimizer=optimizer_function # Here we put the optimizer 
			 )
#sparse_categorical_crossentropy is a loss function similar to binary_crossentropy, the only difference is that if the target variable is binary we use binary_crossentropy but if your target values are normal integers more then two, use sparse categorical crossentropy. Why not use categorical_crossentropy? You may ask. Well, [this article](https://jovianlin.io/cat-crossentropy-vs-sparse-cat-crossentropy/) will help you understand it.
```

## 3 - Fitting the model
	Fitting the model requires that you first select the training configuration, such as the number of epochs, and the batch size.
	Training applies the chosen optimization algorithm to minimize the chosen loss function and updates the model using the backpropagation of error algorithm.
	This is the slow part of the whole process and can take seconds to hours to days, depending on the complexity of the model, the hardware you're using, and the size of the training dataset.
```python
#This is a recommendation for Keras before we start to fit the model.
seed_value = 42
seed(seed_value) # If you build the model with given parameters, set_random_seed will help you produce the same result on multiple execution

# Recommended by Keras -------------------------------------------------------------------------------------
# 1. Set `PYTHONHASHSEED` environment variable at a fixed value
import os
os.environ['PYTHONHASHSEED']=str(seed_value)

# 2. Set `python` built-in pseudo-random generator at a fixed value
import random
random.seed(seed_value)

# 3. Set `numpy` pseudo-random generator at a fixed value
import numpy as np
np.random.seed(seed_value)
# Recommended by Keras -------------------------------------------------------------------------------------

# 4. Set the `tensorflow` pseudo-random generator at a fixed value
tensorflow.random.set_seed(seed_value)
```

after we have all ready, we can process with the fit:

```python
model.fit(x_train,y_train,
		 epochs=n, #=> loops through the training dataset
		 batch_size=n, #=> number of samples in an epoch used to estimate model error
		 verbose= n #=>Verbose: By setting verbose 0,1 or 2 you just say how do you want to 'see' the training progress for each epoch.
	#-Verbose=0 -> Will show you nothing (silent)
	#-Verbose=1 -> Will show you an animated progress bar like this:
#[============================]
	#-Verbose=2 -> Will just mention the number of epoch like this
	)
```

## 4 - Evaluate the model
	For evaluate the model we need to used the data not used in the training procces i.e. the X_Test and Y_Test
```python
model.evaluate(X_Test,Y_Test)
```
The result this give back is value of the loss function assigned in the compile process.

Actually, we can use the model.predict(X_test) for make step-to-step the process background of **evaluate**.

## Hyperparameter Tunning
For models like linear regression we used:
	1- Leaning rate
	2- Epochs
	3-Batch Size

These three parameters are the ones which we can change the values and see the performance of the model with the *Test Data*.

During each iteration, the gradient descent algorithm multiplies the learning rate by the gradient. The resulting product is called the **Gradient Step**.

### Summary of Hyperparameter Tunning

Here are some rules of thumb:
	- Training loss should steadily decrease, steeply at first, and then more slowly until the slope of the curve reaches or approaches zero.
	- If the training loss does not converge, train for more epochs.
	- If the training loss decreases too slowly, increase the learning rate. Note that setting the learning rate too high may also prevent training loss from converging.
	- If the training loss varies wildly (that is, the training loss jumps around), decrease the learning rate.
	- Lowering the learning rate while increasing the number of epochs or the batch size is often a good combination.
	- Setting the batch size to a very small batch number can also cause instability. First, try large batch size values. Then, decrease the batch size until you see degradation.
	- For real-world datasets consisting of a very large number of examples, the entire dataset might not fit into memory. In such cases, you'll need to reduce the batch size to enable a batch to fit into memory.

There are some libraries that help us to make a iterative evaluation of differents values for the params. Some of the more famous are Scikit-learn (GridSearchCV) and Keras (RandomSearch).



# Classification

The idea of classification is divides the given data points into two or more classes.
There are some classification which we can split or divide just with a **Straight Line =>linear boundary** but there are some case which are more complex and it's necessary more than a linear boundary, this is known as **Non-Linear Boundary**.

The Perceptron model works on the mos basic form of a Neural Network, but we use Deep Neural Network or Multi-Layer Perceptrons for realistic data classification.


# Tool with TensorFlow

## TensorBoard

This toolkit provides the visualizatiion and tooling needed for machine learning experimentation:
	- Tracking and visualizing metrics such as loss and accuracy
	- Visualizing the model graph
	- Viewing histograms of weights, biases, or other tensors as they change over time
	- Displaying images, test, and audio data
	- 

