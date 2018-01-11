---
title: "使用 Microsoft 工具的 Docker 应用程序 DevOps 工作流"
description: "使用 Microsoft 平台的容器化 Docker 应用程序生命周期和使用 Microsoft 工具的 ToolsDevOps 工作流"
keywords: "Docker, 微服务, ASP.NET, 容器"
author: CESARDELATORRE
ms.author: wiwagn
ms.date: 09/22/2017
ms.workload:
- dotnet
- dotnetcore
ms.openlocfilehash: 8539e8c0a6d0c6c9d558b91e062184e7ef135856
ms.sourcegitcommit: e7f04439d78909229506b56935a1105a4149ff3d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2017
---
# <a name="docker-application-devops-workflow-with-microsoft-tools"></a><span data-ttu-id="96350-104">使用 Microsoft 工具的 Docker 应用程序 DevOps 工作流</span><span class="sxs-lookup"><span data-stu-id="96350-104">Docker application DevOps workflow with Microsoft tools</span></span>

<span data-ttu-id="96350-105">Microsoft Visual Studio、Visual Studio Team Services、Team Foundation Server 和 Application Insights 为开发和 IT 运营提供了综合的生态系统，以便为团队提供管理项目和快速生成、测试和部署容器化应用程序的工具。</span><span class="sxs-lookup"><span data-stu-id="96350-105">Microsoft Visual Studio, Visual Studio Team Services, Team Foundation Server, and Application Insights provide a comprehensive ecosystem for development and IT operations that give your team the tools to manage projects and rapidly build, test, and deploy containerized applications.</span></span>

<span data-ttu-id="96350-106">通过 Visual Studio、云中的 Visual Studio Team Services 以及本地 Team Foundation Server，开发团队可以有效地生成、测试和发布面向任何平台（Windows 或 Linux）的容器化应用程序。</span><span class="sxs-lookup"><span data-stu-id="96350-106">With Visual Studio and Visual Studio Team Services in the cloud, along with Team Foundation Server on-premises, development teams can productively build, test, and release containerized applications directed toward any platform (Windows or Linux).</span></span>

<span data-ttu-id="96350-107">Microsoft 工具可以自动完成容器化应用程序（Docker、.NET Core 或与其他平台的任意组合）的具体实现管道，包括全局生成、持续集成 (CI)、使用 Visual Studio Team Services 或 Team Foundation Server 进行测试、持续部署 (CD) 到 Docker 环境（开发、暂存、生产），以及通过 Application Insights 将服务的分析信息传输给开发团队。</span><span class="sxs-lookup"><span data-stu-id="96350-107">Microsoft tools can automate the pipeline for specific implementations of containerized applications—Docker, .NET Core, or any combination with other platforms—from global builds and Continuous Integration (CI) and tests with Visual Studio Team Services or Team Foundation Server, to Continuous Deployment (CD) to Docker environments (Development, Staging, Production), and to transmit analytics information about the services to the development team through Application Insights.</span></span> <span data-ttu-id="96350-108">每个代码提交都能启动生成 (CI) 过程并自动将服务部署到特定的容器化环境 (CD)。</span><span class="sxs-lookup"><span data-stu-id="96350-108">Every code commit can initiate a build (CI) and automatically deploy the services to specific containerized environments (CD).</span></span>

<span data-ttu-id="96350-109">开发者和测试者可以使用 Microsoft Azure 中的模板快速轻松地配置生产环境，如基于 Docker 的开发和测试环境。</span><span class="sxs-lookup"><span data-stu-id="96350-109">Developers and testers can easily and quickly provision production-like development and test environments based on Docker by using templates in Microsoft Azure.</span></span>

