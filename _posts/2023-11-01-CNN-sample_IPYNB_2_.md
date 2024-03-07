---
toc: True
comments: True
layout: post
title: Personal Project - Convolutional Neural Network
description: CNN development
type: hacks
courses: {'csp': {'week': 10, 'categories': ['4.A']}}
categories: ['C1.4']
---

# Searching for Planets with Convolutional Neural Networks
<p>This is a section of code from a AI-based scientific investigation of circumbinary planets. I will not explain the exact specifics of the code objectives since they are irrelevant to this class but all the features developed are here. Note that this does NOT work in VSCode - an excessive number of external dependencies are necessary and I am not working on it in here.</p>

#### Key Features:
- Passes negative and positive training data in numpy .npz files to a custom Keras convolutional neural network
- Manufactures training datasets which the CNN can use
- Trains the neural network using Adam optimizer
- Allows user to select device from CUDA visible options and determine training parameters
- Trains and saves a neural network model using all parameters passed


```python
import numpy as np
import matplotlib.pyplot as plt
import os
# os.environ["CUDA_DEVICE_ORDER"] = "PCI_BUS_ID"   # see issue #152
# os.environ["CUDA_VISIBLE_DEVICES"] = ""
from os.path import join as opj
import tensorflow as tf
from tensorflow.python.client import device_lib
import astropy

from IPython.core.display import display, HTML
display(HTML("<style>.container { width:100% !important; }</style>"))

'''
Imports packages of functions from transit_utils and model_training_toolkit, which are my own libraries

import transit_utils as utils
import model_training_toolkit as modelkit
'''

from time import process_time
```

    /var/folders/mh/dn_3qv0s6dndm54j9k1xw61h0000gn/T/ipykernel_7115/2357884589.py:11: DeprecationWarning: Importing display from IPython.core.display is deprecated since IPython 7.14, please import from IPython display
      from IPython.core.display import display, HTML



<style>.container { width:100% !important; }</style>



```python
# Select a hardware device on which to run the CNN training

proc_hardware_choice = 0


if proc_hardware_choice == 0:
    proc_hardware_name = '/gpu:0'
    os.environ['CUDA_VISIBLE_DEVICES'] = '1'
    
elif proc_hardware_choice == 1:
    proc_hardware_name = '/gpu:1'
    
elif proc_hardware_choice == 2:
    proc_hardware_name = '/cpu:0'
    os.environ['CUDA_VISIBLE_DEVICES'] = '-1'
else:
    print('ERROR: You didnt make a proper choice. Defaulting to CPU processing.')
    proc_hardware_name = '/cpu:0'
    
print('Using hardware name =', proc_hardware_name)
```


```python
#These names are npz files I made through an iterative data synthesis model based on the other file
# filelist = ['100K_transformed.npz', 'recovery/training_data/5K_foldless_trainingdata.npz']
filelist = ['recovery/training_data/5K_transformed.npz']

plc = []
nlc = []

for name in filelist:
    p = np.load(name)['poslc']
    n = np.load(name)['neglc']
    
    plc.append(p)
    nlc.append(n)
    
positive_matrix = np.vstack(plc)
negative_matrix = np.vstack(nlc)
```


```python
# Plot a sample from the loaded data as a sanity check.

i = np.random.randint(0, negative_matrix.shape[0])

plt.figure()
plt.plot(positive_matrix[i, :])
```


```python
# Make testing and training datasets
'''mk_set is a function from my package model_traning_toolkit which takes two sets of arrays 
(positive_matrix and negative_matrix) and randomly shuffles them into a 2D x_train and y_train array.
'''
x_train, y_train = modelkit.mk_set(positive_matrix, negative_matrix)


# Reshape arrays to make tensorflow happy.
y_train = y_train.reshape((-1, 1))
x_train = x_train.reshape((x_train.shape[0], x_train.shape[1], 1))

np.shape(x_train)
```


```python
#Training process parameters to pass to keras
model_name = 'model_folded_v2' # Name the model to write to

batch_size = 32
epochs = 80
data_dir = os.path.join(os.getcwd(), 'data')
log_dir = os.path.join(os.getcwd(), 'tb_logs')
checkpoint_dir = os.path.join(os.getcwd(), 'data', 'models')
```


