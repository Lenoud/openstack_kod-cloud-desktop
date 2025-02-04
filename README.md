# openstack_kod-cloud-desktop
openstack私有云平台+可道云桌面
项目于2023年年底完成
-------------------------

# 1 设计背景
## 1.1项目简介
随着云计算技术的快速发展，云桌面系统成为了一种高效、灵活和安全的办公方式，大大提升了企业和用户的工作效率和便利性。可道云桌面系统是一款基于开源软件OpenStack的云桌面解决方案，其具有强大的虚拟化能力和易用性，可以满足各类企业和个人对于云桌面环境的需求。本课题旨在通过研究和实践，搭建可道云桌面系统并探索其优化和应用，以提供一种可行的云桌面解决方案。另外，可道云桌面系统注重易用性和用户体验。它提供了友好的图形界面和简洁的操作流程，用户可以轻松管理和访问自己的云桌面环境。无论是创建新的虚拟机、部署应用程序还是备份和恢复数据，用户都可以通过直观的界面完成操作。这种易用性使得企业可以快速部署和扩展云桌面系统，而个人用户也能够方便地使用和管理自己的云桌面环境。

## 1.2课题目标
本课题的目标是基于OpenStack云平台搭建可道云桌面系统，实现一种灵活、高效、安全的云桌面解决方案。通过搭建可道云桌面系统，用户可以在任意设备上访问自己的个人桌面环境，并享受到与传统桌面相似的使用体验。可道云桌面系统的部署基于OpenStack云平台，OpenStack是一个开源的云计算平台，它提供了虚拟化、网络管理、存储等功能，可以为可道云桌面系统提供强大的基础设施支持。通过利用OpenStack的虚拟化技术，可道云桌面系统可以将用户的个人桌面环境虚拟化，并将其部署在云端服务器上。这样的架构使得用户可以通过网络连接访问自己的个人桌面环境，而无需依赖特定的物理设备。无论是在办公室、家中还是旅途中，只要有网络连接，用户就可以随时随地使用自己的桌面环境。这种灵活性为用户带来了极大的便利，使得工作、学习或娱乐变得更加自由和高效。

<font style="color:#000000;"></font>

# 2 设计思路
## 2.1开发环境与工具
本系统基于centos7.9.2009发行版，OpenStack-train版本，使用VMware虚拟化软件创建虚拟机搭建，搭建具体见下表2-1。

表2-1系统开发环境

| **环境** | **<font style="color:black;">版本</font>** |
| :---: | :---: |
| centos | 7.9.2009 |
| OpenStack | train |
| 可道云桌面 | 4.7.1 |
| VMware Workstation Pro | 16 |


现将这些工具和开发环境简单介绍如下：

### 2.1.1 centos7.9.2009
内核版本：CentOS 7.9.2009使用Linux内核版本为3.10.0。这是一个稳定且经过广泛测试的内核版本。

支持架构：CentOS 7.9.2009支持多种硬件架构，包括64位x86、PowerPC和ARM架构。

软件包管理：CentOS 7.9.2009使用yum作为软件包管理工具。您可以使用yum命令来安装、更新和删除软件包。

### 2.1.2 OpenStack-train
T 版（T version）指的是 OpenStack 的第十六个主要版本，也被称为 OpenStack Train，它是 OpenStack 项目中的一个重要版本，引入了一些新特性、改进和修复。

以下是 OpenStack Train 版本中的一些主要特性和改进：

Ironic 驱动程序扩展：Train 版本引入了多种新的 Ironic 驱动程序，包括 Redfish 和 iLO 5，使得 Ironic 在裸金属服务中更加灵活和多样化。

改进的网络性能：Train 版本在 OpenStack Neutron 中引入了一些改进，提高了网络性能和数据平面的可伸缩性。

安全增强：Train 版本引入了一些安全增强措施，包括加密通信、认证和访问控制的改进。

改进的用户体验：Train 版本对 OpenStack Dashboard 进行了一些改进，提升了用户界面的易用性和功能性。

### 2.1.3 可道云桌面
可道云是一种基于OpenStack的私有云解决方案。它是由中国电信创建和推出的，旨在提供企业级的云计算服务。可道云平台基于OpenStack开源项目，并集成了虚拟化、存储、网络等技术，为企业用户提供灵活、安全、高性能的私有云环境。

通过可道云，企业用户可以建立自己的私有云环境，拥有独立的计算、存储和网络资源，以满足其特定的业务需求。可道云还提供了管理控制台，使用户可以轻松管理和监控其云资源，并进行自动化运维和弹性扩展。

可道云具有以下特点：

安全可靠：可道云采用世界领先的安全技术和策略，确保用户数据的安全性和可靠性。

高性能：可道云利用OpenStack的虚拟化和分布式架构，提供高性能的计算和存储能力。

灵活扩展：可道云支持按需扩展，根据用户的实际需求进行弹性调整和资源分配。

