---
title: "How to resolve: AttributeError: module ‘tensorflow’ has no attribute ‘placeholder'"
date: 2020-8-31 05:34:28 -0400
categories: Tensorflow
tags:
  - tensorflow 
  - placeholder
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-09-8
---

# Issue 
---------------------------------------

* As **tensorflow** has been updated to **2.x**, it no longer supports **tf.placeholder**. 

<script src="https://gist.github.com/gimoonnam/116dae24c5d91a128b36ffb85aa28701.js"></script>

* the code above will raise an error that **placeholder** cannot be found.

<img src="/assets/images/tf_placeholder_error.png" width="800px" >


There are two ways to get around this issue.  

   

   

# Solution 1: to follow the update scheme of Tensorflow 2.0 
---------------------------------------

First method is apply changes in **Tensorflow 2.0**. Please refer to the details on the update [this link](https://www.tensorflow.org/guide/migrate).

**placeholder** can be replaced by **variable** as shown below.  

<script src="https://gist.github.com/gimoonnam/224fdfa50c17e29d9fcae4dd6757626a.js"></script>




   



# Solution 2: to use compatibility mode 
---------------------------------------

The second method is to disable the updated features in 2.0 by applying **compatibility mode 적용**. This can be implemented as following, then you will still be able to declare **tf.placeholder**. 

<script src="https://gist.github.com/gimoonnam/3b057a0a2ad8fcdc698509e56e055ead.js"></script>




