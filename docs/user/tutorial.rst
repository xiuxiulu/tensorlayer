.. _tutorial:

========
Tutorial
========

For deep learning, this tutorial will walk you through building a handwritten
digits classifier using the MNIST dataset, arguably the "Hello World" of neural
networks. For reinforcement learning, we will let computer learns to play Pong
game from the original screen inputs.

.. note::
    For experts: Read the source code of ``InputLayer`` and ``DenseLayer``, you
    will understand how TensorLayer work. After that, we recommend you to read
    the codes for tutorial directly.

Before we start
===============

The tutorial assumes that you are somewhat familiar with neural networks and
TensorFlow (the library which TensorLayer is built on top of). You can try to learn
both at once from the `Deeplearning Tutorial`_.

For a more slow-paced introduction to artificial neural networks, we recommend
`Convolutional Neural Networks for Visual Recognition`_ by Andrej Karpathy et
al., `Neural Networks and Deep Learning`_ by Michael Nielsen.

To learn more about TensorFlow, have a look at the `TensorFlow tutorial`_. You will not
need all of it, but a basic understanding of how TensorFlow works is required to be
able to use TensorLayer. If you're new to TensorFlow, going through that tutorial.


Run the MNIST example
=====================

In the first part of the tutorial, we will just run the MNIST example that's
included in the source distribution of TensorLayer.

We assume that you have already run through the :ref:`installation`. If you
haven't done so already, get a copy of the source tree of TensorLayer, and navigate
to the folder in a terminal window. Enter the folder and run the ``tutorial_mnist.py``
example script:

.. code-block:: bash

  python tutorial_mnist.py

If everything is set up correctly, you will get an output like the following:

.. code-block:: text

  tensorlayer: GPU MEM Fraction 0.300000
  Downloading train-images-idx3-ubyte.gz
  Downloading train-labels-idx1-ubyte.gz
  Downloading t10k-images-idx3-ubyte.gz
  Downloading t10k-labels-idx1-ubyte.gz

  X_train.shape (50000, 784)
  y_train.shape (50000,)
  X_val.shape (10000, 784)
  y_val.shape (10000,)
  X_test.shape (10000, 784)
  y_test.shape (10000,)
  X float32   y int64

  tensorlayer:Instantiate InputLayer input_layer (?, 784)
  tensorlayer:Instantiate DropoutLayer drop1: keep: 0.800000
  tensorlayer:Instantiate DenseLayer relu1: 800, <function relu at 0x11281cb70>
  tensorlayer:Instantiate DropoutLayer drop2: keep: 0.500000
  tensorlayer:Instantiate DenseLayer relu2: 800, <function relu at 0x11281cb70>
  tensorlayer:Instantiate DropoutLayer drop3: keep: 0.500000
  tensorlayer:Instantiate DenseLayer output_layer: 10, <function identity at 0x115e099d8>

  param 0: (784, 800) (mean: -0.000053, median: -0.000043 std: 0.035558)
  param 1: (800,) (mean: 0.000000, median: 0.000000 std: 0.000000)
  param 2: (800, 800) (mean: 0.000008, median: 0.000041 std: 0.035371)
  param 3: (800,) (mean: 0.000000, median: 0.000000 std: 0.000000)
  param 4: (800, 10) (mean: 0.000469, median: 0.000432 std: 0.049895)
  param 5: (10,) (mean: 0.000000, median: 0.000000 std: 0.000000)
  num of params: 1276810

  layer 0: Tensor("dropout/mul_1:0", shape=(?, 784), dtype=float32)
  layer 1: Tensor("Relu:0", shape=(?, 800), dtype=float32)
  layer 2: Tensor("dropout_1/mul_1:0", shape=(?, 800), dtype=float32)
  layer 3: Tensor("Relu_1:0", shape=(?, 800), dtype=float32)
  layer 4: Tensor("dropout_2/mul_1:0", shape=(?, 800), dtype=float32)
  layer 5: Tensor("add_2:0", shape=(?, 10), dtype=float32)

  learning_rate: 0.000100
  batch_size: 128

  Epoch 1 of 500 took 0.342539s
    train loss: 0.330111
    val loss: 0.298098
    val acc: 0.910700
  Epoch 10 of 500 took 0.356471s
    train loss: 0.085225
    val loss: 0.097082
    val acc: 0.971700
  Epoch 20 of 500 took 0.352137s
    train loss: 0.040741
    val loss: 0.070149
    val acc: 0.978600
  Epoch 30 of 500 took 0.350814s
    train loss: 0.022995
    val loss: 0.060471
    val acc: 0.982800
  Epoch 40 of 500 took 0.350996s
    train loss: 0.013713
    val loss: 0.055777
    val acc: 0.983700
  ...

