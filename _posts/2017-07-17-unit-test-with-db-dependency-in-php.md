---
layout: post
title: 关于php中单元测试的数据库依赖的问题
date: 2017-07-17 12:21:11.000000000 +09:00
tags: phpunit, unit-test
---
> 占位，未完待续

## 什么是单元测试
在博文“[自动化测试目的](http://blog.adrianbolboaca.ro/2017/01/automated-tests-purposes/)”中，Bolboacă指出，单元测试应该完成如下工作：

> * 单元测试关注一个方法或一个类。它应该非常小，最多只有几行代码。
> * 人们在编写单元测试时会犯许多错误，所以这不是小事。
> * 因为它们非常小，所以它们应该在内存中运行，而且，一个单元测试应该在几毫秒内运行完成。
> * 任何用到外部依赖（数据库、WebService、文件系统、I/O）的测试都不是一个单元测试，那是其他的东西（“集成测试（integration test）”、“综合测试（integrated test）”、验收测试、端到端测试，等等）。