### 2.1.4 VMware Workstation
多操作系统支持：VMware Workstation支持多种操作系统，包括Windows、Linux、macOS等。您可以在同一台计算机上同时运行不同操作系统的虚拟机。

虚拟机快照：您可以使用VMware Workstation创建虚拟机的快照，即保存当前虚拟机的状态。在进行配置更改或安装新软件之前，您可以先创建一个快照，以便在需要时恢复到该状态。

克隆和部署：VMware Workstation允许您快速克隆现有的虚拟机，并将其部署到其他计算机上。这对于创建测试环境或分发虚拟机非常有用。

网络模拟：VMware Workstation提供了强大的网络模拟功能，可以模拟各种网络环境和拓扑结构，包括虚拟局域网（VLAN）、NAT网络等。

## 2.2系统架构
### 2.2.1 OpenStack架构
OpenStack是一个开源的云计算平台，它提供了一系列的组件和服务，用于构建和管理云基础设施。下面是OpenStack的典型架构组件：

Nova（计算服务）：负责管理计算资源，提供虚拟机和容器实例的创建、调度、管理和监控。

Neutron（网络服务）：提供虚拟网络的创建和管理，包括网络拓扑、子网、路由器、防火墙等。

Cinder（块存储服务）：提供持久化的块存储卷，用于虚拟机和容器实例的数据存储和访问。

Glance（镜像服务）：负责管理虚拟机和容器实例的镜像，用于创建和启动实例。

Keystone（身份认证服务）：提供用户认证、授权和服务访问控制，确保只有授权用户可以访问OpenStack服务。

Skyline（Web界面）：提供基于Web的用户界面，用于管理和监控OpenStack资源和服务。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990592475-7837d9af-bed8-4340-b485-3e800963e1fd.png)

图2-1 OpenStack架构

### 2.2.2 可道云桌面架构
可道云桌面（KodExplorer）是一款基于Web的文件管理器和协作平台，支持在线查看、编辑和共享各种文件类型，具有高效、简便、安全等特点。其桌面版架构如下：

前端Web界面：可道云桌面的用户界面采用Web技术实现，可以通过浏览器访问，无需安装任何客户端软件。

中间层应用服务器：可道云桌面的中间层应用服务器负责处理用户请求，执行文件传输、共享、管理等功能。它使用PHP语言编写，运行在Web服务器上，如Apache、Nginx等。

数据库服务器：可道云桌面的数据库服务器使用MySQL或其它关系型数据库管理系统存储用户数据，如文件、目录结构、用户信息、权限控制等。

文件存储服务器：可道云桌面的文件存储服务器负责存储实际的文件数据，以及备份和恢复。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990592783-237c8ffe-4c08-4aab-a82c-e9f99dea968e.png)

图2-2 可道云桌面架构



# 3 需求分析
## 3.1系统目标
提供高效的云桌面服务：提供快速启动和停止云桌面实例的能力，以满足用户需求，提供高性能的虚拟化基础设施管理功能，以确保云桌面系统的稳定性和性能。

提升用户体验和满意度：提供友好和易用的用户界面，以方便用户管理和使用云桌面系统，提供具有良好响应时间的系统，以提高用户体验和满意度。

保障数据安全和隐私：提供严格的访问控制和数据加密机制，以确保数据的安全性和隐私，提供安全审计功能，以便发现和追踪系统中的安全事件。

提高系统的可靠性和可用性：提供具有容错和快速恢复能力的系统，以最大程度地减少系统故障和错误导致的影响，提供具有高可扩展性和易维护性的系统，以方便进行后续功能扩展和升级。

优化资源利用率和降低成本：提供具有资源自动调整机制的系统，以最大程度地优化资源利用，提供可灵活配置的硬件资源，以更好地适应不同用户的需求，并尽可能降低系统成本。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990593128-dc797689-7e91-4857-a84e-1b14b58c369e.png)

图3-1 系统目标

## 3.2功能性需求
用户管理需求：支持用户注册、登录和身份验证机制。提供用户权限管理，包括角色定义和访问控制。支持用户个人信息管理和账户设置，提供用户组管理功能，以便对用户进行分组和授权。

虚拟化基础设施管理需求：实现基于OpenStack的私有云环境搭建和管理，提供虚拟机实例管理，包括创建、删除、启动、停止和调整规模等功能。支持虚拟机硬件资源配置，如CPU核数、内存大小、磁盘空间等。提供网络拓扑管理，包括虚拟网络和子网的创建和配置。

可道云桌面系统需求：提供云桌面实例管理，包括创建、删除、启动、停止和回收等功能。支持云桌面规模调整和资源分配，以满足不同用户需求。提供云桌面的应用程序和数据存储，支持用户数据隔离和安全性。

系统性能和可靠性需求：提供系统监控和日志记录功能，以便实时监控系统状态并识别潜在问题。支持故障恢复和容错机制，以确保系统的高可用性和稳定性。考虑系统负载均衡和资源调度，以优化系统性能和资源利用率。

