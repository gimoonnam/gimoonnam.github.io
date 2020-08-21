---
title: "Image Segmentation(이미지 분할) by K-Means Clustering with OpenCV"
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

**이미지 분할(segmentation)** 은 컴퓨터 비전에서 물체를 인식하고 분리하는데 기초가 되는 중요한 이미지 처리 방법이다. 
이번 포스팅에서는 **K-Means clustering**을 이용한 이미지 분할이 어떻게 이루어지는지 공부해 보도록 하겠다. K-Means Clustering를 지원하는 많은 라이브러리 중 
**OpenCV**를 이용하도록 하겠다. 


## 1. Pre-test with a few points  
   
   먼저 몇개의 포인트로 이루어진 데이터에 대해서 **OpenCV**의 **K-means clustering**이 어떻게 작동하는지 테스트 해보도록 하겠다. 
   다음의 12개의 좌표로 이루어진 데이터가 있다. 이 데이터의 차원은 **(12, 2(x,y))**가 될 것이다. 
   
   <img src="/assets/images/kmeans_test_fig1.jpeg" width="450px" >
   
   3개의 클러스터로 이루어져있다고 금방 알 수 있다. 이것을 알고리즘이 잘 찾는지 확인해 보자. 
   
   우선 필요한 모듈을 import 한다. 
   
   <script src="https://gist.github.com/gimoonnam/93baf6bef05d8ad50e35c10bec85e017.js"></script>

   cv2에 K-means함수가 포함되어 있다. matplotlib는 결과를 그리기 위해 로딩했다. 
   
   
   데이터를 읽어 numpy array로 저장한다. 
   
   <script src="https://gist.github.com/gimoonnam/bee9944aeb37d7ce84e4cb035d297fab.js"></script>
   
   
   실행전 알고리즘을 멈출 조건을 다음과 같이 주도록 한다. 
   
   <script src="https://gist.github.com/gimoonnam/8c8de044e14f64cea1fe1a0bf05924cb.js"></script>
  
   > * **cv2.TERM_CRITERIA_EPS**: ***epsilon***으로 주어진 정확도를 만족하면 반복을 멈춘다. 
   > * **cv2.TERM_CRITERIA_MAX_ITER**: 정확도와 상관없이 미리 정해진 반복 횟수를 다 채우면 알고리즘을 멈춘다. 
   > * **cv2.TERM_CRITERIA_EPS + cv2.TERM_CRITERIA_MAX_ITER** : 위 둘 중 한 조건이 만족되면 멈춘다.
   > 여기에서 **max_iter=10**, **epsilon=1.0** 으로 주었다.   
 
   
   조건을 주었다면 알고리즘을 실행한다. 
     
   <script src="https://gist.github.com/gimoonnam/c026d247b49a97269a7ecdca721cc959.js"></script>
  
   **K**는 데이터를 분류할 클러스터의 수이다. 이 예제에서는 3으로 주어 기대한대로 분류를 잘 하는지 보도록 한다. **attempts**는 알고리즘의 실행 횟수이다. 
   10으로 주었다. 따라서 10번의 독립적인 실행으로 분류를 한 후 **최적의 밀집도(compactness)** 를 가지는 결과를 리턴하게 될 것이다. 
   
   세 개의 output 변수가 있다. 
   
   > * **ret**: 밀집도(compactness)이다. 이것은 각 클러스터의 중심으로부터 거리제곱의 합이다.   
   > * **labels**: 각 점이 어느 클러스터에 속하게 되었는지 표시한다   
   > * **centers**: 클러스터의 중심 좌표를 리턴한다. K개의 데이터를 가진다.   
   

   다음과 같이 결과를 그려본다. 
   
   <script src="https://gist.github.com/gimoonnam/4f85865b84be3c2a7701bef89cc4d94e.js"></script>
   
   <img src="/assets/images/kmeans_test_fig3.png" width="400px" >
   
   예상한대로 분류가 잘 된 것을 볼 수 있다. 
   
 

## 2. Image segmentation using *K*-Means clustering with OpenCV 
   
   실제 이미지에 대한 **K-Means clustering**를 실행해 보도록 하겠다. 

   다음의 코드는 이미지를 읽고 **K-means clustering**을 진행하는 함수를 보여준다. 
   여기에서 주의해야 할 것은 **cv2.kmeans**에 입력하는 데이터는 반드시 **float32 타입**이어야 한다는 것이다. 
   변환하지 않고 입력하면 **assertion error**를 낼 것이다. 위의 예제에도 동일하게 적용된다. 
   
   <script src="https://gist.github.com/gimoonnam/de7268174895c7ac86aff8da26cb0669.js"></script>
   
   세 개의 다른 $K=3,5,7$에 대해서 결과를 확인해 보도록 하자. 
   
   <img src="/assets/images/kmeans_result_K3.png" width="800px" >

   <img src="/assets/images/kmeans_result_K5.png" width="800px" >

   <img src="/assets/images/kmeans_result_K7.png" width="800px" >   
   
   

# Wrapping it up 




# References 

  1. [reference](https://towardsdatascience.com/introduction-to-image-segmentation-with-k-means-clustering-83fd0a9e2fc3)   
  2. [Open Source Computer Vision](https://docs.opencv.org/master/d1/d5c/tutorial_py_kmeans_opencv.html)   
  3. [Wikipedia](https://ko.wikipedia.org/wiki/K-%ED%8F%89%EA%B7%A0_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)  
  
