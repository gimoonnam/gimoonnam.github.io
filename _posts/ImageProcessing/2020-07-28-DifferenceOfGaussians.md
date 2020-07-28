---
title: "Image Edge Enhancement: Difference of Gaussians(DoG)"
date: 2020-7-28 12:32:28 -0400
categories: ImageProcessing
tags:
   - Difference of Gaussian
   - edge detection 
   - Laplace operator
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-07-28
---


# Introduction 

   지난 포스팅에서 이미지의 가장자리를 강화(edge enhancement)하는 알고리즘 중의 하나인 **Laplace operator**에 대해서 보았습니다. 이 전 포스팅은 아래 링크를 참고하세요. 이 방법은 많이 사용되는 반면 노이즈를 증가시키는 역효과를 발생시킵니다. 이것은 이미 잘 알려진 side effect인데요. 이점을 보완하는 알고리즘이 있습니다. **Difference of Gaussians(DoG)** 라는 방법입니다. 

 **DoG**가 라플라스에 비해 특별히 뛰어나기보다 노이즈를 줄인채 edge를 감지한다는 것에서 장점이 있습니다. 하지만 edge enhancement만 놓고 보면 라플라스가 떠 효과적이라고 할 수 있습니다. 


# Thoery: Difference of Gaussian (DoG)  

분산이 다른 두개의 가우시안 필터를 고려합니다. 이미지이기 때문에 2차원 가우시안 함수가 되고 수식으로는 아래와 같이 표현합니다.

$$
G_1(x,y) = \frac{1}{\sqrt{2\pi\sigma_1^2}}\exp\left(-(x^2+y^2)/2\sigma_{1}^2\right)\nonumber\\ 
G_2(x,y) = \frac{1}{\sqrt{2\pi\sigma_2^2}}\exp\left(-(x^2+y^2)/2\sigma_{2}^2\right)\nonumber
\tag{1} 
$$

여기에서 $\sigma_1$과 $\sigma_2$는 분산이고 이것이 가우시안 블러링의 정도를 결정합니다. 즉, 분산이 커질수록 이미지가 흐려지는 정도가 커지게 됩니다.
**DoG**는 이 두 가우시안 빼는 것입니다. 이때 기억해야 할 것이 빼는 가우시안의 분산이 더 크게 하는 것입니다. 만약 **G1-G2**를 구한다면 G2의 분산이 더 커야 한다는 것입니다. 

 $$
 \sigma_1 < \sigma_2
 \tag{2}
 $$ 

1차원 DoG으로 확인하면 아래와 같이 sigma가 1.0(<span style="color:yellow">노랑</span>) 인 분포를 0.3(<span style="color:red">빨강</span>)으로부터 빼서 <span style="color:blue"> Difference(파랑)</span>을 얻습니다. 

<center>
<img src="/assets/images/DoG_mexicanHat.jpeg" width="600px" >
</center>
   
결과인 파란색 곡선은 mexican hat을 닮은 모양이 됩니다. 평균값에서 주변이 음수로 떨어지며 경계를 뚜렷하게 하는 결과를 만듭니다. 

$f(x,y)$라는 이미지가 있으면 다음과 같이 계산해서 **DoG**가 적용된 이미지를 얻을 수 있습니다. 

$$
f_{\mathrm{sharpened}}(x,y) = f(x,y)* G_1(x,y) - f(x,y) * G_2(x,y)
\tag{3}
$$

여기에서 $* $는 합성곱을 표기한다. 

결과는 흑백 이미지가 되며, 이것은 **band-pass filter**를 적용한 것과 동일하며, 원본 이미지에서 **spatial frequencies**를 제거한 상태가 된다. 이것이 사람의 눈이 사물을 보고 구체적인 정보를 인식하는 과정과 동일하다고 한다. 

# Implementation

## 파이썬 코드(Code)
 
<script src="https://gist.github.com/gimoonnam/18348ab61a82cb9140ed9672d296b8d2.js"></script>


## 결과 (Results)


## 설명 (Explanation)



# Wrapping up


# References 
  
  1. [Interactive tutorial on Difference of Gaussians Edge Enhancement](https://micro.magnet.fsu.edu/primer/java/digitalimaging/processing/diffgaussians/index.html) 
  2. [Blob detection on wikipedia](https://en.wikipedia.org/wiki/Blob_detection#The_Laplacian_of_Gaussian)  
  3. [Unsharp filter](https://homepages.inf.ed.ac.uk/rbf/HIPR2/unsharp.htm)   
  4. [Laplace operator in OpenCV](https://docs.opencv.org/3.4/d5/db5/tutorial_laplace_operator.html)   
  
  
  
  
  
  
