---
title: "이미지 노출융합(exposure fusion)이란?"
date: 2020-7-21 12:32:28 -0400
categories: ImageProcessing
tags:
  - openCV 
  - exposure fusion
  - Multiresolution blending
  - tone mapping (톤맵핑)
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-07-22
---


# Introduction 

 노출융합(exposure fusion)은 노출시간이 다른 여러장의 사진을 합쳐서 빛의 동적 범위(dynamic range, DR) 사진을 얻어내는 방법이다. 
 동적 범위는 사진상 빛의 가장 밝은 부분과 어두운 부분의 비율을 뜻한다. 이 범위에 따라 사진의 어두운 부분과 밝은 부분이 표현되는 정도가 결정된다. 
 
 즉, 동적 범위가 넓을수록 어두운 부분에서 밝은 부분으로 변화하는 정도가 더 세분화되어 표현하여 좋은 사진을 만든다.    
 
<img src="/assets/images/kid_inTwoDifferentExposures.png" width="600px" >  

 위의 두 사진중 왼쪽은 낮은 동적 범위의 표현이고, 오른쪽은 높은 동적 범위의 사진이다. 왼쪽의 사진에서 하늘은 빛이 밝아 하얀색으로만 표현된 반면, 
 오른쪽 사진에선 구름이 보일 정도로 세밀하게 표현되었다. 이는 동적 범위가 넓어 빛의 밝기가 변하는 단계가 많기 때문이다. 
 
 오른쪽과 사진과 같이 동적범위가 높게 찍힌 것을 High Dynamic Range(HDR) 이미지라고 한다. 반면 왼쪽은 Low DR (LDR) 이미지이다. 
 LDR은 대개 8비트 이미지로 픽셀의 밝기가 0-255 사이로 표현되는 반면, HDR은 범위의 최소 16비트 이상의 실수 픽셀값을 가진다. 
 
 위의 사진에서 보여지듯이 HDR은 LDR에 비해 세부사항을 잘 잡아낸다. 하지만, HDR은 카메라에서 별도의 처리과정을 통해 얻어진다.
 기본적인 방법은 빛의 노출이 다른 사진을 여러장 찍어 융합하는 것이다. 

 아래 사진은 4개의 다른 노출시간으로 찍은 사진을 보여준다. 


  ![Four different exposure images](/assets/images/house.png)


 노출시간이 적은 것을 underexposed, 긴 것을 overexposed 되었다고 한다. 적절한 노출시간을 준다고 해도 밝은 부분과 어두운 부분을 동시에 세밀하게 나타난 이미지를 
 얻는 것은 쉽지 않다. 따라서 이렇게 노출시간을 달리하며 여러장의 사진을 찍어 이것들을 융합해 이미지의 모든 부분을 세밀하게 표현한 사진을 얻는 것이다. 
 
 노출시간이 짧은 사진은 빛이 많은 부분을 세밀하게 표현할 수 있는 반면 어두운 부분은 충분한 빛을 받지 못해 어둡게 나온다. 
 대조적으로 노출시간이 긴 사진은 어두운 부분은 세밀하게 표현하지만, 밝은 부분은 하얗게만 표현된다. 
 
 아래 사진은 위의 사진들을 융합한 결과이다. 집의 내부와 외부의 모습 모두 세밀하게 표현되어있다. 
 
 이결과는 Mertens이 제안한 다중 해상도를 이용해서 융합한 결과이다. 이 방법은 HDR 이미지의 획득없이 최종결과를 얻을 수 있다는 장점이 있다. 
 이 알고리즘에 대한 자세한 설명은 아래 링크에서 볼 수 있다. 
 
 <img src="/assets/images/houseFused.png" width="600px" >
 
 

# Exposure Fusion algorithms 
 
 융합하는 방법에는 크게 두 가지 방법이 있다. 

 1. 카메라 반응 곡선을 통한 융합 (Camera Repsonse Function)   
    [Debevec et al. 1997](https://dl.acm.org/doi/10.1145/258734.258884)   
    [구체적인 내용은 이 링크를 참고하세요](https://gimoonnam.github.io/imageprocessing/Debevec_HDR/)   
    
 2. 다중 해상도를 이용한 융합 (multiresolution blending)   
    [Mertens et al. 2009](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-8659.2008.01171.x)   
    [구체적인 내용은 이 링크를 참고하세요](https://gimoonnam.github.io/imageprocessing/MertensFusion/)   
 

## 카메라 반응 곡선을 이용한 융합 


## 다중 해상도를 이용한 융합


# 마무리 
  
  [영어 버전 포스팅](https://gimoonnam.github.io/imageprocessing/MertensFusion/)
  [full code](https://github.com/gimoonnam/ImageProcessing/blob/master/Mertens_algorithm/mergeMertens_fromScratches.ipynb)
  



