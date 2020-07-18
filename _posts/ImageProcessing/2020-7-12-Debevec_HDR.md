---
title: "Recovering HDR Radiance map by Camera Response Curves"
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

In this post, I will review and implement the Debevec's algorithm for recovering HDR radiance map from photographs taken at different exposure times. 
This post is written as a series of study on exposure fusion to obtain a full detail image from differently exposed images. 
The implementation is made in Python using openCV.

## What is High Dynamic Range(HDR)? 
 
 The Dynamic Range(DR) is defined as a ratio between darkest and brightest values. The High DR (HDR) refers then to an extended dynamic range of the brigthness. The brightness in the normal DR is ranged between 0 and 255 as 8-bit image, while the HDR extends such range to much larger than 255, up to $2^{32}-1 $ for 32-bit image. Thus, this extension allows to accommodate a high resolution of changes in the brighness, so that the HDR image captures great details in both bright and dark regions compared to DR images. 
 
 ![ ](/assets/images/kid_inTwoDifferentExposures.png)
 
 As shown in the two pictures above, the right one, which is HDR image, draws details in both the sky and the ground, corresponding to relatively bright and dark areas, respectively.
 On the other hand, in the left picture, the sky just appears as white background, which is due to limited dynamic range. 
 
 Recenlty, the HDR images have become very popular technique as they can be obtained at the level of software development. 
 
## Camera Response Function(CRF)
  
  One very early attempt to produce an HDR image is to use a camera response curve, which relates the pixel values to irradiance of an object.   
  
* The film exposure is defined as $X = E \Delta t$, where $E$ is an irradiance at the film and $\Delta t$ is an exposure time, 
  so $X$ is in unit of $J/m^2$. The exposure measures the total number of photons that each pixel absorb during the exposure time.  
  
  The assumption of this definition holds well in a reasonable range of the exposure times, but 
  can break down under extreme conditions of very large or very low $\Delta t$.
   

* the film reponse to variations in exposure $X$ is a non-linear function, called "characteristic curve" of the film, 
      accounting for a non-linear relationship between pixel exposure $X$ and its intensity $Z$


# Debevec's Algorithm
 
  The goal of this method is to render HDR cenes on conventional display devices, to be tested with real radiance maps as well as synthetically computed radiancce solutions
   
* To cover the full dynamic range, one can take a series of photographs with different exposures, 
      raising a question on **how to combine these separate images into a composite radiance map** 
    
* input: a number of digitized photographs taken from the same point with different exposure times
  (assumed that the scene is static and gathering these process is completed quickly enough so that the change in lighting can be safely ignored) 


## 1. Camera Response Function 

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

## 2. Weighted Objective Function for CRF Optimization 

$$
O = \sum_{i=1}^{N}\sum_{j=1}^{P}  \left( \omega(Z_{ij})\left[g(Z_{ij}) - \ln E_i - \ln \Delta t_j \right]\right)^2 + \\ \lambda \sum_{z=Z_{min}+1}^{Z_{max}+1} \left[ \omega(Z_{ij})g^{''}(z)\right]^2 
\tag{4}
$$

The first term ensures that the solution satisfies eq.3 in a least square sense. The second term gives a smoothness, 
where the second derivative is given as a discrete form $g^{''}(z) = g(z-1) - 2g(z) + g(z+1)$ and $\lambda$ is a weight of the second term over the first one.
$P$ and $N$ are the number of photographs and of pixels, respectively. 

$\omega(z)$ is a weight function to impose the smoothness and fitting terms toward the middle of the response curve, which is chosen as a simple hat function as 

$$
\omega(z) = \begin{cases}
    z-Z_{min}, & \text{for} \,z \leq \frac{1}{2}\left(Z_{min}+Z_{max}\right) 
    \\ Z_{max}-z, & \text{for}\, z > \frac{1}{2}\left(Z_{min}+Z_{max}\right) 
  \end{cases}
\tag{5}
$$

When measuring the response curve, the pixel locations should be chosen in a way that they are reasonably evenly distributed over $Z_{min}$ and $Z_{max}$, 
so that the pixels are to be well sampled from the images.


## 3. Constructing HDR Radiance Map 

  Once the response curves have been obtained, the original images can be merged into a single HDR image via 
  
  $$  
  \ln E = \frac{\sum_{j=1}^{P}\omega(Z_{ij})\left(g(Z_{ij} - \ln \Delta t_{j}) \right)    }{\sum_{j=1}^{P}\omega(Z_{ij})}
  \tag{6}
  $$

  Combining the mutiple exposures has the effect of reducing noises. 
  The picture below is the merged HDR map, which looks somewhat bright, 
  this is because the sampling of bright pixels was made with an equal probability as dark parts. 
    

# Python Implemention 

