---
title: 登录到 Azure Notebooks
description: 快速登录到 Azure Notebooks 并设置用户 ID，这使你能够访问已保存的项目并与他人共享笔记本。
services: app-service
documentationcenter: ''
author: kraigb
manager: douge
ms.assetid: fb8c94b1-6d0a-4b77-8d14-ae6efcdd99f4
ms.service: azure-notebooks
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/15/2019
ms.author: kraigb
ms.openlocfilehash: eb8ba7f23de99d333693430d806a8d887c55a678
ms.sourcegitcommit: 5f348bf7d6cf8e074576c73055e17d7036982ddb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2019
ms.locfileid: "59608150"
---
# <a name="quickstart-sign-in-and-set-a-user-id"></a>快速入门：登录并设置用户 ID

虽然始终都可以在未登录的情况下查看 Azure Notebooks，但必须登录才能运行笔记本、访问保存的项目和笔记本以及与他人共享笔记本。

## <a name="sign-in"></a>登录

1. 选择 [notebooks.azure.com](https://notebooks.azure.com/) 右上角的“登录”。

    ![Azure Notebooks 上“登录”命令的位置](media/accounts/sign-in-command.png)

1. 出现提示时，输入 Microsoft 帐户或者工作或学校帐户的电子邮件地址，并选择“下一步”。 [Azure Notebooks 的用户帐户](azure-notebooks-user-account.md)一文介绍了帐户类型。 如果你没有 Microsoft 帐户，或想要创建一个专门用于 Azure Notebooks 的帐户，请选择“创建一个”：

    ![登录提示中的新建 Microsoft 帐户命令](media/accounts/create-new-microsoft-account.png)

    > [!Tip]
    > 如果尝试使用已有与之关联的帐户的电子邮件地址创建新帐户，可能会看到消息"不能在此处注册使用工作或学校电子邮件地址。 使用个人电子邮件，如 Gmail 或 yahoo ！，或获取新的 Outlook 电子邮件。" 在这种情况下，请尝试使用工作电子邮件地址登录而无需创建一个新的帐户。

1. 根据提示输入密码。

1. 如果是首次登录，Azure Notebooks 会请求访问你帐户的权限。 选择“是”继续：

    ![帐户权限提示](media/accounts/account-permission-prompt.png)

## <a name="set-a-user-id"></a>设置用户 ID

1. 首次登录时，系统会向你分配一个临时用户 ID，例如“anon-idrca3”。 只要用户 ID 以“anon-”开头，Azure Notebooks 都会提示你创建一个自己的 ID。 用户 ID 会用于你获取的任何 URL 中，用于共享项目和笔记本，所以选择使用对你而言独特且有意义的 ID 吧。

    ![输入 Azure Notebooks 用户 ID 的提示](media/accounts/create-user-id.png)

    如果选择“不，谢谢”，Azure Notebooks 会继续在每次登录时提示你输入用户 ID。 还可以在[用户个人资料](azure-notebooks-user-profile.md)中随时设置用户 ID。

1. 成功登录后，Azure Notebooks 导航到你的公用个人资料页面，你可以在此页上选择“编辑个人资料信息”填写你的其余信息（有关详细信息，请参阅[你的个人资料和用户 ID](azure-notebooks-user-profile.md)）：

    ![Azure Notebooks 个人资料页的初始视图](media/accounts/profile-page-new.png)

> [!NOTE]
> 如果看到消息"用户 ID 已在使用中，"请尝试不同的 id。 用户 Id 是唯一的所有 Azure Notebooks 帐户，以及 Azure 笔记本也会保留某些用户 Id，例如 Microsoft 品牌名称。

## <a name="sign-out"></a>注销

若要注销，请选择页面右上方的用户名，然后选择“注销”：

![Azure Notebooks 上“注销”命令的位置](media/accounts/sign-out-command.png)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [快速入门：创建和共享笔记本](quickstart-create-share-jupyter-notebook.md)
