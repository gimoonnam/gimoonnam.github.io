---
title: "Bayer's Pattern"
date: 2020-7-3 18:22:28 -0400
categories: OpenCV
tags:
  - BayerPattern 
  - Color Filter Array(CFA)
  - Demosaicing 
  - interpolation algorithm 
use_math: true
---

# Goal 
  Bayer's pattern에 대해서 이해한다. 
  
# Bayer filter

  Bayer filter mosaic은 RGB 컬러를 필터링 하기 위한 2차원 격자 배열이다. 이 배열은 디지털 사진에 컬러를 입히는데 사용되는 Color Filter Array(CFA)의 대표적인 필터링이다. 
  이것은 Kodak의 연구원이었던 Bryce Bayer가 처음으로 고안하여 지금까지 거의 모든 디지털 카메라에 사용되고 있다. 
  
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FxHLex%2FbtqFtKiGpxL%2FpysnUzBETa4Ge7mC50kA1K%2Fimg.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="Bryce Bayer">

  Bayer필터는 50%(Green), 25%(Red), and 25%(Blue)로 이루어있다. 인간의 눈은 자연광에서 녹색에 가장 민감하게 반응하기 때문에 Bayer필터에는 
  Green이 Blue나 Red보다 많이 들어있으며, 녹색은 휘도감지, 즉 빛의 밝기에 민감한 센서요소가 되며, 빨강과 파랑은 색차를 감지하는데 좋은 요소이다. 이것을 영어로 다음과 같이 표현한다. 
  
    1. Green photosensors for luminance-sensitive element (휘도감지요소)
    2. Red and Blue for chrominance-sensitive elements (색차감지요소)
 
   
# Demosaicing 
 
  The raw output of Bayer-filter cameras is called a Bayer pattern image, which is a record of one of three colors in each pixel. 
  However, in this image, each pixel cannot fully specify each of the red, green, blue values.
  
  To obtain a full-color image, 다양한 알고리즘이 interpolation을 통해서 각 픽셀당 RGB의 조합을 찾아낸다.
  이 알고리즘의 기본은 주변의 픽셀값들을 이용한다는 것이다. 이것을 **demosaicing** or **debayering** 이라고 부른다. 

  Color Filter Array(CFA)는 디지털 카메라내에 이미지 센서 앞에 위치한다. 따라서 빛이 들어오면 센서에 감지되는 것은 필터링된 컬러이다. 
   
  즉, Bayer filter를 사용했을때 각 픽셀에 R,G,B 컬러 셋중 하나씩 raw intensity로 기록된다. 
  이것은 알고리즘을 통해 픽셀당 RGB컬의 조합을 찾아내는 것이다. 이것을 demosaicing이라고 한다. 
   
   여러가지 알고리즘 중 가장 많이 사용되는 것은 interpolation(내삽)을 이용한 방법이다. 대표적으로 다음의 두 가지 간단한 내삽을 사용한다.
   
    - nearest-neighbor interpolation (poor result but good for previews) 
    - bilinear interpolation (a bit more complicated algorithm)
    - linear interpolation (the most good results)
    
   
      

   
   
  
  
  
