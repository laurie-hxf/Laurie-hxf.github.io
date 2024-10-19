---
layout: post
title: Discrete Mathematics lecture4
date: 2024-10-19 19:46:00 +0800
description: NP problem
tags: 数学
categories: sample-posts
---
NP问题是一系列的不知道是否存在有效解决办法的问题
然后如果知道了其中一个的问题的有效解法，那么所有的NP问题就都有有效的解决办法
#### Input size of problems
input size of problems是对问题输入进行编码所需要的bit数，例如当输入一个数进入函数的时候，计算机通常解决的是这个数的二进制那么input size of problems通常是$\log_2 n$


#### Decision problem& Optimization problem
###### Decision problem决策问题
a problem that has a yes or no answer
eg.Given n>0, is integer m such that $m^m<n$?
###### Optimization problem优化问题
a problem that asks for some answer that maximizes or minimizes a particular objective function
eg.Given n>0, what is the largest integer m such that $m^m<n$?


#### Polynomial-Time Algorithms
an algorithm that runs in time $O(n^c)$where c>0 is a constant number independent of n and n is the input size of the problem that the algorithms

#### Non-Polynomial-Time Algorithms
an algorithm of which the running time is not $O(n^c)$for any constant c>0.
比如$O(2^n),O(n!)$等等


#### P类
就是对于一个Decision problem，可以用Polynomial-Time Algorithms来解决它，这类Decision problem的集合就是P类

#### NP类
还是对于一个Decision problem，不一定能够用Polynomial-Time Algorithms来找到一个解，但可以用Polynomial-Time来验证一个解是不是正确的

#### $P\subseteq NP$
证明这个很简单，就是如果一个解可以在Polynomial-Time解出来，那么它一定可以在Polynomial-Time被验证
但是反过来证明$NP\subseteq P$这个就不知道，因为如果一个解可以在Polynomial-Time内被验证，那么它是否一定能在Polynomial-Time时间内解出来呢

所以这就是著名的P=NP问题