安全性和隐私需求：采用安全的身份认证和访问控制机制，以防止未经授权的用户访问。提供数据加密和隔离机制，保护用户数据的安全性和隐私。支持防火墙和入侵检测系统，以保护系统免受恶意攻击。

系统功能结构图。如图3-2。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990593539-2c5eedcb-f47a-4b5a-b8b3-133eea6393ff.png)

图3-2 系统功能结构图

## 3.3非功能性需求
（1）性能需求：

响应时间：系统应能够在合理的时间内对用户请求作出响应，快速启动和停止云桌面实例。吞吐量：系统应支持同时处理多个用户的请求，并确保资源分配合理，不出现性能瓶颈。资源利用率：系统应优化资源的利用，提高虚拟机和云桌面实例的利用率，尽量减少资源浪费。

（2）可靠性和可用性需求：

可靠性：系统应具有高度可靠性，能够保证关键功能的连续可用，并尽量减少故障和错误的发生。回复能力：系统应具备快速恢复功能，以最小化系统故障对用户体验的影响，并能够迅速恢复到正常工作状态。

（3）安全性需求：

访问控制：系统应具备严格的访问控制机制，确保只有经过授权的用户才能访问系统和相关数据。数据加密：系统应支持对重要数据进行加密，以保护数据的机密性和完整性。安全审计：系统应能够记录和监控用户活动，并提供安全审计功能，以便进行安全事件的检测和溯源。

（4）可维护性需求：

易操作性：系统应具备良好的用户界面和操作提示，使管理员能够方便地管理和监控系统。可扩展性：系统应具备良好的扩展性，能够方便地进行功能扩展和后续升级。可测试性：系统应易于测试和调试，以保证其功能的正确性和稳定性。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990594094-0d031e63-2143-4c40-81d1-7500aba3e66f.png)

图3-3 需求分析

<font style="color:#000000;"></font>

# 4 系统设计
## 4.1系统功能整体设计
### 4.1.1用户界面
登录界面：允许用户输入凭据以访问系统。

主界面：提供导航到不同功能模块的入口，如文件管理、云办公、日历等。

文件管理界面：用于上传、下载、浏览和管理文档。

云办公界面：提供可道云桌面的虚拟办公环境。

日历和任务界面：允许用户创建、查看和编辑日程安排和任务列表。

用户设置界面：用户可以管理其个人资料、安全设置和通知首选项。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990594590-35eecbe8-bd0e-4fb9-ae1b-bfdd3445bc9e.png)

图4-1用户界面

### 4.1.2应用层功能
用户身份验证：用户可以使用用户名和密码登录

文件管理：用户可以上传、下载、删除和分享文件，支持版本控制。

云办公：提供云中的文档编辑、表格、幻灯片等办公功能。

日历：用户可以创建和管理日程事件，接收提醒。

通知系统：系统可发送通知和提醒，如文件共享邀请、任务更新等。

搜索功能：允许用户搜索文件、任务、日历事件等。

权限管理：定义不同用户角色和权限，确保数据安全性。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990594962-404cff82-1adc-4851-8c94-67c585660cd5.png)

图4-2应用层功能

### 4.1.3云计算平台层
虚拟机管理：创建、启动、停止、销毁云主机。

资源分配：分配计算、存储和网络资源以满足用户需求。

负载均衡：确保系统的高可用性和性能。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990595398-1edd854c-ccac-4261-8b19-d8ef54916cec.png)

图4-3云计算平台层

## 4.2系统详细设计
### 4.2.1 OpenStack云平台设计
OpenStack是一个开源云计算平台，用于管理和提供虚拟化资源。下面是OpenStack的关键组件和功能设计：

（1）Nova

Nova是OpenStack的计算组件，用于管理虚拟机实例。它负责创建、启动、停止和删除虚拟机。

（2）Neutron

Neutron是OpenStack的网络组件，用于管理虚拟网络资源。它负责虚拟机的网络连接和安全性。

（2）Cinder

Cinder是OpenStack的块存储组件，用于管理虚拟机的块存储卷。它允许虚拟机附加和分离卷。

（4）Glance：

Glance是OpenStack的镜像组件，用于存储虚拟机镜像。虚拟机实例可以从这些镜像中创建。

（5）Keystone：

Keystone是OpenStack的身份认证组件，用于管理用户、角色和项目。它提供了用户身份验证和访问控制。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990595737-ad2f1386-e27c-4702-a55a-625a6ac90c2f.png)

图4-4 OpenStack云平台设计

### 4.2.2 可道云桌面平台设计
可道云平台是一个协作办公平台，提供文件管理、云办公和协作工具。以下是可道云平台的关键组件和功能设计：

文件管理模块：允许用户上传、下载、管理和共享文件。它包括版本控制和权限管理。

云办公模块：提供在线文档编辑、表格、幻灯片制作等功能，支持多用户协作。

日历和任务模块：用户可以创建、编辑和管理日程事件和任务列表。

