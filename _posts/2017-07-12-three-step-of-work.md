---
layout: post
title: 三步工作法以及四种工作类型 - 摘自《凤凰项目》
date: 2017-07-12 20:09:11.000000000 +09:00
tags: devops
---

## 对四种工作类型的理解
> 业务项目 - (需求工作)
因为书中讲述的是运维团队的工作管理，原文中描述的业务项目，是说业务开发部门的新增项目，在此我们觉得我们可以理解为 需求工作，或者新增需求。

> IT内部项目
由于业务需求而衍生出来的一些内部改进任务\项目，在某些场景可被称为“技术负债”。
	
> 变更
由于以上两种类型的工作引起的第三方工具\服务的变更，通常也是需要通过 **任务管理系统**，例如jira等跟踪管理。

> 计划外工作或救火工作
包括操作事故和操作问题，通常由上述三种类型的工作导致，而且往往以牺牲其他计划内工作为代价。

## 对三步工作法的解释
> ### 第一工作法
第一工作法是关于从开发到IT运维再到客户的整个自左向右的工作流。为了使流量最大化，我们需要小的批量规模和工作间隔，决不让缺陷向下游工作中心，并且不断为了整体目标（相对于开发功能完成率、测试发现/修复比率或运维有效性指标等局部目标）进行优化。

必要的做法包括：

* 持续构建、集成以及部署；
* 按需创建环境；
* 严控半成品(work-in-process)；
* 构建起能够顺利变更的安全系统和组织；

> ### 第二工作法
第二工作法是关于价值流各阶段自右向左的快速持续反馈流，放大其效益以确保防止问题再次发生，或者更快地发现和修复问题。这样，我们就能在所需之处获取或嵌入只是，从源头上保证质量。

必要的做法包括：

* 在部署管道中的构建和测试失败时“停止生产线”；
* 日复一日地持续改进日常工作；
* 创建快速的自动化测试工具，以确保代码自那个事处于可部署的状态；
* 在开发和IT运维之间建立共同的目标和共同解决问题的机制；
* 建立普遍的产品遥测技术，让每一个人都能知道，代码和环境是否在按照设定的运行，以及是否达到了客户的目标。

> ### 第三工作法
第三工作法是关于创建公司文化，改文化可带动两个风气的形成：

* 不断尝试，这需要承担风险并从成功和失败中西区经验教训；
* 理解重复和联系是熟练掌握的前提。

尝试和承担风险让我们能够不懈地改进工作系统，这经常要求我们去做一些与几十年来做法大不相同的事。一旦出了问题，不断重复日常操练赋予我们的技能和经验，令我们可以撤回至安全区域并恢复正常运作。

必要的做法包括：

* 营造一种勇于创新、敢于冒险（相对与畏惧或盲目服从命令）以及高信任度（相对于低信任度和命令控制）的文化，把至少20%的开发和IT运维周期拨给非功能性需求，并且不断鼓励进行改进。