The example script allows you to try different models, including Multi-Layer Perceptron,
Dropout, Dropconnect, Stacked Denoising Autoencoder and Convolutional Neural Network.
Select different models from ``if __name__ == '__main__':``.

.. code-block:: python

  main_test_layers(model='relu')
  main_test_denoise_AE(model='relu')
  main_test_stacked_denoise_AE(model='relu')
  main_test_cnn_layer()


Run the Pong Game example
=========================

In the second part of the tutorial, we will run the Deep Reinforcement Learning
example that is introduced by Karpathy in `Deep Reinforcement Learning: Pong from Pixels <http://karpathy.github.io/2016/05/31/rl/>`_.

.. code-block:: bash

  python tutorial_atari_pong.py

Before running the tutorial code, you need to install `OpenAI gym environment <https://gym.openai.com/docs>`_
which is a benchmark for Reinforcement Learning.
If everything is set up correctly, you will get an output like the following:

.. code-block:: text

  [2016-07-12 09:31:59,760] Making new env: Pong-v0
    tensorlayer:Instantiate InputLayer input_layer (?, 6400)
    tensorlayer:Instantiate DenseLayer relu1: 200, <function relu at 0x1119471e0>
    tensorlayer:Instantiate DenseLayer output_layer: 3, <function identity at 0x114bd39d8>
    param 0: (6400, 200) (mean: -0.000009, median: -0.000018 std: 0.017393)
    param 1: (200,) (mean: 0.000000, median: 0.000000 std: 0.000000)
    param 2: (200, 3) (mean: 0.002239, median: 0.003122 std: 0.096611)
    param 3: (3,) (mean: 0.000000, median: 0.000000 std: 0.000000)
    num of params: 1280803
    layer 0: Tensor("Relu:0", shape=(?, 200), dtype=float32)
    layer 1: Tensor("add_1:0", shape=(?, 3), dtype=float32)
  episode 0: game 0 took 0.17381s, reward: -1.000000
  episode 0: game 1 took 0.12629s, reward: 1.000000  !!!!!!!!
  episode 0: game 2 took 0.17082s, reward: -1.000000
  episode 0: game 3 took 0.08944s, reward: -1.000000
  episode 0: game 4 took 0.09446s, reward: -1.000000
  episode 0: game 5 took 0.09440s, reward: -1.000000
  episode 0: game 6 took 0.32798s, reward: -1.000000
  episode 0: game 7 took 0.74437s, reward: -1.000000
  episode 0: game 8 took 0.43013s, reward: -1.000000
  episode 0: game 9 took 0.42496s, reward: -1.000000
  episode 0: game 10 took 0.37128s, reward: -1.000000
  episode 0: game 11 took 0.08979s, reward: -1.000000
  episode 0: game 12 took 0.09138s, reward: -1.000000
  episode 0: game 13 took 0.09142s, reward: -1.000000
  episode 0: game 14 took 0.09639s, reward: -1.000000
  episode 0: game 15 took 0.09852s, reward: -1.000000
  episode 0: game 16 took 0.09984s, reward: -1.000000
  episode 0: game 17 took 0.09575s, reward: -1.000000
  episode 0: game 18 took 0.09416s, reward: -1.000000
  episode 0: game 19 took 0.08674s, reward: -1.000000
  episode 0: game 20 took 0.09628s, reward: -1.000000
  resetting env. episode reward total was -20.000000. running mean: -20.000000
  episode 1: game 0 took 0.09910s, reward: -1.000000
  episode 1: game 1 took 0.17056s, reward: -1.000000
  episode 1: game 2 took 0.09306s, reward: -1.000000
  episode 1: game 3 took 0.09556s, reward: -1.000000
  episode 1: game 4 took 0.12520s, reward: 1.000000  !!!!!!!!
  episode 1: game 5 took 0.17348s, reward: -1.000000
  episode 1: game 6 took 0.09415s, reward: -1.000000

