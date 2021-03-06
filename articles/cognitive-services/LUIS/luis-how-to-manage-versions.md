---
title: 管理版本
titleSuffix: Language Understanding - Azure Cognitive Services
description: 版本允许你构建和发布不同的模型。 较好的做法是在对模型进行更改之前将当前的活动模型复制到一个不同的应用版本。
services: cognitive-services
author: diberry
manager: nitinme
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: article
ms.date: 04/16/2019
ms.author: diberry
ms.openlocfilehash: f919651cf39d1f2c48fca87da935e49e3affa79f
ms.sourcegitcommit: c3d1aa5a1d922c172654b50a6a5c8b2a6c71aa91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59678524"
---
# <a name="use-versions-to-edit-and-test-without-impacting-staging-or-production-apps"></a>使用版本进行编辑和测试，而不会影响暂存应用或生产应用

版本允许你构建和发布不同的模型。 较好的做法是在对模型进行更改之前将当前的活动模型复制到一个不同的应用[版本](luis-concept-version.md)。 

若要处理版本，请在“我的应用”页面上通过选择你的应用名称来将其打开，在顶栏中选择“管理”，然后在左侧导航栏中选择“版本”。 

版本的列表显示了已发布的版本，其中发布，以及哪一个版本是当前处于活动状态。 

[![“管理”部分的“版本”页](./media/luis-how-to-manage-versions/versions-import.png "“管理”部分的“版本”页")](./media/luis-how-to-manage-versions/versions-import.png#lightbox)

## <a name="clone-a-version"></a>克隆版本

1. 选择要克隆的版本，然后从工具栏中选择“克隆”。 

2. 在“克隆版本”对话框中，键入新版本的名称，如“0.2”。

   ![“克隆版本”对话框](./media/luis-how-to-manage-versions/version-clone-version-dialog.png)
 
     > [!NOTE]
     > 版本 ID 可以仅包含字符、数字或“.”，长度不得超过 10 个字符。
 
   此时，指定名称的新版本已创建，且设置为活动版本。

## <a name="set-active-version"></a>设置活动版本

从列表中选择一个版本，然后从工具栏中选择“激活”。 

[![在“管理”部分的“版本”页，执行版本操作](./media/luis-how-to-manage-versions/versions-other.png "在“管理”部分的“版本”页，执行版本操作")](./media/luis-how-to-manage-versions/versions-other.png#lightbox)

## <a name="import-version"></a>导入版本

1. 从工具栏中选择“导入版本”。 

2. 在“导入新版本”弹出窗口中，输入新的由十个字符构成的版本名称。 仅当应用中已有 JSON 文件中的版本时，才需要设置版本 ID。

    ![在“管理”部分的“版本”页，导入新版本](./media/luis-how-to-manage-versions/versions-import-pop-up.png)

    导入后，新版本就会成为活动版本。

### <a name="import-errors"></a>导入错误

* 标记器错误：如果收到**标记器错误**导入时，你尝试导入使用不同的版本[标记器](luis-language-support.md#custom-tokenizer-versions)不是应用程序当前使用。 若要解决此问题，请参阅[标记器版本之间迁移](luis-language-support.md#migrating-between-tokenizer-versions)。

<a name = "export-version"></a>

## <a name="other-actions"></a>其他操作

* 若要**删除**某个版本，请从列表中选择一个版本，然后从工具栏中选择“删除”。 选择“确定”。 
* 若要**重命名**某个版本，请从列表中选择一个版本，然后从工具栏中选择“重命名”。 输入新名称并选择“完成”。 
* 若要**导出**某个版本，请从列表中选择一个版本，然后从工具栏中选择“导出应用”。 选择要导出的备份中，选择 JSON**导出的容器**到[使用 LUIS 容器中的此应用](luis-container-howto.md)。  

