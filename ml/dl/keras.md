# Keras

![image-20200521182632496](/Users/neil/Library/Application Support/typora-user-images/image-20200521182632496.png)

### Example

```python
X, y = make_moons(n_samples=1000, noise=0.05, random_state=0)

model = Sequential()
model.add(Dense(4, input_shape=(2,), activation='tanh'))
model.add(Dense(2, activation='tanh'))
model.add(Dense(1, activation='sigmoid'))

model.compile(Adam(lr=0.01), 'binary_crossentropy', metrics=['accuracy'])

history = model.fit(X, y, verbose=0, epochs=100)

plot_loss_accuracy(history)
```

#### *Dense*()

* constructs a fully connected neural network layer
* automatically initializing the weights and biases randomly
* add several Dense layers one after another. The output of one layer becomes the input of the next
*  arguments:
  * *units*:  the number of nodes in this layer
  * *input_shape*: In this case, our input dimensionality is 2, the x and y coordinates. The input_shape parameter expects a vector
  * *activation*: The activation function is the *logistic* function, altenatively called as *sigmoid*.
    * relu, softmax, tanh

#### compile()

* compile the Keras model
* specifying the optimizer to use
* specifying the loss function to minimize
* arguments:
  * *optimizer*: most of them based on gradient descent. 
  * lr: learning rate, depends on GD algorithm
  * *loss*: a binary 0/1 classifier, the loss function to minimize is *binary_crossentropy*
  * *metrics*: for classification problems we set this as *accuracy*.

```Python
opt_dict = {'nadam':Nadam,
            'adam':Adam,
            'sgd':SGD,
            'rmsprop':RMSprop,
            'adadelta':Adadelta,
            'adagrad':Adagrad}
```



#### fit()

* arguments:
  * *x*: The input data, we defined it as *X* above. It contains the x and y coordinates of the input points
  * *y*: The class we're trying to predict: binary/multi
  * *verbose*: Prints out the loss and accuracy
  * *epochs*: Number of times to go over the training data
  * *batch_size*:  if 128, then 54000/128=421 times per epoch of GD
  * *validation_split*: 0.1

```python
def build_dropout_model():
  model = Sequential()
  # The input layer requires the special input_shape parameter which should match
  # the shape of our training data.
  model.add(Dense(units=32, activation='sigmoid', input_shape=(image_vector_size,)))
  model.add(Dropout(0.2))
  model.add(Dense(units=num_classes, activation='softmax'))
  return model

```

#### Dropout()

* Dropout acts as a regularisation method
* it randomly throws away neurons from the model during trainig with a rate r
  * r = 0.2	