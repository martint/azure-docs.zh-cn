---
title: 如何在 Azure 中更改 SQL Server VM 的许可模型 | Microsoft Docs
description: 了解如何在 Azure 中切换 SQL 虚拟机的许可。
services: virtual-machines-windows
documentationcenter: na
author: MashaMSFT
manager: craigg
tags: azure-resource-manager
ms.assetid: aa5bf144-37a3-4781-892d-e0e300913d03
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 02/13/2019
ms.author: mathoma
ms.reviewer: jroth
ms.openlocfilehash: c68bae87440bddf704d18b575aeb1f4ba4760bbb
ms.sourcegitcommit: 48a41b4b0bb89a8579fc35aa805cea22e2b9922c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/15/2019
ms.locfileid: "59578237"
---
# <a name="how-to-change-the-licensing-model-for-a-sql-server-virtual-machine-in-azure"></a>如何在 Azure 中更改 SQL Server 虚拟机的许可模型
本文介绍如何在 Azure 中使用新的 SQL VM 资源提供程序 **Microsoft.SqlVirtualMachine** 来更改 SQL Server 虚拟机的许可模型。 有两个许可模型为虚拟机 (VM) 托管 SQL Server 的即用即付，并自带许可 (BYOL)。 和现在，使用 Azure 门户、 Azure CLI 或 PowerShell，您可以修改 SQL Server 虚拟机使用哪个许可模式。 

**即用即付**(PAYG) 模型的推出意味着 Azure VM 运行的每秒费用包括 SQL Server 许可证的费用。

