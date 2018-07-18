---
title: 教程：Azure Active Directory 与 BenSelect 集成 | Microsoft Docs
description: 了解如何在 Azure Active Directory 和 BenSelect 之间配置单一登录。
services: active-directory
documentationCenter: na
author: jeevansd
manager: mtillman
ms.assetid: ffa17478-3ea1-4356-a289-545b5b9a4494
ms.service: active-directory
ms.component: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: jeedes
ms.openlocfilehash: 5884978895d8cfe72c35a3879a2575d1b58077c7
ms.sourcegitcommit: 16ddc345abd6e10a7a3714f12780958f60d339b6
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36216878"
---
# <a name="tutorial-azure-active-directory-integration-with-benselect"></a>教程：Azure Active Directory 与 BenSelect 集成

在本教程中，了解如何将 BenSelect 与 Azure Active Directory (Azure AD) 集成。

将 BenSelect 与 Azure AD 集成提供以下优势：

- 可在 Azure AD 中控制谁有权访问 BenSelect
- 可使用户通过其 Azure AD 帐户自动登录 BenSelect（单一登录）
- 可以在一个中心位置（即 Azure 门户）管理帐户

如需了解有关 SaaS 应用与 Azure AD 集成的详细信息，请参阅 [Azure Active Directory 的应用程序访问与单一登录是什么](../manage-apps/what-is-single-sign-on.md)。

## <a name="prerequisites"></a>先决条件

若要配置 Azure AD 与 BenSelect 的集成，需要以下项目：

- Azure AD 订阅
- 已启用 BenSelect 单一登录的订阅

> [!NOTE]
> 为了测试本教程中的步骤，我们不建议使用生产环境。

测试本教程中的步骤应遵循以下建议：

