---
title: 教程 - 创建 Azure Active Directory B2C 租户 | Microsoft Docs
description: 了解如何通过使用 Azure 门户创建 Azure Active Directory B2C 租户来准备注册应用程序。
services: B2C
author: davidmu1
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 01/11/2019
ms.author: davidmu
ms.subservice: B2C
ms.openlocfilehash: b8878eccb079bf78c45ff9c1e4040659d109b1ab
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/29/2019
ms.locfileid: "55152920"
---
# <a name="tutorial-create-an-azure-active-directory-b2c-tenant"></a>教程：创建 Azure Active Directory B2C 租户

必须在你管理的租户中注册应用程序，然后这些应用程序才能与 Azure Active Directory (Azure AD) B2C 交互。

在本文中，学习如何：

> [!div class="checklist"]
> * 创建 Azure AD B2C 租户
> * 将租户链接到订阅

在下一个教程中，学习如何注册应用程序。

如果没有 Azure 订阅，请在开始之前创建一个[免费帐户](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。

## <a name="create-an-azure-ad-b2c-tenant"></a>创建 Azure AD B2C 租户

1. 登录到 [Azure 门户](https://portal.azure.com/)。
2. 请确保使用包含订阅的目录，方法是单击顶部菜单中的“目录和订阅筛选器”，然后选择包含订阅的目录。 此目录不同于将包含 Azure AD B2C 租户的其他目录。

    ![切换到订阅目录](./media/tutorial-create-tenant/switch-directory-subscription.png)

3. 在 Azure 门户的左上角，选择“创建资源”。
4. 搜索并选择“Active Directory B2C”，然后单击“创建”。
5. 选择“新建 Azure AD B2C 租户”，输入租户名称中使用的组织名称和初始域名，选择国家/地区（以后不能更改），然后单击“创建”。

    ![创建租户](./media/tutorial-create-tenant/create-tenant.png)

    在此示例中，租户名是 contoso0926Tenant.onmicrosoft.com

6. 在“创建新的 B2C 租户或链接到现有租户”页上，选择“将现有 Azure AD B2C 租户链接到 Azure 订阅”，依次选择已创建的租户和订阅，然后单击“新建”。
7. 输入将包含该租户的资源组名，选择位置，然后单击“创建”。
8. 若要开始使用新租户，请确保使用包含 Azure AD B2C 租户的目录，方法是单击顶部菜单中的“目录和订阅筛选器”，然后选择包含租户的目录。

    ![切换到租户目录](./media/tutorial-create-tenant/switch-directories.png)

## <a name="next-steps"></a>后续步骤

本文介绍了如何执行以下操作：

> [!div class="checklist"]
> * 创建 Azure AD B2C 租户
> * 将租户链接到订阅

> [!div class="nextstepaction"]
> [注册应用程序](tutorial-register-applications.md)
