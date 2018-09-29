---
title: Azure Monitor 概述 | Microsoft Docs
description: 适用于 Azure 服务和应用程序的完整监视策略所涉及的 Microsoft 服务及功能的概述。
author: bwren
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: azure-monitor
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/14/2018
ms.author: bwren
ms.openlocfilehash: 97cc6d6e922ab0bedd729eddca754ae016f041bf
ms.sourcegitcommit: 32d218f5bd74f1cd106f4248115985df631d0a8c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/24/2018
ms.locfileid: "46958010"
---
# <a name="azure-monitor-overview"></a>Azure Monitor 概述

Azure Monitor 提供用于收集、分析和处理来自云与本地环境的遥测数据的综合解决方案，可将应用程序的可用性和性能最大化。 它可以帮助你了解应用程序的性能，并主动识别影响应用程序及其所依赖资源的问题。

> [!VIDEO https://www.youtube.com/embed/_hGff5bVtkM]

## <a name="overview"></a>概述
下图提供了 Azure Monitor 的概要视图。 示意图的中心是用于存储指标和日志（Azure Monitor 使用的两种基本类型的数据）的数据存储。 左侧是[从不同的受监视资源收集遥测数据](../monitoring/monitoring-data-sources.md)并填充[数据存储](../monitoring/monitoring-data-collection.md)的源。 右侧是 Azure Monitor 针对这些收集的数据执行的不同功能，例如分析、警报和流式传输到外部系统。


![Azure Monitor 概述](media/overview/overview.png)


## <a name="monitoring-data-platform"></a>监视数据平台
Azure Monitor 收集的所有数据属于以下两种基本类型之一：[指标和日志](../monitoring/monitoring-data-collection.md)。 [指标](../monitoring/monitoring-data-collection.md#metrics)是数字值，用于描述系统某些方面在特定时间点的情况。 指标是轻型数据，可以支持近实时方案。 [日志](../monitoring/monitoring-data-collection.md#logs)包含不同类型的已经整理成记录的数据，每种类型都有不同的属性集。 与性能数据一样，事件和跟踪等遥测数据也作为日志存储，因此，可将它们合并以进行分析。

Azure 门户中的“概述”页会直接显示 Azure Monitor 针对许多 Azure 资源收集的数据。 例如，在查看任一虚拟机时，多个图表会显示性能指标。 单击任一图形会在 Azure 门户上的[指标资源管理器](../monitoring-and-diagnostics/monitoring-metric-charts.md)中打开数据，可在其中绘制多个指标在不同时间段的值的图表。  可以通过交互方式查看图表，也可以将其固定到某个仪表板，与其他可视化效果一起查看。

![度量值](media/overview/metrics.png)

Azure Monitor 收集的日志数据存储在 Log Analytics 中。Log Analytics 包含[丰富查询语言](../log-analytics/log-analytics-queries.md)，可以快速检索、合并与分析收集的数据。  可以使用 Azure 门户中的 [Log Analytics 页](../log-analytics/log-analytics-log-search-portals.md)创建和测试查询，然后可以直接使用这些工具分析数据，或者保存查询以便与[可视化效果](visualizations.md)或[警报规则](../monitoring-and-diagnostics/monitoring-overview-alerts.md)配合使用。

Log Analytics 查询语言适用于简单的日志查询，但也包括高级功能，例如聚合、联接、智能分析。 可以通过提供的[多个课程](../log-analytics/query-language/get-started-queries.md)快速了解此查询语言。  特定指南提供给已熟悉 [SQL](../log-analytics/query-language/sql-cheatsheet.md) 和 [Splunk](../log-analytics/query-language/splunk-cheatsheet.md) 的用户。

![日志](media/overview/logs.png)

## <a name="what-data-does-azure-monitor-collect"></a>Azure Monitor 收集哪些数据？
Log Analytics 可从各种源收集数据。 可将应用程序的监视数据视为划分了层次，范围为应用程序、应用程序依赖的任何操作系统和服务，直到平台本身。 Azure Monitor 从以下每个层收集数据：

- **应用程序监视数据**：有关编写的代码的性能和功能的数据，不管平台是什么。
- **来宾 OS 监视数据**：有关运行应用程序的操作系统的数据。 此应用程序可以在 Azure 中运行，也可以在其他云中或本地运行。 
- **Azure 资源监视数据**：有关 Azure 资源操作的数据。
- **Azure 订阅监视数据**：有关 Azure 订阅操作和管理的数据，以及有关 Azure 本身运行状况和操作的数据。 
- **Azure 租户监视数据**：有关租户级 Azure 服务（例如 Azure Active Directory）操作的数据。

在创建 Azure 订阅并开始添加虚拟机和 Web 应用等资源后，Azure Monitor 会立即开始收集数据。  [活动日志](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)记录创建或修改资源的时间。 [指标](../monitoring-and-diagnostics/monitoring-overview-metrics.md)告知资源的性能如何，以及该资源消耗的资源。 

通过[启用诊断](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)并[将代理添加](../log-analytics/log-analytics-agent-windows.md)到计算资源，将数据收集范围扩展到资源的实际操作。 这会收集资源内部操作的遥测数据，并可让你配置不同的[数据源](../log-analytics/log-analytics-data-sources.md)用于从 Windows 和 Linux 来宾操作系统收集日志与指标。 

[将检测包添加到应用程序](../application-insights/app-insights-azure-web-apps.md)，使 Application Insights 能够收集有关应用程序的详细信息，包括页面视图、应用程序请求和异常。 通过配置[可用性测试](../application-insights/app-insights-monitor-web-app-availability.md)来模拟用户流量，进一步验证应用程序的可用性。

### <a name="custom-sources"></a>自定义源
Azure Monitor 可以使用[数据收集器 API](../log-analytics/log-analytics-data-collector-api.md) 从任何 REST 客户端收集日志数据。 这样，便可以创建自定义监视方案，并将监视范围扩展到不通过其他源公开遥测数据的资源。



## <a name="insights"></a>洞察力
仅当能够有利于洞察计算环境的操作时，监视数据才有作用。 Azure Monitor 包含多种功能和工具，可以提供应用程序及其依赖的其他资源的有用见解。 [监视解决方案](../monitoring/monitoring-solutions.md)和 [Application Insights](../application-insights/app-insights-overview.md) 与 Container Insights 等功能在应用程序和特定 Azure 服务的不同方面提供深入见解。 

### <a name="application-insights"></a>Application Insights
无论 Web 应用程序托管在云中还是本地，[Application Insights](http://azure.microsoft.com/documentation/services/application-insights) 都可以监视其可用性、性能和使用情况。 它利用 Log Analytics 中的强大数据分析平台来提供应用程序操作的深入见解，并可以诊断错误，无需等到用户报告这些问题。 Application Insights 包含各种开发工具的连接点，并与 Visual Studio 集成以支持 DevOps 过程。

![App Insights](media/overview/app-insights.png)

### <a name="azure-monitor-for-containers"></a>用于容器的 Azure Monitor
用于容器的 Azure Monitor 功能旨在监视部署到 Azure Kubernetes 服务 (AKS) 上托管的托管 Kubernetes 群集的容器工作负荷的性能。 它通过指标 API 从 Kubernetes 中提供的控制器、节点和容器收集内存和处理器指标，来提供性能可见性。 容器日志也会收集。  从 Kubernetes 群集启用监视后，将通过适用于 Linux 的 Log Analytics 代理的容器化版本自动收集这些指标和日志，并将其存储在 Log Analytics 中。

![容器运行状况](media/overview/container-insights.png)

### <a name="azure-monitor-for-vms"></a>用于 VM 的 Azure Monitor
Azure Monitor VM Insights 分析 Windows 和 Linux VM 的性能与运行状况，包括其不同的进程以及与其他资源和外部进程之间的相互依赖关系，可以大规模监视 Azure 虚拟机 (VM)。 该解决方案支持监视本地或其他云提供程序中托管的 VM 的性能和应用程序依赖项。  


![VM Insights](media/overview/vm-insights.png)

### <a name="monitoring-solutions"></a>监视解决方案
Azure Monitor 中的[监视解决方案](../monitoring/monitoring-solutions.md)是打包的逻辑集，提供有关特定应用程序或服务的见解。 它们将数据连同其他监视数据一起收集到 Log Analytics 中，并使用[查询](../log-analytics/log-analytics-queries.md)进行分析，使用[视图](../log-analytics/log-analytics-view-designer.md)进行可视化。 监视解决方案由 [Microsoft](../monitoring/monitoring-solutions-inventory.md) 或合作伙伴提供，可针对各种 Azure 服务和其他应用程序提供监视。

![监视解决方案](../monitoring/media/monitoring-solutions/overview.png)

## <a name="responding-to-critical-situations"></a>应对关键状况
除了让你以交互方式分析监视数据以外，有效的监视解决方案必须能够主动应对所收集的数据中指出的关键状况。 应对措施可以是向负责调查问题的管理员发送短信或邮件。 或者，可以启动自动化过程来尝试纠正错误状况。


### <a name="alerts"></a>警报
[Azure Monitor 中的警报](../monitoring-and-diagnostics/monitoring-overview-alerts.md)会主动发送有关关键状况的通知，并可能尝试采取纠正措施。 基于指标的警报规则根据数值提供近实时的警报，而基于日志的规则允许对多个源中的数据采用复杂的逻辑。

Azure Monitor 中的警报规则使用[操作组](../monitoring-and-diagnostics/monitoring-action-groups.md)，其中包含可在多个规则之间共享的独特接收者和操作集。 操作组可根据要求执行多种操作，例如，使用 Webhook 来让警报启动外部操作，或者与 ITSM 工具集成。

![警报](media/overview/alerts.png)

### <a name="autoscale"></a>自动缩放
自动缩放是指在处理应用程序负载时让适当数量的资源运行。 自动缩放允许创建规则，这些规则使用 Azure Monitor 收集的指标来确定何时要自动添加资源来应对负载增大的情况，并在空闲期删除资源以节省成本。 可以指定最小和最大实例数，并创建逻辑来控制何时要增加或减少资源。

![自动缩放](media/overview/autoscale.png)

## <a name="visualizing-monitoring-data"></a>可视化监视数据
图表和表等[可视化效果](visualizations.md)是用于汇总监视数据并向不同的受众呈现这些数据的有效工具。 Azure Monitor 具有自身的可视化监视数据的功能，并可利用其他 Azure 服务将这些数据发布到不同的受众。

### <a name="dashboards"></a>仪表板
使用 [Azure 仪表板](../azure-portal/azure-portal-dashboards.md)可将不同类型的数据（包括指标和日志）合并到 [Azure 门户](https://portal.azure.com)的单个窗格中。 可以选择与其他 Azure 用户共享仪表板。 除了任何日志查询或指标图表的输出以外，还可将整个 Azure Monitor 中的元素添加到 Azure 仪表板。 例如，可以创建一个包含多个磁贴的仪表板，这些磁贴分别用于显示指标图、活动日志表、Application Insights 的使用情况图表，以及 Log Analytics 的查询输出。

![仪表板](media/overview/dashboard.png)

### <a name="views"></a>视图
[Azure Monitor 中的视图](../log-analytics/log-analytics-view-designer.md)在 Log Analytics 中直观显示日志数据。  每个视图包含单个磁贴，使用该磁贴可以向下钻取到各种可视化效果的组合，例如汇总了关键数据的列表，以及条形图和折线图。  监视解决方案包含的视图汇总了特定应用程序的数据。你可以创建自己的视图来显示任何 Log Analytics 日志搜索的数据。 与 Azure Monitor 中的其他元素一样，可将视图添加到 Azure 仪表板。

![Log Analytics 视图](media/overview/view.png)

### <a name="power-bi"></a>Power BI
[Power BI](https://powerbi.microsoft.com) 是一个业务分析服务，可针对各种数据源提供交互式可视化效果，并且是将数据提供给组织内部和外部的其他人的有效方式。 可将 Power BI 配置为[自动从 Azure Monitor 导入日志数据](../log-analytics/log-analytics-powerbi.md)，以利用这些附加的可视化效果。


![Power BI](media/overview/power-bi.png)


## <a name="integrate-and-export-data"></a>集成和导出数据
通常，我们需要将 Azure Monitor 与其他系统集成，并生成使用监视数据的自定义解决方案。 其他 Azure 服务使用 Azure Monitor 来提供这种集成。

### <a name="event-hub"></a>事件中心
[Azure 事件中心](https://docs.microsoft.com/azure/event-hubs)是一个流式传输平台和事件引入服务，可以使用任何实时分析提供程序或批处理/存储适配器来转换和存储数据。 使用事件中心可[将 Azure Monitor 中的日志数据流式传输](../monitoring-and-diagnostics/monitor-stream-monitoring-data-event-hubs.md)到合作伙伴 SIEM 和监视工具。

> [!VIDEO https://www.youtube.com/embed/SPHxCgbcvSw]

### <a name="logic-apps"></a>逻辑应用
使用[逻辑应用](https://azure.microsoft.com/services/logic-apps)服务可以通过与不同系统和服务集成的工作流将任务和业务流程自动化。 其中提供了用于在 Azure Monitor 中读取和写入指标与日志的活动，使你能够生成与其他各种系统相集成的工作流。

![逻辑应用](../log-analytics/media/log-analytics-activity-logs-subscriptions/log-analytics-logic-apps-activity-log-overview.png)

### <a name="api"></a>API
可以使用多个 API 从/向 Azure Monitor 读取和写入指标与日志，以及访问生成的警报。 还可以配置和检索警报。 这样，几乎可以不受限制地生成与 Azure Monitor 集成的自定义解决方案。

## <a name="next-steps"></a>后续步骤
了解有关以下方面的详细信息：

* [Azure Monitor](https://azure.microsoft.com/services/monitor/)，以便开始使用核心监视指标和警报。
* [Application Insights](https://azure.microsoft.com/documentation/services/application-insights/)：如果要尝试诊断应用服务 Web 应用中的问题。
* [Log Analytics](https://azure.microsoft.com/documentation/services/log-analytics/)，以便分析所收集的监视数据和日志。


