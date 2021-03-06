---
title: 限制
titleSuffix: Language Understanding - Azure Cognitive Services
description: 本文介绍 Azure 认知服务语言理解 (LUIS) 的已知限制。 LUIS 具有多个边界区域。 模型边界可控制 LUIS 中的意向、实体和功能。 基于密钥类型的配额限制。 键盘组合可控制 LUIS 网站。
services: cognitive-services
author: diberry
manager: nitinme
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: article
ms.date: 03/12/2019
ms.author: diberry
ms.custom: seodec18
ms.openlocfilehash: 51f5355e365d0dcf7a103deab3356f015e75641e
ms.sourcegitcommit: 5839af386c5a2ad46aaaeb90a13065ef94e61e74
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "57897499"
---
# <a name="boundaries-for-your-luis-model-and-keys"></a>LUIS 模型和密钥的边界
LUIS 具有多个边界区域。 第一个是[模型边界](#model-boundaries)，它可控制 LUIS 中的意向、实体和功能。 第二个是基于密钥类型的[配额限制](#key-limits)。 边界的第三个区域是用于控制 LUIS 网站的[键盘组合](#keyboard-controls)。 第四个是 LUIS 创作网站和 LUIS [终结点](luis-glossary.md#endpoint) API 之间的[世界区域映射](luis-reference-regions.md)。 


## <a name="model-boundaries"></a>模型边界

如果应用超出 LUIS 模型限制和边界，请考虑使用 [LUIS 调度](luis-concept-enterprise.md#dispatch-tool-and-model)应用或使用 [LUIS 容器](luis-container-howto.md)。 

|区域|限制|
|--|:--|
| [应用名称][luis-get-started-create-app] | *默认最大字符长度 |
| [批处理测试][batch-testing]| 10 个数据集，每个数据集 1000 条话语|
| 显式列表 | 每个应用程序 50 个实体|
| [意向][intents]|每个应用程序 500 个意向：499 个自定义意向，以及必需的“无”意向。<br>[基于调度](https://aka.ms/dispatch-tool)的应用程序具有相应的 500 个调度源。|
| [列表实体](./luis-concept-entity-types.md) | 父级：50 个，子级：20,000 项。 规范名称是 *默认最大字符长度。同义词值没有长度限制。 |
| [机器学习实体](./luis-concept-entity-types.md)：<br> 复合、<br>  分层实体<br> 简单|限制为 100 个父实体（不包括分层子实体）或 330 个实体（包括分层子实体），以用户先达到的限制为准。<br><br>具有层次结构的示例是 30 个层次结构，每个层次结构具有 10 个子级。  子级将总共占用 300 个，而层次结构元素将占用剩余的 30 个。 |
| [模式](luis-concept-patterns.md)|每个应用程序 500 个模式。<br>模式的最大长度为 400 个字符。<br>每个模式 3 个 Pattern.any 实体<br>模式中最多 2 个嵌套可选文本|
| [Pattern.any](./luis-concept-entity-types.md)|每个应用程序 100 个，每个模式 3 个 pattern.any 实体 |
| [短语列表][phrase-list]|10 个短语列表，每个列表 5,000 项|
| [预生成实体](./luis-prebuilt-entities.md) | 无限制|
| [正则表达式实体](./luis-concept-entity-types.md)|20 个实体<br>每个正则表达式实体模式 最多 500 个字符|
| [角色](luis-concept-roles.md)|每个应用程序 300 个角色。 每个实体 10 个角色|
| [单条话语][utterances] | 500 个字符|
| [话语][utterances] | 15,000 每个应用程序-为每个意向的语音样本的数量没有限制|
| [版本](luis-concept-version.md)| 无限制 |
| [版本名称][luis-how-to-manage-versions] | 10 个字符，仅限字母数字和句点 (.) |

*默认最大字符长度为 50 个字符。 

## <a name="intent-and-entity-naming"></a>意向和实体命名
意向和实体名称中不要使用以下字符：

|Character|名称|
|--|--|
|`{`|左大括号|
|`}`|右大括号|
|`[`|左中括号|
|`]`|右中括号|
|`\`|反斜杠|

## <a name="key-usage"></a>密钥使用情况

语言理解拥有单独的密钥，一类用于创作，另一类用于查询预测终结点。 若要详细了解密钥类型之间的差异，请参阅 [LUIS 中的创作密钥和查询预测终结点密钥](luis-concept-keys.md)。

## <a name="key-limits"></a>密钥限制

创作密钥对于创作和终结点有不同的限制。 LUIS 服务终结点密钥仅对终结点查询有效。


|密钥|创作|终结点|目的|
|--|--|--|--|
|语言理解创作/入门|1 百万/月，5/秒|1 千/月，5/秒|创作 LUIS 应用|
|语言理解[订阅][pricing] - F0 - 免费层 |无效|1 万/月，5/秒|查询 LUIS 终结点|
|语言理解[订阅][pricing] - S0 - 基本层|无效|50/秒|查询 LUIS 终结点|
|认知服务[订阅][ pricing] - S0 - 标准层|无效|50/秒|查询 LUIS 终结点|
|[情绪分析集成](luis-how-to-publish-app.md#enable-sentiment-analysis)|无效|免费|添加情绪信息，包括关键短语数据提取 |
|语音集成|无效|5.50 美元/1 千终结点请求|将口语话语转为文本话语并返回 LUIS 结果|

## <a name="keyboard-controls"></a>键盘控件

|键盘输入 | 描述 | 
|--|--|
|Control+E|切换话语列表中的令牌和实体|

## <a name="website-sign-in-time-period"></a>网站登录时间段

登录访问权限为 60 分钟。 在此时间段后，会出现此错误。 需重新登录。

[luis-get-started-create-app]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-get-started-create-app
[batch-testing]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-test#batch-testing
[intents]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-intent
[phrase-list]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-feature
[utterances]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-concept-utterance
[luis-how-to-manage-versions]: https://docs.microsoft.com/azure/cognitive-services/luis/luis-how-to-manage-versions
[pricing]: https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/
<!-- TBD: fix this link -->
[speech-to-intent-pricing]: https://azure.microsoft.com/pricing/details/cognitive-services/language-understanding-intelligent-services/