```python
#Keras model layers
from tensorflow.keras.models import Model
from tensorflow.keras.layers import (
    Dense, Input, Flatten, Reshape,
    GlobalMaxPooling1D, Lambda,
    Conv2D, GaussianNoise,
    Cropping2D, Concatenate, ZeroPadding2D)

tf.keras.backend.clear_session()

# -------------------------------------------------
# Circular Convolutional Layer

def CConv2D(filters, kernel_size, strides=(1, 1), activation='linear', padding='valid', kernel_initializer='glorot_uniform', kernel_regularizer=None):
    
    def CConv2D_inner(x):
        # padding (see https://www.tensorflow.org/api_guides/python/nn#Convolution)
        in_height = int(x.get_shape()[1])
        in_width = int(x.get_shape()[2])

        if (in_height % strides[0] == 0):
            pad_along_height = max(kernel_size[0] - strides[0], 0)
        else:
            pad_along_height = max(
                kernel_size[0] - (in_height % strides[0]), 0)
        if (in_width % strides[1] == 0):
            pad_along_width = max(kernel_size[1] - strides[1], 0)
        else:
            pad_along_width = max(kernel_size[1] - (in_width % strides[1]), 0)

        pad_top = pad_along_height // 2
        pad_bottom = pad_along_height - pad_top
        pad_left = pad_along_width // 2
        pad_right = pad_along_width - pad_left

        # left and right side for padding
        pad_left = Cropping2D(cropping=((0, 0), (in_width-pad_left, 0)))(x)
        pad_right = Cropping2D(cropping=((0, 0), (0, in_width-pad_right)))(x)

        # add padding to incoming image
        conc = Concatenate(axis=2)([pad_left, x, pad_right])

        # top/bottom padding options
        if padding == 'same':
            conc = ZeroPadding2D(padding={'top_pad': pad_top,
                                          'bottom_pad': pad_bottom})(conc)
        elif padding == 'valid':
            pass
        else:
            raise Exception('Padding "{}" does not exist!'.format(padding))

        # perform the circular convolution
        cconv2d = Conv2D(filters=filters, kernel_size=kernel_size,
                         strides=strides, activation=activation,
                         padding='valid',
                         kernel_initializer=kernel_initializer,
                         kernel_regularizer=kernel_regularizer)(conc)

        # return circular convolution layer
        return cconv2d
    return CConv2D_inner


# -------------------------------------------------
# The model

def model_fun(data_shape):

    inputs = Input(shape=data_shape)
    
    # New layer: Adds a small amount of noise to each sample during training
    layer = GaussianNoise(stddev=1/100)(inputs)
    
    # New layer: Make tensor 2D for new 2D convolution layers
    layer = Reshape((1, data_shape[0], 1))(layer)
    
    # New layer: Circular convolution layer
    layer = CConv2D(
        filters=128, 
        kernel_size=(1,3), 
        activation='linear',
    )(layer)
    
    # New layer: Circular convolution layer
    cconv2_filter_cnt = 256
    layer = CConv2D(
        filters=cconv2_filter_cnt, 
        kernel_size=(1,6), 
        activation='linear',
    )(layer)
    
    # New layer: Make tensor 1D
    layer = Reshape((data_shape[0], 
                     cconv2_filter_cnt))(layer)
    
    # New layer: Global pooling
    layer = GlobalMaxPooling1D()(layer)
    
    layer = Flatten()(layer)

    layer = Dense(256, activation='relu')(layer)
    
    layer = Dense(256, activation='relu')(layer)
    
    layer = Dense(1, activation='sigmoid')(layer)
    
    return Model(inputs, layer)

# Create model
model = model_fun(x_train.shape[1:])

# Show model summary
model.summary()
```


```python
# Train and test the model
from tensorflow.keras.optimizers import RMSprop, Adam, SGD, Adadelta
from tensorflow.keras.callbacks import ModelCheckpoint, EarlyStopping
from livelossplot.tf_keras import PlotLossesCallback

# Set optimizer and optimization options
# optimizer = SGD(learning_rate=0.001, decay=1e-6, momentum=0.9, nesterov=True)
optimizer = Adam(lr=5e-7)

# Compile the model (required)
model.compile(loss='binary_crossentropy', 
              #optimizer= 'adam',
              optimizer = optimizer,
              metrics=['accuracy'])


# Set early stopping (during training) options
early_stopping = EarlyStopping(monitor='val_loss', 
                               patience=7, 
                               verbose=1, 
                               mode='auto')


# Setup training checkpoint options
model_checkpoint = ModelCheckpoint(opj(checkpoint_dir, str(model_name) + '.hdf5'), 
                                   monitor='val_loss', 
                                   save_best_only=True)


# Define callbacks, which TF will call on after each training epoch finishes
callbacks = [model_checkpoint,  # Make checkpoints
             PlotLossesCallback(), # Show training progress (model accuracy and loss)
            ]
```


```python
#Run the keras model above through the training process with the specified dataset and training epochs

print(proc_hardware_name)

with tf.device(proc_hardware_name): # With the hardware chosen, train the model!
    
    model.fit(x_train, y_train,
              batch_size=batch_size, 
              epochs=epochs,
              validation_split=0.3,
              shuffle=True,
              callbacks=callbacks,
             )
```


```python
# Load the model weights at the checkpoint which had the best results
model.load_weights(opj(data_dir, 'models', str(model_name) + '.hdf5'))
```


```python
# Save the entire model
model.save(opj(data_dir, 'models', str(model_name) + '_save1.hd5'))
```