- 除非必要，请勿使用生产环境。
- 如果没有 Azure AD 试用环境，可以在[此处](https://azure.microsoft.com/pricing/free-trial/)获取一个月的试用版。

## <a name="scenario-description"></a>方案描述
在本教程中，将在测试环境中测试 Azure AD 单一登录。 本教程中概述的方案包括两个主要构建基块：

1. 从库中添加 BenSelect
2. 配置和测试 Azure AD 单一登录

## <a name="adding-benselect-from-the-gallery"></a>从库中添加 BenSelect
要配置 BenSelect 与 Azure AD 的集成，需要将库中的 BenSelect 添加到托管的 SaaS 应用列表。

**若要从库中添加 BenSelect，请执行以下步骤：**

1. 在 **[Azure 门户](https://portal.azure.com)** 的左侧导航面板中，单击“Azure Active Directory”图标。 

    ![Active Directory][1]

2. 导航到“企业应用程序”。 然后转到“所有应用程序”。

    ![应用程序][2]
    
3. 若要添加新应用程序，请单击对话框顶部的“新建应用程序”按钮。

    ![应用程序][3]

4. 在“搜索框”中，键入“BenSelect”。

    ![创建 Azure AD 测试用户](./media/benselect-tutorial/tutorial_benselect_search.png)

5. 在结果窗格中，选择“BenSelect”，然后单击“添加”按钮添加该应用程序。

    ![创建 Azure AD 测试用户](./media/benselect-tutorial/tutorial_benselect_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>配置和测试 Azure AD 单一登录
在本部分中，基于名为“Britta Simon”的测试用户配置和测试 BenSelect 的 Azure AD 单一登录。

对于单一登录到工作帐户，Azure AD 需要知道 Azure AD 用户在 BenSelect 中的对应用户是谁。 换句话说，需要建立 Azure AD 用户与 BenSelect 中相关用户之间的链接关系。

可通过将 Azure AD 中“用户名”的值指定为 BenSelect 中“用户名”的值来建立此关联关系。

若要通过 BenSelect 配置和测试 Azure AD 单一登录，需要完成以下构建基块：

1. **[配置 Azure AD 单一登录](#configuring-azure-ad-single-sign-on)** - 让用户使用此功能。
2. **[创建 Azure AD 测试用户](#creating-an-azure-ad-test-user)** - 使用 Britta Simon 测试 Azure AD 单一登录。
3. **[创建 BenSelect 测试用户](#creating-a-benselect-test-user)** - 在 BenSelect 中创建 Britta Simon 的对应用户，并将其链接到该用户的 Azure AD 表示形式。
4. **[分配 Azure AD 测试用户](#assigning-the-azure-ad-test-user)** - 让 Britta Simon 使用 Azure AD 单一登录。
5. **[测试单一登录](#testing-single-sign-on)** - 验证配置是否正常工作。

### <a name="configuring-azure-ad-single-sign-on"></a>配置 Azure AD 单一登录

在本部分中，将在 Azure 门户中启用 Azure AD 单一登录并在 BenSelect 应用程序中配置单一登录。

**若要配置 BenSelect 的 Azure AD 单一登录，请执行以下步骤：**

1. 在 Azure 门户中的 BenSelect 应用程序集成页上，单击“单一登录”。

    ![配置单一登录][4]

2. 在“单一登录”对话框中，选择“基于 SAML 的单一登录”作为“模式”以启用单一登录。
 
    ![配置单一登录](./media/benselect-tutorial/tutorial_benselect_samlbase.png)

3. 在“BenSelect 域和 URL”部分中，执行以下步骤：

    ![配置单一登录](./media/benselect-tutorial/tutorial_benselect_url.png)

    在“回复 URL”文本框中，使用以下模式键入 URL：`https://www.benselect.com/enroll/login.aspx?Path=<tenant name>`

    > [!NOTE] 
    > 此值不是真实值。 请使用实际回复 URL 更新此值。 请联系 [BenSelect 支持团队](mailto:support@selerix.com)获取此值。
 
4. 在“SAML 签名证书”部分中，单击“证书(原始)”，并在计算机上保存证书文件。

    ![配置单一登录](./media/benselect-tutorial/tutorial_benselect_certificate.png) 

5. BenSelect 应用程序需要采用特定格式的 SAML 断言。 请为此应用程序配置以下声明。 可以在应用程序集成页的“用户属性”部分管理这些属性的值。 以下屏幕截图显示一个示例。

    ![配置单一登录](./media/benselect-tutorial/tutorial_benselect_06.png)

6. 在“单一登录”对话中的“用户属性”部分：

    a. 在“用户标识符”下拉列表中选择“ExtractMailPrefix”。

    b. 在“邮件”下拉列表中，选择“user.userprincipalname”。

7. 单击“保存”按钮。

    ![配置单一登录](./media/benselect-tutorial/tutorial_general_400.png)

8. 在“BenSelect 配置”部分中，单击“配置 BenSelect”打开“配置登录”窗口。 从“快速参考”部分中复制“注销 URL”、“SAML 实体 ID”和“SAML 单一登录服务 URL”。

    ![配置单一登录](./media/benselect-tutorial/tutorial_benselect_configure.png) 

9. 若要在 BenSelect 端配置单一登录，需要将下载的证书(原始)、注销 URL、SAML 实体 ID 和 SAML 单一登录服务 URL 发送给 [BenSelect 支持团队](mailto:support@selerix.com)。

   >[!NOTE]
   >需要声明，此集成需要 SHA256 算法（SHA1 不受支持）才能在相应服务器（例如 app2101 等）上设置 SSO。 
   
> [!TIP]
> 之后在设置应用时，就可以在 [Azure 门户](https://portal.azure.com)中阅读这些说明的简明版本了！  从“Active Directory”>“企业应用程序”部分添加此应用后，只需单击“单一登录”选项卡，即可通过底部的“配置”部分访问嵌入式文档。 可在此处阅读有关嵌入式文档功能的详细信息：[ Azure AD 嵌入式文档]( https://go.microsoft.com/fwlink/?linkid=845985)

### <a name="creating-an-azure-ad-test-user"></a>创建 Azure AD 测试用户
本部分的目的是在 Azure 门户中创建名为 Britta Simon 的测试用户。

![创建 Azure AD 用户][100]

**若要在 Azure AD 中创建测试用户，请执行以下步骤：**

1. 在 **Azure 门户**的左侧导航窗格中，单击“Azure Active Directory”图标。

    ![创建 Azure AD 测试用户](./media/benselect-tutorial/create_aaduser_01.png) 

2. 若要显示用户列表，请转到“用户和组”，单击“所有用户”。
    
    ![创建 Azure AD 测试用户](./media/benselect-tutorial/create_aaduser_02.png) 

3. 若要打开“用户”对话框，请在对话框顶部单击“添加”。
 
    ![创建 Azure AD 测试用户](./media/benselect-tutorial/create_aaduser_03.png) 

4. 在“用户”对话框页上，执行以下步骤：
 
    ![创建 Azure AD 测试用户](./media/benselect-tutorial/create_aaduser_04.png) 

    a. 在“名称”文本框中，键入 **BrittaSimon**。

    b. 在“用户名”文本框中，键入 BrittaSimon 的“电子邮件地址”。

    c. 选择“显示密码”并记下“密码”的值。

    d. 单击“创建”。
 
### <a name="creating-a-benselect-test-user"></a>创建 BenSelect 测试用户

本部分目的是在 BenSelect 中创建名为“Britta Simon”的用户。 请与 [BenSelect 支持团队](mailto:support@selerix.com)协作，在 BenSelect 帐户中添加用户。

### <a name="assigning-the-azure-ad-test-user"></a>分配 Azure AD 测试用户

在本部分中，通过向 Britta Simon 授予 BenSelect 的访问权限支持她使用 Azure 单一登录。

![分配用户][200] 

**要将 Britta Simon 分配到 BenSelect，请执行以下步骤：**

1. 在 Azure 门户中打开应用程序视图，导航到目录视图，接着转到“企业应用程序”，并单击“所有应用程序”。

    ![分配用户][201] 

2. 在应用程序列表中选择“BenSelect”。

    ![配置单一登录](./media/benselect-tutorial/tutorial_benselect_app.png) 

3. 在左侧菜单中，单击“用户和组”。

    ![分配用户][202] 

4. 单击“添加”按钮。 然后在“添加分配”对话框中选择“用户和组”。

    ![分配用户][203]

5. 在“用户和组”对话框的“用户”列表中，选择“Britta Simon”。

6. 在“用户和组”对话框中单击“选择”按钮。

7. 在“添加分配”对话框中单击“分配”按钮。
    
### <a name="testing-single-sign-on"></a>测试单一登录

在本部分中，使用访问面板测试 Azure AD SSO 配置。

当在访问面板中单击“BenSelect”磁贴时，应该会自动登录“BenSelect”应用程序。

## <a name="additional-resources"></a>其他资源

* [有关如何将 SaaS 应用与 Azure Active Directory 集成的教程列表](tutorial-list.md)
* [什么是使用 Azure Active Directory 的应用程序访问和单一登录？](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/benselect-tutorial/tutorial_general_01.png
[2]: ./media/benselect-tutorial/tutorial_general_02.png
[3]: ./media/benselect-tutorial/tutorial_general_03.png
[4]: ./media/benselect-tutorial/tutorial_general_04.png

[100]: ./media/benselect-tutorial/tutorial_general_100.png

[200]: ./media/benselect-tutorial/tutorial_general_200.png
[201]: ./media/benselect-tutorial/tutorial_general_201.png
[202]: ./media/benselect-tutorial/tutorial_general_202.png
[203]: ./media/benselect-tutorial/tutorial_general_203.png
