---
title: "3A Algorithms in Digital Cameras"
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
last_modified_at: 2020-08-22
---
  
# 1. Autofocus(AF) algorithms 

Camera's autofocus automatically adjusts the distance between the camera lens and the CCD through the camera's internal micro-driving motor to ensure that the image plane is projected onto the CCD's image surface.

<img src="/assets/images/AF_fig1.png" width="300px" >

  * Algorithms and formulas are based on perceptions of the **human eyes**, which are more sensitive to brightness/luminance compared to chrominance   
  * **Y** value in the colorspace of both **YUV** and **YCrCb** indicates the **luminance**  
  
  
## a. Contrast Detection AutoFocus (CDAF) 
  
  * measures the contrast at different lens positions 
  * find the **maximum** contrast. 
  * the contrast is defined as **the degree of sharpness** within an image 
    
  
  **Image clarity evaluation methods**

  The complexity of the autofocus algorithm depends on the method to define the contrast, which is different from company to company   
  ```
1. Canny Edge Detection
2. Tenengrad gradient method (using Sobel operator) 
3. Laplacian gradient method (using Laplace operator) 
4. Variance method 
 ```
 
## b. Other algorithms 
 
  * <span style="color:blue"> Phase Detection Auto Focus (PDAF) </span>  [(YouTube video) PDAF vs Original AF](https://www.youtube.com/watch?v=IZ3Wdq8S1O0).   
  * Machine Learning-based definition of contrast


  
# 2. Autoexposure(AE)

<img src="/assets/images/AE_fig1.png" width="500px" >


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




# 3. Autowhitebalance(AWB) (Color Balancing) 

<img src="/assets/images/AWB_fig1.png" width="500px" >

Human eyes adapt to varying illumination conditions that image sensor can't, thus this needs to be computed 

There are two ways of balancing 
- Pre-computed sets 
- Guess with an algorithm 

## Algorithms [ref](https://www.programmersought.com/article/97221124576/)
  
  * Gray World White Balancing Algorithm 
  * perfect reflection 
  * Dynamic threshold 

  
  
  
  
# References 
  1. [Medium: How the camera Autofocus feature works in Digital smartphone](https://medium.com/@sedara/how-the-camera-autofocus-feature-works-in-digital-smartphones-8382d511996c#e3b6).  
  2. [Color conversion in OpenCV](https://docs.opencv.org/3.1.0/de/d25/imgproc_color_conversions.html).  
  3. [Naver blog](https://m.blog.naver.com/PostView.nhn?blogId=pamtek&logNo=220647682375&proxyReferer=https:%2F%2Fwww.google.com%2F).  
  4. [What is PDAF and how does it work?](https://www.androidauthority.com/how-pdaf-works-1102272/). 
  5. [AE: Using Brightness Histogram to perform
Optimum Auto Exposure](http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.149.8920&rep=rep1&type=pdf).
  6. [AWB: Gray World Algorithm](https://web.stanford.edu/~sujason/ColorBalancing/grayworld.html).  
  7. [AWB: By OpenCV on Stack**overflow**](https://stackoverflow.com/questions/46390779/automatic-white-balancing-with-grayworld-assumption)
  
  8. [OpenCV autofocus using gradient operators](https://www.programmersought.com/article/2549148775/) 
     
   
  
 
  
