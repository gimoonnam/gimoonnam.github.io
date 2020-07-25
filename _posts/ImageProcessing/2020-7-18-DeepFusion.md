---
title: "iPhone: 딥 퓨전(Deep Fusion)이란 무엇인가?"
date: 2020-7-18 12:32:28 -0400
categories: ImageProcessing
tags:
  - HDR image 
  - Deep Fusion
  - iPhone 11's Camera 
  - Merging images 
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-07-22
---


<img src="/assets/images/iphone11camera-induction.jpg" width="500px" >

# Introduction

최근 이미지 [노출 융합 (exposure fusion)](https://gimoonnam.github.io/imageprocessing/exposureFusion_Kor/)를 공부하며, 
자연스럽게 Deep Fusion에 관심을 가지게 되었다.  

Deep Fusion은 고전적인 이미지 융합 방법과는 다르게 Deep Learning을 이용하는 방법으로 아이폰에는 11부터 적용되었다. 

구글의 픽셀폰에 비하면 다소 늦은 적용이지만, 아이폰 카메라의 업그레이드에 시기적으로 맞춘 것으로 보인다. 

딥 퓨전은 AI 기술을 이용해 노출시간이 다른 여러장의 사진을 융합하며 사진의 선명함(sharpness)를 개선하는 방법이다. 이것은 아이폰 11의 A13 Bionic Neural Engine을 사용하여 사진속 물체의 질감과 디테일을 향상시키며, 빛이 적을 때는 노이즈 제거하여 사진의 품질을 높인다. 

하지만 아이폰에서 실제 이 딥 퓨전 기능이 있는지 확인할 수 있는 표시는 없다. 
즉, 우리는 찍은 사진이 딥 퓨전으로 찍은 것인지 아닌지 알 수 없다. 단지 주변 빛의 조건을 고려해 자동으로 기능이 활성화 된다고 한다. 

빛의 양이 적을때 그 기능이 활성화 되며, 밝은 곳에서는 ***smart HDR*** 만 작동한다.

또한, 딥 퓨전은 아이폰 11 pro 카메라에서 Tele와 Wide 렌즈에만 작용하며, super-wide 렌즈에는 기능이 없다고 한다. 


<img src="/assets/images/DeepFusionOniPhone.jpeg" width="500px" >


<span style="color:blue"> **Deep Fusion은 어떻게 작동하는가?** </span>  

총 9장의 사진을 찍는다. **이중 8장(짧은 노출로 4장 + 표준 노출로 4장)** 은 셔터를 누르기 전에 카메라가 이미 찍어 놓는다. 
셔터를 누르면 나머지 한장을 긴 노출시간으로 찍는다.  

여기에서 **표준노출**의 사진은 낮은 주파수(low frequency)의 정보를 가진다. 따라서 이것은 세밀한 부분을 캡쳐하기 보다 사진의 컬터톤과 같은 정보를 포함하는 사진이 된다. 반면, **짧은노출**의 사진은 아주 짧은 시간동안만 빛을 받아 높은 주파수의 정보 즉 세밀한 특징을 잡아낸다. 

이 사진들을 가지고 딥 퓨전은 우선 긴 노출 하나와 표준 노출 3개로 **synthetic long**로 불리는 긴 노출 사진을 하나 만든다. 이 synthetic long과 짧은 노출 사진을 뉴럴 네트워크에 넣어 분석한다.

DF는 노이즈 감소하는 필터를 각각의 이미지에 적용하여, 픽셀 by 픽셀로 이미지들을 합성한다. 이렇게 만들어진 사진을 <span style="color:blue"> Computational photography </span>라고 애플은 소개했다. 

사진을 찍는 아주 간단한 작업에서 이렇게 복잡한 과정이 있다는게 신기하기만 한데, 어떤 알고리즘이 사용되는지 
공개되진 않았을 것 같지만, 일반적으로 deep fusion에서 사용되는 알고리즘에 대해서 알아보도록 하겠다. 

# Algorithm

convolution neural network 

# Demo 

DF images compared with Smart HDR 


# References 

1. [Google's night sight on pixel](https://venturebeat.com/2018/11/14/google-pixel-night-sight/)   
2. [Deep Fusion Demo](https://petapixel.com/2019/10/28/deep-fusion-demo-trying-out-apples-computational-photography-tech/)   
3. [Comparison with Smart HDR](https://www.tomsguide.com/hands-on/iphone-11-deep-fusion-camera-tested-how-much-better-is-it)   
4. [paper]() 





