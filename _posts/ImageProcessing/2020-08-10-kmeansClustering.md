---
title: "Image Segmentation by K-Means Clustering with OpenCV"
date: 2020-8-10 11:32:28 -0400
categories: ImageProcessing
tags:
   - image segmentation
   - image thresholding
   - k-means clustering
   - feature extraction
   - 이미지 분할 
   - K-Means clustering with OpenCV
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-08-21
---

# Introduction 

**이미지 분할(segmentation)** 은 컴퓨터 비전에서 중요한 물체를 인식하고 분리하는데 기초가 되는 중요한 이미지 처리 방법이다. 
이번 포스팅에서는 **K-Means clustering**을 이용한 이미지 분할이 어떻게 이루어지는지 공부해 보도록 하겠다. K-Means Clustering를 지원하는 많은 라이브러리 중 
**OpenCV**를 이용하도록 하겠다. 


## Trial application of kmeans in OpenCV with small number of points 
   
   먼저 몇개의 포인트로 이루어진 데이터에 대해서 OpenCV의 K-means clustering이 어떻게 작동하는지 테스트 해보도록 하겠다. 
   다음의 12개의 점들이 주어졌다고 하자. 

   <img src="/assets/images/kmeans_test_fig1.png" width="400px" >
   
   3개의 클러스터로 이루어져있다고 금방 알 수 있다. 이것을 알고리즘이 잘 찾는지 확인해 보자. 
   
   우선 필요한 모듈을 import 한다. 
   
   <script src="https://gist.github.com/gimoonnam/93baf6bef05d8ad50e35c10bec85e017.js"></script>

   cv2에 K-means함수가 포함되어 있다. matplotlib는 결과를 그리기 위해 로딩했다. 
   
   입력 데이터는 txt파일이며 다음의 **(number of points, 2(x,y))** 의 차원을 갖는다. 데이터를 읽어 numpy array로 저장한다. 
   
   <script src="https://gist.github.com/gimoonnam/bee9944aeb37d7ce84e4cb035d297fab.js"></script>
   
   
   


## *K*-Means clustering을 이용한 segmentation
   

   



# References 

  1. [reference](https://towardsdatascience.com/introduction-to-image-segmentation-with-k-means-clustering-83fd0a9e2fc3)   
  2. [Open Source Computer Vision](https://docs.opencv.org/master/d1/d5c/tutorial_py_kmeans_opencv.html)   
  3. [Wikipedia](https://ko.wikipedia.org/wiki/K-%ED%8F%89%EA%B7%A0_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)  
  
