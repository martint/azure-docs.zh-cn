---
author: diberry
ms.author: diberry
ms.service: cognitive-services
ms.topic: include
ms.date: 01/22/2019
ms.openlocfilehash: ed512c0f56d8da5cb8e47b20f2495054fdedf020
ms.sourcegitcommit: 90c6b63552f6b7f8efac7f5c375e77526841a678
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56740734"
---
此容器具有以下配置设置：

|需要|设置|目的|
|--|--|--|
|是|[ApiKey](#apikey-configuration-setting)|用于跟踪账单信息。|
|否|[ApplicationInsights](#applicationinsights-setting)|允许向容器添加 [Azure Application Insights](https://docs.microsoft.com/azure/application-insights) 遥测支持。|
|是|[计费](#billing-configuration-setting)|指定 Azure 上服务资源的终结点 URI。|
|是|[Eula](#eula-setting)| 表示已接受容器的许可条款。|
|否|[Fluentd](#fluentd-settings)|将日志和（可选）指标数据写入 Fluentd 服务器。|
|否|[Http 代理](#http-proxy-credentials-settings)|配置 HTTP 代理以发出出站请求。|
|否|[日志记录](#logging-settings)|为容器提供 ASP.NET Core 日志记录支持。 |
|否|[Mounts](#mount-settings)|从主计算机读取数据并将其写入到容器，以及从容器读回数据并将其写回到主计算机。|
