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
---

# Introduction  

  This post presents a Python implementation on an exposure fusion using openCV. 
  This method is called a multiresolution blending and was proposed by [Mertens et al.][https://onlinelibrary.wiley.com/doi/abs/10.1111/j.1467-8659.2008.01171.x]
 
  The exposure fusion aims to obtain a good quality image from images taken at different exposures. 

  The image blending using such pyramids is a powerful method, and yields a high quality image. 
  Besides, the Mertens' algorithm does not require a conversion to an HDR image, which is thus proposed as an effective method for an image fusion, 
  as a counterpart of others involving the conversion. The demonstration of HDR's fusion will be studied soon though.  

  **Key Points of Mertens' algorithm**
  ``` 
    1. No conversion into HDR images 
    2. Multiresolution blending by Gaussian and Laplacian pyramid images  
    3. No additional post improvements requried 
  ```
 
  <src img="https://github.com/gimoonnam/gimoonnam.github.io/blob/master/assets/images/house.png">
 
 
 
# Theory  


## <span style="color:blue"> Quality measures </span> 

 * **Contrast ($C$)**
    Application of a Laplacian filter to the grayscale version of images, and take the absolute value of the filtered image. The contrast map captures details on images such as edges and texture. The resultant map is indicated as $C$. 

 * **Saturation ($S$)** 
  The Saturation measures the degree of the exposure. A longer exposed image contains desaturated colors, which will eventually be clipped off. It is desirable to have saturated colors to make vivid images. Here, the saturation is measured as a STD of R, G, and B at each pixel.
  
 * **Well-exposedness ($E$)**
  The raw intensities within a channel reveals how well a pixel is exposed, which is used to make sure that the intensities of all pixels are well ranged between 0 and 1, resepctively, under- and over-exposed. The well-exposedness is evaluated by a Gaussian filter with a mean of 0.5, and this filter applies to each channel individually, each of which will be multiplied to yiled the meausre $E$. 

  The weight map with the above three measures are given as a power function

  $$ 
    W_{ij,k} = \left(C_{ij,k}\right)^{\omega_C}\times \left(S_{ij,k}\right)^{\omega_S} \times \left(E_{ij,k}\right)^{\omega_E}                            
  $$

  where $k$ indicates an index of image in given image stack, and $i,j$ are pixel's indices. The relative contributions of each measure to the weight is controlled by the exponents $\omega_{C,S,E}$, varying between 0 and 1.


## Fusion

  Once the weight maps are constructed for each images, the map needs to be normalized to obtain a consistent result as following,

  $$
    \hat{W}_{ij,k} = \frac{W_{ij,k}}{\left[\sum_{k^{\prime}}^{N} W_{ij,k^{\prime}} \right]}
  $$

  The resultant fusion image can then be obtained via a weighted blending of image stack. But it was turned out that the simple fusion produced undesired disturbing seams and halos on resulting images. 

  To get around this problem, the authors employed a multiple resolutions using pyramidal images decomposition. 

  Before blending images, the Laplacian pyramid is generated as a weighted average of Laplacian decompositions for original images and Gaussian pyramid of the weight map. 

  $$
    \mathbf{L}[R]_{ij}^l = \sum_{k=1}^{N}\mathbf{G}[{\hat W}]_{ij,k}^l \mathbf{L}[I]_{ij,k}^l
  $$

  Then the final result is obtained by collapsing the Laplacian pyramid up to the original image size. 

  $$
    R_{ij} = \sum_{k=1}^N \mathbf{L}[R]_{ij} I_{ij,k}
  $$


  
  
  
  
