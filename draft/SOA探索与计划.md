## SOA的探索与计划
### SOA的使命
* 提供完备的基础设施与规范，简化分布式\微服务的开发、管理，提供全生命周期的技术保障，提高整体服务架构的稳定性。

### 名词解释
* 微服务 - 可以独立部署，水平扩展，独立访问的服务单元


### 什么是SOA？
* 我们选取了在SOA领域的主流框架做对比，分别是SpringCloud与K8S,两者都从不同的层面上实现了微服务架构的基础设施。
* SpringCloud从语言框架层面去解决问题，而K8S是高于语言框架的层面去提供了外围的服务。
* 这种不同的思考问题的角度或者说是解决问题的切入点，涵盖了不同程度的SOA或者说微服务架构的方方面面，下图有一个直观的说明： 
* ![](/Users/wadee/Documents/Meitu-SOA.png)

-------------

### K8S简介
#### K8S名词解析
名词 | 解析
----|----
Cluster | 集群是指由Kubernetes使用一系列的物理机、虚拟机和其他基础资源来运行你的应用程序。
Node | 一个node就是一个运行着Kubernetes的物理机或虚拟机，并且pod可以在其上面被调度。
Pod | 一个pod对应一个由相关容器和卷组成的容器组 
Label | 一个label是一个被附加到资源上的键/值对，譬如附加到一个Pod上，为它传递一个用户自定的并且可识别的属性.Label还可以被应用来组织和选择子网中的资源
selector | 是一个通过匹配labels来定义资源之间关系得表达式，例如为一个负载均衡的service指定所目标Pod.
Replication Controller | replication controller 是为了保证一定数量被指定的Pod的复制品在任何时间都能正常工作.它不仅允许复制的系统易于扩展，还会处理当pod在机器在重启或发生故障的时候再次创建一个
Service | 一个service定义了访问pod的方式，就像单个固定的IP地址和与其相对应的DNS名之间的关系。
Volume | 一个volume是一个目录，可能会被容器作为未见系统的一部分来访问。（了解Volume详情）
Kubernetes volume |构建在Docker Volumes之上,并且支持添加和配置volume目录或者其他存储设备。
Secret | Secret 存储了敏感数据，例如能允许容器接收请求的权限令牌。
Name | 用户为Kubernetes中资源定义的名字
Namespace | Namespace 好比一个资源名字的前缀。它帮助不同的项目、团队或是客户可以共享cluster,例如防止相互独立的团队间出现命名冲突
Annotation | 相对于label来说可以容纳更大的键值对，它对我们来说可能是不可读的数据，只是为了存储不可识别的辅助数据，尤其是一些被工具或系统扩展用来操作的数据

#### K8S核心组件
* Kubernetes主要由以下几个核心组件组成：
	* etcd保存了整个集群的状态；
	* apiserver提供了资源操作的唯一入口，并提供认证、授权、访问控制、API注册和发现等机制；
	* controller manager负责维护集群的状态，比如故障检测、自动扩展、滚动更新等；
	* scheduler负责资源的调度，按照预定的调度策略将Pod调度到相应的机器上；
	* kubelet负责维护容器的生命周期，同时也负责Volume（CVI）和网络（CNI）的管理；
	* Container runtime负责镜像管理以及Pod和容器的真正运行（CRI）；
	* kube-proxy负责为Service提供cluster内部的服务发现和负载均衡；

#### K8S核心调用流程
* ![](/Users/wadee/Zend/github/wadee.github.io/draft/kube-architecture.png)

---------

### SOA的组件
微服务架构核心组件 | SpringCloud | K8S
----|-------------|----
配置管理|Config Server, Consul, Netflix Archaius|K8S ConfigMap & Secrets
服务发现|Netflix Eureka, consul|K8S Service & Ingress Resources
负载均衡|Netflix Ribbon|K8S Service
API网关|Netflix Zuul|K8S Service & Ingress Resources
服务安全|SpringCloud Security |  -
集中式数据收集|ELK Stack (LogStash) | EFK Stack (Fluentd)
集中式监控|Netflix Spectator &Atlas| Heapster, Prometheus, Grafana
分布式日志跟踪|Spring Cloud Sleuth, Zipkin| OpenTracing, Zipkin
弹性和失败冗余|NetFlix Hystrix、Turbine、Ribbon|Health Check & autoScaling
打包、部署和调度部署|Spring Boot | K8S Scheduler,Deployment
任务工作管理|Spring Batch|K8S Jobs & Scheduled Jobs
单体应用|Spring 框架|K8S Pods

