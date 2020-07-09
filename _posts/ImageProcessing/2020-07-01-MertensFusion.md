---
title: "Exposure Fusion using Laplacian Pyramids"
date: 2020-7-1 12:32:28 -0400
categories: ImageProcessing
tags:
  - openCV 
  - exposure fusion
  - Mertens' algorithm
  - Multiresolution blending
use_math: true
toc: true
toc_sticky: true
---

# Introduction  

  This post presents a Python implementation on an exposure fusion using openCV. 
  This method is called a multiresolution blending and was proposed by [Mertens et al.](https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-8659.2008.01171.x)
     
  The image blending using such pyramids is a powerful method, and yields a high quality image. 
  Besides, the Mertens' algorithm does not require a conversion to an HDR image, which is thus proposed as an effective method for an image fusion, 
  as a counterpart of others involving the conversion. The demonstration of HDR's fusion will be studied soon though.  

  **Key Points of Mertens' algorithm**
  >1. No conversion into HDR images 
  >2. Not need to know exposure times 
  >3. Multiresolution blending by Gaussian and Laplacian pyramid images   
  >4. No additional post improvements requried 

 
# Multiresolution Exposure Fusion  

## 1. Theory 
  
### <span style="color:blue"> a. Quality measures </span> 

   * **Contrast ($C$)**
   Application of a Laplacian filter to the grayscale version of images, and take the absolute value of the filtered image. The contrast map captures details on images such as edges and texture. The resultant map is indicated as $C$. 

   * **Saturation ($S$)** 
   The Saturation measures the degree of the exposure. A longer exposed image contains desaturated colors, which will eventually be clipped off. It is desirable to have saturated colors to make vivid images. Here, the saturation is measured as a STD of R, G, and B at each pixel.
  
   * **Well-exposedness ($E$)**
    The raw intensities within a channel reveals how well a pixel is exposed, which is used to make sure that the intensities of all pixels are well ranged between 0 and 1, resepctively, under- and over-exposed. The well-exposedness is evaluated by a Gaussian filter with a mean of 0.5, and this filter applies to each channel individually, each of which will be multiplied to yiled the meausre $E$. 

   The weight map with the above three measures are given as a power function

  $$ 
    W_{ij,k} = \left(C_{ij,k}\right)^{\omega_C}\times \left(S_{ij,k}\right)^{\omega_S} \times \left(E_{ij,k}\right)^{\omega_E}  
    \tag{1}
  $$

  where $k$ indicates an index of image in given image stack, and $i,j$ are pixel's indices. The relative contributions of each measure to the weight is controlled by the exponents $\omega_{C,S,E}$, varying between 0 and 1.


### b. Fusion

  Once the weight maps are constructed for each images, the map needs to be normalized to obtain a consistent result as following,

  $$
    \hat{W}_{ij,k} = \frac{W_{ij,k}}{\left[\sum_{k^{\prime}}^{N} W_{ij,k^{\prime}} \right]}
    \tag{2}
  $$

  The resultant fusion image can then be obtained via a weighted blending of image stack. But it was turned out that the simple fusion produced undesired disturbing seams and halos on resulting images. 

  To get around this problem, the authors employed a multiple resolutions using pyramidal images decomposition. 

  Before blending images, the Laplacian pyramid is generated as a weighted average of Laplacian decompositions for original images and Gaussian pyramid of the weight map. 

  $$
    \mathbf{L}[R]_{ij}^l = \sum_{k=1}^{N}\mathbf{G}[{\hat W}]_{ij,k}^l \mathbf{L}[I]_{ij,k}^l
    \tag{3}
  $$

  Then the final result is obtained by collapsing the Laplacian pyramid up to the original image size. 

  $$
    R_{ij} = \sum_{k=1}^N \mathbf{L}[R]_{ij} I_{ij,k}
    \tag{4}    
  $$

## 2. Import 

```
import os
import cv2
import numpy as np
import matplotlib.pyplot as plt
from matplotlib import gridspec
from IPython.display import Image
``` 

## 3. Load Images   

  First, we import images with different exposure and store them as a list stack. 
  
```
  # read images and save them as a stack 
  path = os.getcwd() + "/house/"    

  filenames = ["A.jpg","B.jpg","C.jpg","D.jpg"]    
  self.images = []
        
  for filename in filenames:
      im = cv2.imread(path+filename).astype(np.float32)/255.0
      self.images.append(im)
    
  self.N = len(self.images) # the number of images 
  self.width  = len(self.images[0]) 
  self.height = len(self.images[0][0])
  self.weightParam = weightParam 
  self.nlev = nlev # number of levels in image pyramids   
``` 
  
  This picture shows the original images writh four different exposures, where an underexposed image becomes darker, but loses details in dark region. 
  On the other hand, an overexposed image becomes brighter but loses details in bright region. The goal of the fusion is to obain an image with details over the entire region. 

  ![ ](/assets/images/house.png)
  

## 4. Acquire weight maps

  Three exponents are specified   
```
def getContrastWeight(self): return self.contrast_para
def getSaturationWeight(self): return self.sat_para
def getExposurednessWeight(self): return self.wexp_para
``` 


``` 
def ConstructWeightMap(self):
    self.contrast_para, self.sat_para, self.wexp_para = self.weightParam         
    self.W = np.ones((self.N, self.width,self.height),dtype=np.float32)
        
    if self.contrast_para > 0:
        self.W = np.power(np.multiply(self.W, self.contrast()),self.contrast_para)
            
    if self.sat_para > 0:
        self.W = np.power(np.multiply(self.W, self.saturation()),self.sat_para)
       
    if self.wexp_para > 0:
        self.W = np.power(np.multiply(self.W, self.well_exposedness()),self.wexp_para)    

    # normalize weight map, whose size will be (width,height,n_images)
    W_sum = self.W.sum(axis=0)
    self.W = np.divide(self.W, W_sum+1e-12)
    np.seterr(divide='ignore', invalid='ignore')        
```



## 5. Simple blending of images with weight maps 

  but this yielded a poor quality ... 
  $$
    R_{ij} = \sum_{k=1}^N \hat{W}_{ij,k} I_{ij,k}
    \tag{5}    
  $$



## 6. Multiresolution blending using image pyramid

![ ](/assets/images/LaplacePyramid.png)

   
![alt text](assets/images/house.png)    

## 7. Wrapping it up 
   
   We have studied a multiresolution blending exposure fusion. 
   The full implementation of the exposure fusion can be found [here](https://github.com/gimoonnam/ImageProcessing/blob/master/mergeMertens_fromScratches.ipynb)
   
   
   
