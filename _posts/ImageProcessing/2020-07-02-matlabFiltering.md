---
title: "Image filtering in Matlab"
date: 2020-7-2 18:22:28 -0400
categories: ImageProcessing
tags:
  - matlab image filtering
  - imfilter 
  - filter2 
  - conv2
use_math: true
---
# 매트랩에서 이미지 필터링 방법

## Goal
  매트랩 이용한 이미지 필터링을 이해한다. 아래의 세가지 대표적인 내장 함수가 있다. 이들의 사용법을 보며 이미지의 필터링이 어떻게 이루어지는지 알아본다.
  
     1. imfilter 
     2. filter2  
     3. conv2    
     correlation(상관) 필터링과 convolution(합성) 필터링의 차이를 이해한다. 
  

## Theory 

   필터링 행렬의 슬라이딩으로 원본 행렬의 값을 바꾼다. 필터링에는 원본 행렬(A)과 필터링 행렬(h)이 필요하다. $M$ 과 $N$을 각각 열과 행의 갯수라 하면 

    A의 크기 ($M_a$, $N_a$) 
    h의 크기 ($M_h$, $N_h$)
    
   또한 필터링이 된 결과 행렬(B)이 있을 것이고, 이것의 크기 $(M_b,N_b)$는 다음의 두가지 경우로 나뉜다. 
  
    1. $(M_b, N_b) = (M_a+M_h-1, N_a+N_h-1)$ for option 'full' (그림)
    2. $(M_b, N_b) = (M_a,N_a)$ for option 'same' (image analysis)(그림) 

   1번의 경우는 full filtering의 결과로 원본행렬보다 큰 사이즈의 결과 행렬을 얻는다. 반면, 2번의 경우는 원본과 결과 행렬의 크기가 같다. 
   2번의 이미지 분석을 하는데 사용하는 옵션이다. 즉, 필터링 후에도 이미지의 크기가 변하지 않아야 한다. 

### 상관과 합성필터링의 차이: 

   커널 행렬의 회전하여 원본 행렬에 적용 (상관 :무회전, 합성 필터링: 180도 회전)
  
   1. filter2(h,A): correlation filtering  
   
   2. conv2(A,h): convolution filtering 

   (상관 필터링) imfilter with two shapes: full and same 
   
     1. imfilter(A,h,'full') = filter2(h,A,'full') 
     2. imfilter(A,h,'same') = filter2(h,A) 

   (합성 필터링) imfilter with two shapes: full and same 
   
     1. imfilter(A,h,'full','conv') = conv2(A,h,'full') 
     2. imfilter(A,h,'conv') =  conv2(A,h,'same')


### imfilter: 입력 데이터와 동일한 사이즈의 행렬을 출력한다.

   'replicate' : 배열의 경계 밖에 있는 입력 배열 값은 가장 가까운 배열 테두리 값과 같은 것으로 간주한다. 
     
   'symmetric' : 배열의 경계 밖에 있는 입력 배열 값은 배열 테두리를 기준으로 배열을 대칭 복사하여 계산됩니다.
     
   'circular'  : 배열의 경계 밖에 있는 입력 배열 값은 암시적으로 입력 배열을 주기적이라고 간주하여 계산됩니다.
   
    
    
