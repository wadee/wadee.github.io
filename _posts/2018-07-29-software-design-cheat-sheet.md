---
layout: post
title: 软件设计cheat sheet
date: 2018-07-29 11:39:11.000000000 +08:00
tags: architecture, software-design
---

## 软件设计cheat-sheet

### 抽象层次由高到低分别是：

* 高内聚，低耦合

* 正交四原则

	* 消除重复

	* 分离关注点(SoC)

	* 缩小依赖范围

	* 向稳定依赖

* SOLID原则

	* The Single Responsibility Principle 单一职责

	* The Open Closed Principle 开闭原则

	* The Liskov Substitution Principle 里氏替换原则

	* The Interface Segregation Principle 接口分离原则

	* The Dependency Inversion Principle 依赖倒置原则

* 其他原则

	* DRY(Don’t Repeat Yourself): 在一个系统内，任何一项知识都只应该存在一个明确而权威的表示。（可以有多个表示，但仅一个表示为权威）

	* The Singular Responsibility Principle

	* OAOO(once and only once)

	* YAGNI(You Ain’t Gonna Need It): 尝试预测未来，可能应对未来，绝不实现未来！

	* TDA(Tell，Don’t Ask)

	* KISS(KEEP IT SIMPLE, STUPID!)

	* LKP(Least Knowledge Principle) 最少知识原则/Law of Demeter 笛米特法则

	* Do One Thing, Do It Well.

## 图示
![software-design-principle-architecture-relation](/img/software-design-principle-relation.png)