权限管理模块：定义不同用户角色和权限，以确保数据的安全性和隐私。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990596118-7815c035-25b3-4e08-91b6-ca14448bc236.png)

图4-5可道云桌面平台设计

## 4.3平台功能设计
### 4.3.1 云平台功能设计
云平台功能：

虚拟机管理：Nova允许管理员创建和管理虚拟机实例，包括资源分配和调度。

网络管理：Neutron提供了虚拟网络的管理，包括子网、路由和安全组的配置。

存储管理：Cinder允许虚拟机挂载块存储卷，以满足不同应用程序的存储需求。

镜像管理：Glance允许管理员上传、管理和共享虚拟机镜像。

身份认证：Keystone提供了用户身份认证和访问令牌管理。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990596459-d977d37e-69b1-406a-a666-18fba8e8c182.png)

图4-6 云平台功能设计

### 4.3.2 云桌面功能设计
云桌面功能：

文件管理：用户可以轻松上传、下载、浏览和分享文件，支持版本控制，确保数据的完整性。

云办公：提供云中的文档编辑和协作，使多个用户能够同时编辑文件。

日历和任务管理：用户可以规划日程、设置提醒和共享任务列表，提高工作效率。

权限管理：确保数据安全性，管理员可以分配不同角色和权限给用户。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990596845-5fe12553-8dfa-44dc-af5e-8a29c743c86f.png)

图4-7云桌面功能设计

<font style="color:#000000;"></font>

# 5 系统实现
## 5.1 OpenStack搭建
### 5.1.1 服务器规划
此项目基于两台虚拟机创建的OpenStack平台，服务器配置规划如下表:

表5-1 服务器资源规划

| **节点名称** | **网卡** | **磁盘** | **IP****地址** |
| :---: | :---: | :---: | :---: |
| controller | ens32<br/>ens33 | sda | 192.168.100.90/24<br/>  |
| compute | ens32<br/>ens33 | sda<br/>sdb | 192.168.100.91/24 |


### <font style="color:white;">5.1.2 </font>基础环境准备
在搭建OpenStack之前 ，我们需要先配置服务器的环境，将防火墙关闭，以免影响到服务的正常运行,此外我们需要上传OpenStack的离线安装包,并且配置好yum源，为后续部署OpenStack做好准备。

#所有节点执行。

[root@localhost ~]# systemctl stop firewalld

[root@localhost ~]# systemctl disable firewalld

[root@localhost ~]# setenforce 0

#修改主机名

#controller

[root@localhost ~]# hostnamectl set-hostname controller

[root@localhost ~]# bash

[root@controller ~]#

#compute

[root@localhost ~]# hostnamectl set-hostname compute

[root@localhost ~]# bash

[root@compute ~]#

 

#配置离线安装包

[root@controller ~]# mount OpenStack-Install-v1.0.iso /mnt/

mount: /dev/loop0 写保护，将以只读方式挂载

[root@controller ~]# mkdir /opt/{iaas,centos}

[root@controller ~]# cp -rvf /mnt/*  -c /opt/iaas/

[root@controller ~]# mount /dev/sr0 /opt/centos/

mount: /dev/sr0 写保护，将以只读方式挂载

#配置本地yum

[root@controller yum.repos.d]# nano /etc/yum.repos.d/local.repo

[root@controller yum.repos.d]# cat /etc/yum.repos.d/local.repo

[centos]

name=centos7

baseurl=file:///opt/centos/

gpgcheck=0

enabled=1

 

[iaas]

name=iaas

baseurl=file:///opt/iaas/iaas-repo

gpgcheck=0

enabled=1

#添加hosts主机名称映射

[root@controller ~]# cat /etc/hosts

192.168.100.90 controller

192.168.100.91 compute

#节点免密

[root@controller ~]# ssh-keygen  #默认回车即可

[root@controller ~]# ssh-copy-id compute  #输入compute节点密码

### 5.1.3 编写脚本环境变量
此次我们使用shell脚本部署OpenStack对应的服务，脚本中使用到了一个环境配置文件，我们修改此文件填写对应的值，然后开始部署我们的OpenStack云平台。

#所有节点执行。

mkdir /etc/env

mv openrc.sh /etc/env/

环境配置文件如下图所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990603253-706160a6-7df6-4141-8f4e-fc490f9e2970.png)

图5-1 env环境配置文件

### 5.1.4 安装必要的软件包
在安装OpenStack组件之前我们首先需要把节点之间的时间同步配置好，并且清理iptables规则，安装OpenStack命令客户端，和其它必要的组件。

#所有节点执行。

[root@controller controller]# bash iaas-pre-host-controller.sh

[root@compute compute]# bash iaas-pre-host-compute.sh

#安装完成后需要重启服务器

reboot

Controller和compute脚本代码如下图所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990603636-b67d24c7-10f0-4093-a153-fb435842d8b3.png)

图5-2 Controller 初始化脚本

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990604028-50be17b3-0540-41b5-87f0-e1840913579d.png)

图5-3 compute 初始化脚本

