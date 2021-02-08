---
title: ES6
top: 0
date: 2020-03-16 10:40:41
tags: 前端
toc: true
comment: true
categories:
---

记录一下我的 ES6 学习之旅

<!-- more -->

## 声明

> const，let 作用

-   作用域
    -   全局作用域
    -   函数作用域：`function(){}`
    -   块级作用域：`{}`
-   作用范围
    -   `var` 全局 & 函数作用域
    -   `let const` 块级作用域
-   赋值使用
    -   `const` 声明后必须立即赋值
-   声明方法
    -   `var`、`let`、`const`
    -   `function`、`class`、`import`

> 重点难点

-   不允许重复声明
-   未定义就使用会报错：
-   暂时性死区：`const` 和 `let` 不存在变量提升，声明变量之前都不可用

## 解构赋值

**字符串解构**：`const [a, b, c, d, e] = "hello"`

**数值解构**：`const { toString: s } = 123`

**布尔解构**：`const { toString: b } = true`

**对象解构**

-   形式：`const { x, y } = { x: 1, y: 2 }`
-   默认：`const { x, y = 2 } = { x: 1 }`
-   改名：`const { x, y: z } = { x: 1, y: 2 }`

**数组解构**

-   规则：数据结构具有`Iterator接口`可采用数组形式的解构赋值
-   形式：`const [x, y] = [1, 2]`
-   默认：`const [x, y = 2] = [1]`

**函数参数解构**

-   数组解构：`function Func([x = 0, y = 1]) {}`
-   对象解构：`function Func({ x = 0, y = 1 } = {}) {}`

## 箭头函数

（1）函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象。`this`对象的指向在构造函数中是可变的，但是在箭头函数中，它是固定的。

（2）不能使用`new`命令，不是 构造函数，否则会抛出一个错误。

（3）不能使用`arguments`对象，该对象在函数体内不存在。如果要用，可以用 rest 参数代替。

（4）不能使用`yield`命令，因此箭头函数不能用作 Generator 函数
