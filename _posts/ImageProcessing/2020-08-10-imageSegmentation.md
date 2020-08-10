---
title: "Image Thresholding(이미지 이진화)"
date: 2020-8-10 11:32:28 -0400
categories: ImageProcessing
tags:
   - Otsu's algorithm
   - Hough algorithm
   - segmentation 
   - feature extraction
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-08-10
---


# Image Thresholding 

 이번 포스팅에선 **이미지 이진화(image binarization)** 대해서 공부해 보도록 한다.
 아래 그림에서 보듯이 **이미지 이진화**는 **이미지 분리(image segmentation)** 을 하는 가장 간단한 방법이다. 
  
  <img src="/assets/images/seg_Thresholding.png" width="800px" >
 
 이 방법은 픽셀값이 **0~255**사이의 값을 가지는 흑백 이미지에만 적용할 수 있으며, 그 결과는 0과 1만 갖는 이미지로 환원(reduced)된다. 
 
 작용 방식은 간단하다. 픽셀값이 어떤 기준값(thresh) 보다 크면 1로 작으면 0으로 값을 바꾸면 된다. 그 thresh 값을 대충 짐작으로 주는 것이 1차적인 
 단순한 방법이고, 알고리즘내에서 자동으로 계산되는 것이 좀 더 발전된 방법이라 하겠다.
 
 자동으로 정해지는 방법을 **Otus's method**라고 하며, 이것을 이해하고 구현해 보는 것을 이 포스팅의 목표로 삼아본다.

  
## Simple image thresholding 

   **image thresholding**은 가장 단순하고 간단한 **image segmentation** 방법이다. 
  
   이것을 위해서 분리하는 영역과 배경의 픽셀값을 구분한다. 이것을 이라고 하며, 두 영역을 구분하는 픽셀값을 찾는 것을 뜻한다. 대표적으로 **Otsu**'s 방법이 있다. 

## Otsu's algorithm 
   
   The variance of the image consists of the intra- and inter-class variances, referred to as within- and between-class variances, respectively. 
   
   \begin{equation} 
   \sigma_{T}^2 = \sigma_w^2(t) + \sigma_b^2(t) 
   \label{eq:totalVariance}   
   \end{equation} 

   The within-class variance is defined as 

   \begin{equation} 
   \sigma_w^2(t) = \omega_1(t)\sigma_1^2(t) + \omega_2(t)\sigma_2^2(t) 
   \label{eq:withinClass}   
   \end{equation} 


   the between-class variance is defined as

   \begin{equation} 
   \sigma_b^2(t) = \omega_1(t)\omega_2(t)\left[\mu_1(t)-\mu_2(t) \right]^2
   \label{eq:betweenClass}   
   \end{equation} 
   


## Mumford-Shah functional 

## Hough algorithm 



# References and Image sources

1. [Otus's thresholding with OpenCV](https://www.learnopencv.com/otsu-thresholding-with-opencv/?ck_subscriber_id=572611048).  
2. 
