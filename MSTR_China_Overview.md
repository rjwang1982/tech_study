<img src="aws-partner.png" height="50" />    <img src="vstecs-logo-horizontal.png" height="50" />

# MicroStrategy 中国区业务概述

**作者**: RJ.Wang | 高级工程师<br>
**公司**: 伟仕佳杰 (VSTECS) | AWS Partner<br>
**邮箱**: renjun.wang@vstecs.com<br>
**更新日期**: 2026-04-17

---

## 1. 客户概况

MicroStrategy（微策略）成立于 1989 年，总部位于美国弗吉尼亚州，是全球领先的企业级商业智能（BI）与数据分析平台供应商。其最新一代产品 MicroStrategy ONE 平台融合 AI 驱动分析、云原生架构和统一语义层，为大型企业提供数据发现、交互式仪表盘、移动分析和嵌入式 BI 等全栈能力。MicroStrategy 在中国区通过合作伙伴生态为本地企业客户提供 BI 解决方案，服务覆盖医药与生命科学、金融服务、制造业、零售与消费品等多个行业。

---

## 2. 中国区服务的行业与典型业务场景

在医药与生命科学领域，辉瑞等跨国药企利用 MSTR 平台进行临床试验数据多维分析和药品销售渠道洞察，医疗器械企业借助平台实现供应链可视化和区域销售绩效看板，CRO/CDMO 机构则用于项目进度追踪和运营效率分析。

在金融服务领域，商业银行使用 MSTR 进行风控指标监控和合规报表自动化，保险公司依托平台开展理赔分析、客户画像与精准营销，证券和基金公司则将其应用于投研数据分析和交易行为洞察。

在制造业领域，汽车制造企业通过 MSTR 实现生产线实时监控和质量缺陷追溯，电子制造企业用于良率分析和供应商绩效评估，能源化工企业则借助平台进行设备运维分析和能耗优化。

在零售与消费品领域，快消品牌利用 MSTR 开展全渠道销售分析和促销效果评估，连锁零售企业搭建门店运营看板和库存周转优化体系，电商平台则用于用户行为分析和 GMV 预测。

---

## 3. 中国区部署架构

### 3.1 MicroStrategy 平台组件

MicroStrategy 在中国区的部署包含多个核心组件。Intelligence Server 是核心分析引擎，负责内存 Cube 加载、多维 OLAP 计算和查询处理，对内存和 CPU 要求极高。Web Server 基于 Tomcat 或 IIS 构建，提供报表、仪表盘和 Dossier 的浏览器端访问。Mobile Server 作为移动端 BI 网关，支持 iOS 和 Android 设备的离线缓存和推送分析。Library Server 是协作与内容分发平台，支持个性化内容推荐和团队协作。Platform Analytics 负责平台运维监控，追踪用户使用行为、查询性能和系统健康状态。Distribution Services 提供报表定时调度与分发能力，支持邮件、文件和打印等多种输出方式。Narrowcast Server 作为主动式告警引擎，基于阈值触发自动通知。

### 3.2 AWS 服务使用情况

MicroStrategy 中国区客户在 AWS 中国区域（北京/宁夏）的典型部署使用以下 AWS 服务：

在计算层，生产环境的 Intelligence Server 部署在 u-6tb1.112xlarge 或 u-3tb1.56xlarge 高内存实例上，支撑 TB 级内存 Cube 加载和大规模并发 OLAP 查询。开发和测试环境使用 r6i.16xlarge 或 r6i.24xlarge 内存优化实例。Web Server 和 Library 运行在 m6i.4xlarge 或 m6i.8xlarge 通用计算实例上，承载 Web 应用和 API 服务。Distribution Services 使用 c6i.4xlarge 计算优化实例处理批量报表生成和调度任务。

在数据库层，MSTR Metadata Repository 和 History List 使用 Amazon RDS for SQL Server 或 PostgreSQL，分别存储平台元数据（对象定义、安全策略、用户配置）和报表执行历史及缓存索引。客户业务数据仓库通常部署在 Amazon RDS for SQL Server 或 Oracle 上，Intelligence Server 通过 ODBC/JDBC 连接进行查询。

在存储层，Amazon S3 用于报表导出文件存储（PDF/Excel/CSV）、数据湖对接和备份归档。Amazon EFS 作为 Intelligence Server 集群的共享存储，用于 Cube 文件、日志文件和配置文件的跨节点共享。

此外，部署还使用 Elastic Load Balancing（ALB）实现 Web Server 和 Library 的负载均衡与高可用，Amazon CloudWatch 进行平台监控告警和资源使用率追踪，AWS Backup 实现数据库和 EFS 的自动化备份，Amazon VPC 提供生产、开发、测试环境的网络隔离，AWS Direct Connect 实现客户本地数据中心与 AWS 的专线互联。

---

## 4. 已上线核心业务

在企业级报表与仪表盘方面，已上线面向管理层的经营分析驾驶舱（Executive Dashboard）、各业务线的自助分析门户（Self-Service Analytics Portal），以及定时报表自动生成与邮件分发（Scheduled Report Distribution）。

在移动端 BI 方面，已部署高管移动看板并支持离线浏览和数据刷新，现场销售团队可通过移动端进行数据查询，同时支持基于地理位置的区域业绩可视化。

在嵌入式分析方面，已将 MSTR 分析能力嵌入客户自有业务系统（ERP/CRM/OA），通过 REST API 和 Embedding SDK 实现无缝集成，并支持 SSO 单点登录和细粒度权限控制。

在大规模数据分析方面，TB 级内存 Cube 支撑数十亿行级数据的秒级查询，提供多维交叉分析（Cross-Tab）和钻取（Drill-Down）能力，以及预测分析和趋势建模。

---

## 5. 资源消耗特征

MicroStrategy 属于典型的高算力、高内存消耗型工作负载。Intelligence Server 单节点内存需求可达 3TB 至 6TB，用于加载内存 Cube。高并发查询场景下 CPU 利用率可达 70% 至 90%。Cube 加载和刷新期间会产生大量顺序读写 I/O。Web 和 Mobile 端的并发访问以及数据源查询会产生持续的网络流量。生产环境为 7×24 常驻运行，开发和测试环境按需启停。

---

*本文档由伟仕佳杰 (VSTECS) 作为 AWS Partner 提供*