## 1. Load Images 

  Here, we considered four images taken with different exposure times, which are loaded with exposure times by the following lines 
  
  ```
filenames = ["img0.jpg", "img1.jpg", "img2.jpg", "img3.jpg"]
self.images = [cv2.imread(''.join(path+fn)) for fn in filenames]
self.times = np.array([1/30.0, 0.25, 2.5, 15.0], dtype=np.float32)
  ``` 
  
 where *'self'* comes from the extraction from class (see the full code) 
 
 The loaded images appears as below 
 
 <img src ="https://raw.githubusercontent.com/gimoonnam/ImageProcessing/master/images/saintLouis_tower.png" width="600">
  
 The exposure time increases from right to left. 
 
 The following block defines variables associated with images,  
 ```
self.N = len(self.images)
self.row = len(self.images[0])
self.col = len(self.images[0][0])
self.l = 10 
 ```
 $N$ is the number of images, (here $N=4$), and row and col indicates the height and width of image in pixels. 
 $l$ denotes $\lambda$ as a weighting factor for smoothness of the CRF. 
 
 Then, the images are aligned based on median threshold bitwise(MTB) method  

 ```
# Align input images
alignMTB = cv2.createAlignMTB()
alignMTB.process(self.images, self.images)
 ```
 
 The alignment of images is an important step, otherwise the fused image will get blurred. 
 
## 2. Weight function 
  
  The weight function $\omega(z)$ in eq.5 is constructed as follow  
  
  ```
  def constructWeightingFunction(self):
      # construct a weighting function 
      Zmin = 0 
      Zmax = 255 
      Zmid = (Zmax+Zmin)//2

      self.w = np.zeros((Zmax-Zmin+1))

      for z in range(Zmin,Zmax+1): 
          if z <= Zmid:
              self.w[z] = z - Zmin + 1
          else: 
              self.w[z] = Zmax - z + 1
  ```
  
  The constructed weight function is shown as below, and this function will impose weight to the pixel values around the median of 255 in recovering HDR map. 
  
  <img src ="/assets/images/weightFunction.png" width="300">
 
 
 
## 3. Camera Response Curves 
 
 A response curve is obtained by sampling pixels from given images. The number of samples is determined by $n_{sampling} (P-1) > (Z_{max} - Z_{min})$, which ensures a sufficiently overdetermined system as proposed in the original paper

```
numSamples = math.ceil(255*2/(self.N-1))*2
numPixels = self.row * self.col
        
step = int(np.floor(numPixels/numSamples))
self.sampleIndices = list(range(0,numPixels,step))[:-1]  
``` 

This code block shows that we sampled pixels in an equal interval, and the pixel indices are stored in 'sampleIndices'. 

The following code shows that the sampling is made on individual channels. 

```
# set arrays to store pixel values at sampled locations 
      
self.ZG = np.zeros((numSamples,self.N) ,dtype=np.uint8)
self.ZB = np.zeros((numSamples,self.N,),dtype=np.uint8)
self.ZR = np.zeros((numSamples,self.N) ,dtype=np.uint8)
    
   
# get the sampled pixel values 
for k in range(self.N):            
    self.ZB[:,k] = self.flattenImage[k,0][self.sampleIndices]
    self.ZG[:,k] = self.flattenImage[k,1][self.sampleIndices]
    self.ZR[:,k] = self.flattenImage[k,2][self.sampleIndices]

self.Bij = np.matlib.repmat(np.log(self.times), r*c,1)
```

Also, the exposure times are required to construct the response curve. 
In this procedure, the irrandiance $E$ is assumed to be 1, thus no contribution of $E$ to exposure $X$ is made as $\log E =0$. 

Like many problems in computer vision, the problem of finding the CRF is set up as an optimization problem 
where the goal is to minimize an objective function consisting of a data term and a smoothness term. 
These problems usually reduce to a linear least squares problem which are solved using Singular Value Decomposition (SVD) 
that is part of all linear algebra packages. The details of the CRF recovery algorithm are in the original paper.

The picture below shows the constructed curves for three color channels 

<img src ="/assets/images/ResponseCurve.png" width="300">


## 4. Merge images 
  
  The images are merged by eq.6, which yields a recovered fused radiance map as shown below. 

  <img src ="/assets/images/fusedHDR_radianceMap.jpg" width="600">
  
  This is an HDR image, which needs to be converted into a 24-bit image via tone mapping. 
  Here, we used Drago's method, where the parameters for Drago Tonemap are **(gamma = 1, saturation=1, bias=0.85)**
  
  <script src="https://gist.github.com/gimoonnam/5306c2a8ea357c729710894f8963c64b.js"></script>
  
  <img src ="/assets/images/ldr-Drago-2.jpg" width="600">
  
# Wrapping it up 

We have studied how to recover HDR radiance map from multiple exposure images. The full implementation of the exposure fusion can be found [here](https://github.com/gimoonnam/ImageProcessing/blob/master/Debevec_algorithm/Debevec_fromScratches.ipynb).


# References

1. [Recovering high dynamic range radiance maps from photographs](https://dl.acm.org/doi/10.1145/258734.258884)
2. [High Dynamic Range Imaging by Mantiuk *et* al. 2016](https://www.cl.cam.ac.uk/~rkm38/pdfs/mantiuk15hdri.pdf)
3. [High Dynamic Range (HDR) Imaging using OpenCV](https://www.learnopencv.com/high-dynamic-range-hdr-imaging-using-opencv-cpp-python/)
4. [Drago's tonemapping](http://resources.mpi-inf.mpg.de/tmo/logmap/logmap.pdf) 

