---
title: 什么是
titleSuffix: Azure Machine Learning service
description: Azure 机器学习服务概述 - 这是一个集成式的端到端数据科学解决方案，能够让专业数据科学家以云规模开发、试验和部署高级分析应用程序。
services: machine-learning
ms.service: machine-learning
ms.subservice: core
ms.topic: overview
ms.reviewer: jmartens
author: garyericson
ms.author: garye
ms.date: 12/04/2018
ms.custom: seodec18
ms.openlocfilehash: 26248616c6b490de00028d8ecc8a0e225da0c0a6
ms.sourcegitcommit: c174d408a5522b58160e17a87d2b6ef4482a6694
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59257104"
---
# <a name="what-is-azure-machine-learning-service"></a>什么是 Azure 机器学习服务？

Azure 机器学习服务是一项云服务，可以使用它来训练、部署、自动执行以及管理机器学习模型，所有这些都是在云提供的广泛范围内进行的。

## <a name="what-is-machine-learning"></a>什么是机器学习？

机器学习是一项数据科研技术，可以让计算机根据现有的数据来预测将来的行为、结果和趋势。 使用机器学习，计算机可以在不需显式编程的情况下进行学习。

机器学习的预测可让应用和设备变得更聪明。 例如，在网上购物时，机器学习可根据购买的产品帮助推荐其他产品。 或者，在刷信用卡时，机器学习可将这笔交易与交易数据库进行比较，帮助检测诈骗。 当吸尘器机器人打扫房间时，机器学习可帮助它确定作业是否已完成。

## <a name="what-is-azure-machine-learning-service"></a>什么是 Azure 机器学习服务？

Azure 机器学习服务提供了一个基于云的环境，你可以使用这一环境来准备数据、培训、测试、部署、管理和跟踪机器学习模型。

