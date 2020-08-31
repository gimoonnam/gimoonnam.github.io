---
title: "AttributeError: module ‘tensorflow’ has no attribute ‘placeholder' 해결 방법"
date: 2020-8-31 05:34:28 -0400
categories: Python
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

<img src="/assets/images/tf_placeholder_error.png" width="450px" >




# 해결방법 1 

## Tensorflow의 버전 업데이트에 따른 변화 적용하기 

<script src="https://gist.github.com/gimoonnam/224fdfa50c17e29d9fcae4dd6757626a.js"></script>


# 해결방법 2 

## tensorflor 1.x 버전의 compatibility mode 적용하기 

<script src="https://gist.github.com/gimoonnam/3b057a0a2ad8fcdc698509e56e055ead.js"></script>


