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


# Introduction 
 
  The goal of this method is to render HDR cenes on conventional display devices, to be tested with real radiance maps as well as synthetically computed radiancce solutions
 
## What is High Dynamic Range(HDR)? 
 ...  
    
## Camera Response Function(CRF)

* The film exposure is defined as $X = E \Deta t$, where $E$ is an irradiance at the film and $\Delta t$ is an exposure time, 
  so $X$ is in unit of $J/m^2$. The exposure measures the total number of photons that each pixel absorb during the exposure time.  
  
  The assumption of this definition holds well in a reasonable range of the exposure times, but 
  can break down under extreme conditions of very large or very low $\Delta t$.
   

* the film reponse to variations in exposure $X$ is a non-linear function, called "characteristic curve" of the film, 
      accounting for a non-linear relationship between pixel exposure $X$ and its intensity $Z$

* To cover the full dynamic range, one can take a series of photographs with different exposures, 
      raising a question on **how to combine these separate images into a composite radiance map** 
  
* 
  
  
# Algorithm
  

