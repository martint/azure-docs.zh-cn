---
title: 教程-部署 Azure 容器实例的 YAML 中的多容器组
description: 在本教程中，您将学习如何使用 Azure CLI 使用 YAML 文件将部署包含 Azure 容器实例中的多个容器的容器组。
services: container-instances
author: dlepow
ms.service: container-instances
ms.topic: article
ms.date: 04/03/2019
ms.author: danlep
ms.openlocfilehash: a0a91ece4f219cf822673cd457c064c326b89478
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59006182"
---
# <a name="tutorial-deploy-a-multi-container-group-using-a-yaml-file"></a>教程：部署多容器组使用 YAML 文件

> [!div class="op_single_selector"]
> * [YAML](container-instances-multi-container-yaml.md)
> * [资源管理器](container-instances-multi-container-group.md)
>

Azure 容器实例支持使用[容器组](container-instances-container-groups.md)将多个容器部署到单台主机上。 容器组时，生成的日志记录、 监视或任何其他配置应用程序 sidecar 其中服务需要第二个附加的进程。

在本教程中，您可以按照步骤通过部署使用 Azure CLI 的 YAML 文件运行简单的两个容器 sidecar 配置。 YAML 文件提供用于指定实例设置的简明格式。 学习如何：

> [!div class="checklist"]
> * 配置一个 YAML 文件
> * 部署容器组
> * 查看容器日志

> [!NOTE]
> 多容器组当前仅限于 Linux 容器。

如果还没有 Azure 订阅，可以在开始前创建一个[免费帐户](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)。

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="configure-a-yaml-file"></a>配置一个 YAML 文件

若要部署的多容器组[az 容器创建][ az-container-create]命令在 Azure CLI 中，必须在 YAML 文件中指定的容器组配置。 然后作为参数传递给命令的 YAML 文件。

首先将以下 YAML 复制到一个名为 **deploy-aci.yaml** 的新文件中。 在 Azure Cloud Shell 中，可以使用 Visual Studio Code 在工作目录中创建文件：

```
code deploy-aci.yaml
```

此 YAML 文件定义了一个名为“myContainerGroup”的容器组，其中包含两个容器、一个公共 IP 地址和两个公开端口。 从公共 Microsoft 映像部署容器。 该组中的第一个容器运行面向 Internet 的 Web 应用程序。 第二个容器 sidecar 定期通过容器组的本地网络向在第一个容器中运行的 Web 应用程序发出 HTTP 请求。

```YAML
apiVersion: 2018-10-01
location: eastus
name: myContainerGroup
properties:
  containers:
  - name: aci-tutorial-app
    properties:
      image: mcr.microsoft.com/azuredocs/aci-helloworld:latest
      resources:
        requests:
          cpu: 1
          memoryInGb: 1.5
      ports:
      - port: 80
      - port: 8080
  - name: aci-tutorial-sidecar
    properties:
      image: mcr.microsoft.com/azuredocs/aci-tutorial-sidecar
      resources:
        requests:
          cpu: 1
          memoryInGb: 1.5
  osType: Linux
  ipAddress:
    type: Public
    ports:
    - protocol: tcp
      port: '80'
    - protocol: tcp
      port: '8080'
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

若要使用专用容器映像注册表，将添加`imageRegistryCredentials`属性设置为的容器组中，使用值修改为您的环境：

```YAML
  imageRegistryCredentials:
  - server: imageRegistryLoginServer
    username: imageRegistryUsername
    password: imageRegistryPassword
```

## <a name="deploy-the-container-group"></a>部署容器组

使用 [az group create][az-group-create] 命令创建资源组：

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

使用 [az container create][az-container-create] 命令部署容器组并传递 YAML 文件作为参数：

```azurecli-interactive
az container create --resource-group myResourceGroup --file deploy-aci.yaml
```

将在几秒钟内收到来自 Azure 的初始响应。

## <a name="view-deployment-state"></a>查看部署状态

若要查看部署状态，请运行下面的 [az container show][az-container-show] 命令：

```azurecli-interactive
az container show --resource-group myResourceGroup --name myContainerGroup --output table
```

若要查看正在运行的应用程序，请在浏览器中转到它的 IP 地址。 例如，在此示例输出中，IP 为 `52.168.26.124`：

```bash
Name              ResourceGroup    Status    Image                                                                                               IP:ports              Network    CPU/Memory       OsType    Location
----------------  ---------------  --------  --------------------------------------------------------------------------------------------------  --------------------  ---------  ---------------  --------  ----------
myContainerGroup  danlep0318r      Running   mcr.microsoft.com/azuredocs/aci-tutorial-sidecar,mcr.microsoft.com/azuredocs/aci-helloworld:latest  20.42.26.114:80,8080  Public     1.0 core/1.5 gb  Linux     eastus
```

## <a name="view-container-logs"></a>查看容器日志

使用 [az container logs][az-container-logs] 命令查看容器的日志输出。 `--container-name` 参数指定从中拉取日志的容器。 在此示例中，`aci-tutorial-app`指定容器。

```azurecli-interactive
az container logs --resource-group myResourceGroup --name myContainerGroup --container-name aci-tutorial-app
```

输出：

```console
listening on port 80
::1 - - [21/Mar/2019:23:17:48 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [21/Mar/2019:23:17:51 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [21/Mar/2019:23:17:54 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

若要查看挎斗容器日志，请运行类似的命令指定`aci-tutorial-sidecar`容器。

```azurecli-interactive
az container logs --resource-group myResourceGroup --name myContainerGroup --container-name aci-tutorial-sidecar
```

输出：

```console
Every 3s: curl -I http://localhost                          2019-03-21 20:36:41

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
X-Powered-By: Express
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Wed, 29 Nov 2017 06:40:40 GMT
ETag: W/"67f-16006818640"
Content-Type: text/html; charset=UTF-8
Content-Length: 1663
Date: Thu, 21 Mar 2019 20:36:41 GMT
Connection: keep-alive
```

如你所见，sidecar 通过该组的本地网络定期向主 Web 应用程序发出 HTTP 请求，确保其正在运行。 此 sidecar 示例可以进行扩展，以便在触发警报，如果它收到 HTTP 响应代码而不`200 OK`。

## <a name="next-steps"></a>后续步骤

在本教程中，您可以使用 YAML 文件来部署 Azure 容器实例中的多容器组。 你已了解如何：

> [!div class="checklist"]
> * 配置多容器组的 YAML 文件
> * 部署容器组
> * 查看容器日志

此外可以指定多容器组使用[资源管理器模板](container-instances-multi-container-group.md)。 资源管理器模板可轻松适应于方案时您需要部署容器组与其他 Azure 服务资源。

<!-- LINKS - External -->


<!-- LINKS - Internal -->
[aci-tutorial]: ./container-instances-tutorial-prepare-app.md
[az-container-create]: /cli/azure/container#az-container-create
[az-container-logs]: /cli/azure/container#az-container-logs
[az-container-show]: /cli/azure/container#az-container-show
[az-group-create]: /cli/azure/group#az-group-create
[az-group-deployment-create]: /cli/azure/group/deployment#az-group-deployment-create
[template-reference]: https://docs.microsoft.com/azure/templates/microsoft.containerinstance/containergroups
