---
title: 什么是访问评审？ - Azure Active Directory | Microsoft Docs
description: 使用 Azure Active Directory 访问评审，可以控制组成员资格和应用程序访问权限，以满足监管、 风险管理和组织中的符合性方案。
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.subservice: compliance
ms.date: 01/18/2019
ms.author: rolyon
ms.reviewer: mwahl
ms.collection: M365-identity-device-management
ms.openlocfilehash: 1563a023f397999deb5c6abd40843d6a376b0492
ms.sourcegitcommit: c63fe69fd624752d04661f56d52ad9d8693e9d56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2019
ms.locfileid: "58576116"
---
# <a name="what-are-azure-ad-access-reviews"></a>什么是 Azure AD 访问评审？

Azure Active Directory (Azure AD) 访问评审可以使组织能够有效地管理组成员身份、 对企业应用程序和角色分配访问权限。 可以定期评审用户的访问权限，确保相应人员持续拥有访问权限。

下面的视频简要介绍了访问评审：

>[!VIDEO https://www.youtube.com/embed/kDRjQQ22Wkk]

## <a name="why-are-access-reviews-important"></a>访问评审为何重要？

Azure AD 支持在组织内进行内部协作和与外部组织的用户（例如合作伙伴）进行协作。 用户可以加入组、邀请来宾、连接到云应用以及通过工作或个人设备远程工作。 自助服务的便捷性使人们需要更好的访问管理功能。

- 新员工加入时，如何确保他们获得有助于提高工作效率的相应访问权限？
- 当员工在团队间调动或离开公司时，如何确保删除旧的访问权限，尤其是在涉及来宾时？
- 访问权限过多可能影响审计结果，导致利益受损，因为此类情况表示对访问权限缺乏控制。
- 需要主动与资源所有者联系，确保他们定期评审有权访问其资源的用户。

## <a name="when-to-use-access-reviews"></a>何时使用访问评审？

- **特权角色用户过多：** 它是一个好办法检查多少用户具有管理访问权限，其中的多少一些全球管理员，并且如果有任何受邀来宾或分配来执行管理任务后尚未删除的合作伙伴。 可以再次验证中的角色分配用户[Azure AD 角色](../privileged-identity-management/pim-how-to-perform-security-review.md?toc=%2fazure%2factive-directory%2fgovernance%2ftoc.json)如全局管理员或[Azure 资源角色](../privileged-identity-management/pim-resource-roles-perform-access-review.md?toc=%2fazure%2factive-directory%2fgovernance%2ftoc.json)如用户访问管理员在[Azure AD 特权Identity Management (PIM)](../privileged-identity-management/pim-configure.md)体验。
- **自动化不可行：** 可针对安全组或 Office 365 组中的动态成员资格创建规则，但如果人力资源数据不在 Azure AD 中或者如果用户在离开组后仍需访问权限来培训其接任者应该怎么办？ 对于此类情况，可以对该组创建评审，确保仍需访问权限的用户能够继续获得访问权限。
- **将组用于新用途：** 如果要将组同步到 Azure AD，或计划为所有销售团队组成员启用 Salesforce 应用程序，则要求组所有者在将组用于其他风险内容前评审组成员资格会非常有用。
- **业务关键数据访问权限：** 对于特定资源，可能出于审核目的要求 IT 以外的人员定期注销并提供需要访问权限的正当理由。
- **要维护策略的例外列表：** 在理想情况下，所有用户都会遵循访问策略来保护对组织资源的访问。 但是，有时，某些业务案例要求例外处理。 IT 管理员可以管理此任务、避免忽视策略例外情况，为审核员提供定期评审这些例外情况的证明。
- **要求组所有者确认他们在组中是否仍需要来宾：** 员工的访问权限可能会使用一些本地 IAM，但不是受邀来宾自动执行。 如果组为来宾授予了业务敏感内容的访问权限，则由组所有者负责确认来宾是否仍有对访问权限的合法业务需求。
- **定期重复评审：** 可以设置按设定频率（例如每周、每月、每季度或每年）定期对用户进行访问评审，审阅者将在每次评审开始前收到通知。 审阅者可以借助友好界面和智能建议的帮助，批准或拒绝访问权限。

## <a name="where-do-you-create-reviews"></a>在哪里创建评审？

根据要查看，您将创建访问评审在 Azure AD 访问评审、 （处于预览状态），Azure AD 企业应用或 Azure AD PIM。

| 用户访问权限 | 审阅者身份 | 评审创建位置 | 审阅者体验 |
| --- | --- | --- | --- |
| 安全组成员</br>Office 组成员 | 指定的审阅者</br>组所有者</br>自我评审 | Azure AD 访问评审</br>Azure AD 组 | 访问面板 |
| 分配联网应用 | 指定的审阅者</br>自我评审 | Azure AD 访问评审</br>Azure AD 企业应用（预览版） | 访问面板 |
| Azure AD 角色 | 指定的审阅者</br>自我评审 | Azure AD PIM | Azure 门户 |
| Azure 资源角色 | 指定的审阅者</br>自我评审 | Azure AD PIM | Azure 门户 |

## <a name="prerequisites"></a>必备组件

若要使用访问评审，必须具有以下许可证之一：

- Azure AD Premium P2
- 企业移动性 + 安全性 (EMS) E5 许可证

有关更多信息，请参阅[如何：注册 Azure Active Directory Premium](../fundamentals/active-directory-get-started-premium.md) 或[企业移动性 + 安全性 E5 试用版](https://aka.ms/emse5trial)。

## <a name="get-started-with-access-reviews"></a>访问评审入门

若要了解有关创建和执行访问评审的详细信息，请观看此简短演示：

>[!VIDEO https://www.youtube.com/embed/6KB3TZ8Wi40]

如果已准备好在组织中部署访问评审，请按照视频中的这些步骤来载入访问评审、培训管理员以及创建第一个访问评审！

>[!VIDEO https://www.youtube.com/embed/X1SL2uubx9M]

## <a name="enable-access-reviews"></a>启用访问评审

若要启用访问评审，请执行以下步骤。

1. 作为全局管理员或用户管理员，登录到[Azure 门户](https://portal.azure.com)你想要使用访问评审。

1. 单击“所有服务”并查找访问评审服务。

1. 单击**访问评审**。

    ![所有服务的访问评审](./media/access-reviews-overview/all-services-access-reviews.png)

1. 在导航列表中，单击“载入”，打开“载入访问评审”页。

    ![载入访问评审](./media/access-reviews-overview/onboard-button.png)

1. 单击“创建”，以在当前目录中启用访问评审。

    ![载入访问评审](./media/access-reviews-overview/onboard-access-reviews.png)

    下次启动访问评审，将启用访问权限审查选项。

    ![已启用的访问评审](./media/access-reviews-overview/access-reviews-enabled.png)

## <a name="next-steps"></a>后续步骤

- [创建组或应用程序的访问评审](create-access-review.md)
- [针对充当 Azure AD 管理角色的用户创建访问评审](../privileged-identity-management/pim-how-to-start-security-review.md?toc=%2fazure%2factive-directory%2fgovernance%2ftoc.json)
- [评审访问权限给组或应用程序](perform-access-review.md)
- [完成访问评审的组或应用程序](complete-access-review.md)