### 当前服务架构现状
组件 | 现状
-----|----
配置管理 | 缺失，配置变更依赖代码上线，无法做到配置热更新，缺少配置统一管理。
服务发现 | 缺失或者各自实现不规范统一，服务熔断、服务自恢复能力缺失或者不足。
负载均衡 | 实现不一，目前的实现方式有 依赖自身Client端进行负载均衡、依赖运维DNS服务。
弹性和失败冗余 | 缺失此部分功能，只能依赖运维临时、手工处理，处理速度慢。
API网关| 无API网关层，缺少统一的安全校验，接入校验，流量熔断，版本兼容，接口适配等功能。
集中式数据收集 | 单体服务缺少日志的收集或者缺失日志规范，缺少集中式数据收集的方式与服务，无可视化的界面，无统一规范
集中式监控 | 同 __集中式数据收集__, 服务质量无法科学统计，无直观体现。
分布式日志跟踪 | 同 __集中式数据收集__, 微服务架构广泛应用后问题会更加明显。
打包、部署| 流程缺失，没有引入有效的工具规范打包、部署流程，依赖手工登陆服务器进行登陆。
调度部署 | 无调度部署
任务工作管理 | 缺少任务工作管理系统
单体应用 | 依赖服务开发者的能力，无统一标准库

### SOA目标
* 提高全体服务的稳定性，降低研发成本，加速研发过程，提高硬件使用效率，降低硬件成本

### 实现方案
#### 设计考虑点：
* 需要满足当前php、go、c++技术栈的微服务化
* 复用当前可用的资源，快速实现功能，目前运维可用资源为：IaaS能力、K8S集群，etcd集群，jenkins，gitlab，发布平台、docker镜像中心, ELK, prometheus, Grafana
* 对业务侵入的要降到最低，不增加服务开发者的成本。

#### 方案汇总

组件 | 方案总述
----|-----
配置管理 | 接入K8S,复用K8S的配置管理的能力，引入Helm系统，可视化管理配置变更（版本管理，配置分发，配置热加载）
服务发现 | 接入K8S,复用K8S的服务发现能力，提供统一的服务发现管理可视化系统
负载均衡 | 接入K8S,复用K8S的服务负载均衡能力
弹性和失败冗余 | 接入K8S,复用K8S的资源调度、弹性伸缩、失败冗余能力。（K8S核心能力）
API网关 | 对外需要引入单独的网关，需要单独开发
集中式数据收集，集中式监控 | 规范日志落地、日志格式，对接ELK系统、Prometheus、Grafana,实现可视化服务数据实时查询与监控
分布式日志跟踪 | 引入OpenTracing体系，做到微服务调用栈日志可视化查看
打包、部署 | 引入Helm，gitlab-ci系统，对接运维发布系统(publish.meitu-int.com),对服务的打包、部署配置化，工具化，流程化，版本化
任务工作管理 | 接入K8S,复用K8S的Jobs与Scheduled Jobs,实现单次任务与定时任务的可视化管理
单体应用 | 产出高性能组件库，协助服务方提高单体应用的稳定性

### 方案实施
#### 第一阶段
##### 重点方向
* 监控与日志，用数据展示服务质量与暴露问题，建立 __服务SLA体系__
	* 集中式数据收集与监控
	* 分布式日志跟踪
	
##### 对业务方
* 集中式数据收集与监控: 按照 __日志接入规范__ 落地不同维度的日志, 接入ELK, Prometheus, Grafana集群
* 分布式日志跟踪: 按照 不同语言版本 OpenTracing SDK，落地日志

##### 对基础架构组
* 编写 __日志接入规范__ ，整理日志信息维度, 日志字段, 梳理日志接入流程, 落地Grafana可视化面板与监控报警
	* PS. 目前ElastciSearch接入Grafana报警,Grafana官方尚未支持，可能要借助influxDB技术去完成报警的展开。
* 调研OpenTracing方案落地，搭建OpenTracing集中式监控平台
* 建立电视墙，实时展示服务实时情况
* 建立 __服务SLA体系__

#### 第二阶段
##### 重点方向
* 打包、部署流程自动化

##### 对业务方
* 按照 __打包部署流程接入文档__, 接入打包部署

##### 对基础架构组
* 与运维梳理打包部署流程
* 编写 __打包部署流程接入文档__

#### 第三阶段
##### 重点方向
* 接入K8S
	* 配置管理
	* 服务发现
	* 弹性扩容
	
##### 对业务方
* 按照 __K8S接入规范__, 对业务代码进行改造，例如增加服务可用性探针等接口
* 整理目前的服务依赖资源（操作系统依赖，资源依赖，外部微服务依赖），共同产出Dockerfile与K8S部署配置文件
* 对部署在K8S的服务进行可用性测试与性能测试

##### 对基础架构组
* 产出 __K8S接入规范__
* 调研Helm系统,搭建Helm系统,统一管理业务方的部署方案,对接运维K8S系统
* 对接运维进行K8S的对接梳理

#### 第四阶段
##### 重点方向
* 单体应用的稳定性
	* 单体应用的组件库
	
##### 对业务方
* 替换官方的组件库

##### 对基础架构组
* 产出高性能组件库
