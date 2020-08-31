---
title: "AttributeError: module ‘tensorflow’ has no attribute ‘placeholder' 해결 방법"
date: 2020-8-31 05:34:28 -0400
categories: Tensorflow
tags:
  - tensorflow 
  - placeholder
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-08-31
---

# 증상 

* **텐서플로우가 2.x**으로 업데이트 되면서 **tf.placeholder**를 사용할 수 없게 되었다. 

<script src="https://gist.github.com/gimoonnam/116dae24c5d91a128b36ffb85aa28701.js"></script>

* 다음과 같이 **placeholder** 모듈을 찾을 수 없다는 에러를 낸다. 

<img src="/assets/images/tf_placeholder_error.png" width="800px" >


이를 해결할 수 있는 두 가지 방법을 살펴보도록 하자. 



# Solution 1: Tensorflow의 버전 업데이트에 따른 변화 적용 

첫 번째 방법은 **Tensorflow의 버전 업데이트에 따른 변화 적용**하는 것이다. 업데이트에 대한 자세한 내용은 [이 링크](https://www.tensorflow.org/guide/migrate)를 참고하기 바란다. 

**placeholder** 문제는 다음과 같이 적용하면 해결할 수 있다. 

<script src="https://gist.github.com/gimoonnam/224fdfa50c17e29d9fcae4dd6757626a.js"></script>




# Solution 2: 1.x 버전의 compatibility mode 적용 

두 번째 방법은 **tensorflor 1.x 버전의 compatibility mode 적용**하는 것이다. 이것은 2.x버전의 바뀐 내용을 사용하지 않겠다고 선언해주는 것으로, 
다음과 같이 **tensorflow.compat.v1** 모듈을 읽고 **tf.disable_v2_behavior()**를 실행하면 이전 버전과 동일하게 **placeholder**를 실행할 수 있다. 

<script src="https://gist.github.com/gimoonnam/3b057a0a2ad8fcdc698509e56e055ead.js"></script>


