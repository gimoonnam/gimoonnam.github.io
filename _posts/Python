---
title: "How to Change Elements of a Tuple in Python"
date: 2020-8-12 05:34:28 -0400
categories: Python
tags:
  - Python 
  - tuple
  - list 
  - difference between tuple and list 
use_math: true
toc: true
toc_sticky: true
last_modified_at: 2020-08-12
---

<img src="/assets/images/Python.jpg" width="800px" >

<span style="color:blue"> **Canny Edge Detection**  </span>


# What is the difference between list and tuple in Python? 

This is a common question when dealing with an array in python. 

Also, I often came across the moment to choose which array is good to use among list and tuple. 

I found that they have different properties despite some commons. 
So I wanted to document the commons and differences between list and tuple. List and Tuple are mainly used type of containers to handle an array in Python. 

* <span style="color:blue"> **Commons**  </span>

Both are variable containers, which can accommodate all types of variable such as numbers and strings
Heterogeneous type of variables can be stored in the same container. 


* <span style="color:blue"> **Differences**  </span>

List is mutable, meaning that size and element can be changed 
On the other hand, Tuple is immutable, so once the tuple is defined, it cannot be edited. append() method is not applicable in a tuple

Speed of iteration: Tuple is faster than list



# How to Change Elements of a Tuple in Python! 

Unlike a list, tuple is immutable. Is it still possible to change or mutate an element of a tuple? 

Some postings said that it is possible and there are several ways to do it. 
In this posting, I would like to check out the known methods and show that none of them is a true update of tuple. 

First, a simple tuple is created, and check the contents and the memory address by id(). 

Then, this tuple is changed in two ways: 

* by using append() method after converted to list 
* by slicing a tuple

The ID address of changed tuples are different from the original tuple. 
This means that the changed tuple doesn't occupy the same memory, but just a copy of tuple. 
Thus, these methods are not true way to update, rather produces a new tuple. 

Again the tuple is not mutable object in python. 

We can check that the memory for the original tuple remains still occupied even after the update. So it's recommended to delete the old object by del.

Here, I looked over how to change elements of a tuple in Python, and it turned out that as a tuple is immutable, it's not possible to change tuple. 

In this case, it is often recommended to use weak references. I wrote on the weak reference in other posting. 