This example allow computer to learn how to play Pong game from the screen inputs,
just like human behavior. After training for 15,000 episodes, the computer can
win 20% of the games. The computer win 35% of the games at 20,000 episode,
we can seen the computer learn faster and faster as it has more winning data to
train. If you run it for 30,000 episode, it start to win.

.. code-block:: python

  render = False
  resume = False

Setting 'render' to 'True', if you want to display the game environment. When
you run the code again, you can set 'resume' to 'True', the code will load the
existing model and train the model basic on it.


Run the Word2Vec example
=========================

In the third part of the tutorial, we will run

.. code-block:: bash

  python tutorial_word2vec_basic.py


If everything is set up correctly, you will get an output in the end.

.. _fig_0601:
.. figure:: _static/my_figs/tsne.png

.. image:: _static/my_figs/tsne.png


Understand the MNIST example
============================

Let's now investigate what's needed to make that happen! To follow along, open
up the source code.


Preface
-------

The first thing you might notice is that besides TensorLayer, we also import numpy
and tensorflow:

.. code-block:: python

  import tensorflow as tf
  import tensorlayer as tl
  from tensorlayer.layers import set_keep
  import numpy as np
  import time


As we know, TensorLayer is built on top of TensorFlow, it is meant as a supplement helping
with some tasks, not as a replacement. You will always mix TensorLayer with some
vanilla TensorFlow code. The ``set_keep`` is used to access the placeholder of keeping probabilities
when using Denoising Autoencoder.


Loading data
------------

