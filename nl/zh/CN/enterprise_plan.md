---

copyright:
  years: 2018, 2019
lastupdated: "2019-05-31"

keywords: blockchain network, Enterprise Plan, production-ready network

subcollection: blockchain

---

{:external: target="_blank" .external}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 关于企业套餐
{: #enterprise-plan-about}

<!--[placeholder] Enterprise Plan is deprecated on May 30. No new Enterprise Plan networks can be created then. Your existing networks are not affected, but you can use them and get IBM's support on them for only another 30 days. You might consider using {{site.data.keyword.blockchainfull_notm}} Platform free 2.0 beta instead.
{: note} -->

{{site.data.keyword.blockchainfull}} Platform 企业套餐是一种生产就绪型产品，适用于希望创建或加入区块链网络以开展真实业务的组织。此套餐提供关键基础架构以及工具和支持，可轻松地开始使用高度安全的生产就绪型网络。2018 年 5 月 15 日，企业套餐从 Hyperledger Fabric V1.0 升级到 V1.1。2018 年 5 月 15 日之后创建的所有网络都为 Fabric V1.1 级别。但是，先前创建的网络将保持为 Fabric V1.0 级别。
{:shortdesc}

**企业套餐**是用于提供高级别安全性和支持的生产环境。通过在企业套餐上部署网络，可以利用以下功能：

* 具有许多硬件、固件和软件安全功能的超高安全性环境。
* 强化的体系结构，实现可伸缩性、弹性和可用性。
* 针对性能进行优化，并在全球最快的 Linux 计算上运行。

在 {{site.data.keyword.blockchainfull_notm}} Platform 上操作网络包括用于简化管理任务的工具和功能：

* 用于在网络上监视和管理资源的仪表板。
* 完整代码堆栈无缝升级。
* 集成到门户网站的全天候技术支持。
* 强化的安全堆栈，具有无特权访问、恶意软件和篡改抵制、100% 加密，以及许多其他功能，用于具有受监管行业中敏感数据的网络。
* 企业网络每 24 小时执行一次非现场备份。如果发生灾难，可以将这些网络复原到同一站点或备用站点。

**注：**
- 企业套餐提供的是生产环境。如果您需要开发和测试环境，请参阅[关于入门套餐](/docs/services/blockchain?topic=blockchain-starter-plan-about#starter-plan-about)。
- {{site.data.keyword.blockchainfull_notm}} Platform 是 {{site.data.keyword.cloud_notm}} 上的平台服务，所有成员资格产品均遵循服务级别协议 (SLA) 上的 [{{site.data.keyword.cloud_notm}} 服务条款](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm){: external}。企业套餐网络在单个地理位置的数据中心进行供应。有关可用地理位置的列表，请参阅 [{{site.data.keyword.blockchainfull_notm}} Platform 位置](/docs/services/blockchain?topic=blockchain-ibp-regions-locations#ibp-regions-locations)。

对于即将启动网络的成员，{{site.data.keyword.IBM_notm}} 提供图形用户界面来指导网络启动器完成设置和供应网络的关键步骤。这包括邀请其他成员和设置管控规则。有关更多信息，请参阅[管理企业套餐网络](/docs/services/blockchain?topic=blockchain-getting-started-with-enterprise-plan#getting-started-with-enterprise-plan)。一旦部署了网络，就可以使用交互式图形用户界面（即“网络监视器”）来监视网络的运行状况和活动，管理关键网络活动（包括新部署、添加/除去成员、链代码生命周期和通道管理），以及寻求技术支持。有关更多信息，请参阅[使用网络监视器](/docs/services/blockchain?topic=blockchain-ibp-dashboard#ibp-dashboard)。

现在注册 [{{site.data.keyword.blockchainfull_notm}} 成员资格](https://cloud.ibm.com/catalog/services/ibm-blockchain-5-prod){: external}。

{{site.data.keyword.blockchainfull_notm}} Platform 以关键的 Hyperledger Fabric 组件为基础构建，其中包括一个认证中心 (CA) 和至少 1 个同级（最多 6 个）。企业套餐还为网络成员提供崩溃容错 (CFT) Kafka 排序服务。

Fabric CA 是企业套餐随附的认证中心。每个成员提供了两个中间 CA，用于将成员资格授予网络。通过使用 CA，成员还可以为网络的用户提供成员资格证书。

请务必了解，要将事务处理附加到分类帐，涉及以下三个阶段：
1. 事务处理模拟和支持（同级）
2. 排序（排序服务）
3. 验证和落实（同级）

成员所拥有的 Fabric 同级是应用程序的接口或网关，用于执行链代码，从而提供用于对分类帐执行事务处理的业务逻辑。必须支持所有事务处理。网络的其他成员会执行此支持。背书后，事务处理将发送到 {{site.data.keyword.IBM_notm}} 提供的排序服务。

除了核心区块链组件外，“企业成员资格”选项还提供了具有安全数据存储和通信 (TLS) 以及高可用性的基础架构。虽然 Fabric 网络共享这些基础架构资源，但是为网络中的 Fabric 组件节点提供了隔离，并且每个节点都在用于保护执行环境的安全 Docker 容器中执行。

必须确定的唯一方面是网络所需的同级的大小。此决策基于所需的通道数，以及每个通道的工作负载、内存使用情况和磁盘空间（存储器）。

您应该将企业套餐用于生产级别或接近生产级别的更稳定部署。对于测试用途，请使用[入门套餐](/docs/services/blockchain?topic=blockchain-starter-plan-about#starter-plan-about)或[本地安装 Docker 映像](https://hyperledger-fabric.readthedocs.io/en/release-1.2/build_network.html)。

<!--- The Enterprise plan provides the ordering service and CA. The membership fee is $1,000, and a per peer fee of $1,000 that is associated with the network. If you want to have high availability (HA), you must purchase an additional peer to provide the HA capabilities. For example, one organization (associated membership fee of $1,000) of two peers ($1,000 X 2 peers) with HA ($1,000 X 2 HA peers) requires a monthly charge of $5,000.  --->

## 定价
{: #enterprise-plan-about-pricing}

要使用企业套餐，网络成员必须每月支付 1000 美元的成员资格费用，并且每月为网络中的每个同级额外支付 1000 美元。每月费用按日分派计费。例如，如果一个成员（关联的成员资格费用为 1,000 美元）有两个同级（每个同级的费用 1,000 美元 X 2 个同级），该成员每月需要支付 3,000 美元。如果该月有 30 天，那么该成员每天支付 100 美元（3,000 美元/30）。请注意，如果需要高可用性 (HA)，必须使必需的同级数量翻倍才能提供 HA 功能。

网络成员可以使用自己的 {{site.data.keyword.cloud_notm}} 帐户（其中包含用于创建网络实例的空间）来支付帐单。或者，一个网络成员可以支付网络中所有成员的帐单。有关如何为区块链网络付费的更多信息，请参阅[为网络付费](/docs/services/blockchain/howto?topic=blockchain-paying-mode#paying-mode)。
