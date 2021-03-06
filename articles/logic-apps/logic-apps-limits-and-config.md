---
title: 限制和配置 - Azure 逻辑应用 | Microsoft Docs
description: Azure 逻辑应用的服务限制和配置值
services: logic-apps
documentationcenter: ''
author: ecfan
manager: cfowler
editor: ''
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: logic-apps
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 05/14/2018
ms.author: estfan
ms.openlocfilehash: 8c2ac4b8f55d25d5d3fcfdd6a9bcb6f6c8cfc201
ms.sourcegitcommit: d78bcecd983ca2a7473fff23371c8cfed0d89627
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/14/2018
ms.locfileid: "34166295"
---
# <a name="limits-and-configuration-information-for-azure-logic-apps"></a>Azure 逻辑应用的限制和配置信息

本文介绍使用 Azure 逻辑应用创建和运行自动化工作流的限制和配置的详细信息。 对于 Microsoft Flow，请参阅 [Microsoft Flow 中的配置和限制](https://docs.microsoft.com/flow/limits-and-config)。

<a name="definition-limits"></a>

## <a name="definition-limits"></a>定义限制

下面是针对单个逻辑应用定义的限制：

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| 每个工作流的操作数 | 500 | 要对此限制进行扩展，可根据需要添加嵌套工作流。 |
| 操作的允许嵌套深度 | 8 | 要对此限制进行扩展，可根据需要添加嵌套工作流。 | 
| 每个订阅每个区域的工作流数 | 1,000 | | 
| 每个工作流的触发数 | 10 | 在代码视图中工作时，而不是在设计器中工作时 | 
| Switch 作用域事例限制 | 25 | | 
| 每个工作流的变量数 | 250 | | 
| 每个表达式的字符数 | 8,192 | | 
| `trackedProperties` 的最大大小 | 16,000 个字符 | 
| `action` 或 `trigger` 的名称 | 80 个字符 | | 
| `description` 的长度 | 256 个字符 | | 
| `parameters` 最大值 | 50 | | 
| `outputs` 最大值 | 10 | | 
||||  

<a name="run-duration-retention-limits"></a>

## <a name="run-duration-and-retention-limits"></a>运行持续时间和保留期限制

下面是针对单个逻辑应用运行的限制：

| 名称 | 限制 | 说明 | 
|------|-------|-------| 
| 运行持续时间 | 90 天 | 若要更改此限制，请参阅[更改运行持续时间](#change-duration)。 | 
| 存储保留期 | 90 天（从运行开始时间计算） | 若要更改此限制，请参阅[更改存储保留期](#change-retention)。 | 
| 最小重复间隔 | 1 秒 | | 
| 最大重复间隔 | 500 天 | | 
|||| 

<a name="change-duration"></a>
<a name="change-retention"></a>

### <a name="change-run-duration-and-storage-retention"></a>更改运行持续时间和存储保留期

你可以将此限制更改为 7 天至 90 天之间的值。 但是，若要超出最大限制，[请联系逻辑应用团队](mailto://logicappsemail@microsoft.com)，就你的要求获取帮助。

1. 在 Azure 门户的逻辑应用菜单中，选择“工作流设置”。 

2. 在“运行时选项”下，从“运行历史记录保留天数”列表中选择“自定义”。 

3. 输入或拖动滑块以获得所需的天数。

<a name="looping-debatching-limits"></a>

## <a name="looping-and-debatching-limits"></a>循环和解除批处理限制

下面是针对单个逻辑应用运行的限制：

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| Until 迭代 | 5,000 | | 
| ForEach 项 | 100,000 | 可以使用[查询操作](../connectors/connectors-native-query.md)根据需要筛选更大数组。 | 
| ForEach 并行度 | 50 | 默认值为 20。 <p>要在 ForEach 循环中设置特定并行级别，请在 `foreach` 操作中设置 `runtimeConfiguration` 属性。 <p>要按顺序运行 ForEach 循环，请在 `foreach` 操作中将 `operationOptions` 属性设置为“顺序”。 | 
| SplitOn 项 | 100,000 | | 
|||| 

<a name="throughput-limits"></a>

## <a name="throughput-limits"></a>吞吐量限制

下面是针对单个逻辑应用运行的限制：

| 名称 | 限制 | 说明 | 
| ----- | ----- | ----- | 
| 每 5 分钟执行的操作数 | 100,000 | 若要将限制增加到 300,000，可以在 `High Throughput` 模式下运行逻辑应用。 若要配置高吞吐量模式，请在工作流资源的 `runtimeConfiguration` 下，将 `operationOptions` 属性设置为 `OptimizedForHighThroughput`。 <p>**请注意**：高吞吐量模式处于预览状态。 另外，还可以根据需要在多个应用之间分配工作负荷。 | 
| 操作并发传出调用数 | ~2,500 | 减少并发请求数，或根据需要减少持续时间。 | 
| 运行时终结点：并发传入调用数 | ~1,000 | 减少并发请求数，或根据需要减少持续时间。 | 
| 运行时终结点：每 5 分钟读取的调用数  | 60,000 | 可以根据需要在多个应用之间分配工作负荷。 | 
| 运行时终结点：每 5 分钟调用的调用数| 45,000 |可以根据需要在多个应用之间分配工作负荷。 | 
|||| 

若要在正常处理中超过这些限制，或要运行可能超过这些限制的负载测试，请[与逻辑应用团队联系](mailto://logicappsemail@microsoft.com)，获取满足要求的帮助。

<a name="request-limits"></a>

## <a name="http-request-limits"></a>HTTP 请求限制

以下限制适用于单个 HTTP 请求或同步连接器调用：

#### <a name="timeout"></a>超时

某些连接器操作会进行异步调用或侦听 Webhook 请求，因此，这些操作的超时时间可能会长于以下限制。 有关详细信息，请参阅特定连接器的技术详细信息以及[工作流触发器和操作](../logic-apps/logic-apps-workflow-actions-triggers.md#http-action)。

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| 传出的请求 | 120 秒 | 对于运行时间较长的操作，请使用[异步轮询模式](../logic-apps/logic-apps-create-api-app.md#async-pattern)或 [until 循环](../logic-apps/logic-apps-workflow-actions-triggers.md#until-action)。 | 
| 同步响应 | 120 秒 | 要使原始请求能够获得响应，则除非以嵌套工作流的形式调用其他逻辑应用，否则必须在限制内完成响应的所有步骤。 有关详细信息，请参阅[调用、触发器或嵌套逻辑应用](../logic-apps/logic-apps-http-endpoint.md)。 | 
|||| 

#### <a name="message-size"></a>消息大小

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| 消息大小 | 100 MB | 若要解决此限制问题，请参阅[使用分块处理大型消息](../logic-apps/logic-apps-handle-large-messages.md)。 但是，某些连接器和 API 可能不支持分块，甚至不支持默认限制。 | 
| 使用分块的消息大小 | 1 GB | 此限制适用于本机支持分块或可以在其运行时配置中启用分块支持的操作。 有关详细信息，请参阅[使用分块处理大型消息](../logic-apps/logic-apps-handle-large-messages.md)。 | 
| 表达式计算限制 | 131,072 个字符 | `@concat()`、`@base64()`、`@string()` 表达式的长度不能超过此限制。 | 
|||| 

#### <a name="retry-policy"></a>重试策略

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| 重试次数 | 90 | 默认值为 4。 若要更改默认值，请使用[重试策略参数](../logic-apps/logic-apps-workflow-actions-triggers.md)。 | 
| 重试最大延迟 | 1 天 | 若要更改默认值，请使用[重试策略参数](../logic-apps/logic-apps-workflow-actions-triggers.md)。 | 
| 重试最小延迟 | 5 秒 | 若要更改默认值，请使用[重试策略参数](../logic-apps/logic-apps-workflow-actions-triggers.md)。 |
|||| 

<a name="custom-connector-limits"></a>

## <a name="custom-connector-limits"></a>自定义连接器限制

下面介绍对可通过 Web API 创建的自定义连接器的限制。

| 名称 | 限制 | 
| ---- | ----- | 
| 自定义连接器数 | 每个 Azure 订阅 1,000 | 
| 每分钟的请求数量（对于自定义连接器创建的每个连接） | 每个连接 500 个请求 |
|||| 

<a name="integration-account-limits"></a>

## <a name="integration-account-limits"></a>集成帐户限制

<a name="artifact-number-limits"></a>

### <a name="artifact-limits-per-integration-account"></a>每个集成帐户的项目限制

下面介绍对每个集成帐户的项目数量的限制。 有关详细信息，请参阅[逻辑应用定价](https://azure.microsoft.com/pricing/details/logic-apps/)。

*免费层*

| 项目 | 限制 | 说明 | 
|----------|-------|-------| 
| EDI 参与方 | 25 | | 
| EDI 贸易协议 | 10 | | 
| 地图 | 25 | | 
| 架构 | 25 | 
| 程序集 | 10 | | 
| 批处理配置 | 5 | 
| 证书 | 25 | | 
|||| 

*基本层*

| 项目 | 限制 | 说明 | 
|----------|-------|-------| 
| EDI 参与方 | 2 | | 
| EDI 贸易协议 | 1 | | 
| 地图 | 500 | | 
| 架构 | 500 | 
| 程序集 | 25 | | 
| 批处理配置 | 1 | | 
| 证书 | 2 | | 
|||| 

*标准层*

| 项目 | 限制 | 说明 | 
|----------|-------|-------| 
| EDI 参与方 | 500 | | 
| EDI 贸易协议 | 500 | | 
| 地图 | 500 | | 
| 架构 | 500 | 
| 程序集 | 50 | | 
| 批处理配置 | 5 |  
| 证书 | 50 | | 
|||| 

<a name="artifact-capacity-limits"></a>

### <a name="artifact-capacity-limits"></a>项目容量限制

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| 架构 | 8 MB | 若要上传大于 2 MB 的文件，请使用 [blob URI](../logic-apps/logic-apps-enterprise-integration-schemas.md)。 | 
| 映射（XSLT 文件） | 2 MB | | 
| 运行时终结点：每 5 分钟读取的调用数 | 60,000 | 你可根据需要在多个帐户之间分配工作负荷。 | 
| 运行时终结点：每 5 分钟调用的调用数 | 45,000 | 你可根据需要在多个帐户之间分配工作负荷。 | 
| 运行时终结点：每 5 分钟跟踪的调用数 | 45,000 | 你可根据需要在多个帐户之间分配工作负荷。 | 
| 运行时终结点：阻止并发调用数 | ~1,000 | 你可减少并发请求数，或根据需要减少持续时间。 | 
||||  

<a name="b2b-protocol-limits"></a>

### <a name="b2b-protocol-as2-x12-edifact-message-size"></a>B2B 协议（AS2、X12、EDIFACT）消息大小

以下限制适用于 B2B 协议：

| 名称 | 限制 | 说明 | 
| ---- | ----- | ----- | 
| AS2 | 50 MB | 适用于解码和编码 | 
| X12 | 50 MB | 适用于解码和编码 | 
| EDIFACT | 50 MB | 适用于解码和编码 | 
|||| 

<a name="configuration"></a>

## <a name="configuration-ip-addresses"></a>配置：IP 地址

### <a name="azure-logic-apps-service"></a>Azure 逻辑应用服务

某个区域中的所有逻辑应用都使用相同范围内的 IP 地址。
由逻辑应用直接使用 [HTTP](../connectors/connectors-native-http.md)、[HTTP + Swagger](../connectors/connectors-native-http-swagger.md) 或其他 HTTP 请求发出的调用来自此列表中的 IP 地址。 

| 逻辑应用区域 | 出站 IP |
|-------------------|-------------|
| 澳大利亚 | 13.73.114.207, 13.77.3.139, 13.70.159.205 |
| 澳大利亚东部 | 13.75.149.4, 104.210.91.55, 104.210.90.241 |
| 巴西南部 | 191.235.82.221, 191.235.91.7, 191.234.182.26 |
| 加拿大中部 | 52.233.29.92、52.228.39.241、52.228.39.244 |
| 加拿大东部 | 52.232.128.155、52.229.120.45、52.229.126.25 |
| 印度中部 | 52.172.154.168, 52.172.186.159, 52.172.185.79 |
| 美国中部 | 13.67.236.125, 104.208.25.27, 40.122.170.198 |
| 东亚 | 13.75.94.173, 40.83.127.19, 52.175.33.254 |
| 美国东部 | 13.92.98.111, 40.121.91.41, 40.114.82.191 |
| 美国东部 2 | 40.84.30.147, 104.208.155.200, 104.208.158.174 |
| 日本东部 | 13.71.158.3, 13.73.4.207, 13.71.158.120 |
| 日本西部 | 40.74.140.4, 104.214.137.243, 138.91.26.45 |
| 美国中北部 | 168.62.248.37, 157.55.210.61, 157.55.212.238 |
| 北欧 | 40.113.12.95, 52.178.165.215, 52.178.166.21 |
| 美国中南部 | 104.210.144.48, 13.65.82.17, 13.66.52.232 |
| 印度南部 | 52.172.50.24, 52.172.55.231, 52.172.52.0 |
| 东南亚 | 13.76.133.155, 52.163.228.93, 52.163.230.166 |
| 美国中西部 | 52.161.27.190, 52.161.18.218, 52.161.9.108 |
| 欧洲西部 | 40.68.222.65, 40.68.209.23, 13.95.147.65 |
| 印度西部 | 104.211.164.80, 104.211.162.205, 104.211.164.136 |
| 美国西部 | 52.160.92.112, 40.118.244.241, 40.118.241.243 |
| 美国西部 2 | 13.66.210.167, 52.183.30.169, 52.183.29.132 |
| 英国南部 | 51.140.74.14、51.140.73.85、51.140.78.44 |
| 英国西部 | 51.141.54.185、51.141.45.238、51.141.47.136 |
| | |

| 逻辑应用区域 | 入站 IP |
|-------------------|-------------|
| 澳大利亚东部 | 3.75.153.66、104.210.89.222、104.210.89.244 |
| 澳大利亚东南部 | 13.73.115.153、40.115.78.70、40.115.78.237 |
| 巴西南部 | 191.235.86.199、191.235.95.229、191.235.94.220 |
| 加拿大中部 | 13.88.249.209、52.233.30.218、52.233.29.79 |
| 加拿大东部 | 52.232.129.143、52.229.125.57、52.232.133.109 |
| 印度中部 | 52.172.157.194、52.172.184.192、52.172.191.194 |
| 美国中部 | 13.67.236.76、40.77.111.254、40.77.31.87 |
| 东亚 | 168.63.200.173、13.75.89.159、23.97.68.172 |
| 美国东部 | 137.135.106.54、40.117.99.79、40.117.100.228 |
| 美国东部 2 | 40.84.25.234、40.79.44.7、40.84.59.136 |
| 日本东部 | 13.71.146.140、13.78.84.187、13.78.62.130 |
| 日本西部 | 40.74.140.173、40.74.81.13、40.74.85.215 |
| 美国中北部 | 168.62.249.81、157.56.12.202、65.52.211.164 |
| 北欧 | 13.79.173.49、52.169.218.253、52.169.220.174 |
| 美国中南部 | 52.172.9.47、52.172.49.43、52.172.51.140 |
| 印度南部 | 52.172.9.47、52.172.49.43、52.172.51.140 |
| 东南亚 | 52.163.93.214、52.187.65.81、52.187.65.155 |
| 美国中西部 | 52.161.26.172、52.161.8.128、52.161.19.82 |
| 欧洲西部 | 13.95.155.53、52.174.54.218、52.174.49.6 |
| 印度西部 | 104.211.164.112、104.211.165.81、104.211.164.25 |
| 美国西部 | 52.160.90.237、138.91.188.137、13.91.252.184 |
| 美国西部 2 | 13.66.224.169、52.183.30.10、52.183.39.67 |
| 英国南部 | 51.140.79.109、51.140.78.71、51.140.84.39 |
| 英国西部 | 51.141.48.98、51.141.51.145、51.141.53.164 |
| | |

### <a name="connectors"></a>连接器

[连接器](../connectors/apis-list.md)进行的调用来自此列表中的 IP 地址。

| 逻辑应用区域 | 出站 IP |
|-------------------|-------------|
| 澳大利亚东部 | 40.126.251.213 |
| 澳大利亚东南部 | 40.127.80.34 |
| 巴西南部 | 191.232.38.129 |
| 加拿大中部 | 52.233.31.197、52.228.42.205、52.228.33.76、52.228.34.13 |
| 加拿大东部 | 52.229.123.98、52.229.120.178、52.229.126.202、52.229.120.52 |
| 印度中部 | 104.211.98.164 |
| 美国中部 | 40.122.49.51 |
| 东亚 | 23.99.116.181 |
| 美国东部 | 191.237.41.52 |
| 美国东部 2 | 104.208.233.100 |
| 日本东部 | 40.115.186.96 |
| 日本西部 | 40.74.130.77 |
| 美国中北部 | 65.52.218.230 |
| 北欧 | 104.45.93.9 |
| 美国中南部 | 104.214.70.191 |
| 印度南部 | 104.211.227.225 |
| 东南亚 | 13.76.231.68 |
| 欧洲西部 | 40.115.50.13 |
| 印度西部 | 104.211.161.203 |
| 美国西部 | 104.40.51.248 |
| 英国南部 | 51.140.80.51 |
| 英国西部 | 51.141.47.105 |
| | | 

## <a name="next-steps"></a>后续步骤  

* [创建第一个逻辑应用](../logic-apps/quickstart-create-first-logic-app-workflow.md)  
* [常见示例和方案](../logic-apps/logic-apps-examples-and-scenarios.md)
* [视频：使用逻辑应用自动执行业务流程](http://channel9.msdn.com/Events/Build/2016/T694) 
* [视频：将系统与逻辑应用集成](http://channel9.msdn.com/Events/Build/2016/P462)
