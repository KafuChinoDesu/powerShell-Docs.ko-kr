---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: DSC를 사용하여 연속 통합 및 연속 배포 파이프라인 빌드
ms.openlocfilehash: a3803a8e6fe6ff1b93758a73ccd54754d7bb2a84
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
---
# <a name="building-a-continuous-integration-and-continuous-deployment-pipeline-with-dsc"></a><span data-ttu-id="22f12-103">DSC를 사용하여 연속 통합 및 연속 배포 파이프라인 빌드</span><span class="sxs-lookup"><span data-stu-id="22f12-103">Building a Continuous Integration and Continuous Deployment pipeline with DSC</span></span>

<span data-ttu-id="22f12-104">이 예제에는 PowerShell, DSC, Pester 및 Visual Studio TFS(Team Foundation Server)를 사용하여 CI/CD(연속 통합/연속 배포) 파이프라인을 빌드하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-104">This example demonstrates how to build a Continuous Integration/Continuous Deployment (CI/CD) pipeline by using PowerShell, DSC, Pester, and Visual Studio Team Foundation Server (TFS).</span></span>

<span data-ttu-id="22f12-105">빌드 및 구성한 파이프라인은 DNS 서버와 관련 호스트 레코드를 완전하게 배포, 구성 및 테스트하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-105">After the pipeline is built and configured, you can use it to fully deploy, configure and test a DNS server and associated host records.</span></span>
<span data-ttu-id="22f12-106">이 프로세스에서는 개발 환경에서 사용되는 파이프라인의 첫 부분을 시뮬레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-106">This process simulates the first part of a pipeline that would be used in a development environment.</span></span>

<span data-ttu-id="22f12-107">자동화된 CI/CD 파이프라인을 사용하면 소프트웨어를 보다 안정적이며 빠르게 업데이트할 수 있으며, 모든 코드를 테스트하고 코드의 최신 빌드를 항상 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-107">An automated CI/CD pipeline helps you update software faster and more reliably, ensuring that all code is tested, and that a current build of your code is available at all times.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22f12-108">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="22f12-108">Prerequisites</span></span>

<span data-ttu-id="22f12-109">이 예제를 사용하려면 다음에 대해 잘 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-109">To use this example, you should be familiar with the following:</span></span>

