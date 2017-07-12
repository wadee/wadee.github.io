---
layout: post
title: 如何打造一个小而美的团队 
# date: 2017-07-12 16:11:11.000000000 +09:00
tags: devops continuous-integration agile user-story docker gitlab-ci merge-request test-driven-development domain-driven-design common-language 
---
### 为什么需要小而美的团队

### 如何打造小而美的团队
*  聚焦于交付流程，而非仅仅是研发团队

#### 需求分析阶段
* 用户故事
	* 物理卡片墙
	* 3H - Who, What, How
	* 3C - Card, Conversation, Confirm
* trello
	* 会后整理 - 电子版的卡片墙，丰富内容（链接wiki或者其他链接）

#### 交付研发阶段
* trello 的最右的泳道应该是**细颗粒度**、**可执行的**、**可验收**的任务
* 将此部分的卡片进入jira2中的需求池泳道中
* 从中挑选、评审 若干任务到 一个sprint（冲刺）中
* 可视化很重要，卡片从左到右的推进，从而评估我们团队自身的瓶颈与最大工作量。
* 不断调整sprint的任务量

#### 研发各任务交付阶段
* 以DDD为指导，先设计，设计出来的类图作为组内成员（注意是所有人，包括产品）沟通的依据，统一所有的词汇。
* 不需要严格推行TDD - 严格的TDD是是需要测试先行的,但是需要以追求代码覆盖率为目标，提高发布的信心。

#### 开发联调交付阶段
* 开发
* merge-request的方式来提高任务的合并，任务级的合并需要code review.
* 配置gitlab-ci, 以gitlab pipeline来支持自动化测试。
* **配置即代码**，将所有的环境配置包含到代码库中，配置**docker镜像交付**，消除环境部署与环境不一致的问题导致的 **反工作类型的问题排查** 以及 **不必要的沟通**。

#### 测试联调交付阶段

#### 可用版本交付阶段

#### 团队的核心文化
* 以自服务，自动化和协作 作为核心文化

* 自服务

* 自动化

* 协作