[![Azure 机器学习服务工作流](./media/overview-what-is-azure-ml/aml.png)](./media/overview-what-is-azure-ml/aml.png#lightbox)

Azure 机器学习服务完全支持开源技术。 因此，你可以使用几万个包含机器学习组件的开源 Python 包， 例如 PyTorch、TensorFlow 和 scikit-learn。
它支持丰富的工具，可让你以交互方式轻松浏览和准备数据，然后开发和测试模型。 工具示例包括 [Jupyter Notebook](https://jupyter.org) 或[适用于 Visual Studio Code 的 Azure 机器学习](https://marketplace.visualstudio.com/items?itemName=ms-toolsai.vscode-ai#overview)扩展。
此外，Azure 机器学习服务还包括[自动化模型生成和优化](tutorial-auto-train-models.md)的功能，能够帮助你轻松、高效和准确地创建模型。

使用 Azure 机器学习服务可以先在本地计算机上开始训练，然后扩展到云中。 借助许多可用的[计算目标](how-to-set-up-training-targets.md)（例如 Azure 机器学习计算和 [Azure Databricks](/azure/azure-databricks/what-is-azure-databricks)）以及[高级超参数优化服务](how-to-tune-hyperparameters.md)，可以利用云的强大功能更快地生成更好的模型。

在拥有合适的模型后，即可轻松地将其部署在 Docker 等的容器中。 因此，可以轻松部署到 Azure 容器实例或 Azure Kubernetes 服务。 或者，你可以在自己的本地部署或云部署中使用容器。 有关详细信息，请参阅有关[部署方式及位置](how-to-deploy-and-where.md)的文章。

在尝试寻找最佳解决方案时，可以管理已部署的模型并跟踪多个运行。
部署后，模型可以基于大量数据[实时](how-to-consume-web-service.md)或[异步](how-to-run-batch-predictions.md)返回预测结果。

使用高级[机器学习管道](concept-ml-pipelines.md)，你可以针对数据准备、模型训练和评估以及部署的所有步骤进行协作。

## <a name="what-can-i-do-with-azure-machine-learning-service"></a>通过 Azure 机器学习服务，我可以执行哪些操作？

使用适用于 Azure 机器学习的<a href="https://aka.ms/aml-sdk" target="_blank">主 Python SDK</a> 和<a href="https://aka.ms/data-prep-sdk" target="_blank">数据准备 SDK</a> 以及开源 Python 包，可以在 Azure 机器学习服务工作区中自行生成和训练高度准确的机器学习和深度学习模型。
可以从开源 Python 包中提供的许多机器学习组件中进行选择，例如：

- <a href="https://scikit-learn.org/stable/" target="_blank">Scikit-learn</a>
- <a href="https://www.tensorflow.org" target="_blank">Tensorflow</a>
- <a href="https://pytorch.org" target="_blank">PyTorch</a>
- <a href="https://mxnet.io" target="_blank">MXNet</a>

Azure 机器学习服务还可以自动训练模型和自动优化模型。
有关示例，请参阅[使用自动化机器学习训练回归模型](tutorial-auto-train-models.md)。

生成模型后，使用它来创建可部署在本地进行测试的容器（例如 Docker）。 完成测试后，可以在 Azure 容器实例或 Azure Kubernetes 服务中将该模型部署为生产 Web 服务。 有关详细信息，请参阅有关[部署方式及位置](how-to-deploy-and-where.md)的文章。

然后，可以使用[适用于 Python 的 Azure 机器学习 SDK](https://aka.ms/aml-sdk) 或 [Azure 门户](https://portal.azure.com/)来管理已部署的模型。
你可以在跟踪模型的试验的同时评估模型指标、重新训练和重新部署模型的新版本。

若要开始使用 Azure 机器学习服务，请参阅[后续步骤](#next-steps)。

## <a name="how-is-azure-machine-learning-service-different-from-machine-learning-studio"></a>Azure 机器学习服务与机器学习工作室有何不同？

[Azure 机器学习工作室](../studio/what-is-ml-studio.md)是一个协作式拖放可视化工作区，无需编写代码即可生成、测试和部署机器学习解决方案。 它使用预生成和预配置的机器学习算法与数据处理模块。

如果想要快速轻松地试验机器学习模型，请使用机器学习工作室，并且内置的机器学习算法足以供你的解决方案使用。

如果你在 Python 环境中工作并且希望更好地控制机器学习算法，或者你想使用开放源代码机器学习库，那么机器学习服务将是你的最佳选择。

> [!NOTE]
> Azure 机器学习服务无法部署或管理在 Azure 机器学习工作室中创建的模型。

## <a name="free-trial"></a>免费试用

如果还没有 Azure 订阅，请在开始前创建免费帐户。 立即试用 [Azure 机器学习服务免费版或付费版](https://aka.ms/AMLFree)。

你将获得可用于 Azure 服务的额度。 信用额度用完后，可以保留该帐户并继续使用[免费的 Azure 服务](https://azure.microsoft.com/free/)。 除非显式更改设置并要求付费，否则不会对信用卡收取任何费用。 或者[激活 MSDN 订户权益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F)，享受每月试用付费版 Azure 服务的信用额度。

## <a name="next-steps"></a>后续步骤

- [创建机器学习服务工作区](setup-create-workspace.md)以开始使用。

- 按照完整的教程进行操作： 
  + [使用 Azure 机器学习服务训练图像分类模型](tutorial-train-models-with-aml.md) 
  + [准备数据并使用自动化机器学习来自动训练回归模型](tutorial-data-prep.md)

- 使用 [Azure 机器学习数据准备 SDK](https://aka.ms/data-prep-sdk) 准备数据。

- 了解[机器学习管道](/azure/machine-learning/service/concept-ml-pipelines)，以便生成、优化和管理机器学习方案。

- 阅读深入的 [Azure 机器学习服务体系结构和概念](concept-azure-machine-learning-architecture.md)文章。

- 有关详细信息，请参阅 [Microsoft 提供的其他机器学习产品](/azure/architecture/data-guide/technology-choices/data-science-and-machine-learning)。
