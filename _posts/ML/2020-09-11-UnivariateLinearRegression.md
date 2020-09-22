---
title: "Univariate Linear Regression (Numpy, tensorflow2.0, and Keras)"
date: 2020-9-11 05:34:28 -0400
categories: MachineLearning
tags:
  - Linear regression 
  - Numpy
  - tensorflow 2.0
  - Keras 
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-09-11
---

# Univariate Linear Regression (ULR) 

In this post, I study a Linear Regression(LR), which is a basic subject in Machine Learning (ML) algorithm. A single variable LR is considered. I will implement the LR with three different tools: Numpy, Tensorflow, and Keras, and their results will be compared to each other. 

## Hypothesis and loss function 

* Hypothesis 
    $y = w*x + b$ ($w$ for weight and $b$ for bias)
    
* Cost (loss) function is defined as a mean-squared error 

    \begin{equation} 
    J(w,b) = \frac{1}{2N}\sum_{i=1}^{N}\left( \hat{y}^{(i)} - y^{(i)} \right)^2 
    \label{eq:loss}
    \end{equation}
    
    where $\hat{y}^{(i)}$ is a predicted value for $i$th data point, and $N$ is the total number of data points
     The cost function is a quadratic function that would have a single global minima. 
    The factor 2 in the cost function is a conventional introduction for the sake of simple calculation. 
    
    
* The cost function is optimized by Gradient Descent
    The parameters w and b are updated as 
     
    \begin{equation} 
        w = w - \alpha \frac{\partial J}{\partial w}, \quad b = b - \alpha \frac{\partial J}{\partial b}
        \label{eq:w_updated}
    \end{equation}     
    \begin{equation} 
       \frac{\partial J}{\partial w} = \frac{1}{N}\sum_{i=1}^{N}\left(wx^{(i)}+b - y^{(i)} \right)x^{(i)}
       \label{eq:dJ_dw}
    \end{equation}     
    \begin{equation} 
       \frac{\partial J}{\partial b} = \frac{1}{N}\sum_{i=1}^{N}\left(wx^{(i)}+b - y^{(i)} \right)
       \label{eq:dJ_db}       
    \end{equation}     



# Implementation 

## 0. Module load and Data Acquisition 

Loading modules 
```python
from sklearn.datasets import make_regression
import matplotlib.pyplot as plt
import numpy as np
import tensorflow as tf
import time
```

```
X, y = make_regression(n_samples=100, 
                       n_features=1, 
                       bias=10.0, noise=10.0, random_state=2)
```                       
where X is input data and y is a label data. 

The dimemsion of label data is changed to (n_samples, 1). 
```
y = np.expand_dims(y, axis=1)
```


Split the date into train and test sets with 80% and 20%, respectively. 

```
train_x, train_y = X[:80], y[:80]
test_x, test_y   = X[80:], y[80:]
```

## 1. ULR with Numpy as ***from-scratch*** approach

The implementation in a class is as below 

<script src="https://gist.github.com/gimoonnam/6c7afda5e27ea883a1e54f9b3f4775ce.js"></script>

The result of the training is 

<img src="/assets/images/result_ULR_numpy.png" width="800px" >



## 2. ULR with Tensorflow 2.0 

Next, we implement the ULR with the same dataset with tensorflow. Since the tensorflow is a software library, there are several functions to study. Besides, the LR is carried out in a batched data, which is much faster than training by individual data input. 

<script src="https://gist.github.com/gimoonnam/b08e8d3d6987d6b81ade25e44f3601db.js"></script>


As shown in the result below, the batch train produces a noisy profile of loss function, which is eventually saturated at an optimized value. The result of train fits the data pretty well. 

<img src="/assets/images/result_ULR_TF.png" width="800px" >



## 3. ULR with Keras 

<script src="https://gist.github.com/gimoonnam/6fa1ded9a20fff781188119652bc87c4.js"></script>

<script src="https://gist.github.com/gimoonnam/de16ed4d9564536650ff70686a7db476.js"></script>


<img src="/assets/images/result_ULR_Keras.png" width="800px" >


# Concluding remarks

In this post, I have studied the Linear Regression of a single variable set (weight and bias). For complete study, I have implemented the Linear Regression with three different libraries: Numpy, Tensorflow 2.0, and Keras. This low- to high-level implementation provided a comprehensive understanding on how the algorithm works, which is especially very helpful for a beginner. 

In the following post, as a continuation of self-study on ML, I will study a logistic regression. 








