---
title: "Edge Enhancement: Laplace Operator"
date: 2020-7-29 12:32:28 -0400
categories: ImageProcessing
tags:
   - Laplacian of Gaussian
   - edge detection 
   - Laplace operator
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-07-28
---


# Introduction 

이미지 처리에서 sharpening이라고 하는 즉 선명도를 증가시키는 방법이 몇 가지 있습니다. 이 포스팅에선 **Laplace Operator** 에 대해서 보도록 하겠습니다.

# Theory 

## 1. Laplace Operator 

$$
\begin{eqnarray}
\mathbf{L} &=& \nabla^2 f(x,y) \nonumber\\
&=& \left[\frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2}  \right] f(x,y) \nonumber
\end{eqnarray}
\tag{1}
$$

where $f(x,y)$ denotes a 2-D intensity map of original image, where $x,y$ indicate a coordinate of pixels on the images. 


|<img src="/assets/images/DoG.png" width="400px" >|
|:--:| 
|taken from Ref.1|


## 2. Laplace of Gaussian (LoG)

Thesecond one is the Laplace of Gaussian, in which Gaussian filter is applied to Laplacian operator as shown below. 

$$ 
\begin{eqnarray}
\mathrm{LoG} &=& \nabla^2 G(x,y) \nonumber\\
&=& -\frac{1}{\pi \sigma^2}\left[ 1- \frac{x^2+y^2}{2\sigma^2} \right] \mathrm{e} ^{-\left(x^2+y^2\right)/2\sigma^2}\nonumber
\end{eqnarray}
\tag{4}
$$

The Laplacian filter is very sensitive to noise despite a better performancce on edge detection. 
These counterpart properties are resolved by applying Laplace operator to Gaussian blurred image that has already removed noise by blurring. 
LoG is more widely used to sharpen images than Laplace and DoG. 


# Implementation 

<script src="https://gist.github.com/gimoonnam/11f62474df4c93626bb61c879199b0e0.js"></script>


## 코딩 

## 결과 


# Wrapping up


# References 
  
  1. [Interactive tutorial on Difference of Gaussians Edge Enhancement](https://micro.magnet.fsu.edu/primer/java/digitalimaging/processing/diffgaussians/index.html) 
  2. [Blob detection on wikipedia](https://en.wikipedia.org/wiki/Blob_detection#The_Laplacian_of_Gaussian)  
  3. [Unsharp filter](https://homepages.inf.ed.ac.uk/rbf/HIPR2/unsharp.htm)   
  4. [Laplace operator in OpenCV](https://docs.opencv.org/3.4/d5/db5/tutorial_laplace_operator.html)   
  
  
  
  
  
  
  