- <span data-ttu-id="22f12-110">CI-CD 개념.</span><span class="sxs-lookup"><span data-stu-id="22f12-110">CI-CD concepts.</span></span> <span data-ttu-id="22f12-111">[릴리스 파이프라인 모델](http://aka.ms/thereleasepipelinemodelpdf)에서 유용한 참조 정보를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-111">A good reference can be found at [The Release Pipeline Model](http://aka.ms/thereleasepipelinemodelpdf).</span></span>
- <span data-ttu-id="22f12-112">[Git](https://git-scm.com/) 소스 제어</span><span class="sxs-lookup"><span data-stu-id="22f12-112">[Git](https://git-scm.com/) source control</span></span>
- <span data-ttu-id="22f12-113">[Pester](https://github.com/pester/Pester) 테스트 프레임워크</span><span class="sxs-lookup"><span data-stu-id="22f12-113">The [Pester](https://github.com/pester/Pester) testing framework</span></span>
- [<span data-ttu-id="22f12-114">Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="22f12-114">Team Foundation Server</span></span>](https://www.visualstudio.com/tfs/)

## <a name="what-you-will-need"></a><span data-ttu-id="22f12-115">필요한 사항</span><span class="sxs-lookup"><span data-stu-id="22f12-115">What you will need</span></span>

<span data-ttu-id="22f12-116">이 예제를 빌드하고 실행하려면 여러 컴퓨터 및/또는 가상 컴퓨터가 포함된 환경이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-116">To build and run this example, you will need an environment with several computers and/or virtual machines.</span></span>

### <a name="client"></a><span data-ttu-id="22f12-117">Client</span><span class="sxs-lookup"><span data-stu-id="22f12-117">Client</span></span>

<span data-ttu-id="22f12-118">예제를 설정하고 실행하는 모든 작업을 수행할 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-118">This is the computer where you'll do all of the work setting up and running the example.</span></span>

<span data-ttu-id="22f12-119">클라이언트 컴퓨터는 다음 항목이 설치된 Windows 컴퓨터여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-119">The client computer must be a Windows computer with the following installed:</span></span>
- [<span data-ttu-id="22f12-120">Git</span><span class="sxs-lookup"><span data-stu-id="22f12-120">Git</span></span>](https://git-scm.com/)
- <span data-ttu-id="22f12-121">https://github.com/PowerShell/Demo_CI에서 복제된 로컬 Git 리포지토리</span><span class="sxs-lookup"><span data-stu-id="22f12-121">a local git repo cloned from https://github.com/PowerShell/Demo_CI</span></span>
- <span data-ttu-id="22f12-122">[Visual Studio Code](https://code.visualstudio.com/)와 같은 텍스트 편집기</span><span class="sxs-lookup"><span data-stu-id="22f12-122">a text editor, such as [Visual Studio Code](https://code.visualstudio.com/)</span></span>

### <a name="tfssrv1"></a><span data-ttu-id="22f12-123">TFSSrv1</span><span class="sxs-lookup"><span data-stu-id="22f12-123">TFSSrv1</span></span>

<span data-ttu-id="22f12-124">빌드와 릴리스를 정의할 TFS 서버를 호스트하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-124">The computer that hosts the TFS server where you will define your build and release.</span></span>
<span data-ttu-id="22f12-125">이 컴퓨터에는 [Team Foundation Server 2017](https://www.visualstudio.com/tfs/)이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-125">This computer must have [Team Foundation Server 2017](https://www.visualstudio.com/tfs/) installed.</span></span>

### <a name="buildagent"></a><span data-ttu-id="22f12-126">BuildAgent</span><span class="sxs-lookup"><span data-stu-id="22f12-126">BuildAgent</span></span>

<span data-ttu-id="22f12-127">프로젝트를 빌드하는 Windows 빌드 에이전트를 실행할 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-127">The computer that runs the Windows build agent that builds the project.</span></span>
<span data-ttu-id="22f12-128">이 컴퓨터에는 빌드 에이전트가 설치되어 있으며 실행 중이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-128">This computer must have a Windows build agent installed and running.</span></span>
<span data-ttu-id="22f12-129">Windows 빌드 에이전트를 설치하고 실행하는 방법에 대한 지침은 [Windows에서 에이전트 배포](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22f12-129">See [Deploy an agent on Windows](https://www.visualstudio.com/en-us/docs/build/actions/agents/v2-windows) for instructions on how to install and run a Windows build agent.</span></span>

<span data-ttu-id="22f12-130">또한 이 컴퓨터에는 `xDnsServer` 및 `xNetworking` DSC 모듈을 둘 다 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-130">You also need to install both the `xDnsServer` and `xNetworking` DSC modules on this computer.</span></span>

### <a name="testagent1"></a><span data-ttu-id="22f12-131">TestAgent1</span><span class="sxs-lookup"><span data-stu-id="22f12-131">TestAgent1</span></span>

<span data-ttu-id="22f12-132">이 예제에서 DSC 구성을 통해 DNS 서버로 구성하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-132">This is the computer that is configured as a DNS server by the DSC configuration in this example.</span></span>
<span data-ttu-id="22f12-133">이 컴퓨터에서는 [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016)을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-133">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

### <a name="testagent2"></a><span data-ttu-id="22f12-134">TestAgent2</span><span class="sxs-lookup"><span data-stu-id="22f12-134">TestAgent2</span></span>

<span data-ttu-id="22f12-135">이 예제에서 구성하는 웹 사이트를 호스트하는 컴퓨터입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-135">This is the computer that hosts the website this example configures.</span></span>
<span data-ttu-id="22f12-136">이 컴퓨터에서는 [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016)을 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-136">The computer must be running [Windows Server 2016](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016).</span></span>

## <a name="add-the-code-to-tfs"></a><span data-ttu-id="22f12-137">TFS에 코드 추가</span><span class="sxs-lookup"><span data-stu-id="22f12-137">Add the code to TFS</span></span>

<span data-ttu-id="22f12-138">먼저 TFS에서 Git 리포지토리를 만들고 클라이언트 컴퓨터의 로컬 리포지토리에서 코드를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-138">We'll start out by creating a Git repository in TFS, and importing the code from your local repository on the client computer.</span></span>
<span data-ttu-id="22f12-139">클라이언트 컴퓨터에 Demo_CI 리포지토리를 아직 복제하지 않은 경우 다음 git 명령을 실행하여 지금 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-139">If you have not already cloned the Demo_CI repository to your client computer, do so now by running the following git command:</span></span>

`git clone https://github.com/PowerShell/Demo_CI`

1. <span data-ttu-id="22f12-140">클라이언트 컴퓨터의 웹 브라우저에서 TFS 서버로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-140">On your client computer, navigate to your TFS server in a web browser.</span></span>
1. <span data-ttu-id="22f12-141">TFS에서 Demo_CI라는 [새 팀 프로젝트를 만듭니다](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project).</span><span class="sxs-lookup"><span data-stu-id="22f12-141">In TFS, [Create a new team project](https://www.visualstudio.com/en-us/docs/setup-admin/create-team-project) named Demo_CI.</span></span>

    <span data-ttu-id="22f12-142">**버전 제어**가 **Git**으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-142">Make sure that **Version control** is set to **Git**.</span></span>
1. <span data-ttu-id="22f12-143">클라이언트 컴퓨터에서 다음 명령을 사용하여 방금 TFS에서 만든 리포지토리에 remote를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-143">On your client computer, add a remote to the repository you just created in TFS with the following command:</span></span>

    `git remote add tfs <YourTFSRepoURL>`

    <span data-ttu-id="22f12-144">여기서 `<YourTFSRepoURL>`은 이전 단계에서 만든 TFS 리포지토리의 복제 URL입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-144">Where `<YourTFSRepoURL>` is the clone URL to the TFS repository you created in the previous step.</span></span>

    <span data-ttu-id="22f12-145">이 URL을 확인할 수 있는 위치를 모르는 경우 [기존 Git 리포지토리 복제](https://www.visualstudio.com/en-us/docs/git/tutorial/clone)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22f12-145">If you don't know where to find this URL, see [Clone an existing Git repo](https://www.visualstudio.com/en-us/docs/git/tutorial/clone).</span></span>
1. <span data-ttu-id="22f12-146">다음 명령을 사용하여 로컬 리포지토리의 코드를 TFS 리포지토리로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-146">Push the code from your local repository to your TFS repository with the following command:</span></span>

    `git push tfs --all`
1. <span data-ttu-id="22f12-147">TFS 리포지토리에 Demo_CI 코드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-147">The TFS repository will be populated with the Demo_CI code.</span></span>

><span data-ttu-id="22f12-148">**참고:** 이 예제에서는 Git 리포지토리의 `ci-cd-example` 분기에 있는 코드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-148">**Note:** This example uses the code in the `ci-cd-example` branch of the Git repo.</span></span>
><span data-ttu-id="22f12-149">TFS 프로젝트에서, 그리고 작성하는 CI/CD 트리거에 대해 이 분기를 기본 분기로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-149">Be sure to specify this branch as the default branch in your TFS project, and for the CI/CD triggers you create.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="22f12-150">코드 파악</span><span class="sxs-lookup"><span data-stu-id="22f12-150">Understanding the code</span></span>

<span data-ttu-id="22f12-151">빌드 및 배포 파이프라인을 만들기 전에 몇 가지 코드를 확인하여 수행되는 작업을 파악해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-151">Before we create the build and deployment pipelines, let's look at some of the code to understand what is going on.</span></span>
<span data-ttu-id="22f12-152">클라이언트 컴퓨터에서 자주 사용하는 텍스트 편집기를 열고 Demo_CI Git 리포지토리의 루트로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-152">On your client computer, open your favorite text editor and navigate to the root of your Demo_CI Git repository.</span></span>

### <a name="the-dsc-configuration"></a><span data-ttu-id="22f12-153">DSC 구성</span><span class="sxs-lookup"><span data-stu-id="22f12-153">The DSC configuration</span></span>

<span data-ttu-id="22f12-154">로컬 Demo_CI 리포지토리의 루트에서 `DNSServer.ps1` 파일을 엽니다(`./InfraDNS/Configs/DNSServer.ps1`).</span><span class="sxs-lookup"><span data-stu-id="22f12-154">Open the file `DNSServer.ps1` (from the root of the local Demo_CI repository, `./InfraDNS/Configs/DNSServer.ps1`).</span></span>

<span data-ttu-id="22f12-155">이 파일에는 DNS 서버를 설정하는 DSC 구성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-155">This file contains the DSC configuration that sets up the DNS server.</span></span> <span data-ttu-id="22f12-156">전체 구성은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-156">Here it is in its entirety:</span></span>

```powershell
configuration DNSServer
{
    Import-DscResource -module 'xDnsServer','xNetworking', 'PSDesiredStateConfiguration'

    Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
    {
        WindowsFeature DNS
        {
            Ensure  = 'Present'
            Name    = 'DNS'
        }

        xDnsServerPrimaryZone $Node.zone
        {
            Ensure    = 'Present'
            Name      = $Node.Zone
            DependsOn = '[WindowsFeature]DNS'
        }

        foreach ($ARec in $Node.ARecords.keys) {
            xDnsRecord $ARec
            {
                Ensure    = 'Present'
                Name      = $ARec
                Zone      = $Node.Zone
                Type      = 'ARecord'
                Target    = $Node.ARecords[$ARec]
                DependsOn = '[WindowsFeature]DNS'
            }
        }

        foreach ($CName in $Node.CNameRecords.keys) {
            xDnsRecord $CName
            {
                Ensure    = 'Present'
                Name      = $CName
                Zone      = $Node.Zone
                Type      = 'CName'
                Target    = $Node.CNameRecords[$CName]
                DependsOn = '[WindowsFeature]DNS'
            }
        }
    }
}
```

<span data-ttu-id="22f12-157">아래의 `Node` 문을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="22f12-157">Notice the `Node` statement:</span></span>

```powershell
Node $AllNodes.Where{$_.Role -eq 'DNSServer'}.NodeName
```

<span data-ttu-id="22f12-158">이 문은 `DevEnv.ps1` 스크립트를 통해 작성되는 [구성 데이터](configData.md)에서 역할이 `DNSServer`로 정의된 노드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-158">This finds any nodes that were defined as having a role of `DNSServer` in the [configuration data](configData.md), which is created by the `DevEnv.ps1` script.</span></span>

<span data-ttu-id="22f12-159">CI 수행 시에는 구성 데이터를 사용하여 노드를 정의해야 합니다. 노드 정보는 환경 간에 변경될 가능성이 높은데, 구성 데이터를 사용하면 구성 코드를 변경하지 않고도 노드 정보를 쉽게 변경할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-159">Using configuration data to define nodes is important when doing CI because node information will likely change between environments, and using configuration data allows you to easily make changes to node information without changing the configuration code.</span></span>

<span data-ttu-id="22f12-160">첫 번째 리소스 블록에서 구성은 [WindowsFeature](windowsFeatureResource.md)를 호출하여 DNS 기능이 사용하도록 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-160">In the first resource block, the configuration calls the [WindowsFeature](windowsFeatureResource.md) to ensure that the DNS feature is enabled.</span></span>
<span data-ttu-id="22f12-161">그 다음 리소스 블록은 [xDnsServer](https://github.com/PowerShell/xDnsServer) 모듈의 리소스를 호출하여 주 영역 및 DNS 레코드를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-161">The resource blocks that follow call resources from the [xDnsServer](https://github.com/PowerShell/xDnsServer) module to configure the primary zone and DNS records.</span></span>

<span data-ttu-id="22f12-162">두 `xDnsRecord` 블록은 구성 데이터의 배열에서 반복되는 `foreach` 루프에 래핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-162">Notice that the two `xDnsRecord` blocks are wrapped in `foreach` loops that iterate through arrays in the configuration data.</span></span>
<span data-ttu-id="22f12-163">이 구성 데이터 역시 `DevEnv.ps1` 스크립트를 통해 작성됩니다. 다음으로는 구성 데이터에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-163">Again, the configuration data is created by the `DevEnv.ps1` script, which we'll look at next.</span></span>

### <a name="configuration-data"></a><span data-ttu-id="22f12-164">구성 데이터</span><span class="sxs-lookup"><span data-stu-id="22f12-164">Configuration data</span></span>

<span data-ttu-id="22f12-165">로컬 Demo_CI 리포지토리의 `DevEnv.ps1` 파일(`./InfraDNS/DevEnv.ps1`)은 해시 테이블에서 환경별 구성 데이터를 지정한 다음 `DscPipelineTools.psm`(`./Assets/DscPipelineTools/DscPipelineTools.psm1`)에 정의된 `New-DscConfigurationDataDocument` 함수 호출로 해당 해시 테이블을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-165">The `DevEnv.ps1` file (from the root of the local Demo_CI repository, `./InfraDNS/DevEnv.ps1`) specifies the environment-specific configuration data in a hashtable, and then passes that hashtable to a call to the `New-DscConfigurationDataDocument` function, which is defined in `DscPipelineTools.psm` (`./Assets/DscPipelineTools/DscPipelineTools.psm1`).</span></span>

<span data-ttu-id="22f12-166">`DevEnv.ps1` 파일은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-166">The `DevEnv.ps1` file:</span></span>

```powershell
param(
    [parameter(Mandatory=$true)]
    [string]
    $OutputPath
)

Import-Module $PSScriptRoot\..\Assets\DscPipelineTools\DscPipelineTools.psd1 -Force

# Define Unit Test Environment
$DevEnvironment = @{
    Name                        = 'DevEnv';
    Roles = @(
        @{  Role                = 'DNSServer';
            VMName              = 'TestAgent1';
            Zone                = 'Contoso.com';
            ARecords            = @{'TFSSrv1'= '10.0.0.10';'Client'='10.0.0.15';'BuildAgent'='10.0.0.30';'TestAgent1'='10.0.0.40';'TestAgent2'='10.0.0.50'};
            CNameRecords        = @{'DNS' = 'TestAgent1.contoso.com'};
        }
    )
}

Return New-DscConfigurationDataDocument -RawEnvData $DevEnvironment -OutputPath $OutputPath
```

<span data-ttu-id="22f12-167">`\Assets\DscPipelineTools\DscPipelineTools.psm1`에 정의된 `New-DscConfigurationDataDocument` 함수는 `RawEnvData` 및 `OtherEnvData` 매개 변수로 전달되는 해시 테이블(노드 데이터) 및 배열(비노드 데이터)에서 구성 데이터 문서를 프로그래밍 방식으로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-167">The `New-DscConfigurationDataDocument` function (defined in `\Assets\DscPipelineTools\DscPipelineTools.psm1`) programmatically creates a configuration data document from the hashtable (node data) and array (non-node data) that are passed as the `RawEnvData` and `OtherEnvData` parameters.</span></span>

<span data-ttu-id="22f12-168">이 예제에서는 `RawEnvData` 매개 변수만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-168">In our case, only the `RawEnvData` parameter is used.</span></span>

### <a name="the-psake-build-script"></a><span data-ttu-id="22f12-169">psake 빌드 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-169">The psake build script</span></span>

<span data-ttu-id="22f12-170">Demo_CI 리포지토리 루트(`./InfraDNS/Build.ps1`)의 `Build.ps1`에 정의된 [psake](https://github.com/psake/psake) 빌드 스크립트는 빌드의 일부분인 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-170">The [psake](https://github.com/psake/psake) build script defined in `Build.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Build.ps1`) defines tasks that are part of the build.</span></span>
<span data-ttu-id="22f12-171">또한 각 작업이 사용하는 다른 작업도 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-171">It also defines which other tasks each task depends on.</span></span>
<span data-ttu-id="22f12-172">psake 스크립트는 호출 시 지정된 작업(작업이 지정되지 않은 경우 이름이 `Default`인 작업)이 실행되는지와 모든 종속성도 실행되는지를 확인합니다. 즉, 재귀적인 방식으로 종속성, 종속성의 종속성 등이 모두 실행되는지를 순차적으로 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-172">When invoked, the psake script ensures that the specified task (or the task named `Default` if none is specified) runs, and that all dependencies also run (this is recursive, so that dependencies of dependencies run, and so on).</span></span>

<span data-ttu-id="22f12-173">이 예제에서 `Default` 작업은 다음과 같이 정의됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-173">In this example, the `Default` task is defined as:</span></span>

```powershell
Task Default -depends UnitTests
```

<span data-ttu-id="22f12-174">`Default` 작업 자체의 구현은 없으며 `CompileConfigs` 작업에 대한 종속성만 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-174">The `Default` task has no implementation itself, but has a dependency on the `CompileConfigs` task.</span></span>
<span data-ttu-id="22f12-175">작업 종속성의 결과 체인은 빌드 스크립트의 모든 작업이 실행되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-175">The resulting chain of task dependencies ensures that all tasks in the build script are run.</span></span>

<span data-ttu-id="22f12-176">이 예제에서는 Demo_CI 리포지토리의 루트에 있는 `Initiate.ps1` 파일에서 `Invoke-PSake`를 호출하여 psake 스크립트를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-176">In this example, the psake script is invoked by a call to `Invoke-PSake` in the `Initiate.ps1` file (located at the root of the Demo_CI repository):</span></span>

```powershell
param(
    [parameter()]
    [ValidateSet('Build','Deploy')]
    [string]
    $fileName
)

#$Error.Clear()

Invoke-PSake $PSScriptRoot\InfraDNS\$fileName.ps1

<#if($Error.count)
{
    Throw "$fileName script failed. Check logs for failure details."
}
#>
```

<span data-ttu-id="22f12-177">TFS에서 예제용 빌드 정의를 작성할 때 이 스크립트의 `fileName` 매개 변수로 psake 스크립트 파일을 제공할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-177">When we create the build definition for our example in TFS, we will supply our psake script file as the `fileName` parameter for this script.</span></span>

<span data-ttu-id="22f12-178">빌드 스크립트는 다음과 같은 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-178">The build script defines the following tasks:</span></span>

#### <a name="generateenvironmentfiles"></a><span data-ttu-id="22f12-179">GenerateEnvironmentFiles</span><span class="sxs-lookup"><span data-stu-id="22f12-179">GenerateEnvironmentFiles</span></span>

<span data-ttu-id="22f12-180">구성 데이터 파일을 생성하는 `DevEnv.ps1`을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-180">Runs `DevEnv.ps1`, which generates the configuration data file.</span></span>

#### <a name="installmodules"></a><span data-ttu-id="22f12-181">InstallModules</span><span class="sxs-lookup"><span data-stu-id="22f12-181">InstallModules</span></span>

<span data-ttu-id="22f12-182">구성 `DNSServer.ps1`에 필요한 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-182">Installs the modules required by the configuration `DNSServer.ps1`.</span></span>

#### <a name="scriptanalysis"></a><span data-ttu-id="22f12-183">ScriptAnalysis</span><span class="sxs-lookup"><span data-stu-id="22f12-183">ScriptAnalysis</span></span>

<span data-ttu-id="22f12-184">[PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer)를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-184">Calls the [PSScriptAnalyzer](https://github.com/PowerShell/PSScriptAnalyzer).</span></span>

#### <a name="unittests"></a><span data-ttu-id="22f12-185">UnitTests</span><span class="sxs-lookup"><span data-stu-id="22f12-185">UnitTests</span></span>

<span data-ttu-id="22f12-186">[Pester](https://github.com/pester/Pester/wiki) 단위 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-186">Runs the [Pester](https://github.com/pester/Pester/wiki) unit tests.</span></span>

#### <a name="compileconfigs"></a><span data-ttu-id="22f12-187">CompileConfigs</span><span class="sxs-lookup"><span data-stu-id="22f12-187">CompileConfigs</span></span>

<span data-ttu-id="22f12-188">`GenerateEnvironmentFiles` 작업을 통해 생성된 구성 데이터를 사용하여 구성(`DNSServer.ps1`)을 MOF 파일로 컴파일합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-188">Compiles the configuration (`DNSServer.ps1`) into a MOF file, using the configuration data generated by the `GenerateEnvironmentFiles` task.</span></span>

#### <a name="clean"></a><span data-ttu-id="22f12-189">정리</span><span class="sxs-lookup"><span data-stu-id="22f12-189">Clean</span></span>

<span data-ttu-id="22f12-190">예제에 사용되는 폴더를 만들고 이전 실행의 테스트 결과, 구성 데이터 파일 및 모듈을 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-190">Creates the folders used for the example, and removes any test results, configuration data files, and modules from previous runs.</span></span>

### <a name="the-psake-deploy-script"></a><span data-ttu-id="22f12-191">psake 배포 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-191">The psake deploy script</span></span>

<span data-ttu-id="22f12-192">Demo_CI 리포지토리 루트(`./InfraDNS/Deploy.ps1`)의 `Deploy.ps1`에 정의된 [psake](https://github.com/psake/psake) 배포 스크립트는 구성을 배포하고 실행하는 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-192">The [psake](https://github.com/psake/psake) deployment script defined in `Deploy.ps1` (from the root of the Demo_CI repository, `./InfraDNS/Deploy.ps1`) defines tasks that deploy and run the configuration.</span></span>

<span data-ttu-id="22f12-193">`Deploy.ps1`은 다음 작업을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-193">`Deploy.ps1` defines the following tasks:</span></span>

#### <a name="deploymodules"></a><span data-ttu-id="22f12-194">DeployModules</span><span class="sxs-lookup"><span data-stu-id="22f12-194">DeployModules</span></span>

<span data-ttu-id="22f12-195">`TestAgent1`에서 PowerShell 세션을 시작하고 구성에 필요한 DSC 리소스가 포함된 모듈을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-195">Starts a PowerShell session on `TestAgent1` and installs the modules containing the DSC resources required for the configuration.</span></span>

#### <a name="deployconfigs"></a><span data-ttu-id="22f12-196">DeployConfigs</span><span class="sxs-lookup"><span data-stu-id="22f12-196">DeployConfigs</span></span>

<span data-ttu-id="22f12-197">[Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) cmdlet을 호출하여 `TestAgent1`에서 구성을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-197">Calls the [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration.md) cmdlet to run the configuration on `TestAgent1`.</span></span>

#### <a name="integrationtests"></a><span data-ttu-id="22f12-198">IntegrationTests</span><span class="sxs-lookup"><span data-stu-id="22f12-198">IntegrationTests</span></span>

<span data-ttu-id="22f12-199">[Pester](https://github.com/pester/Pester/wiki) 통합 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-199">Runs the [Pester](https://github.com/pester/Pester/wiki) integration tests.</span></span>

#### <a name="acceptancetests"></a><span data-ttu-id="22f12-200">AcceptanceTests</span><span class="sxs-lookup"><span data-stu-id="22f12-200">AcceptanceTests</span></span>

<span data-ttu-id="22f12-201">[Pester](https://github.com/pester/Pester/wiki) 수용 테스트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-201">Runs the [Pester](https://github.com/pester/Pester/wiki) acceptance tests.</span></span>

#### <a name="clean"></a><span data-ttu-id="22f12-202">정리</span><span class="sxs-lookup"><span data-stu-id="22f12-202">Clean</span></span>

<span data-ttu-id="22f12-203">이전 실행에서 설치된 모듈을 제거하고 테스트 결과 폴더가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-203">Removes any modules installed in previous runs, and ensures that the test result folder exists.</span></span>

### <a name="test-scripts"></a><span data-ttu-id="22f12-204">테스트 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-204">Test scripts</span></span>

<span data-ttu-id="22f12-205">수용, 통합 및 단위 테스트는 Demo_CI 리포지토리 루트의 `Tests` 폴더(`./InfraDNS/Tests`)에서 정의되며 각각 해당 폴더의 `DNSServer.tests.ps1` 파일에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-205">Acceptance, Integration, and Unit tests are defined in scripts in the `Tests` folder (from the root of the Demo_CI repository, `./InfraDNS/Tests`), each in files named `DNSServer.tests.ps1` in their respective folders.</span></span>

<span data-ttu-id="22f12-206">테스트 스크립트는 [Pester](https://github.com/pester/Pester/wiki) 및 [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-206">The test scripts use [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="unit-tests"></a><span data-ttu-id="22f12-207">단위 테스트</span><span class="sxs-lookup"><span data-stu-id="22f12-207">Unit tests</span></span>

<span data-ttu-id="22f12-208">단위 테스트에서는 DSC 구성 자체를 테스트하여 구성을 실행하면 필요한 작업이 수행되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-208">The unit tests test the DSC configurations themselves to ensure that the configurations will do what is expected when they run.</span></span>
<span data-ttu-id="22f12-209">단위 테스트 스크립트는 [Pester](https://github.com/pester/Pester/wiki)를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-209">The unit test script uses [Pester](https://github.com/pester/Pester/wiki).</span></span>

#### <a name="integration-tests"></a><span data-ttu-id="22f12-210">통합 테스트</span><span class="sxs-lookup"><span data-stu-id="22f12-210">Integration tests</span></span>

<span data-ttu-id="22f12-211">통합 테스트에서는 시스템 구성을 테스트하여 다른 구성 요소와 통합하는 경우 시스템이 올바르게 구성되는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-211">The integration tests test the configuration of the system to ensure that when integrated with other components, the system is configured as expected.</span></span> <span data-ttu-id="22f12-212">이러한 테스트는 DSC를 통해 구성된 대상 노드에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-212">These tests run on the target node after it has been configured with DSC.</span></span>
<span data-ttu-id="22f12-213">통합 테스트 스크립트는 [Pester](https://github.com/pester/Pester/wiki) 및 [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) 구문을 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-213">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

#### <a name="acceptance-tests"></a><span data-ttu-id="22f12-214">수용 테스트</span><span class="sxs-lookup"><span data-stu-id="22f12-214">Acceptance tests</span></span>

<span data-ttu-id="22f12-215">수용 테스트에서는 시스템을 테스트하여 정상적으로 동작하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-215">Acceptance tests test the system to ensure that it behaves as expected.</span></span>
<span data-ttu-id="22f12-216">예를 들어 웹 페이지 쿼리 시 올바른 정보가 반환되는지를 테스트하여 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-216">For example, it tests to ensure a web page returns the right information when queried.</span></span>
<span data-ttu-id="22f12-217">이러한 테스트는 실제 시나리오를 테스트하기 위해 대상 노드에서 원격으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-217">These tests run remotely from the target node in order to test real world scenarios.</span></span>
<span data-ttu-id="22f12-218">통합 테스트 스크립트는 [Pester](https://github.com/pester/Pester/wiki) 및 [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) 구문을 함께 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-218">The integration test script uses a mixture of [Pester](https://github.com/pester/Pester/wiki) and [PoshSpec](https://github.com/Ticketmaster/poshspec/wiki/Introduction) syntax.</span></span>

## <a name="define-the-build"></a><span data-ttu-id="22f12-219">빌드 정의</span><span class="sxs-lookup"><span data-stu-id="22f12-219">Define the build</span></span>

<span data-ttu-id="22f12-220">지금까지 코드를 TFS에 업로드하고 코드가 수행하는 작업을 살펴보았습니다. 그러면 이제 빌드를 정의해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-220">Now that we've uploaded our code to TFS and looked at what it does, let's define our build.</span></span>

<span data-ttu-id="22f12-221">여기서는 빌드에 추가할 빌드 단계에 대해서만 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-221">Here, we'll cover only the build steps that you'll add to the build.</span></span> <span data-ttu-id="22f12-222">TFS에서 빌드 정의를 작성하는 방법에 대한 지침은 [빌드 정의 만들기 및 큐에 넣기](https://www.visualstudio.com/en-us/docs/build/define/create)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="22f12-222">For instructions on how to create a build definition in TFS, see [Create and queue a build definition](https://www.visualstudio.com/en-us/docs/build/define/create).</span></span>

<span data-ttu-id="22f12-223">**빈** 템플릿을 선택하여 새 빌드 정의 "InfraDNS"를 만들고</span><span class="sxs-lookup"><span data-stu-id="22f12-223">Create a new build definition (select the **Empty** template) named "InfraDNS".</span></span>
<span data-ttu-id="22f12-224">빌드 정의에 다음 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-224">Add the following steps to you build definition:</span></span>

- <span data-ttu-id="22f12-225">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-225">PowerShell Script</span></span>
- <span data-ttu-id="22f12-226">테스트 결과 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-226">Publish Test Results</span></span>
- <span data-ttu-id="22f12-227">파일 복사</span><span class="sxs-lookup"><span data-stu-id="22f12-227">Copy Files</span></span>
- <span data-ttu-id="22f12-228">아티팩트 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-228">Publish Artifact</span></span>

<span data-ttu-id="22f12-229">이러한 빌드 단계를 추가한 후에 다음과 같이 각 단계의 속성을 편집합니다. </span><span class="sxs-lookup"><span data-stu-id="22f12-229">After adding these build steps, edit the properties of each step as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="22f12-230">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-230">PowerShell Script</span></span>

1. <span data-ttu-id="22f12-231">**형식** 속성을 `File Path`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-231">Set the **Type** property to `File Path`.</span></span>
1. <span data-ttu-id="22f12-232">**스크립트 경로** 속성을 `initiate.ps1`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-232">Set the **Script Path** property to `initiate.ps1`.</span></span>
1. <span data-ttu-id="22f12-233">`-fileName build`를 **인수** 속성에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-233">Add `-fileName build` to the **Arguments** property.</span></span>

<span data-ttu-id="22f12-234">이 빌드 단계는 psake 빌드 스크립트를 호출하는 `initiate.ps1` 파일을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-234">This build step runs the `initiate.ps1` file, which calls the psake build script.</span></span>

### <a name="publish-test-results"></a><span data-ttu-id="22f12-235">테스트 결과 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-235">Publish Test Results</span></span>

1. <span data-ttu-id="22f12-236">**테스트 결과 형식**을 `NUnit`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-236">Set **Test Result Format** to `NUnit`</span></span>
1. <span data-ttu-id="22f12-237">**테스트 결과 파일**을 `InfraDNS/Tests/Results/*.xml`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-237">Set **Test Results Files** to `InfraDNS/Tests/Results/*.xml`</span></span>
1. <span data-ttu-id="22f12-238">**테스트 실행 제목**을 `Unit`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-238">Set **Test Run Title** to `Unit`.</span></span>
1. <span data-ttu-id="22f12-239">**제어 옵션** **사용** 및 **항상 실행**이 둘 다 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-239">Make sure **Control Options** **Enabled** and **Always run** are both selected.</span></span>

<span data-ttu-id="22f12-240">이 빌드 단계는 앞에서 살펴본 Pester 스크립트에서 단위 테스트를 실행하고 결과를 `InfraDNS/Tests/Results/*.xml` 폴더에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-240">This build step runs the unit tests in the Pester script we looked at earlier, and stores the results in the `InfraDNS/Tests/Results/*.xml` folder.</span></span>

### <a name="copy-files"></a><span data-ttu-id="22f12-241">파일 복사</span><span class="sxs-lookup"><span data-stu-id="22f12-241">Copy Files</span></span>

1. <span data-ttu-id="22f12-242">다음 각 줄을 **내용**에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-242">Add each of the following lines to **Contents**:</span></span>

    ```
    initiate.ps1
    **\deploy.ps1
    **\Acceptance\**
    **\Integration\**
    ```

1. <span data-ttu-id="22f12-243">**TargetFolder**를 `$(Build.ArtifactStagingDirectory)\`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-243">Set **TargetFolder** to `$(Build.ArtifactStagingDirectory)\`</span></span>

<span data-ttu-id="22f12-244">이 단계는 다음 단계에서 빌드 아티팩트로 게시할 수 있도록 빌드 및 테스트 스크립트를 스테이징 디렉터리에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-244">This step copies the build and test scripts to the staging directory so that the can be published as build artifacts by the next step.</span></span>

### <a name="publish-artifact"></a><span data-ttu-id="22f12-245">아티팩트 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-245">Publish Artifact</span></span>

1. <span data-ttu-id="22f12-246">**게시할 경로**를 `$(Build.ArtifactStagingDirectory)\`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-246">Set **Path to Publish** to `$(Build.ArtifactStagingDirectory)\`</span></span>
1. <span data-ttu-id="22f12-247">**아티팩트 이름**을 `Deploy`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-247">Set **Artifact Name** to `Deploy`</span></span>
1. <span data-ttu-id="22f12-248">**아티팩트 형식**을 `Server`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-248">Set **Artifact Type** to `Server`</span></span>
1. <span data-ttu-id="22f12-249">**제어 옵션**에서 `Enabled`를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-249">Select `Enabled` in **Control Options**</span></span>

## <a name="enable-continuous-integration"></a><span data-ttu-id="22f12-250">연속 통합을 사용하도록 설정</span><span class="sxs-lookup"><span data-stu-id="22f12-250">Enable continuous integration</span></span>

<span data-ttu-id="22f12-251">이제 git 리포지토리의 `ci-cd-example` 분기에 변경 내용을 체크 인할 때마다 프로젝트가 빌드되도록 하는 트리거를 설정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-251">Now we'll set up a trigger that causes the project to build any time a change is checked in to the `ci-cd-example` branch of the git repository.</span></span>

1. <span data-ttu-id="22f12-252">TFS에서 **빌드 및 릴리스** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-252">In TFS, click the **Build & Release** tab</span></span>
1. <span data-ttu-id="22f12-253">`DNS Infra` 빌드 정의를 선택하고 **편집**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-253">Select the `DNS Infra` build definition, and click **Edit**</span></span>
1. <span data-ttu-id="22f12-254">**트리거** 탭을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-254">Click the **Triggers** tab</span></span>
1. <span data-ttu-id="22f12-255">**연속 통합(CI)**을 선택하고 분기 드롭다운 목록에서 `refs/heads/ci-cd-example`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-255">Select **Continuous integration (CI)**, and select `refs/heads/ci-cd-example` in the branch drop-down list</span></span>
1. <span data-ttu-id="22f12-256">**저장**, **확인**을 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-256">Click **Save** and then **OK**</span></span>

<span data-ttu-id="22f12-257">이제 TFS git 리포지토리에서 변경을 수행하면 자동화된 빌드가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-257">Now any change in the TFS git repository triggers an automated build.</span></span>

## <a name="create-the-release-definition"></a><span data-ttu-id="22f12-258">릴리스 정의 만들기</span><span class="sxs-lookup"><span data-stu-id="22f12-258">Create the release definition</span></span>

<span data-ttu-id="22f12-259">다음으로는 코드를 체크 인할 때마다 개발 환경에 프로젝트가 배포되도록 릴리스 정의를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-259">Let's create a release definition so that the project is deployed to the development environment with every code check-in.</span></span>

<span data-ttu-id="22f12-260">이렇게 하려면 앞에서 만든 `InfraDNS` 빌드 정의와 연결된 새 릴리스 정의를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-260">To do this, add a new release definition associated with the `InfraDNS` build definition you created previously.</span></span>
<span data-ttu-id="22f12-261">새 빌드를 완료할 때마다 새 릴리스가 트리거되도록 **연속 배포**를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-261">Be sure to select **Continuous deployment** so that a new release will be triggered any time a new build is completed.</span></span>
<span data-ttu-id="22f12-262">해당 방법은 [방법: 릴리스 정의 작업](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)을 참조하세요. 다음과 같이 새 릴리스 정의를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-262">([How to: Work with release definitions](https://www.visualstudio.com/en-us/docs/build/actions/work-with-release-definitions)) and configure it as follows:</span></span>

<span data-ttu-id="22f12-263">릴리스 정의에 다음 단계를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-263">Add the following steps to the release definition:</span></span>

- <span data-ttu-id="22f12-264">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-264">PowerShell Script</span></span>
- <span data-ttu-id="22f12-265">테스트 결과 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-265">Publish Test Results</span></span>
- <span data-ttu-id="22f12-266">테스트 결과 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-266">Publish Test Results</span></span>

<span data-ttu-id="22f12-267">다음과 같이 단계를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-267">Edit the steps as follows:</span></span>

### <a name="powershell-script"></a><span data-ttu-id="22f12-268">PowerShell 스크립트</span><span class="sxs-lookup"><span data-stu-id="22f12-268">PowerShell Script</span></span>

1. <span data-ttu-id="22f12-269">**스크립트 경로** 필드를 `$(Build.DefinitionName)\Deploy\initiate.ps1"`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-269">Set the **Script Path** field to `$(Build.DefinitionName)\Deploy\initiate.ps1"`</span></span>
1. <span data-ttu-id="22f12-270">**인수** 필드를 `-fileName Deploy`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-270">Set the **Arguments** field to `-fileName Deploy`</span></span>

### <a name="first-publish-test-results"></a><span data-ttu-id="22f12-271">테스트 결과 첫 번째 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-271">First Publish Test Results</span></span>

1. <span data-ttu-id="22f12-272">**테스트 결과 형식** 필드에서 `NUnit`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-272">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="22f12-273">**테스트 결과 파일** 필드를 `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-273">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Integration*.xml`</span></span>
1. <span data-ttu-id="22f12-274">**테스트 실행 제목**을 `Integration`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-274">Set the **Test Run Title** to `Integration`</span></span>
1. <span data-ttu-id="22f12-275">**제어 옵션**에서 **항상 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-275">Under **Control Options**, check **Always run**</span></span>

### <a name="second-publish-test-results"></a><span data-ttu-id="22f12-276">테스트 결과 두 번째 게시</span><span class="sxs-lookup"><span data-stu-id="22f12-276">Second Publish Test Results</span></span>

1. <span data-ttu-id="22f12-277">**테스트 결과 형식** 필드에서 `NUnit`을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-277">Select `NUnit` for the **Test Result Format** field</span></span>
1. <span data-ttu-id="22f12-278">**테스트 결과 파일** 필드를 `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-278">Set the **Test Result Files** field to `$(Build.DefinitionName)\Deploy\InfraDNS\Tests\Results\Acceptance*.xml`</span></span>
1. <span data-ttu-id="22f12-279">**테스트 실행 제목**을 `Acceptance`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-279">Set the **Test Run Title** to `Acceptance`</span></span>
1. <span data-ttu-id="22f12-280">**제어 옵션**에서 **항상 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-280">Under **Control Options**, check **Always run**</span></span>

## <a name="verify-your-results"></a><span data-ttu-id="22f12-281">결과 확인</span><span class="sxs-lookup"><span data-stu-id="22f12-281">Verify your results</span></span>

<span data-ttu-id="22f12-282">이제 `ci-cd-example` 분기에서 TFS에 변경 내용을 푸시할 때마다 새 빌드가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-282">Now, any time you push changes in the `ci-cd-example` branch to TFS, a new build will start.</span></span>
<span data-ttu-id="22f12-283">빌드가 정상적으로 완료되면 새 배포가 트리거됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-283">If the build completes successfully, a new deployment is triggered.</span></span>

<span data-ttu-id="22f12-284">클라이언트 컴퓨터에서 브라우저를 열고 `www.contoso.com`으로 이동하면 배포 결과를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-284">You can check the result of the deployment by opening a browser on the client machine and navigating to `www.contoso.com`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22f12-285">다음 단계</span><span class="sxs-lookup"><span data-stu-id="22f12-285">Next steps</span></span>

<span data-ttu-id="22f12-286">이 예제에서는 `www.contoso.com` URL이 `TestAgent2`로 확인되도록 DNS 서버 `TestAgent1`을 구성하지만 웹 사이트가 실제로 배포되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-286">This example configures the DNS server `TestAgent1` so that the URL `www.contoso.com` resolves to `TestAgent2`, but it does not actually deploy a website.</span></span>
<span data-ttu-id="22f12-287">웹 사이트 배포를 위한 코드 구조는 리포지토리의 `WebApp` 폴더에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-287">The skeleton for doing so is provided in the repo under the `WebApp` folder.</span></span>
<span data-ttu-id="22f12-288">제공된 스텁을 사용하여 psake 스크립트, Pester 테스트 및 DSC 구성을 만들어서 웹 사이트를 직접 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22f12-288">You can use the stubs provided to create psake scripts, Pester tests, and DSC configurations to deploy your own website.</span></span>