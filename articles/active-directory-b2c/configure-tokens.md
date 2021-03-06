---
title: 配置令牌-Azure Active Directory B2C |Microsoft Docs
description: 了解如何在 Azure Active Directory B2C 中配置令牌生存期和兼容性设置。
services: active-directory-b2c
author: davidmu1
manager: daveba
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 04/16/2019
ms.author: davidmu
ms.subservice: B2C
ms.openlocfilehash: 2455b8c12ed042af3a06a158a4e5c60a0aee748b
ms.sourcegitcommit: c3d1aa5a1d922c172654b50a6a5c8b2a6c71aa91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2019
ms.locfileid: "59685729"
---
# <a name="configure-tokens-in-azure-active-directory-b2c"></a>配置 Azure Active Directory B2C 中的令牌

在本文中，您将学习如何配置[生存期和令牌的兼容性](active-directory-b2c-reference-tokens.md)Azure Active Directory (Azure AD) B2C 中。

## <a name="prerequisites"></a>必备组件

[创建用户流](tutorial-create-user-flows.md)，以便用户能够注册并登录应用程序。

## <a name="configure-token-lifetime"></a>配置令牌生存期

可以在任何用户流上配置令牌生存期。

1. 登录到 [Azure 门户](https://portal.azure.com)。
2. 请确保使用包含 Azure AD B2C 租户的目录。 选择**目录和订阅筛选器**顶部菜单中选择包含你的 Azure AD B2C 租户的目录。
3. 选择 Azure 门户左上角的“所有服务”，然后搜索并选择“Azure AD B2C”。
4. 选择**用户流 （策略）**。
5. 打开之前创建的用户流。 
6. 选择“属性”。
7. 下**令牌生存期**，调整以满足你的应用程序需要的以下属性：

    ![配置令牌生存期](./media/configure-tokens/token-lifetime.png)

8. 单击“ **保存**”。

## <a name="configure-token-compatibility"></a>配置令牌兼容性

1. 选择**用户流 （策略）**。
2. 打开之前创建的用户流。 
3. 选择“属性”。
4. 下**令牌兼容性设置**，调整以满足你的应用程序需要的以下属性：

    ![配置令牌兼容性](./media/configure-tokens/token-compatibility.png)

5. 单击“ **保存**”。

## <a name="next-steps"></a>后续步骤

详细了解如何[使用访问令牌](active-directory-b2c-access-tokens.md)。



