---
title: 欧洲客户标识数据存储 - Azure Active Directory | Microsoft Docs
description: 了解 MAzure Active Directory 在哪个位置存储其欧洲客户的标识相关数据。
services: active-directory
author: eross-msft
manager: daveba
ms.author: lizross
ms.service: active-directory
ms.subservice: fundamentals
ms.workload: identity
ms.topic: conceptual
ms.date: 03/04/2019
ms.custom: it-pro, seodec18
ms.collection: M365-identity-device-management
ms.openlocfilehash: b21f82dc0a1eb8edf571da13e0d34fecae5f401b
ms.sourcegitcommit: 8b41b86841456deea26b0941e8ae3fcdb2d5c1e1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57337679"
---
# <a name="identity-data-storage-for-european-customers-in-azure-active-directory"></a>Azure Active Directory 中的欧洲客户标识数据存储
Azure Active Directory (Azure AD) 可帮助管理用户标识，并创建智能化的访问策略用于帮助保护组织的资源。 标识数据的存储位置基于订阅服务时（例如，订阅 Office 365 或 Azure 时） 组织提供的地址。 有关标识数据存储位置的具体信息，请参阅 Microsoft 信任中心的[数据存储在何处？](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located)部分。

虽然大多数 Azure AD 相关欧洲标识数据将保留在欧洲数据中心中，有一些运营、 特定于服务的数据所需的常规 Azure AD 操作，这在美国存储和不包含任何个人数据。

## <a name="data-stored-outside-of-european-datacenters-for-european-customers"></a>存储在欧洲数据中心外部的欧洲客户数据

营业地址位于欧洲的组织的大部分 Azure AD 相关欧洲标识数据都会保留在欧洲数据中心。 存储在欧洲数据中心并复制到美国数据中心的 Azure AD 数据包括：

- **Microsoft Azure 多重身份验证 (MFA) 和 Azure AD 自助密码重置 (SSPR)**
    
    MFA 在欧洲数据中心存储所有用户静态数据。 但是，某些特定于 MFA 服务的数据存储在美国，包括：
    
    - 如果使用 MFA 或 SSPR，双重身份验证及其相关个人数据可能会存储在美国。

        - 使用电话呼叫或短信的所有双重身份验证可能由美国的运营商完成。
    
        - 使用 Microsoft Authenticator 应用的推送通知需要从制造商的通知服务（Apple 或 Google）发送的通知，此过程可能在欧洲外部完成。
    
        - OATH 代码始终在美国验证。 
    
    - 某些 MFA 和 SSPR 日志在美国存储 30 天，不管身份验证类型是什么。

- **Microsoft Azure Active Directory B2C (Azure AD B2C)**

    Azure AD B2C 在欧洲数据中心存储所有用户静态数据。 但是，操作日志（已删除个人数据）会保留在用户访问服务时所在的位置。 例如，如果某个 B2C 用户访问位于美国的服务，则操作日志会保留在美国。此外，不包含个人数据的所有策略配置数据只会存储在美国。有关策略配置的详细信息，请参阅 [Azure Active Directory B2C：内置策略](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-reference-policies)一文。

- **Microsoft Azure Active Directory B2B (Azure AD B2B)** 
    
    Azure AD B2B 在欧洲数据中心存储所有用户静态数据。 但是，B2B 将表格中的非个人元数据存储在美国数据中心。 此表格包含 redeemUrl、invitationTicket、资源租户 ID、InviteRedirectUrl 和 InviterAppId 等字段。

- **Microsoft Azure Active Directory 域服务 (Azure AD DS)**

    Azure AD DS 将用户数据存储在客户选择的 Azure 虚拟网络所在的同一位置。 因此，如果该网络位于欧洲外部，则会复制数据并将其存储在欧洲外部。

- **与 Azure AD 集成的服务和应用**

    与 Azure AD 集成的任何服务和应用都有权访问标识数据。 请评估每个服务和应用，以确定该特定服务和应用如何处理标识数据，以及它们是否满足公司的数据存储要求。

    有关 Microsoft 服务的数据存放的详细信息，请参阅 Microsoft 信任中心的[数据存储在何处？](https://www.microsoft.com/trustcenter/privacy/where-your-data-is-located)部分。

## <a name="next-steps"></a>后续步骤
有关上述任何功能的详细信息，请参阅以下文章：
- [什么是多重身份验证？](https://docs.microsoft.com/azure/active-directory/authentication/multi-factor-authentication)

- [Azure AD 自助密码重置](https://docs.microsoft.com/azure/active-directory/authentication/active-directory-passwords-overview)

- [什么是 Azure Active Directory B2C？](https://docs.microsoft.com/azure/active-directory-b2c/active-directory-b2c-overview)

- [什么是 Azure AD B2B 协作？](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b)

- [Azure Active Directory (AD) 域服务](https://docs.microsoft.com/azure/active-directory-domain-services/active-directory-ds-overview)