**自带的自己的许可证**(BYOL) 模型是也称为[Azure 混合权益 (AHB)](https://azure.microsoft.com/pricing/hybrid-benefit/)，并且可以将 SQL Server 许可证用于运行 SQL Server 的虚拟机。 有关价格的详细信息，请参阅 [SQL Server VM 定价指南](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-pricing-guidance)。

在两个许可证模型之间进行切换不会导致停机，不会重启 VM，不会增加费用（事实上，激活 AHB 会降低费用），并且会立即生效。 

## <a name="remarks"></a>备注

 - CSP 客户可通过首先部署即用即付 VM，然后将它转换为自带许可，来利用 AHB 权益。 
 - 当注册资源提供程序的自定义 SQL Server VM 映像，指定许可证类型 = AHUB。 将保留该许可证类型为空白，也可指定 PAYG 将导致注册失败。 
 - 如果您删除 SQL Server VM 资源，将返回到该映像的硬编码的许可证设置。 
 - 若要更改的许可模式，您是 SQL 虚拟机资源提供程序的功能。 自动部署通过 Azure 门户的 marketplace 映像注册资源提供程序的 SQL Server VM。 但是，在自安装 SQL Server 的客户将需要手动[注册其 SQL Server 虚拟机](#register-sql-server-vm-with-the-sql-vm-resource-provider)。 

 
## <a name="limitations"></a>限制

 - 当前，仅当从即用即付 SQL Server VM 映像开始时，才能使用转换许可模型的功能。 如果从门户首先使用自带许可映像，则无法将该映像转换为即用即付。
 - 使用资源管理器模型部署的虚拟机仅支持更改授权模型。 不支持使用经典模型部署的 Vm。 
 - 公共云安装仅启用更改授权模型。
 - 仅在具有单个 NIC （网络接口） 的虚拟机上支持更改授权模型。 在具有多个 NIC 的虚拟机，你应首先删除其中一个 Nic （通过使用 Azure 门户） 在尝试此过程之前。 否则，将遇到如下错误：`The virtual machine '\<vmname\>' has more than one NIC associated.` 尽管您可以将 NIC 添加回 VM 后更改的授权模式，将不再被视为的 SQL 配置边栏选项卡，如自动修补和备份，通过执行的操作支持。

## <a name="prerequisites"></a>必备组件

使用 SQL VM 资源提供程序需要安装 SQL IaaS 扩展。 因此，若要继续利用 SQL VM 提供程序，需要：
- 一个 [Azure 订阅](https://azure.microsoft.com/free/)。
- [软件保障](https://www.microsoft.com/licensing/licensing-programs/software-assurance-default)。 
- 一个*即用即付* [SQL Server 虚拟机](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-portal-sql-server-provision)与[SQL IaaS 扩展](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-agent-extension)安装。 

## <a name="with-the-azure-portal"></a>使用 Azure 门户

您可以修改直接从门户的授权模型。 

1. 导航到 SQL Server VM 内[Azure 门户](https://portal.azure.com)。 
1. 选择**SQL Server 配置**中**设置**窗格。 
1. 选择**编辑**中**SQL Server 许可证**窗格，可以修改该许可证。 

![在门户中的 AHB](media/virtual-machines-windows-sql-ahb/ahb-in-portal.png)

  >[!NOTE]
  > 此选项不可用的自带的自己的许可证映像。 

## <a name="with-azure-cli"></a>使用 Azure CLI

可以通过 Azure CLI 更改许可模型。  

下面的代码段将切换到 BYOL （或使用 Azure 混合权益） 即用即付许可证模型：

```azurecli
# Switch your SQL Server VM license from pay-as-you-go to bring-your-own
# example: az sql vm update -n AHBTest -g AHBTest --license-type AHUB

az sql vm update -n <VMName> -g <ResourceGroupName> --license-type AHUB
```

下面的代码段将切换到即用即付自带的自己的许可证模型： 

```azurecli
# Switch your SQL Server VM license from bring-your-own to pay-as-you-go
# example: az sql vm update -n AHBTest -g AHBTest --license-type PAYG

az sql vm update -n <VMName> -g <ResourceGroupName> --license-type PAYG
```
## <a name="with-powershell"></a>使用 PowerShell
可以使用 PowerShell 更改许可模型。

下面的代码段将切换到 BYOL （或使用 Azure 混合权益） 即用即付许可证模型：

```powershell
# Switch your SQL Server VM license from pay-as-you-go to bring-your-own
#example: $SqlVm = Get-AzResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName AHBTest -ResourceName AHBTest
$SqlVm = Get-AzResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName <resource_group_name> -ResourceName <VM_name>
$SqlVm.Properties.sqlServerLicenseType="AHUB"
<# the following code snippet is only necessary if using Azure Powershell version > 4
$SqlVm.Kind= "LicenseChange"
$SqlVm.Plan= [Microsoft.Azure.Management.ResourceManager.Models.Plan]::new()
$SqlVm.Sku= [Microsoft.Azure.Management.ResourceManager.Models.Sku]::new() #>
$SqlVm | Set-AzResource -Force 
```

下面的代码段将切换到即用即付 BYOL 模型：

```powershell
# Switch your SQL Server VM license from bring-your-own to pay-as-you-go
#example: $SqlVm = Get-AzResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName AHBTest -ResourceName AHBTest
$SqlVm = Get-AzResource -ResourceType Microsoft.SqlVirtualMachine/SqlVirtualMachines -ResourceGroupName <resource_group_name> -ResourceName <VM_name>
$SqlVm.Properties.sqlServerLicenseType="PAYG"
<# the following code snippet is only necessary if using Azure Powershell version > 4
$SqlVm.Kind= "LicenseChange"
$SqlVm.Plan= [Microsoft.Azure.Management.ResourceManager.Models.Plan]::new()
$SqlVm.Sku= [Microsoft.Azure.Management.ResourceManager.Models.Sku]::new() #>
$SqlVm | Set-AzResource -Force 
```


## <a name="register-sql-server-vm-with-the-sql-vm-resource-provider"></a>使用 SQL VM 资源提供程序注册 SQL Server 虚拟机
在某些情况下，可能需要使用 SQL VM 资源提供程序手动注册到 SQL Server VM。 若要执行此操作，可能还需要手动将资源提供程序注册到订阅。 


### <a name="register-sql-vm-resource-provider-with-subscription"></a>SQL VM 资源提供程序注册订阅 

若要向 SQL 资源提供程序注册 SQL Server VM，必须将资源提供程序注册到订阅。 可以使用 Azure 门户或 Azure CLI 执行操作。 

#### <a name="with-the-azure-portal"></a>使用 Azure 门户
以下步骤将注册到 Azure 订阅使用 Azure 门户的 SQL 资源提供程序。 

1. 打开 Azure 门户，导航到“所有服务”。 
1. 导航到“订阅”，选择感兴趣的订阅。  
1. 在“订阅”边栏选项卡中，导航到“资源提供程序”。 
1. 在筛选器中键入 `sql`，以便显示与 SQL 相关的资源提供程序。 
1. 根据所需操作为 **Microsoft.SqlVirtualMachine** 提供程序选择“注册”、“重新注册”或“取消注册”。 

   ![修改提供程序](media/virtual-machines-windows-sql-ahb/select-resource-provider-sql.png)

#### <a name="with-azure-cli"></a>使用 Azure CLI
下面的代码段将注册到 Azure 订阅的 SQL VM 资源提供程序。 

```azurecli
# Register the new SQL resource provider to your subscription 
az provider register --namespace Microsoft.SqlVirtualMachine 
```

#### <a name="with-powershell"></a>使用 PowerShell

下面的代码段将注册到 Azure 订阅的 SQL 资源提供程序。

```powershell
# Register the new SQL resource provider to your subscription
Register-AzResourceProvider -ProviderNamespace Microsoft.SqlVirtualMachine
```

### <a name="register-sql-server-vm-with-sql-resource-provider"></a>将 SQL Server VM 注册到 SQL 资源提供程序
一旦 SQL 虚拟机资源提供程序已注册到你的订阅，您可以向资源提供程序使用 Azure CLI 中注册 SQL Server VM。 

#### <a name="with-azure-cli"></a>使用 Azure CLI
注册 SQL Server 虚拟机使用以下代码片段中使用 Azure CLI: 

```azurecli
# Register your existing SQL Server VM with the new resource provider
az sql vm create -n <VMName> -g <ResourceGroupName> -l <VMLocation>
```
#### <a name="with-powershell"></a>使用 PowerShell
注册 SQL Server 虚拟机使用以下代码片段使用 PowerShell:

```powershell
# Register your existing SQL Server VM with the new resource provider
# example: $vm=Get-AzVm -ResourceGroupName AHBTest -Name AHBTest
$vm=Get-AzVm -ResourceGroupName <ResourceGroupName> -Name <VMName>
New-AzResource -ResourceName $vm.Name -ResourceGroupName $vm.ResourceGroupName -Location $vm.Location -ResourceType Microsoft.SqlVirtualMachine/sqlVirtualMachines -Proper
```



## <a name="known-errors"></a>已知错误

### <a name="sql-iaas-extension-is-not-installed-on-virtual-machine"></a>虚拟机上未安装 SQL IaaS 扩展
必须安装 SQL IaaS 扩展才能将 SQL Server VM 注册到 SQL VM 资源提供程序。 如果尝试在安装 SQL IaaS 扩展之前注册 SQL Server VM，将遇到以下错误：

`Sql IaaS Extension is not installed on Virtual Machine: '{0}'. Please make sure it is installed and in running state and try again later.`

若要解决此问题，请在尝试注册 SQL Server VM 之前先安装 SQL IaaS 扩展。 

  > [!NOTE]
  > 安装 SQL IaaS 扩展会重启 SQL Server 服务，请只在维护时段进行安装。 有关详细信息，请参阅 [SQL IaaS 扩展安装](https://docs.microsoft.com/azure/virtual-machines/windows/sql/virtual-machines-windows-sql-server-agent-extension#installation)。 


### <a name="the-resource-microsoftsqlvirtualmachinesqlvirtualmachinesresource-group-under-resource-group-resource-group-was-not-found-the-property-sqlserverlicensetype-cannot-be-found-on-this-object-verify-that-the-property-exists-and-can-be-set"></a>找不到资源 Microsoft.SqlVirtualMachine/SqlVirtualMachines/ < 资源组 > 资源组 < 资源组 > 下。 此对象上找不到 sqlServerLicenseType 的属性。 验证属性存在并且可以设置。
尝试更改与 SQL 资源提供程序尚未注册 SQL Server VM 上的许可模式时，将发生此错误。 将需要注册资源提供程序为你[订阅](#register-sql-vm-resource-provider-with-subscription)，并将 SQL 注册 SQL Server 虚拟机[资源提供程序](#register-sql-server-vm-with-sql-resource-provider)。 

### <a name="cannot-validate-argument-on-parameter-sku"></a>无法验证参数“Sku”中的自变量
尝试使用 4.0 以上版本的 Azure PowerShell 更改 SQL Server VM 许可模型时，可能会遇到以下错误：集 AzResource:无法验证参数 Sku 的参数。 参数为 null 或为空。 提供的参数，不为 null 或为空，然后再重试该命令。
若要解决此错误，请在切换许可模型时，取消注释上述 PowerShell 代码片段中的以下行：

```powershell
# the following code snippet is necessary if using Azure Powershell version > 4
$SqlVm.Kind= "LicenseChange"
$SqlVm.Plan= [Microsoft.Azure.Management.ResourceManager.Models.Plan]::new()
$SqlVm.Sku= [Microsoft.Azure.Management.ResourceManager.Models.Sku]::new()
```

使用以下代码验证 Azure PowerShell 版本：

```powershell
Get-Module -ListAvailable -Name Azure -Refresh
```

## <a name="next-steps"></a>后续步骤

有关详细信息，请参阅以下文章： 

* [Windows VM 上的 SQL Server 概述](virtual-machines-windows-sql-server-iaas-overview.md)
* [Windows VM 上的 SQL Server 常见问题解答](virtual-machines-windows-sql-server-iaas-faq.md)
* [Windows VM 上的 SQL Server 定价指南](virtual-machines-windows-sql-server-pricing-guidance.md)
* [Windows VM 上的 SQL Server 发行说明](virtual-machines-windows-sql-server-iaas-release-notes.md)


