---
title: "Autofocus algorithm in Digital smartphones"
date: 2020-7-3 23:34:28 -0400
categories: ImageProcessing
tags:
  - 3A algorithm
  - Autofocus
  - AutoWhiteBalance
  - AutoExposure
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-08-11
---

# Introduction 
  
  
## Autofocus algorithms 

  * Algorithms and formulas are based on perceptions of the **human eyes**, which are more sensitive to brightness/luminance compared to chrominance   
  * Y value in both **YUV** and the **YCrCb** color space indicates the **luminance**  
  
  
### Contrast-based Autofocus as the basic algorithm 
  
  a. measures the contrast at different lens positions 
  b. find the **maximum** contrast. 
  c. the contrast is defined as **the degree of sharpness** within an image 
  
  
### How to define contrast? 

  a. The complexity of the autofocus algorithm depends on the method to define the contrast, which is differene from company to company   
  b. <span style="color:blue"> **Canny Edge Detection**  </span>: one basic method for assigning a contrast value, available in **OpenCV**.  
 
 
### Other common algorithms 
 
  a. PDAF (Phase Detection Auto Focus) 
  b. Laser 
  c. Machine Learning-based definition of contrast 


  {% include 파일명.html id="https://www.youtube.com/watch?v=IZ3Wdq8S1O0" %}  

  
  
# References 
  1. [Medium: How the camera Autofocus feature works in Digital smartphone](https://medium.com/@sedara/how-the-camera-autofocus-feature-works-in-digital-smartphones-8382d511996c#e3b6).  
  2. [Color conversion in OpenCV](https://docs.opencv.org/3.1.0/de/d25/imgproc_color_conversions.html).  
  3. 
  
  
     
   
  
 
  
