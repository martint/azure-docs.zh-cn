---
title: 对于在 Azure 应用程序网关的允许列表后端所需证书
description: 本文提供如何将 SSL 证书转换为身份验证证书和受信任的根证书的示例所需的 Azure 应用程序网关的允许列表的后端实例
services: application-gateway
author: abshamsft
ms.service: application-gateway
ms.topic: article
ms.date: 3/14/2019
ms.author: absha
ms.openlocfilehash: 72ee9123ad959c0c7240d4f7a906adc1a4dd1a93
ms.sourcegitcommit: aa3be9ed0b92a0ac5a29c83095a7b20dd0693463
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2019
ms.locfileid: "58260419"
---
# <a name="create-certificates-for-whitelisting-backend-with-azure-application-gateway"></a>通过 Azure 应用程序网关创建为列入允许列表后端的证书

若要执行端到端 SSL，应用程序网关需要通过身份验证/受信任根证书上传要加入允许列表的后端实例。 如果 v1 SKU，身份验证证书所需而发生 v2 SKU 时受信任的根证书所需的允许列表的证书

在本文中，学习如何：

> [!div class="checklist"]
>
> - 从后端证书的身份验证证书导出 （适用于 v1 SKU)
> - 从后端证书 （适用于 v2 SKU) 中导出受信任的根证书

## <a name="prerequisites"></a>必备组件

需要现有的后端证书来生成所需的应用程序网关的允许列表的后端实例的受信任的根证书的身份验证证书。 后端证书可以是与 SSL 证书相同或不同为了提高安全性。 应用程序网关不会向你提供任何机制来创建或购买的 SSL 证书。 出于测试目的，可以创建自签名的证书，但您应将其用于生产工作负荷。 

## <a name="export-authentication-certificate-for-v1-sku"></a>导出身份验证证书 （适用于 v1 SKU)

身份验证证书所需应用程序网关 v1 中的允许列表后端实例 SKU。 身份验证证书是 Base-64 在后端服务器证书的公钥编码的 X.509 (。CER) 格式。 在此示例中，我们将用于后端证书的 SSL 证书并将其用作身份验证证书的公钥导出。 此外，在此示例中，我们将使用 Windows 证书管理器工具导出所需的证书。 您可以选择使用任何其他工具根据你的方便。

从 SSL 证书，请将导出公用密钥.cer 文件 （不是私钥）。 以下步骤可帮助您导出.cer 文件采用 Base-64 编码 X.509 (。你的证书的 CER) 格式：

1. 若要获取证书 .cer 文件，请打开“管理用户证书”。 通常在 Certificates-Current User\Personal\Certificates，找到证书，并右键单击。 单击“所有任务”，并单击“导出”。 此操作将打开“证书导出向导”。 如果在 Current User\Personal\Certificates 下找不到证书，可能会意外地打开“Certificates - Local Computer”而不是“Certificates - Current User”）。 如果想要使用 PowerShell 在当前用户范围内打开证书管理程序，请在控制台窗口中键入“certmgr”。

   ![导出](./media/certificates-for-backend-authentication/export.png)

2. 在向导中，单击“下一步”。

   ![导出证书](./media/certificates-for-backend-authentication/exportwizard.png)

3. 选择“否，不导出私钥”，并单击“下一步”。

   ![不要导出私钥](./media/certificates-for-backend-authentication/notprivatekey.png)

4. 在“导出文件格式”页上，选择“Base-64 编码的 X.509 (.CER)”，并单击“下一步”。

   ![Base-64 编码](./media/certificates-for-backend-authentication/base64.png)

5. 对于“要导出的文件”，“浏览”到要将证书导出的目标位置。 在“文件名”中，为证书文件命名。 然后单击“下一步”。

   ![浏览](./media/certificates-for-backend-authentication/browse.png)

6. 单击“完成”导出证书。

   ![完成](./media/certificates-for-backend-authentication/finish.png)

7. 证书已成功导出。

   ![Success](./media/certificates-for-backend-authentication/success.png)

   导出的证书类似于以下内容：

   ![已导出](./media/certificates-for-backend-authentication/exported.png)

8. 如果使用记事本打开导出的证书，则会看到类似于此示例的一些内容。 蓝色的部分包含上传到应用程序网关的信息。 如果使用记事本打开证书，并且内容不与此类似，则这通常意味着你没有使用 Base-64 编码的 X.509(.CER) 格式将其导出。 此外，如果希望使用其他文本编辑器，请注意，某些编辑器可能会在后台引入意外的格式设置。 将此证书中的文本上传到 Azure 时，这可能会产生问题。

   ![使用记事本打开](./media/certificates-for-backend-authentication/format.png)

## <a name="export-trusted-root-certificate-for-v2-sku"></a>导出受信任的根证书 （适用于 v2 SKU)

受信任的根证书是为应用程序网关 v2 中的允许列表后端实例所需 SKU。 根证书是 Base-64 编码 X.509 (。从后端服务器证书的 CER) 格式的根证书。 在此示例中，我们将用于后端证书的 SSL 证书、 导出其公钥，然后从中要获取受信任的根证书的 base64 编码格式的公钥导出受信任的 CA 的根证书。 

以下步骤帮助你导出证书的.cer 文件：

1. 使用步骤 1-9 部分所述 **（适用于 v1 SKU) 的后端证书中的导出身份验证证书**上述命令以从后端证书导出公钥。

2. 导出公钥后, 打开的文件。

   ![开放授权证书](./media/certificates-for-backend-authentication/openAuthcert.png)

   ![有关证书](./media/certificates-for-backend-authentication/general.png)

3. 将移动到视图，在证书路径的证书颁发机构。

   ![证书详细信息](./media/certificates-for-backend-authentication/certdetails.png)

4. 选择根证书，然后单击**查看证书**。

   ![证书路径](./media/certificates-for-backend-authentication/rootcert.png)

   您应能够查看根证书的详细信息。

   ![证书信息](./media/certificates-for-backend-authentication/rootcertdetails.png)

5. 将移动到**详细信息**查看，然后单击**复制到文件...**

   ![复制根证书](./media/certificates-for-backend-authentication/rootcertcopytofile.png)

6. 此时，你必须从后端的证书来提取根证书的详细信息。 你将看到**证书导出向导**。 现在，使用步骤 2-9 部分所述 **（适用于 v1 SKU) 的后端证书中的导出身份验证证书**上面导出受信任的根证书采用 Base-64 编码 X.509 (。CER) 格式。

## <a name="next-steps"></a>后续步骤

现在你拥有证书/受信任的身份验证的根证书采用 Base-64 编码的 X.509 (。CER) 格式。 可以添加此应用程序网关加入允许列表到后端服务器以实现端到端 SSL 加密。 请参阅[如何配置端到端 SSL 加密](https://docs.microsoft.com/azure/application-gateway/application-gateway-end-to-end-ssl-powershell)。