---
title: 会议实例实体属性 - 学术知识 API
titlesuffix: Azure Cognitive Services
description: 了解可以在学术知识 API 中与会议实例实体结合使用的属性。
services: cognitive-services
author: alch-msft
manager: nitinme
ms.service: cognitive-services
ms.subservice: academic-knowledge
ms.topic: conceptual
ms.date: 03/23/2017
ms.author: alch
ms.openlocfilehash: 183a307159adb5dfdb248eb0cf4862462a626db6
ms.sourcegitcommit: 90cec6cccf303ad4767a343ce00befba020a10f6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/07/2019
ms.locfileid: "55879184"
---
# <a name="conference-instance-entity"></a>会议实例实体

<sub> *以下属性特定于会议实例实体。(Ty = '4') </sub>

Name    |说明                            |Type       | 操作
------- | ------------------------------------- | --------- | ----------------------------
ID      |实体 ID                              |Int64      |等于
CIN     |会议实例规范化名称 ({ConferenceSeriesNormalizedName} {ConferenceInstanceYear})        |String     |等于
DCN     |会议实例显示名称 ({ConferenceSeriesName} : {ConferenceInstanceYear})       |String     |无
CIL     |会议实例的位置    |String     |Equals、<br/>-StartsWith
CISD    |会议实例的开始日期  |日期       |Equals、<br/>IsBetween
CIED    |会议实例的结束日期    |日期       |Equals、<br/>IsBetween
CIARD   |会议实例的摘要注册截止日期  |日期       |Equals、<br/>IsBetween
CISDD   |会议实例的提交截止日期     |日期       |Equals、<br/>IsBetween
CIFVD   |会议实例的最终版本截止日期  |日期       |Equals、<br/>IsBetween
CINDD   |会议实例的通知日期   |日期       |Equals、<br/>IsBetween
CD.T    |会议实例事件的标题   |日期       |Equals、<br/>IsBetween
CD.D    |会议实例事件的日期    |日期       |Equals、<br/>IsBetween
PCS.CN  |实例的会议系列名称 |String     |等于
PCS.CId |实例的会议系列 ID |Int64    |等于
CC      |会议实例引文总计数           |Int32      |无  
ECC     |会议实例估计引文总计数 |Int32      |无


## <a name="extended-metadata-attributes"></a>扩展的元数据属性 ##

Name    | 说明               
--------|---------------------------    
FN      | 会议实例全名
