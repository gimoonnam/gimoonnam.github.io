---
title: "Weak Reference in Python"
date: 2020-8-12 05:34:28 -0400
categories: Python
tags:
  - Python 
  - tuple
  - list 
  - weak reference 
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-08-12
---

<img src="/assets/images/Python.jpg" width="800px" >


In this post, I will look over what the weak reference in Python is. 

This is associated with memory management and seems to be important in understanding the concept of memory

I also came across it while studying the memory management. 

We may ask the following questions: 

## What is the weak reference? 

A weak reference to an object is not enough to keep the object alive. 
When the only remaining references to a referent are **weak references**, 
**garbage collection** is free to destroy the referent and reuse its memory for something else. 
However, until the object is actually destroyed the weak reference may return the object even if there are no strong references to it. 

## What is the purpose of using weak reference? 

The primary use for weak references is to implement caches or mapping holding large objects, 
where it's desired that a large object not be kept alive solely because it appears in a cache or mapping. 
Use weak-reference if you need to index a large object for some reasons, but don't want to keep it around if something else deletes it. 

=============

Perhaps if you are storing cryptographic classes, which contain quite a bit of internal stuff, in a dictionary. 
If one of the classes is deleted, then you can save memory. 

The above code shows a difference between weak-referenced and normal dictionary object. 
In [2], a dictionary declared by weak reference returns no contents when value is deleted. 
Whereas, normal dict still holds contents after value is deleted as shown in [3]. 

This means that the normal dict still occupies memory even though its value is deleted, wasting memory. 


