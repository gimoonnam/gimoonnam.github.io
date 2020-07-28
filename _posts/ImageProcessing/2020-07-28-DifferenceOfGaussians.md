---
title: "Image Edge Enhancement: Difference of Gaussians(DoG)"
date: 2020-7-28 12:32:28 -0400
categories: ImageProcessing
tags:
   - DoG 
   - LoG
   - edge detection 
   - Laplace operator
   - exposure fusion
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-07-26
---


# Introduction 

In this post, we will look over how to improve edges and other detailedd features on images. There are several methods, most of which uses convolutions with a filter. 

## 2. Difference of Gaussian (DoG)  

$$
G_1(x,y) = \frac{1}{\sqrt{2\pi\sigma_1^2}}\exp\left(-(x^2+y^2)/2\sigma_{1}^2\right)\nonumber\\ 
G_2(x,y) = \frac{1}{\sqrt{2\pi\sigma_2^2}}\exp\left(-(x^2+y^2)/2\sigma_{2}^2\right)\nonumber
\tag{2} 
$$

These two Gaussian filter produces two blurred images. Differencce of Gaussians is then made by subtracting more blurred image from less blurred one, 
ensuring that $\sigma_1 < \sigma_2$. 

$$
f_{\mathrm{sharpened}}(x,y) = f(x,y)* G_1(x,y) - f(x,y) * G_2(x,y)
\tag{3}
$$

where $* $ indicates convolution operator. 


The resulting curve resembles a Mexican hat as shown below. 

|<img src="/assets/images/DoG.png" width="400px" >|
|:--:| 
|taken from Ref.1|

## 파이썬 코드 

<script src="https://gist.github.com/gimoonnam/18348ab61a82cb9140ed9672d296b8d2.js"></script>


## 설명

# Wrapping up


# References 
  
  1. [Interactive tutorial on Difference of Gaussians Edge Enhancement](https://micro.magnet.fsu.edu/primer/java/digitalimaging/processing/diffgaussians/index.html) 
  2. [Blob detection on wikipedia](https://en.wikipedia.org/wiki/Blob_detection#The_Laplacian_of_Gaussian)  
  3. [Unsharp filter](https://homepages.inf.ed.ac.uk/rbf/HIPR2/unsharp.htm)   
  4. [Laplace operator in OpenCV](https://docs.opencv.org/3.4/d5/db5/tutorial_laplace_operator.html)   
  
  
  
  
  
  
  