安装完成后需重启服务器。

### 5.1.5 安装数据库等服务
数据库和缓存以及消息队列服务器是OpenStack所必须要依赖的三个服务，OpenStack平台的用户数据、资源数据都需要通过这个三个服务协同工作才能正常创建，下面我们将使用shell脚本安装mysql服务。

#controller执行命令。

[root@controller controller]# bash iaas-install-mysql.sh

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990604411-e0ae16ec-7736-4b23-a671-d2f5c281078f.png)

图5-4 数据库安装脚本

### 5.1.6 安装keystone服务
Keyston在OpenStack中担任用户认证的角色，所有访问OpenStack平台的用户都需要通过keystone的认证后才能对集群进行操作，下面我们使用脚本部署keystone服务。

#controller执行命令。

[root@controller controller]# bash iaas-install-keystone.sh

Keystone安装脚本如下图:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990604715-fe8a4af3-2ba7-46e2-864b-8a559105fcf9.png)

图5-5 keystone服务安装脚本

### 5.1.7 安装glance服务
Glance在OpenStack平台中担任镜像管理的角色。

#controller执行命令。

[root@controller controller]# bash iaas-install-glance.sh

Glance安装脚本如下图:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990605169-be0377b5-3b93-48a1-853e-663b9bc0ec52.png)

图5-6控制节点glance脚本代码

### 5.1.8 安装placement服务
Placement提供元数据服务，在s版之前placement是合并在nova服务里面的，s版后作为一个独立的组件被分离出来。

#controller执行命令。

[root@controller controller]# bash iaas-install-placement.sh

Placement安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990605632-7f67f137-f1b1-4343-a5f8-739ecffeda26.png)

图5-7控制节点placement脚本代码

### 5.1.9 安装nova服务
#### 5.1.9.1 controller节点安装nova
Nova是OpenStack里面的一个核心组件，由它提供计算服务，并且主机的调度和资源的分配都是由nova来执行。

#controller执行命令。

[root@controller controller]# bash iaas-install-placement.sh

Controller节点Nova安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990606096-49092379-4fe9-4e15-94e5-e74e28b08ef8.png)

图5-8控制节点nova脚本代码

#### 5.1.9.2 compute节点安装nova
Compute节点也需要安装nova相关组件，负责提供资源创建云主机。

#compute执行命令。

[root@compute compute]# bash iaas-install-nova-compute.sh

compute节点Nova安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990606546-6b11de41-5d6e-4f91-a6be-f0268d407abd.png)

图5-9计算节点nova脚本代码

### 5.1.10 安装neutron服务
#### 5.1.10.1 controller节点安装Neutron
Neutron在OpenStack中提供网络服务，Neutron也是一个非常核心的组件，OpenStack所有的云主机网络服务都是由Neutron提供，包括路由器，安全组防火墙规则。

#controller执行命令。

[root@controller controller]# bash iaas-install-neutron-controller.sh

controller节点Neutron安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990607019-d00ffe49-ffa8-4267-a96e-d7a73f01ba35.png)

图5-10控制节点Neutron脚本代码

 

#### 5.1.10.2 compute节点安装Neutron
Compute节点同样安装neutron服务。

#compute执行命令。

[root@compute compute]# bash iaas-install-neutron-compute.sh

compute节点Neutron安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990607447-ed0e8600-5d69-4839-b4a6-c00a6b70c2e9.png)

图5-11计算节点Neutron脚本代码

### 5.1.11 安装cinder服务
#### 5.1.11.1 controller节点安装cinder
#controller执行命令。

[root@controller controller]# bash iaas-install-cinder-controller.sh

controller节点cinder安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990607879-88fc8d2a-1b39-4512-894f-4fb677ce391c.png)

图5-12 控制节点cinder脚本代码

 

#### 5.1.11.2 compute节点安装cinder
Cinder服务主要要依靠compute节点提供资源创建存储卷。

#compute执行命令。

[root@compute compute]# bash iaas-install-cinder-compute.sh

compute节点cinder安装脚本如下如所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990608279-53bd59b5-42ed-431e-8ebe-82886ae78dac.png)

图5-13 计算节点cinder脚本代码

 

### 5.1.12 部署skyline服务
Skyline是一个经过UI和UE优化的OpenStack仪表盘。它支持OpenStack Train及更高版本，并具有现代化的技术栈和生态系统。这使得开发者能够更容易地进行维护，用户能够更轻松地进行操作，并提供更高的并发性能。

Skyline的吉祥物是九色鹿，灵感来自于敦煌壁画《九色鹿本生》。九色鹿象征着佛理中的因果与知恩图报的思想，这与九州云自创办以来秉持的拥抱和回馈社区理念一致。我们希望Skyline能像九色鹿一样，既轻巧、优雅又强大，为OpenStack社区和用户提供更优质的仪表盘服务。

#controller执行命令。

#创建数据库

[root@controller ~]# mysql -uroot -p000000 -e "CREATE DATABASE skyline DEFAULT CHARACTER SET utf8 DEFAULT COLLATE utf8_general_ci;"

