---
title: 最终用户身份验证：对 Azure Data Lake Storage Gen1 结合使用 Azure Active Directory 和 .NET SDK | Microsoft Docs
description: 了解如何结合使用 .NET SDK 和 Azure Active Directory 进行 Azure Data Lake Storage Gen1 最终用户身份验证
services: data-lake-store
documentationcenter: ''
author: twooley
manager: cgronlun
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: twooley
ms.openlocfilehash: 78a290d8136f8804e853d36a9bc95571625ed89c
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58876762"
---
# <a name="end-user-authentication-with-azure-data-lake-storage-gen1-using-net-sdk"></a>使用 .NET SDK 进行 Azure Data Lake Storage Gen1 最终用户身份验证
> [!div class="op_single_selector"]
> * [使用 Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [使用 .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [使用 Python](data-lake-store-end-user-authenticate-python.md)
> * [使用 REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
>  

本文介绍了如何使用 .NET SDK 进行 Azure Data Lake Storage Gen1 最终用户身份验证。 有关使用 .NET SDK 的 Data Lake Storage Gen1 服务到服务身份验证，请参阅[使用 .NET SDK 进行 Data Lake Storage Gen1 服务到服务身份验证](data-lake-store-service-to-service-authenticate-net-sdk.md)。

## <a name="prerequisites"></a>必备组件
* **Visual Studio 2013、2015 或 2017**。 以下说明使用的是 Visual Studio 2017。

* **Azure 订阅**。 请参阅[获取 Azure 免费试用版](https://azure.microsoft.com/pricing/free-trial/)。

* **创建 Azure Active Directory“本机”应用程序**。 必须已完成[使用 Azure Active Directory 进行 Data Lake Storage Gen1 最终用户身份验证](data-lake-store-end-user-authenticate-using-active-directory.md)中的步骤。

## <a name="create-a-net-application"></a>创建 .NET 应用程序
1. 打开 Visual Studio，创建一个控制台应用程序。
2. 在“文件”菜单中，单击“新建”，并单击“项目”。
3. 在“新建项目”中，键入或选择以下值 ：

   | 属性 | 值 |
   | --- | --- |
   | 类别 |模板/Visual C#/Windows |
   | 模板 |控制台应用程序 |
   | 名称 |CreateADLApplication |

4. 单击“确定”以创建该项目  。

5. 将 NuGet 包添加到项目。

   1. 在解决方案资源管理器中右键单击项目名称，单击“管理 NuGet 包” 。
   2. 在“NuGet 包管理器”选项卡上，确保“包源”设置为“nuget.org”，“包含预发行版”复选框处于选中状态。
   3. 搜索并安装以下 NuGet 包：

      * `Microsoft.Azure.Management.DataLake.Store` - 本教程使用 v2.1.3-预览版。
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - 本教程使用 v2.2.12。

        ![添加 Nuget 源](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "创建新的 Azure Data Lake 帐户")
   4. 关闭“NuGet 包管理器”。

6. 打开 **Program.cs**
7. 将 using 语句替换为以下行：

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Collections.Generic;
            
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure.Management.DataLake.Store;
    using Microsoft.Azure.Management.DataLake.Store.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    ```     

## <a name="end-user-authentication"></a>最终用户身份验证
在 .NET 客户端应用程序中添加此代码片段。 将占位符值替换为从 Azure AD 本机应用程序（作为必备组件列出）检索到的值。 通过此代码片段，可以“交互方式”对应用程序进行 Data Lake Storage Gen1 身份验证，这意味着系统会提示你输入 Azure 凭据。

为了便于使用，下面的代码片段针对客户端 ID 和重定向 URI 使用了对任何 Azure 订阅都有效的默认值。 在下面的代码片段中，只需要提供你的租户 ID 的值。 可以使用[获取租户 ID](../active-directory/develop/howto-create-service-principal-portal.md#get-tenant-id) 中提供的说明来检索租户 ID。
    
- 将 Main() 函数替换为以下代码：

    ```csharp
    private static void Main(string[] args)
    {
        //User login via interactive popup
        string TENANT = "<AAD-directory-domain>";
        string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
        System.Uri ARM_TOKEN_AUDIENCE = new System.Uri(@"https://management.core.windows.net/");
        System.Uri ADL_TOKEN_AUDIENCE = new System.Uri(@"https://datalake.azure.net/");
        string MY_DOCUMENTS = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);
        string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");
        var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
        var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
        var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
    }
    ```

对于以上代码片段，需要注意以下几个问题：

* 上述代码片段使用 helper 函数 `GetTokenCache` 和 `GetCreds_User_Popup`。 可在[此处（GitHub 上）](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#gettokencache)获取这些 helper 函数的代码。
* 为了帮助读者更快完成本教程，此代码片段使用了为所有 Azure 订阅默认提供的本机应用程序客户端 ID。 因此，可以**在应用程序中按原样使用此代码片段**。
* 但是，如果想要使用自己的 Azure AD 域和应用程序客户端 ID，则必须创建一个 Azure AD 本机应用程序，并使用所创建的应用程序的 Azure AD 租户 ID、客户端 ID 和重定向 URI。 有关说明，请参阅[创建 Active Directory 应用程序，以便进行 Data Lake Storage Gen1 最终用户身份验证](data-lake-store-end-user-authenticate-using-active-directory.md)。

  
## <a name="next-steps"></a>后续步骤
本文介绍如何使用 .NET SDK 通过最终用户身份验证进行 Azure Data Lake Storage Gen1 身份验证。 接下来，可以查看以下介绍如何使用 .NET SDK 在 Azure Data Lake Storage Gen1 中执行操作的文章。

* [使用 .NET SDK 对 Data Lake Storage Gen1 上的帐户管理操作](data-lake-store-get-started-net-sdk.md)
* [使用 NET SDK 在 Data Lake Storage Gen1 中进行的数据操作](data-lake-store-data-operations-net-sdk.md)

