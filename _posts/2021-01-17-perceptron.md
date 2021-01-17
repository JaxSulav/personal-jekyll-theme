---
layout: post
section-type: post
title: Perceptron - A basis of a Neural Network
category: Neural Network
tags: [ 'Machine Learning', 'Neural Network' ]
---

# Perceptron

*A perceptron is a basic unit of a neural network. Basically, a neural network is made up of many perceptrons combined together.*

Many people say that a neural network is a mathematical model of a neuron in human brain but I think that it might take a little bit more than a perceptron to map a complex thing like neuron of our brain. Yet, the structure of a perceptron is based upon a neuron system of a human brain.

So, this is a basic structure of a perceptron. 

![p](/img/posts/perceptron/ptron1.jpg)<br>

A perceptron can have many number of inputs(i) and weights(w) associated with each imput. A bias value is a pre initialized value which is used to adjust the output along with the weighted sum of the inputs to the neuron. It can help to fit the data more towards left or right when using activation function. Inside a perceptron there are two sectors, a net summed value and the activated value. Net summed value(Z) is just the summation of the product of each input value and it's weight. There are a lots of activation functions we can use to get an activated value like [relu and it's variations](https://en.wikipedia.org/wiki/ReLU), [sigmoid](https://en.wikipedia.org/wiki/Sigmoid_function), [tanh](https://en.wikipedia.org/wiki/Hyperbolic_functions#Hyperbolic_tangent) etc.. <br>

In the figure above, a sigmoid activation function is used. Now, let's discuss why we need an activation function, why we don't pass the net summed value(Z) as an output to a perceptron but first there is one more concept we need to know and that is the the concept of linearity and non linearity. In the figure below there are two classes which can be separated simply by a straight line. This is called a linearly separable data. 

![p](/img/posts/perceptron/ptron2.jpg)<br>

Non linearly separable data are the data those which cannot be separated like the above figure, by a straigh line. As we look in the figure down below, we need a curve to separate the red and blues classes. So, this is an example of a linearly unseparable data or non linearly separable data. 

![p](/img/posts/perceptron/ptron3.jpg)<br>

If we look at the formula for Net Summed Value(Z), which is Z = (i<sub>1</sub>w<sub>1</sub> + ... + i<sub>j</sub>w<sub>j</sub>) + bias. Basically, it is <br>
**Z = iw + b**, which is exaclty the equation of straight line **Y = mx + c**. So, if we use this value as output to our perceptron then, we can only separate the linearly separable data. This is why we pass the value from linear function to an activation function, which is a non linear function and it gives us the value between o and 1. 

<br>

The neural network is a multi layer perceptron where few layers of perceptrons are connected together and each perceptron is called a neuron. This concept of multilayer perceptron was invented to solve the XOR classification problem. Generally, the AND and OR gate data was separable by a perceptron but the XOR data was not linearly separable so this is where the multi layer perceptron concept played an important role.