[root@controller ~]# mysql -uroot -p000000 -e "GRANT ALL PRIVILEGES ON skyline.* TO 'skyline'@'localhost'    IDENTIFIED BY '000000';"

[root@controller ~]# mysql -uroot -p000000 -e "GRANT ALL PRIVILEGES ON skyline.* TO 'skyline'@'%'    IDENTIFIED BY '000000';"

#部署docker

sudo yum install -y docker-ce docker-ce-cli containerd.io

sudo systemctl start docker

docker load -i 99cloud_skyline.tar.gz

docker tag  c83673fef076 skyline_dashboard:v1.0

mkdir -p /etc/skyline /var/log/skyline /var/lib/skyline /var/log/nginx

#编写docker-compose启动skyline

cat docker-compose.yaml

version: '3'

services:

  skyline:

    image: skyline_dashboard:v1.0

    container_name: skyline

    restart: always

    volumes:

      - /var/log/skyline:/var/log/skyline

      - /etc/skyline/skyline.yaml:/etc/skyline/skyline.yaml

      - /tmp/skyline:/tmp

network_mode: host

#启动skyline

[root@controller skyline]# docker-compose up -d

[+] Running 1/1

 ✔ Container skyline  Started

Skyline部署成功后访问[http://controllerip:8080](http://controllerip:8080)登录云平台，如图所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990608780-efa80160-19dc-4c9c-a450-514e68630afa.png)

图5-14访问云平台

登录平台测试是否正常如图所示:

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990609557-c75de923-0f04-4159-aded-d88cdb6db5c5.png)

图5-15登录云平台

### 5.1.13 检查各个服务的状态
现在我们已经部署了OpenStack平台，接下来我们测试各个组件的状态是否正常。

#controller执行命令。

#查看keystone组件是否正常

[root@controller ~]# openstack token issue

+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

| Field      | Value                                                                                                                                                                                   |

+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+

| expires    | 2023-10-22T16:24:56+0000                                                                                                                                                                |

| id         | gAAAAABlNT7IOYRLkhPRP9VSW8WkFyYF8XrSkdDVokNRK395E31i6AHNmmQF-LoH-vkFi0f4R5cHKUtThp1KDYLwYAop5LD0y2xSZJQQ8jv20gmKAR-9J22JIJpSLMmNRY-zTDQKMnBYmMN5NWW3F59EckHGzguTOc_gxRNLpiHERTPxnZSOvgc |

| project_id | 1c531648a3d44dd79435f3a496b99da3                                                                                                                                                        |

| user_id    | 43a574ace18d473fb821aa88d5faf194                                                                                                                                                        |

+------------+-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+  

#测试glance组件

glance image-create --name "cirros" --file cirros-0.4.0-x86_64-disk.img --disk-format qcow2 --container-format bare --visibility=public

# 查看镜像运行状态

root@controller:~# openstack image list

+--------------------------------------+--------+--------+

| ID                                   | Name   | Status |

+--------------------------------------+--------+--------+

| 12a404ea-5751-41c6-a319-8f63de543cd8 | cirros | active |

+--------------------------------------+--------+--------+

#测试placement组件

[root@controller ~]# placement-status upgrade check

+----------------------------------+

| Upgrade Check Results            |

+----------------------------------+

| Check: Missing Root Provider IDs |

| Result: Success                  |

| Details: None                    |

+----------------------------------+

| Check: Incomplete Consumers      |

| Result: Success                  |

| Details: None                    |

+----------------------------------+

#测试nova组件

 

[root@controller ~]#  openstack compute service list

+----+----------------+------------+----------+---------+-------+----------------------------+

| ID | Binary         | Host       | Zone     | Status  | State | Updated At                 |

+----+----------------+------------+----------+---------+-------+----------------------------+

|  4 | nova-conductor | controller | internal | enabled | up    | 2023-10-22T15:27:47.000000 |

|  5 | nova-scheduler | controller | internal | enabled | up    | 2023-10-22T15:27:52.000000 |

|  6 | nova-compute   | compute    | nova     | enabled | up    | 2023-10-22T15:27:51.000000 |

+----+----------------+------------+----------+---------+-------+----------------------------+

#测试neutron组件

[root@controller ~]# neutron agent-list

neutron CLI is deprecated and will be removed in the future. Use openstack CLI instead.

+--------------------------------------+--------------------+------------+-------------------+-------+----------------+---------------------------+

| id                                   | agent_type         | host       | availability_zone | alive | admin_state_up | binary                    |

+--------------------------------------+--------------------+------------+-------------------+-------+----------------+---------------------------+

| 23838928-0334-4713-b158-66652ddac93c | L3 agent           | controller | nova              | :-)   | True           | neutron-l3-agent          |

| 43cc3185-d5ea-408e-8ff3-98205e8e52f6 | Linux bridge agent | compute    |                   | :-)   | True           | neutron-linuxbridge-agent |

