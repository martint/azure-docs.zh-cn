---
title: 常见问题解答 - 内容审查器
titlesuffix: Azure Cognitive Services
description: 获取内容审查器常见问题解答。
services: cognitive-services
author: sanjeev3
manager: nitinme
ms.service: cognitive-services
ms.subservice: content-moderator
ms.topic: conceptual
ms.date: 03/21/2019
ms.author: sajagtap
ms.openlocfilehash: df8d957fc2de620d63567a9cc1b14b24b73052bb
ms.sourcegitcommit: 87bd7bf35c469f84d6ca6599ac3f5ea5545159c9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2019
ms.locfileid: "58351127"
---
# <a name="frequently-asked-questions-faq"></a>常见问题 (FAQ)

### <a name="what-does-my-content-moderator-subscription-include"></a>我的内容审查器订阅包括哪些内容？

内容审查器订阅包括访问评审工具和 Api。 可以决定是要使用其中一种，还是两种都要使用，具体视业务需求而定。

### <a name="what-are-the-limitsrestrictions-of-the-content-that-can-be-moderated-by-using-the-api"></a>可使用 API 审查的内容有什么限制？

使用 API 时，图像至少必须为 128 像素，且文件大小不得超过 4MB。 文本长度不得超过 1024 个字符。 视频时长没有限制。

### <a name="what-happens-if-the-content-passed-to-the-text-api-or-the-image-api-exceeds-the-size-limits"></a>如果传递到文本 API 或图像 API 的内容超过大小限制，会发生什么？

文本 API 会返回错误代码，指明文本超过长度上限。 图像 API 也会返回错误代码，指明图像不符合大小要求。

#### <a name="do-you-keep-the-images-text-or-videos-that-are-submitted-for-moderation"></a>Microsoft 是否保留已提交审查的图像、文本或视频？

内容是你自己的。未经你同意，Microsoft 不得保留任何内容。 Microsoft 使用业界领先的安全措施来帮助保护你的内容。

### <a name="can-i-use-content-moderator-to-screen-for-illegal-child-exploitation-images"></a>我能否使用内容审查器筛查非法儿童剥削图像？

不是。 不过，合格组织可以使用 [PhotoDNA 云服务](https://www.microsoft.com/photodna "Microsoft PhotoDNA 云服务")筛查此类内容。

### <a name="how-many-review-teams-can-a-user-join-can-the-user-switch-between-teams"></a>多少查看团队可以用户联接？ 用户能否切换团队？

用户一次只能加入一个团队。

### <a name="what-kind-of-team-member-roles-are-supported-by-the-review-tool-how-are-they-different"></a>审阅工具支持哪种团队成员角色？ 那么其不同之处在哪里？

审阅工具目前允许分配管理员和审阅者角色。 管理员可以邀请其他用户，并有权访问配置设置，而审阅者只能审阅审查结果，以及标记或取消标记内容。

### <a name="what-is-a-tag-does-the-review-tool-support-custom-tags"></a>什么是标记？ “审阅”工具是否支持自定义标记？

标记的挑逗性等是一个或两个字母短代码表示审查标志，如 a 的成人，r。 管理员可以根据需要为业务定义新标记。

### <a name="how-many-team-members-can-i-have-in-my-review-team"></a>我的审阅团队可以有多少名团队成员？

您可以最多 5 名团队成员，包括管理员，在团队中。
