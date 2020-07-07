---
title: "Bayer's Pattern"
date: 2020-7-3 18:22:28 -0400
categories: OpenCV
tags:
  - BayerPattern 
use_math: true
---



# Goal 
  Bayer's pattern에 대해서 이해한다. 
  
# Bryce Bayer: an inventor of the Bayer's filter 
  <img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fk.kakaocdn.net%2Fdn%2FxHLex%2FbtqFtKiGpxL%2FpysnUzBETa4Ge7mC50kA1K%2Fimg.jpg" width="450px" height="300px" title="px(픽셀) 크기 설정" alt="Bryce Bayer">

  
# Theory 
  Bayer filter mosaic은 RGB 컬러를 필터링 하기 위한 2차원 격자 배열이다. 이 필터는 50%(Green), 25%(Red), and 25%(Blue)로 이루어져있다. 
  이런 비율로 인해 BGGR, RGBG, GRGB, RGGB로 불리기로 한다. 
  
    Green photosensors for luminance-sensitive element (휘도감지요소)
    Red and Blue for chrominance-sensitive elements (색차감지요소)
  
  인간의 각막(retina)는 M과 L cone cell이라는 것을 이용해서 during daylight 녹색빛에 가장 민감하게 반응하도록 한다. 
  반면, 최근에는 cyan-magenta-yellow의 조합이 빛을 흡수하는데 양자효율을 높이는데 좋은 조합으로 쓰이기도 한다. 
  
  The raw output of Bayer-filter cameras is called a Bayer pattern image, which is a record of one of three colors in each pixel. 
  However, in this image, each pixel cannot fully specify each of the red, green, blue values.
  
  그래서 to obtain a full-color image, 다양한 demosaicing 알고리즘이 interpolation을 통해서 각 픽셀당 RGB의 조합을 찾아낸다. 이 알고리즘의 기본은 주변의 픽셀값들을 이용한다는 것이다. 
  
  
  
  
  
  