<span data-ttu-id="96350-110">容器化应用程序开发的复杂度根据业务复杂度和可伸缩性需要逐步增加。</span><span class="sxs-lookup"><span data-stu-id="96350-110">The complexity of containerized application development increases steadily depending on the business complexity and scalability needs.</span></span> <span data-ttu-id="96350-111">一个很好的示例就是基于微服务体系结构的应用程序。</span><span class="sxs-lookup"><span data-stu-id="96350-111">A good example of this are applications based on microservices architectures.</span></span> <span data-ttu-id="96350-112">要在此类环境中取得成功，你的项目必须在整个生命周期（而不仅是在生成和部署阶段）实现自动化，同时还必须管理版本并收集遥测数据。</span><span class="sxs-lookup"><span data-stu-id="96350-112">To succeed in such an environment, your project must automate the entire life cycle—not only the build and deployment, but it also must manage versions along with the collection of telemetry.</span></span> <span data-ttu-id="96350-113">Visual Studio Team Services 和 Azure 提供了以下功能：</span><span class="sxs-lookup"><span data-stu-id="96350-113">Visual Studio Team Services and Azure offer the following capabilities:</span></span>

-   <span data-ttu-id="96350-114">Visual Studio Team Services/Team Foundation Server 源代码管理（基于 Git 或 Team Foundation 版本控制）、敏捷规划（支持敏捷方法、Scrum 和 CMMI）、CI、发布管理，以及其他适用于敏捷团队的工具。</span><span class="sxs-lookup"><span data-stu-id="96350-114">Visual Studio Team Services/Team Foundation Server source code management (based on Git or Team Foundation Version Control), Agile planning (Agile, Scrum, and CMMI are supported), CI, release management, and other tools for Agile teams.</span></span>

-   <span data-ttu-id="96350-115">Visual Studio Team Services/Team Foundation Server 包括功能强大且不断增长的第一方和第三方扩展生态系统，使用此生态系统可以轻松为微服务构造 CI、生成、测试、交付和发布管理管道。</span><span class="sxs-lookup"><span data-stu-id="96350-115">Visual Studio Team Services/Team Foundation Server include a powerful and growing ecosystem of first- and third-party extensions with which you easily can construct a CI, build, test, delivery, and release management pipeline for microservices.</span></span>

-   <span data-ttu-id="96350-116">在 Visual Studio Team Services 的生成管道中运行自动测试。</span><span class="sxs-lookup"><span data-stu-id="96350-116">Run automated tests as part of your build pipeline in Visual Studio Team Services.</span></span>

-   <span data-ttu-id="96350-117">Visual Studio Team Services 可以通过交付到多个环境（不仅适用于生产环境，还适用于测试环境）缩短 DevOps 生命周期，包括 A/B 试验、[Canary 发布](http://martinfowler.com/bliki/CanaryRelease.html)等。</span><span class="sxs-lookup"><span data-stu-id="96350-117">Visual Studio Team Services can tighten the DevOps life cycle with delivery to multiple environments, not just for production environments, but also for testing, including A/B experimentation, [canary releases](http://martinfowler.com/bliki/CanaryRelease.html), and so on.</span></span>

-   <span data-ttu-id="96350-118">组织可以使用 Azure 资源管理器和熟悉的工具，轻松从 Azure 容器注册表中存储的专用映像配置 Docker 容器以及 Azure 组件（数据、PaaS 等）的任何依赖项。</span><span class="sxs-lookup"><span data-stu-id="96350-118">Organizations easily can provision Docker containers from private images stored in Azure Container Registry along with any dependency on Azure components (Data, PaaS, etc.) using Azure Resource Manager templates with tools with which they are already comfortable working.</span></span>


>[!div class="step-by-step"]
<span data-ttu-id="96350-119">[上一篇] (../design-develop-containerized-apps/set-up-windows-containers-with-powershell.md) [下一篇] (docker-application-outer-loop-devops-workflow.md)</span><span class="sxs-lookup"><span data-stu-id="96350-119">[Previous] (../design-develop-containerized-apps/set-up-windows-containers-with-powershell.md) [Next] (docker-application-outer-loop-devops-workflow.md)</span></span>