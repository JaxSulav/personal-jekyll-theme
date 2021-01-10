---
layout: post
section-type: post
title: A Step By Step approach to a Neural Network and Backpropagation Algorithm
category: Neural network
tags: [ 'Machine Learning', 'Neural Network' ]
---

*What happens inside a neural network? How are values assigned to a neuron? Lets try to walk through each step of a neural network pipeline.*

This is not a basic - what is a neural network guide. So I assume you already know what a neural network is and it's two main entities:
* Perceptron
* Gradient Descent

*You can follow through my above linked articles about the topics.*
  
What we will do today is, consider the following neural network as an example and run through every step from start to end, of how the network learns while training.

<br>![nn](/img/posts/nn-step/nn2.jpg)<br>

This particular network consists of 3 layers i.e input, hidden and output layer and 2 neurons in each layer. We take only two neurons in each layer in our example because if we understand the sole concept, adding neurons and layers is a child's play.

Let's start with a simple pipeline, the way a Neural Network learns:

PIPELINE IMAGE

<br>

# Inputs:

Usually, inputs are the feature vectors of some kind. If you are performing a image classification as a cat or dog classifier, the input is the collection of values which represent features of some kind of the image that is in your training data. The simplest feature vector extractor is [local binary pattern](https://en.wikipedia.org/wiki/Local_binary_patterns) in which the vector is the collection of 0's and 1's and the size of the vector is equal to (A multiplied by B), if the resolution of image is AxB. You can go through more advanced [feature extraction techniques](https://opencv-python-tutroals.readthedocs.io/en/latest/py_tutorials/py_feature2d/py_table_of_contents_feature2d/py_table_of_contents_feature2d.html) if you like, but we will not cover that here.

<br>

# Feed Forward:

Lets' consider the following neural network with input vector (0.5, -0.5), which means the first neuron of the input layer will have value 0.5 and second neuron will have -0.5. Each neuron has a bias value associated with it so that it can help, fire up the neurons if weigghts and imputs are not sufficient. Now, to have some weights to work with we randomly initialize the weights here for the sake of simplicity but in real world, there are things we should consider during weight initialization. You can go through [weight initialization techniques in a neural network](#) to know about why we should not use same weights for all neurons or simply random values as weights.

<br>![nn](/img/posts/nn-step/nn3.jpg)<br>

Lets take a concept of [perceptron](#) analysis and move forward. Remember as we discussed in perceptron section, each neuron has two values in it, the Net Summed (Z) and the activated (S) value. <br>
For the 1st neuron of 2nd (hidden) layer, we calculate the Net Summed value and activated value as follows:

<br>![nn](/img/posts/nn-step/nn4.jpg)<br>