The first piece of code defines a function ``load_mnist_dataset()``. Its purpose is
to download the MNIST dataset (if it hasn't been downloaded yet) and return it
in the form of regular numpy arrays. There is no TensorLayer involved at all, so
for the purpose of this tutorial, we can regard it as:

.. code-block:: python

  X_train, y_train, X_val, y_val, X_test, y_test = tl.files.load_mnist_dataset(shape=(-1,784))

``X_train.shape`` is ``(50000, 784)``, to be interpreted as: 50,000
images and each image has 784 pixels. ``y_train.shape`` is simply ``(50000,)``, which is a vector the same
length of ``X_train`` giving an integer class label for each image -- namely,
the digit between 0 and 9 depicted in the image (according to the human
annotator who drew that digit).

For Convolutional Neural Network example, the MNIST can be load as 4D version as follow:

.. code-block:: python

  X_train, y_train, X_val, y_val, X_test, y_test = tl.files.load_mnist_dataset(shape=(-1, 28, 28, 1))

``X_train.shape`` is ``(50000, 28, 28, 1)`` which represents 50,000 images with 1 channel, 28 rows and 28 columns each.
Channel one is because it is a grey scale image, every pixel have only one value.

Building the model
------------------

This is where TensorLayer steps in. It allows you to define an arbitrarily
structured neural network by creating and stacking or merging layers.
Since every layer knows its immediate incoming layers, the output layer (or
output layers) of a network double as a handle to the network as a whole, so
usually this is the only thing we will pass on to the rest of the code.

As mentioned above, ``tutorial_mnist.py`` supports four types of models, and we
implement that via easily exchangeable functions of the same interface.
First, we'll define a function that creates a Multi-Layer Perceptron (MLP) of
a fixed architecture, explaining all the steps in detail. We'll then implement
a Denosing Autoencoder (DAE), after that we will then stack all Denoising Autoencoder and
supervised fine-tune them. Finally, we'll show how to create a
Convolutional Neural Network (CNN).


Multi-Layer Perceptron (MLP)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The first script, ``main_test_layers()``, creates an MLP of two hidden layers of
800 units each, followed by a softmax output layer of 10 units. It applies 20%
dropout to the input data and 50% dropout to the hidden layers.

To feed data into the network, TensofFlow placeholders need to be defined as follow.
The ``None`` here means the network will accept input data of arbitrary batchsize after compilation.
The ``x`` is used to hold the ``X_train`` data and ``y_`` is used to hold the ``y_train`` data.
If you know the batchsize beforehand and do not need this flexibility, you should give the batchsize
here -- especially for convolutional layers, this can allow TensorFlow to apply
some optimizations.

.. code-block:: python

    x = tf.placeholder(tf.float32, shape=[None, 784], name='x')
    y_ = tf.placeholder(tf.int64, shape=[None, ], name='y_')

The foundation of each neural network in TensorLayer is an
:class:`InputLayer <tensorlayer.layers.InputLayer>` instance
representing the input data that will subsequently be fed to the network. Note
that the ``InputLayer`` is not tied to any specific data yet.

.. code-block:: python

    network = tl.layers.InputLayer(x, name='input_layer')

Before adding the first hidden layer, we'll apply 20% dropout to the input
data. This is realized via a :class:`DropoutLayer
<tensorlayer.layers.DropoutLayer>` instance:

.. code-block:: python

    network = tl.layers.DropoutLayer(network, keep=0.8, name='drop1')

Note that the first constructor argument is the incoming layer, the second
argument is the keeping probability for the activation value. Now we'll proceed
with the first fully-connected hidden layer of 800 units. Note
that when stacking a :class:`DenseLayer <tensorlayer.layers.DenseLayer>`.

.. code-block:: python

    network = tl.layers.DenseLayer(network, n_units=800, act = tf.nn.relu, name='relu1')

Again, the first constructor argument means that we're stacking ``network`` on
top of ``network``.
``n_units`` simply gives the number of units for this fully-connected layer.
``act`` takes an activation function, several of which are defined
in :mod:`tensorflow.nn` and `tensorlayer.activation`. Here we've chosen the rectifier, so
we'll obtain ReLUs. We'll now add dropout of 50%, another 800-unit dense layer and 50% dropout
again:

.. code-block:: python

    network = tl.layers.DropoutLayer(network, keep=0.5, name='drop2')
    network = tl.layers.DenseLayer(network, n_units=800, act = tf.nn.relu, name='relu2')
    network = tl.layers.DropoutLayer(network, keep=0.5, name='drop3')

Finally, we'll add the fully-connected output layer which the ``n_units`` equals to
the number of classes.

.. code-block:: python

    network = tl.layers.DenseLayer(network, n_units=10, act = tl.activation.identity, name='output_layer')

As mentioned above, each layer is linked to its incoming layer(s), so we only
need the output layer(s) to access a network in TensorLayer:

.. code-block:: python

    y = network.outputs
    y_op = tf.argmax(tf.nn.softmax(y), 1)
    cost = tf.reduce_mean(tf.nn.sparse_softmax_cross_entropy_with_logits(y, y_))

Here, ``network.outputs`` is the 10 identity outputs from the network (in one hot format), ``y_op`` is the integer
output represents the class index. While ``cost`` is the cross-entropy between target and predicted labels.

Denoising Autoencoder (DAE)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Autoencoder is a unsupervised learning models which able to extract representative features,
it has become more widely used for learning generative models of data and Greedy layer-wise pre-train.
For vanilla Autoencoder see `Deeplearning Tutorial`_.

The script ``main_test_denoise_AE()`` implements a Denoising Autoencoder with corrosion rate of 50%.
The Autoencoder can be defined as follow, where an Autoencoder is represented by a ``DenseLayer``:

.. code-block:: python

    network = tl.layers.InputLayer(x, name='input_layer')
    network = tl.layers.DropoutLayer(network, keep=0.5, name='denoising1')
    network = tl.layers.DenseLayer(network, n_units=200, act=tf.nn.sigmoid, name='sigmoid1')
    recon_layer1 = tl.layers.ReconLayer(network, x_recon=x, n_units=784, act=tf.nn.sigmoid, name='recon_layer1')

To train the ``DenseLayer``, simply run ``ReconLayer.pretrain()``, if using denoising Autoencoder, the name of
corrosion layer (a ``DropoutLayer``) need to be specified as follow. To save the feature images, set ``save`` to True.
There are many kinds of pre-train metrices according to different architectures and applications. For sigmoid activation,
the Autoencoder can be implemented by using KL divergence, while for rectifer, L1 regularization of activation outputs
can make the output to be sparse. So the default behaviour of ``ReconLayer`` only provide KLD and cross-entropy for sigmoid
activation function and L1 of activation outputs and mean-squared-error for rectifing activation function.
We recommend you to modify ``ReconLayer`` to achieve your own pre-train metrice.

.. code-block:: python

    recon_layer1.pretrain(sess, x=x, X_train=X_train, X_val=X_val, denoise_name='denoising1', n_epoch=200, batch_size=128, print_freq=10, save=True, save_name='w1pre_')

In addition, the script ``main_test_stacked_denoise_AE()`` shows how to stacked multiple Autoencoder to one network and then
fine-tune.


Convolutional Neural Network (CNN)
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Finally, the ``main_test_cnn_layer()`` script creates two CNN layers and
max pooling stages, a fully-connected hidden layer and a fully-connected output
layer.

At the begin, we add a :class:`Conv2dLayer
<tensorlayer.layers.Conv2dLayer>` with 32 filters of size 5x5 on top, follow by
max-pooling of factor 2 in both dimensions. And then apply a ``Conv2dLayer`` with
64 filters of size 5x5 again and follow by a max_pool again. After that, flatten
the 4D output to 1D vector by using ``FlattenLayer``, and apply a dropout with 50%
to last hidden layer.


.. code-block:: python

    network = tl.layers.InputLayer(x, name='input_layer')
    network = tl.layers.Conv2dLayer(network,
                            act = tf.nn.relu,
                            shape = [5, 5, 1, 32],  # 32 features for each 5x5 patch
                            strides=[1, 1, 1, 1],
                            padding='SAME',
                            name ='cnn_layer1')     # output: (?, 28, 28, 32)
    network = tl.layers.PoolLayer(network,
                            ksize=[1, 2, 2, 1],
                            strides=[1, 2, 2, 1],
                            padding='SAME',
                            pool = tf.nn.max_pool,
                            name ='pool_layer1',)   # output: (?, 14, 14, 32)
    network = tl.layers.Conv2dLayer(network,
                            act = tf.nn.relu,
                            shape = [5, 5, 32, 64], # 64 features for each 5x5 patch
                            strides=[1, 1, 1, 1],
                            padding='SAME',
                            name ='cnn_layer2')     # output: (?, 14, 14, 64)
    network = tl.layers.PoolLayer(network,
                            ksize=[1, 2, 2, 1],
                            strides=[1, 2, 2, 1],
                            padding='SAME',
                            pool = tf.nn.max_pool,
                            name ='pool_layer2',)   # output: (?, 7, 7, 64)
    network = tl.layers.FlattenLayer(network, name='flatten_layer')                                # output: (?, 3136)
    network = tl.layers.DropoutLayer(network, keep=0.5, name='drop1')                              # output: (?, 3136)
    network = tl.layers.DenseLayer(network, n_units=256, act = tf.nn.relu, name='relu1')           # output: (?, 256)
    network = tl.layers.DropoutLayer(network, keep=0.5, name='drop2')                              # output: (?, 256)
    network = tl.layers.DenseLayer(network, n_units=10, act = tl.identity, name='output_layer')    # output: (?, 10)


.. note::
    For experts: ``Conv2dLayer`` will create a convolutional layer using
    ``tensorflow.nn.conv2d``, TensorFlow's default convolution.



Training the model
------------------

The remaining part of the ``tutorial_mnist.py`` script copes with setting up and running
a training loop over the MNIST dataset by using cross-entropy only.


Dataset iteration
^^^^^^^^^^^^^^^^^

An iteration function for synchronously iterating over two
numpy arrays of input data and targets, respectively, in mini-batches of a
given number of items. More iteration function can be found in ``tensorlayer.iterate``

.. code-block:: python

    tl.iterate.minibatches(inputs, targets, batchsize, shuffle=False)


Loss and update expressions
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Continuing, we create a loss expression to be minimized in training:

.. code-block:: python

    y = network.outputs
    y_op = tf.argmax(tf.nn.softmax(y), 1)
    cost = tf.reduce_mean(tf.nn.sparse_softmax_cross_entropy_with_logits(y, y_))


More cost or regularization can be applied here, take ``main_test_layers()`` for example,
to apply max-norm on the weight matrices, we can add the following line:

.. code-block:: python

    cost = cost + tl.cost.maxnorm_regularizer(1.0)(network.all_params[0]) + tl.cost.maxnorm_regularizer(1.0)(network.all_params[2])

Depending on the problem you are solving, you will need different loss functions,
see :mod:`tensorlayer.cost` for more.

Having the model and the loss function defined, we create update expressions
for training the network. TensorLayer do not provide many optimizer, we used TensorFlow's
optimizer instead:

.. code-block:: python

    train_params = network.all_params
    train_op = tf.train.AdamOptimizer(learning_rate, beta1=0.9, beta2=0.999, epsilon=1e-08, use_locking=False).minimize(cost, var_list=train_params)


For training the network, we fed data and the keeping probabilities to the ``feed_dict``.

.. code-block:: python

    feed_dict = {x: X_train_a, y_: y_train_a}
    feed_dict.update( network.all_drop )
    sess.run(train_op, feed_dict=feed_dict)

While, for validation and testing, we use slightly different way. All
dropout, dropconnect, corrosion layers need to be disable.
``tl.utils.dict_to_one`` set all ``network.all_drop`` to 1.

.. code-block:: python

    dp_dict = tl.utils.dict_to_one( network.all_drop )
    feed_dict = {x: X_test_a, y_: y_test_a}
    feed_dict.update(dp_dict)
    err, ac = sess.run([cost, acc], feed_dict=feed_dict)

As an additional monitoring quantity, we create an expression for the
classification accuracy:

.. code-block:: python

    correct_prediction = tf.equal(tf.argmax(y, 1), y_)
    acc = tf.reduce_mean(tf.cast(correct_prediction, tf.float32))


What Next?
^^^^^^^^^^^

We also have a more advanced image classification example in ``tutorial_cifar10.py``.
Please read the code and notes, figure out how to generate more training data and what
is local response normalization. After that, try to implement
`Residual Network <http://doi.org/10.3389/fpsyg.2013.00124>`_ (Hint: you will need
to use the Layer.outputs).








Understand Reinforcement learning
==================================

Pong Game
---------

To understand Reinforcement Learning, we let computer to learn how to play
Pong game from the original screen inputs. Before we start, we highly recommend
you to go through a famous blog called `Deep Reinforcement Learning: Pong from Pixels <http://karpathy.github.io/2016/05/31/rl/>`_
which is a minimalistic implementation of Deep Reinforcement Learning by
using python-numpy and OpenAI gym environment.


.. code-block:: bash

  python tutorial_atari_pong.py



Policy Network
---------------

In Deep Reinforcement Learning, the Policy Network is the same with Deep Neural
Network, it is our player (or “agent”) who output actions to tell what we should
do (move UP or DOWN); in Karpathy's code, he only defined 2 actions, UP and DOWN
and using a single simgoid output;
In order to make our tutorial more generic, we defined 3 actions which are UP,
DOWN and STOP (do nothing) by using 3 softmax outputs.

.. code-block:: python

    states_batch_pl = tf.placeholder(tf.float32, shape=[None, D])     # observation for training
    network = tl.layers.InputLayer(states_batch_pl, name='input_layer')
    network = tl.layers.DenseLayer(network, n_units=H, act = tf.nn.relu, name='relu1')
    network = tl.layers.DenseLayer(network, n_units=3, act = tl.activation.identity, name='output_layer')
    probs = network.outputs
    sampling_prob = tf.nn.softmax(probs)

Then when our agent is playing Pong, it calculates the probabilities of different
actions, and then draw sample (action) from this uniform distribution. As the
actions are represented by 1, 2 and 3, but the softmax outputs should be start
from 0, we calculate the label value by minus 1.

.. code-block:: python

    prob = sess.run(
        sampling_prob,
        feed_dict={states_batch_pl: x}
    )
    # action. 1: STOP  2: UP  3: DOWN
    action = np.random.choice([1,2,3], p=prob.flatten())
    ...
    ys.append(action - 1)


Policy Gradient
---------------

The key of Deep Reinforcement Learning is how to train the Policy Network,
there are many way to do

Q-learning xxxxx

AlphaGo is using xxxx


Dataset iteration
^^^^^^^^^^^^^^^^^

In Reinforcement Learning, we consider a final decision as an episode.
In Pong game, a episode is a few dozen games, because the games go up to score
of 21 for either player. Then the batch size is how many episode we consider
to update the model.
In the tutorial, we train a 2-layer policy network with 200 hidden layer units
using RMSProp on batches of 10 episodes.

Loss and update expressions
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Continuing, we create a loss expression to be minimized in training:

.. code-block:: python

    actions_batch_pl = tf.placeholder(tf.int32, shape=[None])
    discount_rewards_batch_pl = tf.placeholder(tf.float32, shape=[None])
    loss = tl.rein.cross_entropy_reward_loss(probs, actions_batch_pl, discount_rewards_batch_pl)
    ...
    ...
    sess.run(
        train_op,
        feed_dict={
            states_batch_pl: epx,
            actions_batch_pl: epy,
            discount_rewards_batch_pl: disR
        }
    )

The loss in a batch is relate to all outputs of Policy Network, all actions we
made and the corresponding discounted rewards in a batch. We first compute the
loss of each action by multiplying the discounted reward and the cross-entropy
between its output and its true action. The final loss in a batch is the sum of
all loss of the actions.


What Next?
-----------

The tutorial above shows how you can build your own agent, end-to-end.
While it has reasonable quality, the default parameters will not give you
the best agent model. Here are a few things you can improve.

First of all, instead of conventional MLP model, we can use CNNs to capture the
screen information better as `Playing Atari with Deep Reinforcement Learning <https://www.cs.toronto.edu/~vmnih/docs/dqn.pdf>`_
describe.

Also, the default parameters of the model are not tuned. You can try changing
the learning rate, decay, or initializing the weights of your model in a
different way.

Finally, you can try the model on different tasks (games).


Understand Natural Language Processing
======================================

Word Embedding
----------------


Dataset iteration
^^^^^^^^^^^^^^^^^


Loss and update expressions
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Many to One
----------------


Dataset iteration
^^^^^^^^^^^^^^^^^


Loss and update expressions
^^^^^^^^^^^^^^^^^^^^^^^^^^^

Many to Many (Seq2seq)
----------------


Dataset iteration
^^^^^^^^^^^^^^^^^


Loss and update expressions
^^^^^^^^^^^^^^^^^^^^^^^^^^^


More info
==========

For more information on what you can do with TensorLayer's layers, just continue
reading through readthedocs.
Finally, the reference lists and explains as follow.

layers (:mod:`tensorlayer.layers`),

weight initializers (:mod:`tensorlayer.init`),

activation (:mod:`tensorlayer.activation`),

natural language processing (:mod:`tensorlayer.nlp`),

reinforcement learning (:mod:`tensorlayer.rein`),

cost expressions and regularizers (:mod:`tensorlayer.cost`),

load and save files (:mod:`tensorlayer.files`),

operating system (:mod:`tensorlayer.ops`),

helper functions (:mod:`tensorlayer.utils`),

visualization (:mod:`tensorlayer.visualize`),

iteration functions (:mod:`tensorlayer.iterate`),

preprocessing functions (:mod:`tensorlayer.preprocess`),




.. _Deeplearning Tutorial: http://deeplearning.stanford.edu/tutorial/
.. _Convolutional Neural Networks for Visual Recognition: http://cs231n.github.io/
.. _Neural Networks and Deep Learning: http://neuralnetworksanddeeplearning.com/
.. _TensorFlow tutorial: https://www.tensorflow.org/versions/r0.9/tutorials/index.html
.. _Understand Deep Reinforcement Learning: http://karpathy.github.io/2016/05/31/rl/
.. _Understand Recurrent Neural Network: http://karpathy.github.io/2015/05/21/rnn-effectiveness/