| 7061f27c-f368-424d-b8d9-f11a32a098af | Metadata agent     | controller |                   | :-)   | True           | neutron-metadata-agent    |

| ac0ccd41-a429-41ad-8a32-31275e0e9175 | Linux bridge agent | controller |                   | :-)   | True           | neutron-linuxbridge-agent |

| cb8b8420-a5fc-49ff-87d3-cef151365927 | DHCP agent         | controller | nova              | :-)   | True           | neutron-dhcp-agent        |

+--------------------------------------+--------------------+------------+-------------------+-------+----------------+---------------------------+

#测试

[root@controller ~]# cinder service-list

+------------------+-------------+------+---------+-------+----------------------------+---------+-----------------+---------------+

| Binary           | Host        | Zone | Status  | State | Updated_at                 | Cluster | Disabled Reason | Backend State |

+------------------+-------------+------+---------+-------+----------------------------+---------+-----------------+---------------+

| cinder-scheduler | controller  | nova | enabled | up    | 2023-10-22T15:30:24.000000 | -       | -               |               |

| cinder-volume    | compute@lvm | nova | enabled | up    | 2023-10-22T15:30:21.000000 | -       | -               | up            |

+------------------+-------------+------+---------+-------+----------------------------+---------+-----------------+---------------+

## 5.2 可道云桌面服务搭建
### 5.2.1 创建一个启动镜像
我们可以直接使用命令创建一个启动云硬盘，用来创建我们的云主机。

#controller执行命令

#创建一个启动盘

[root@controller skyline_install]#openstack image create --container-format bare --disk-format qcow2 --min-disk 10  --min-ram 1024 --file /opt/CentOS-7-x86_64-2009.qcow2 centos7.2009

[root@controller skyline_install]# openstack volume create --image centos7.2009 --bootable --size 20 centos7

### 5.2.2 使用skyline创建网络
#controller执行命令

#创建一个外部网络

openstack network create --provider-physical-network provider --provider-network-type flat  --external extnal

使用dashboard创建整个网络系统，如下图所示:。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990609960-284fdff8-741b-4440-8611-3eda2a5a0f8d.png)

图5-16创建内部网络

创建外部网络子网。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990610503-3ee71cc3-f4ef-46f3-bb6f-016f47aa339c.png)

图5-17创建外网子网

创建路由器连接内部网络和外部网络。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990611385-ae37933c-3e5a-416f-8732-eb2e81b55fa8.png)

图5-18添加外部网关

在路由器上添加内网网关端口。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990611753-ca238c3f-2f0e-494f-8c4f-62add4ff6c01.png)

图5-19路由器绑定接口

  测试网络是否正常。

#controller执行命令

#添加一条静态路由  ping 内网网关

[root@controller skyline_install]# route add -net 172.20.0.0/24 gw 192.168.100.159

[root@controller skyline_install]# ping 172.20.0.1

PING 172.20.0.1 (172.20.0.1) 56(84) bytes of data.

64 bytes from 172.20.0.1: icmp_seq=1 ttl=64 time=0.257 ms

64 bytes from 172.20.0.1: icmp_seq=2 ttl=64 time=0.469 ms

  网关地址如下图所示。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990612170-44b71227-2924-4a1b-a0e2-b4654f591fff.png)

图5-20查看网关

 

### 5.2.3 创建云主机
使用skyline创建一台云主机。

点击云主机——>创建云主机——>选择实例类型和硬盘——>网络设置——>系统设置——>创建实例。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990612501-1768ea91-eadd-4c57-99d9-c188196d91eb.png)

图5-21创建云主机

 设置密码，创建云主机。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990612898-bfdfe14b-3aaa-4354-8ccf-f788bc5c7e98.png)

图5-22设置云主机密码

申请浮动ip。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990613371-ff6e8f74-678a-4179-b754-d75869ece577.png)

图5-23分配浮动IP

绑定浮动ip连接云主机。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990613888-59fa42c9-b1ff-4bdd-9477-5794311bafa8.png)

图5-24查看浮动IP

### 5.2.4 开始部署可道云桌面
使用ssh连接云主机。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990614331-0995566b-7779-49ab-b5b1-aaeb0ea13462.png)

图5-25连接云主机

#云主机执行命令

tar -zxvf kodcloud-desktop.tar.gz

#配置源

