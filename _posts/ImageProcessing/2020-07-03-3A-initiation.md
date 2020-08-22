---
title: "3A Algorithms in Digital Smartphones"
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
  
# 1. Autofocus(AF) algorithms 

  * Algorithms and formulas are based on perceptions of the **human eyes**, which are more sensitive to brightness/luminance compared to chrominance   
  * **Y** value in the colorspace of both **YUV** and **YCrCb** indicates the **luminance**  
  
  
## Contrast-based Autofocus as the basic algorithm 
  
  * measures the contrast at different lens positions 
  * find the **maximum** contrast. 
  * the contrast is defined as **the degree of sharpness** within an image 
  
  
## How to define contrast? 

  * The complexity of the autofocus algorithm depends on the method to define the contrast, which is different from company to company   
  * <span style="color:blue"> **Canny Edge Detection**  </span>: one basic method for assigning a contrast value, available in **OpenCV**.  
 
 
## Other common algorithms 
 
  * <span style="color:blue"> PDAF (Phase Detection Auto Focus) </span>  [(YouTube video) PDAF vs Original AF](https://www.youtube.com/watch?v=IZ3Wdq8S1O0).  
  * Laser   
  * Machine Learning-based definition of contrast.   


  
# 2. Autoexposure(AE)

## General Scheme of Algorithm 

Auto exposure is to find an optimal exposure time at a given environment, which is 
typically made in the following steps.  

**Step 1**: A pre-determined exposure value can be calculated as follow
 
 
 \begin{equation}
 EV = \log_2\left(F^2/T \right) = 2\log_2(F) - \log_2(T)
 \label{eq:EVpre}
 \end{equation}
 
 * **$EV$**: Exposure value   
 * **F**: Aperture size 
 * **T**: exposure time (duration) 


**Step 2**: Convert the **RGB** values to Brightness $B$  
**Step 3**: Derive a single number $B_{pre}$ from the brightness picture   
**Step 4**: Calculate the optimum exposure $EV_{opt}$ 

\begin{equation}
EV_{opt} = EV_{pre} + \log_2(B_{pre}) + \log_2(B_{opt}) 
\end{equation}


## Mean Value AE (Ref.5) 
 
 
## High Dynamic-Range Histogram(HDH) AE





# 3. Autowhitebalance(AWB)

  
  
  
# References 
  1. [Medium: How the camera Autofocus feature works in Digital smartphone](https://medium.com/@sedara/how-the-camera-autofocus-feature-works-in-digital-smartphones-8382d511996c#e3b6).  
  2. [Color conversion in OpenCV](https://docs.opencv.org/3.1.0/de/d25/imgproc_color_conversions.html).  
  3. [Naver blog](https://m.blog.naver.com/PostView.nhn?blogId=pamtek&logNo=220647682375&proxyReferer=https:%2F%2Fwww.google.com%2F).  
  4. [What is PDAF and how does it work?](https://www.androidauthority.com/how-pdaf-works-1102272/). 
  5. [Using Brightness Histogram to perform
Optimum Auto Exposure](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.149.8920&rep=rep1&type=pdf).
  
     
   
  
 
  
