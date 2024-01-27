# Hyperparameters

This rules can help to find the best set of hyperparameters for any dataset.

* Training loss should steadily decrease, steeply at first, and then more slowly until the slope of the curve reaches or approaches zero.
* If the training loss does not converge, train for more epochs.
* If the training loss decreases too slowly, increase the learning rate. Note that setting the learning rate too high may also prevent training loss from converging.
* Lowering the learning rate while increasing the number of epochs or the batch size is often a good combination.
* Setting the batch size to a very small batch number can also cause instability. First, try large batch size values. Then, decrease the batch size until you see degradation.