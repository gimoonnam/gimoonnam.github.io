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


# Introduction 

  이번 포스팅에서는 **이미지 세그멘테이션**의 가장 간단한 케이스인 **이미지 2진화(image binarization)** 대해서 공부해 보도록 하겠다. 
  
  
  <img src="/assets/images/seg_Thresholding.png" width="800px" >
  
  
  **이미지 2진화**는 이미지내의 물체와 배경을 0과 1 혹은 그 반대로 주어 구분하는 것을 말한다. 
  
  
# Algorithms 

## Simple image thresholding 

   **image thresholding**은 가장 단순하고 간단한 **image segmentation** 방법이다. 
  
   이것을 위해서 분리하는 영역과 배경의 픽셀값을 구분한다. 이것을 이라고 하며, 두 영역을 구분하는 픽셀값을 찾는 것을 뜻한다. 대표적으로 **Otsu**'s 방법이 있다. 


## Otsu's algorithm 

## *K*-Means clustering을 이용한 segmentation
   
   [reference](https://towardsdatascience.com/introduction-to-image-segmentation-with-k-means-clustering-83fd0a9e2fc3)
   

## Mumford-Shah functional 

## Hough algorithm 

