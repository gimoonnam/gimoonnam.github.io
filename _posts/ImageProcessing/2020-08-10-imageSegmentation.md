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

   <img src="/assets/images/thresholding_sample.png" width="800px" >
 
 이번 포스팅에선 **이미지 이진화(image binarization)** 대해서 공부해 보도록 한다.

 **이미지 이진화**는 **이미지 분리(image segmentation)** 을 하는 가장 간단한 방법으로 이미지내의 물체와 배경을 0과 1, 또는 그 반대로, 두 값만으로 픽셀값을 재설정 하는 것이다. 
 
  <img src="/assets/images/seg_Thresholding.png" width="800px" >
 
 이 방법은 픽셀값이 **0~255**사이의 값을 가지는 흑백 이미지에만 적용할 수 있다. 
 
 픽셀값을 0과 1로 바꾸는 것은 thresh라는 임계값을 기준으로 정해진다. 
 
 이 값을 수동으로 주는 것이 기본적인 **image thresholding** 이며, 자동으로 알고리즘 내에서 정해지도록 하는 방법 중 가장 많이 사용되는 것은 **Otus's method**이다.
 
 여기에서 이 두 방법으로 **이미지 이진화**를 실행해 보도록 하겠다.  
 
 
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
