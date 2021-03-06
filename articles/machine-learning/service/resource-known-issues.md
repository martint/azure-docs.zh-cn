---
title: 已知问题与故障排除
titleSuffix: Azure Machine Learning service
description: 获取 Azure 机器学习服务的已知问题、解决方法和故障排除的列表。
services: machine-learning
author: j-martens
ms.author: jmartens
ms.reviewer: mldocs
ms.service: machine-learning
ms.subservice: core
ms.topic: conceptual
ms.date: 03/29/2019
ms.custom: seodec18
ms.openlocfilehash: db0eccb542cb4253e6e891fa9fa51e60fb7951a1
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "58892732"
---
# <a name="known-issues-and-troubleshooting-azure-machine-learning-service"></a>Azure 机器学习服务的已知问题和故障排除

本文可帮助你查找和更正使用 Azure 机器学习服务时遇到的错误或失败。

## <a name="sdk-installation-issues"></a>SDK 安装问题

**错误消息：无法卸载 'PyYAML'**

适用于 Python 的 Azure 机器学习 SDK：PyYAML 是 distutils 安装的项目。 因此，在部分卸载的情况下，我们无法准确确定哪些文件属于它。 若要在忽略此错误的同时继续安装 SDK，请使用：

```Python
pip install --upgrade azureml-sdk[notebooks,automl] --ignore-installed PyYAML
```

## <a name="trouble-creating-azure-machine-learning-compute"></a>创建 Azure 机器学习计算时发生故障

如果用户在 GA 发布之前已通过 Azure 门户创建了自己的 Azure 机器学习工作区，则他们很可能无法在该工作区中创建 Azure 机器学习计算。 可对服务提出支持请求，也可通过门户或 SDK 创建新的工作区以立即解除锁定。

## <a name="image-building-failure"></a>映像生成失败

部署 Web 服务时映像生成失败。 解决方法是将“pynacl==1.2.1”作为 pip 依赖项添加到 Conda 文件以进行映像配置。

## <a name="deployment-failure"></a>部署失败

如果观察到 `['DaskOnBatch:context_managers.DaskOnBatch', 'setup.py']' died with <Signals.SIGKILL: 9>`，请将部署中使用的 VM 的 SKU 更改为具有更多内存的 SKU。

## <a name="fpgas"></a>FPGA

你将无法在 FPGA 上部署模型，直到已请求并获得 FPGA 配额批准为止。 若要请求访问权限，请填写配额请求表单： https://aka.ms/aml-real-time-ai

## <a name="automated-machine-learning"></a>自动化机器学习

Tensor Flow 自动执行机器学习当前不支持 tensor flow 版本 1.13。 安装此版本将导致包依赖项停止工作。 我们正在努力在将来的版本中修复此问题。 


## <a name="databricks"></a>Databricks

Databricks 和 Azure 机器学习问题。

### <a name="failure-when-installing-packages"></a>安装包时失败

安装多个包时，azure 机器学习 SDK 安装在 Azure Databricks 上失败。 某些包（如 `psutil`）可能会导致冲突。 若要避免出现安装错误，请通过冻结的库版本安装包。 此问题与到 Databricks 而不适用于 Azure 机器学习服务 SDK。 您也可能会遇到其他库，这一问题。 示例：

```python
psutil cryptography==1.5 pyopenssl==16.0.0 ipython==2.2.0
```

或者，可以使用 init 脚本，如果保留安装的 Python 库的问题。 此方法不正式支持。 有关详细信息，请参阅[群集范围 init 脚本](https://docs.azuredatabricks.net/user-guide/clusters/init-scripts.html#cluster-scoped-init-scripts)。

### <a name="cancel-an-automated-machine-learning-run"></a>取消的自动化的机器学习运行

当使用自动化的机器学习在 Azure Databricks 上的功能时，若要取消运行并开始新的试验运行，请重新启动 Azure Databricks 群集。

### <a name="10-iterations-for-automated-machine-learning"></a>> 自动的机器学习的 10 余次迭代

在自动化机器学习设置，如果有超过 10 个迭代，设置`show_output`到`False`提交运行时。

### <a name="widget-for-the-azure-machine-learning-sdkautomated-machine-learning"></a>在 Azure 机器学习 SDK/自动化机器学习的小组件

Azure 机器学习 SDK 小组件不支持在 Databricks 笔记本中，因为笔记本不能分析的 HTML 小组件。 在 Azure Databricks notebook 单元格中使用以下 Python 代码，可以在门户中查看该小组件：

```
displayHTML("<a href={} target='_blank'>Azure Portal: {}</a>".format(local_run.get_portal_url(), local_run.id))
```

### <a name="import-error-no-module-named-pandascoreindexes"></a>导入错误：名为 pandas.core.indexes 没有模块

如果看到此错误时使用自动机器学习：

1. 运行以下命令在 Azure Databricks 群集中安装两个包： 

   ```
   scikit-learn==0.19.1
   pandas==0.22.0
   ```

1. 分离并重新附加到你的 notebook 群集。 

如果以上步骤无法解决此问题，请尝试重新启动群集。

## <a name="azure-portal"></a>Azure 门户

如果直接通过 SDK 或门户的共享链接查看工作区，则将无法在扩展程序中查看包含订阅信息的常规概述页。 也将无法切换到另一个工作区。 如果需要查看其他工作区，解决方法是直接转到 [Azure 门户](https://portal.azure.com)并搜索工作区名称。

## <a name="diagnostic-logs"></a>诊断日志

如果在请求帮助时可以提供诊断信息，有时会很有帮助。 若要查看某些日志，请访问[Azure 门户](https://portal.azure.com)并转到工作区并选择**工作区 > 试验 > 运行 > 日志**。

## <a name="resource-quotas"></a>资源配额

了解使用 Azure 机器学习时可能遇到的[资源配额](how-to-manage-quotas.md)。

## <a name="authentication-errors"></a>身份验证错误

如果通过远程作业对某个计算目标执行管理操作，会收到以下错误之一：

```json
{"code":"Unauthorized","statusCode":401,"message":"Unauthorized","details":[{"code":"InvalidOrExpiredToken","message":"The request token was either invalid or expired. Please try again with a valid token."}]}
```

```json
{"error":{"code":"AuthenticationFailed","message":"Authentication failed."}}
```

例如，如果尝试通过一个为实施远程执行操作而提交的机器学习管道创建或附加计算目标，会收到错误。
