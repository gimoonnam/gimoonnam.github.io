---
title: "A Review on Recovering HDR Radiance map from Photographs"
date: 2020-7-12 12:32:28 -0400
categories: ImageProcessing
tags:
  - openCV 
  - exposure fusion
  - Debevec's algorithm
  - recovering HDR radiance map 
  - film response function 
use_math: true
toc: true
toc_sticky: true
---

In this post, I will review and implement the Debevec's algorithm for recovering HDR radiance map from photographs taken at different exposure times. 
This post is followed by Mertens' algorithm as a series of study on exposure fusion to obtain a full detail image from differently exposed images. 
The implementation is made in Python using openCV.

# Introduction 
 
  The goal of this method is to render HDR cenes on conventional display devices, to be tested with real radiance maps as well as synthetically computed radiancce solutions
 
## What is High Dynamic Range(HDR)? 
 ...  
    
## Camera Response Function(CRF)

* The film exposure is defined as $X = E \Delta t$, where $E$ is an irradiance at the film and $\Delta t$ is an exposure time, 
  so $X$ is in unit of $J/m^2$. The exposure measures the total number of photons that each pixel absorb during the exposure time.  
  
  The assumption of this definition holds well in a reasonable range of the exposure times, but 
  can break down under extreme conditions of very large or very low $\Delta t$.
   

* the film reponse to variations in exposure $X$ is a non-linear function, called "characteristic curve" of the film, 
      accounting for a non-linear relationship between pixel exposure $X$ and its intensity $Z$

* To cover the full dynamic range, one can take a series of photographs with different exposures, 
      raising a question on **how to combine these separate images into a composite radiance map** 
  
  
  
# Algorithm
  
* input: a number of digitized photographs taken from the same point with different exposure times
  (assumed that the scene is static and gathering these process is completed quickly enough so that the change in lighting can be safely ignored) 


## Camera Response Function 

Suppose that we have a nonlinear function $f$ mapping the exposure $X$ to pixel values $Z$, 

$$ 
f(X) = Z   \longleftrightarrow  X = f^{-1}(Z), 
\tag{1}
$$

Then the reconstruction of the irradiance map from the pixel values can be obtained by applying inverse $f$, 
where $f$ is assumed to be a smooth and continuous function. 

Eq.1 can be expressed with pixel($i$) and image($j$) indices as follow 

$$
E_i \Delta t_{j} = f^{-1}(Z_{ij})
\tag{2}
$$

where $Z_{ij}$ indicates $i$th pixel values of $j$th image. This equation can be rewritten as follow 

$$
g(Z_{ij}) = \ln E_i + \ln \Delta t_j
\tag{3}
$$

where $g = \ln f^{-1}$. 

## Objective function for the optimization of CRF 

$$
O = \sum_{i=1}^{N}\sum_{j=1}^{P} \[g(Z_{ij}) - \ln E_i - \ln \Delta t_j \]^2 + \lambda \sum_{z=Z_{min}+1}^{Z_{max}+1} g^{\dprime}(z)^2 
\tag{4}
$$
