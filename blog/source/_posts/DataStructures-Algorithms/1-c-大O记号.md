---
title: 第一章 绪论：大 O 记号
top: 0
date: 2020-03-30 11:54:48
tags:
toc: true
comment: true
categories:
    - CS Course
    - Data Structures & Algorithms
---

大 $O$ 记号、高效解、有效解、难解、增长速度

<!-- more -->

## 大 $O$ 记号

![大 $O$ 记号推导](/../images/DataStructures-Algorithms/big-o.png)

$O$ 是 $T(n)$ 的上届，属于最坏情况

1、确定一个常数 $c$，当 $n$ 远大于 2 时，$T(n) < c * f(n)$  
2、简化函数（对函数进行放大，数字替换成 $n$）  
3、常系数可以忽略：$O(f(n)) = O(c * f(n))$  
4、低次项可以忽略：$O(n^a + n^b) = O(n^a)，a > b > c$

## 其他记号

![其他记号](/../images/DataStructures-Algorithms/otherMark.png)

1、$\Omega$ 是 $T(n)$ 的下届，属于最理想情况  
2、$\Theta$ 是 $T(n)$ 的确界

## 高效解 $O(1)$

![$O(1)$](/../images/DataStructures-Algorithms/O1.png)

## 高效解 $O(log^cn)$

![$O(log^cn)$](/../images/DataStructures-Algorithms/Olog.png)

## 有效解 $O(n^c)$

![$O(n)$](/../images/DataStructures-Algorithms/On.png)
$n^c (c > 0)$ 即属于多项式，多项式复杂度视作 可解

## 难解 $O(2^n)$

![$O(2^n)$](/../images/DataStructures-Algorithms/O2n.png)

![Subset](/../images/DataStructures-Algorithms/O2n1.png)
![Subset](/../images/DataStructures-Algorithms/O2n2.png)

## 增长速度

![增长速度 - 小规模](/../images/DataStructures-Algorithms/Ospeed.png)
![增长速度 - 大规模](/../images/DataStructures-Algorithms/Ospeed1.png)
