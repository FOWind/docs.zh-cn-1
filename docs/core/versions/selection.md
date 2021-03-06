---
title: .NET Core 版本选择
description: 了解 .NET Core 如何查找和选择适用于程序的运行时版本。
author: billwagner
ms.author: wiwagn
ms.date: 06/27/2018
ms.openlocfilehash: 21697aa773abfbd88288d47323402a48c51d69ae
ms.sourcegitcommit: c7f3e2e9d6ead6cc3acd0d66b10a251d0c66e59d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2018
ms.locfileid: "44204859"
---
# <a name="net-core-version-selection"></a>.NET Core 版本选择

[!INCLUDE [topic-appliesto-net-core-2plus](../../../includes/topic-appliesto-net-core-2plus.md)]

本文介绍 .NET Core 工具、SDK 和运行时在选择版本时所使用的策略。 这些策略可通过使用指定版本，使正在运行的应用程序之间达到平衡，同时实现开发人员和最终用户计算机的轻松升级。 这些策略执行以下操作：

- 实现 .NET Core 的轻松高效部署，包括安全性和可靠性更新。
- 使用独立于目标运行时的最新工具和命令。

需要选择版本的情况如下：

- 运行 SDK 命令时，[SDK 使用最新安装的版本](#the-sdk-uses-the-latest-installed-version)。
- 生成程序集时，[目标框架名字对象定义生成时 API](#target-framework-monikers-define-build-time-apis)。
- 运行 .NET Core 应用程序时，[依赖于目标框架的应用程序将前滚](#framework-dependent-apps-roll-forward)。
- 发布独立应用程序时，[独立部署包括所选的运行时](#self-contained-deployments-include-the-selected-runtime)。

本文档其余部分将介绍这四种方案。

## <a name="the-sdk-uses-the-latest-installed-version"></a>SDK 使用最新安装的版本

SDK 命令包括 `dotnet new`、  、或 `dotnet run`。 `dotnet` CLI 必须为所有命令选择 SDK 版本。 .NET Core CLI 默认情况下使用计算机上安装的最新 SDK。 即使处理的项目面向 .NET Core 运行时 2.0，仍将使用 .NET Core SDK v2.1.301（如果已安装）。 使用最新的预览版以及发布版本。 面向较旧的 .NET Core 运行时版本时，可利用最新的 SDK 功能和功能改进。 可在不同项目上面向 .NET Core 的多个运行时版本，同时对所有项目使用相同的 SDK 工具。

在少数情况下，可能需要使用版本较旧的 SDK。 在 [global.json 文件](../tools/global-json.md)中指定该版本。 “使用最新”策略表示仅使用 global.json 指定早于最新安装版本的一个 .NET Core SDK 版本。

可将 global.json 放置在文件层次结构中的任何位置。 CLI 从项目目录中向上搜索其找到的第一个 global.json。 由用户控制对哪些项目应用给定的 global.json（按其在文件系统中的位置）。 .NET CLI 从当前工作目录路径向上导航，以迭代方式搜索 global.json 文件。 找到的第一个 global.json 文件指定要使用的版本。 如果已安装该版本，则使用该版本。 如果未找到 global.json 中指定的 SDK，则 .NET CLI 前滚到安装的最新 SDK。 前滚操作与未找到 global.json 文件时的默认行为相同。

下面的示例演示 global.json 语法：

``` json
{
  "sdk": {
    "version": "2.0.0"
  }
}
```

选择 SDK 版本的过程如下：

1. `dotnet` 从当前工作目录向下导航路径，以迭代方式搜索 global.json 文件。
1. `dotnet` 使用所找到的第一个 global.json 中指定的 SDK。
1. 如果未找到 global.json，`dotnet` 使用最新安装的 SDK。

有关选择 SDK 版本的详细信息，可参阅 global.json 相关文章的[匹配规则](../tools/global-json.md#matching-rules)部分。

## <a name="target-framework-monikers-define-build-time-apis"></a>目标框架名字对象用于定义生成时 API

针对在“目标框架名字对象”(TFM) 中定义的 API 构建项目。 在项目文件中指定[目标框架](../../standard/frameworks.md)。 按如下示例所示，设置项目文件中的 `TargetFramework` 元素：

``` xml
<TargetFramework>netcoreapp2.0</TargetFramework>
```

可能会针对多个 TFM 构建项目。 对库设置多个目标框架更为常见，但也可对应用程序执行此操作。 指定 `TargetFrameworks` 属性（`TargetFramework` 的复数形式）。 目标框架以分号分隔，如下例所示：

``` xml
<TargetFrameworks>netcoreapp2.0;net47</TargetFrameworks>
```

给定的 SDK 支持固定的一组框架，其中的上限框架为 SDK 附带的运行时的目标框架。 例如，.NET Core 2.0 SDK 包含 .NET Core 2.0 运行时，该运行时是 `netcoreapp2.0` 目标框架的一个实现。 .NET Core 2.0 SDK 支持 `netcoreapp1.0`、`netcoreapp1.1` 和 `netcoreapp2.0`，但不支持 `netcoreapp2.1`（或更高版本）。 安装 .NET Core 2.1 SDK 以针对 `netcoreapp2.1` 进行构建。

.NET Standard 目标框架中的上限框架同样是 SDK 附带的运行时的目标框架。 .NET Core 2.0 SDK 的上限为 `netstandard2.0`。

## <a name="framework-dependent-apps-roll-forward"></a>依赖于框架的应用会前滚

使用 [`dotnet run`](../tools/dotnet-run.md) 从源运行应用程序。 `dotnet run` 可生成和运行应用程序。 `dotnet` 可执行文件是开发环境中的应用程序的主机。

该主机选择计算机上安装的最新修补程序版本。 例如，如果在项目文件中指定 `netcoreapp2.0`，并且 `2.0.4` 是安装的最新 .NET 运行时，则使用 `2.0.4` 运行时。

如果未找到可接受的 `2.0.*` 版本，则使用新的 `2.*` 版本。 例如，如果指定了 `netcoreapp2.0` 并且仅安装了 `2.1.0`，则应用程序在运行时使用 `2.1.0` 运行时。 此行为称为“次要版本前滚”。 此外，不会考虑较低版本。 如果未安装可接受的运行时，应用程序将不会运行。

以下几个用法示例演示了此行为：

- 2.0.4 是必需的。 2.0.5 是安装的最高修补程序版本。 则使用 2.0.5。
- 2.0.4 是必需的。 未安装 2.0.* 版本。 1.1.1 是安装的最高运行时版本。 会显示一条错误消息。
- 2.0.4 是必需的。 2.0.0 是安装的最高版本。 会显示一条错误消息。
- 2.0.4 是必需的。 未安装 2.0.* 版本。 2.2.2 是安装的最高 2.x 运行时版本。 则使用 2.2.2。
- 2.0.4 是必需的。 未安装 2.x 版本。 已安装 3.0.0（不是当前可用的版本）。 会显示一条错误消息。

次要版本回滚会产生一个可能影响最终用户的副作用。 请参考以下方案：

- 2.0.4 是必需的。 未安装 2.0.* 版本。 已安装 2.2.2。 则使用 2.2.2。
- 后期安装了 2.0.5。 则 2.0.5 将用于后续应用程序启动，而不是 2.2.2。 与更高的次要版本相比，更倾向使用所需次要版本的最新修补程序。
- 2.0.5 和 2.2.2 可能具有不同行为，序列化二进制数据等方案中尤其如此。

## <a name="self-contained-deployments-include-the-selected-runtime"></a>独立部署包括所选的运行时

可以将应用程序作为[独立分发](../deploying/index.md#self-contained-deployments-scd)进行发布。 此方法可将 .NET Core 运行时和库与应用程序进行捆绑。 独立部署不具有对运行时环境的依赖关系。 在发布时（而不是运行时）选择运行时版本。

发布进程将选择给定运行时系列中的最新修补程序版本。 例如，`dotnet publish` 将选择 .NET Core 2.0.4（如果它是 .NET Core 2.0 运行时系列中的最新修补程序版本）。 目标框架（包括最新安装的安全修补程序）与应用程序捆绑打包。

如果为应用程序指定的最新版本不满足要求，会出现错误。 `dotnet publish` 绑定到最新的运行时修补程序版本（在给定的主要及次要版本系列内）。 `dotnet publish` 不支持 `dotnet run` 的前滚语义。 有关修补程序和独立部署的详细信息，请参阅有关 .NET Core 应用程序部署中[运行时修补程序选择](../deploying/runtime-patch-selection.md)的文章。

独立部署可能需要特定修补程序版本。 可以重写项目文件中的最低运行时修补程序版本（重写为更高或更低版本），如下例所示：

``` xml
<RuntimeFrameworkVersion>2.0.4</RuntimeFrameworkVersion>
```

`RuntimeFrameworkVersion` 元素重写默认版本策略。 对于独立部署，`RuntimeFrameworkVersion` 指定确切的运行时框架版本。 对于依赖于框架的应用程序，`RuntimeFrameworkVersion` 指定所需的最低运行时框架版本。
