---
title: include 文件
description: include 文件
services: azure-app-configuration
author: yegu
ms.service: azure-app-configuration
ms.topic: include
ms.date: 01/22/2019
ms.author: yegu
ms.custom: include file
ms.openlocfilehash: 0f066915046e363932652c104fabe96ed0a9d4c4
ms.sourcegitcommit: 12d67f9e4956bb30e7ca55209dd15d51a692d4f6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58227178"
---
1. 要创建新应用程序配置存储区，请登录 [Azure 门户](https://aka.ms/azconfig/portal)。 在页面的左上角，选择“+ 创建资源”。 在“搜索市场”框中，输入“应用程序配置”并按 Enter。

    ![搜索应用配置](../articles/azure-app-configuration/media/quickstarts/azure-app-configuration-new.png)

2. 在搜索结果中选择“应用程序配置”，然后选择“创建”。

3. 在“应用程序配置” > “创建”页中，输入以下设置。

    | 设置 | 建议的值 | 说明 |
    |---|---|---|
    | **资源名称** | 全局唯一名称 | 输入用于应用配置存储区资源的唯一资源名称。 该名称必须是包含 1 到 63 个字符的字符串，只能包含数字、字母和 `-` 字符。 该名称的开头或末尾不能是 `-` 字符，并且连续的 `-` 字符无效。  |
    | **订阅** | 订阅 | 选择要用来测试应用配置的 Azure 订阅。 如果帐户只有一个订阅，则会自动选择该订阅并且不显示“订阅”下拉菜单。 |
    | **资源组** | AppConfigTestResources | 为应用配置存储区资源选择或创建资源组。 此组可用于组织多个资源，删除该资源组可以同时删除这些资源。 有关详细信息，请参阅[使用资源组管理 Azure 资源](/azure/azure-resource-manager/resource-group-overview)。 |
    | **位置** | *美国中部* | 使用“位置”指定在其中托管应用配置存储区的地理位置。 为获得最佳性能，请在应用程序的其他组件所在的同一区域创建资源。 |

    ![创建应用配置存储区资源](../articles/azure-app-configuration/media/quickstarts/azure-app-configuration-create.png)

4. 选择“创建”。 部署可能需要几分钟时间才能完成。

5. 部署完成后，选择“设置” > “访问密钥”。 记下只读主键或读写主键连接字符串。 稍后将使用此连接字符串来配置应用程序，以与创建的应用程序配置存储区进行通信。

6. 选择“键/值资源管理器” > “+创建”来添加以下键值对：

    | 密钥 | 值 |
    |---|---|
    | TestApp:Settings:BackgroundColor | 白色 |
    | TestApp:Settings:FontSize | 24 |
    | TestApp:Settings:FontColor | 黑色 |
    | TestApp:Settings:Message | Azure 应用配置的数据 |

    暂时将“标签”和“内容类型”保留为空。