curl -o /etc/yum.repos.d/CentOS-Base.repo [https://mirrors.aliyun.com/repo/Centos-7.repo](https://mirrors.aliyun.com/repo/Centos-7.repo)

yum install -y epel-release

#安装php和mariadb

yum -y install mariadb mariadb-server

yum -y install httpd php php-cli php-gd php-mbstring -y

#解压离线包

tar -zxvf kodcloud.tar.gz -C /var/www/html/

chmod -R 777 /var/www/html

sed -i 's/#ServerName www.example.com:80/ServerName localhost:80/g' /etc/httpd/conf/httpd.conf

systemctl enable httpd

#配置数据库

mysql_install_db --user=root

mysqld_safe --user=root &

mysqladmin -u root password 'root'

mysql -uroot -proot -e "grant all on *.* to 'root'@'%' identified by 'root'; flush privileges;"

#关闭防火墙

Setenforce 0

#启动云桌面

systemctl start httpd

  启动apache服务后，浏览器访问http://云主机IP，首次启动需要设置管理员密码，如图所示：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990614931-dfd57653-f791-496c-9e04-e7543b3dd2af.png)

图5-26访问服务

### 5.2.5 登录可道云桌面平台
设置好管理员账号密码后登录云桌面，如图所示：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990615842-598abedf-843c-4fcb-9a5e-6fd41b649cfd.png)

图5-27 登录云桌面

<font style="color:#000000;"></font>

# 6 系统测试
## 6.1测试用例
可道云桌面可在任何能够访问web服务的终端使用，接下来我们测试各平台的使用情况。

桌面端、移动端，平台使用情况设计表：

表 6-1 使用情况设计表

|   | **桌面端** | **移动端**  |
| :---: | :---: | :---: |
| **访问平台** | 测试是否能够成功访问到平台 | |
| **上传文件** | 测试是否可以成功上传文件 | |
| **观看视频** | 测试是否可以无障碍播放并观看视频 | |
| **编辑文档** | 测试编辑功能是否顺畅，保存与加载是否正常 | |


用户功能测试：测试用户注册、登录和身份验证、权限管理。

表6-2测试账号设计

| **用户注册** | **权限管理** |
| :---: | :---: |
| Yunwei01 | 访问开发和运维部 |
| Kaifa01 | 访问开发部 |
| Caiwu01 | 访问财务部 |


 

## 6.2测试过程
### 6.2.1测试访问云桌面
桌面端访问云桌面：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990616561-40e8dd00-6362-4f8f-a783-b7a15e3bcbc7.png)

图6-1 桌面端访问

可以看到能够成功访问使用云桌面，证明功能ok。

移动端访问平台：

![](https://cdn.nlark.com/yuque/0/2023/jpeg/35492615/1698990617431-9bcfc370-14c2-4b8b-8eef-162f9b94b74d.jpeg)

图6-2 移动端访问

### 6.2.2测试**上传文件功能**
桌面端上传一个视频到云桌面：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990618074-cfae1b2c-d950-454f-8761-e7eb29772ac8.png)

图6-3 桌面端上传视频

移动端上传一个视频到云桌面：

![](https://cdn.nlark.com/yuque/0/2023/jpeg/35492615/1698990618691-f1c3ffea-624d-478c-8c29-9394df76622e.jpeg)

图6-4 移动端上传视频

### 6.2.3测试**视频播放功能**
桌面端视频播放测试：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990619366-c6b1fe2c-d5dd-45dc-9850-53b825430023.png)

图6-5桌面端视频播放

移动端视频播放测试：

![](https://cdn.nlark.com/yuque/0/2023/jpeg/35492615/1698990620116-ea82cfdd-9d63-40f8-9a97-8b3a9e749e1f.jpeg)

图6-6移动端视频播放

 

### 6.2.4测试文件编辑**功能**
桌面端文件编辑测试：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990620742-c08440c6-fb1a-4a71-afe8-066a2de0d17d.png)

图6-7桌面端文件编辑

移动端文件编辑测试：

![](https://cdn.nlark.com/yuque/0/2023/jpeg/35492615/1698990621433-041f5650-7456-422f-a57f-8630523845bf.jpeg)

图6-8移动端文件编辑

### 6.2.5测试用户**功能**
创建用户：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990622046-956b45f1-f9bd-4d56-ba2e-312352256d6d.png)

图6-9创建用户

此处创建一个运维账号，其它两个不再演示。

三个账号创建完成：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990622707-8e2a5f50-15b8-47ad-9bc9-81a1bdd1b20d.png)

图6-10测试用户创建完毕

配置用户权限：

演示赋予给运维部门部分权限。

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990623277-16bade33-0e4c-42b3-8254-742ece92cce6.png)

图6-11 权限修改

测试登录，并且创建文件：

![](https://cdn.nlark.com/yuque/0/2023/png/35492615/1698990623847-38d15a70-9173-4cda-971d-54e4c8b1c6c6.png)

图6-12 张三登录

测试所有模块完成。

## 6.3测试结果
云桌面使用情况测试:

表 6-3 测试结果

|   | **桌面端** | **移动端** |
| :---: | :---: | :---: |
| **访问平台** | √ | √ |
| **上传文件** | √ | √ |
| **观看视频** | √ | √ |
| **编辑文档** | √ | √ |
| **用户注册** | √ | √ |
| **权限管理** | √ | √ |


云平台基本功能测试完成，可以看到整体情况还是成功的，可以实现修改代码、云网盘、随时随地访问等功能，还有部分插件功能能够实现更多的扩展功能，这里就不一一演示。

至此项目部署完毕。
