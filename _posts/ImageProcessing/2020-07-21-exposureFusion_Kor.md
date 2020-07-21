---
title: "이미지 노출융합(exposure fusion)이란?"
date: 2020-7-21 12:32:28 -0400
categories: ImageProcessing
tags:
  - openCV 
  - exposure fusion
  - Mertens' algorithm
  - Multiresolution blending
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-07-21
---


# Introduction 

 노출융합(exposure fusion)은 노출시간이 다른 여러장의 사진을 합쳐서 빛의 동적 범위(dynamic range, DR) 사진을 얻어내는 방법이다. 
 동적 범위는 사진상 빛의 가장 밝은 부분과 어두운 부분의 비율을 뜻한다. 이 범위에 따라 사진의 어두운 부분과 밝은 부분이 표현되는 정도가 결정된다. 
 
 즉, 동적 범위가 넓을수록 어두운 부분에서 밝은 부분으로 변화하는 정도가 더 세분화되어 표현하여 좋은 사진을 만든다. 
 
 ![ ](/assets/images/kid_inTwoDifferentExposures.png)
 
 위의 두 사진중 왼쪽은 낮은 동적 범위의 표현이고, 오른쪽은 높은 동적 범위의 사진이다. 왼쪽의 사진에서 하늘은 빛이 밝아 하얀색으로만 표현된 반면, 
 오른쪽 사진에선 구름이 보일 정도로 세밀하게 표현되었다. 이는 동적 범위가 넓어 빛의 밝기가 변하는 단계가 많기 때문이다. 
 
 오른쪽과 사진과 같이 동적범위가 높게 찍힌 것을 High Dynamic Range(HDR) 이미지라고 한다. 반면 왼쪽은 Low DR (LDR) 이미지이다. 
 LDR은 8비트 이미지로 픽셀의 밝기가 0-255 사이로 표현되는 반면, HDR은 16비트 이상의 픽셀값을 가진다. 대개 한 컬러 채널당 16비트의 범위를 가진다. 
 
 위의 사진에서 보여지듯이 HDR은 LDR에 비해 세부사항을 잘 잡아낸다. 하지만, HDR은 카메라에서 별도의 처리과정을 통해 얻어진다.
 기본적인 방법은 빛의 노출이 다른 사진을 여러장 찍어 융합하는 것이다. 
 
 
 ![ ](/assets/images/house.png)
 
 
 

 
 융합하는 방법에는 크게 두 가지 방법이 있다. 
 
 ```
 1. 카메라 반응 곡선을 통한 융합
    [Debevec et al. 1997](https://dl.acm.org/doi/10.1145/258734.258884)  
    
 2. 다중 해상도를 이용한 융합 (multiresolution blending)
    [Mertens et al. 2009](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-8659.2008.01171.x)
 ```
 



# 간략한 이론

## 1. quality measures 

## 2. Gaussian and Laplacian Pyramid

## 3. Multiresolution blending 

## 4. 결과 

# 마무리 
  
  [영어 버전 포스팅](https://gimoonnam.github.io/imageprocessing/MertensFusion/)
  [full code](https://github.com/gimoonnam/ImageProcessing/blob/master/Mertens_algorithm/mergeMertens_fromScratches.ipynb)
  



