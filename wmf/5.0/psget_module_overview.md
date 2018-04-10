---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 82b8046d5cbb47300f090ce2ffbf3c279ed19458
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
---
# <a name="powershell-module-discovery-install-and-inventory-with-powershellget"></a><span data-ttu-id="c2cf5-102">PowerShellGet을 사용하여 PowerShell 모듈 검색, 설치 및 인벤토리에 추가</span><span class="sxs-lookup"><span data-stu-id="c2cf5-102">PowerShell Module Discovery, Install and Inventory with PowerShellGet</span></span>

<span data-ttu-id="c2cf5-103">PowerShellGet은 이번 WMF 릴리스에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="c2cf5-103">PowerShellGet is included in this release of WMF:</span></span>
-   <span data-ttu-id="c2cf5-104">Find-Module은 -Tag 매개 변수를 사용하여 모듈 메타데이터를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2cf5-104">Find-Module can filter on module metadata with the -Tag parameter</span></span>
-   <span data-ttu-id="c2cf5-105">Find-Module은 -Filter 매개 변수를 사용하여 리포지토리 관련 검색 언어를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2cf5-105">Find-Module can filter on repository-specific search language with the -Filter parameter</span></span>
-   <span data-ttu-id="c2cf5-106">Find-Module은 -Command, -DscResource 및 -Includes 매개 변수를 사용하여 모듈 콘텐츠를 기반으로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c2cf5-106">Find-Module can filter based on module contents with the -Command, -DscResource, and -Includes parameters</span></span>
-   <span data-ttu-id="c2cf5-107">Find-DscResource는 리포지토리에서 개별 DSC 리소스의 검색을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="c2cf5-107">Find-DscResource allows discovery of individual DSC resources in repositories</span></span>
-   <span data-ttu-id="c2cf5-108">NuGet을 사용하여 파일 공유에서 설치 및 파일 공유에 게시를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="c2cf5-108">Support for installing from and publishing to file shares with NuGet</span></span>

## <a name="example-commands"></a><span data-ttu-id="c2cf5-109">예제 명령</span><span class="sxs-lookup"><span data-stu-id="c2cf5-109">Example commands</span></span>
```powershell
\# Find all modules with tags Azure or DSC
Find-Module -Tag Azure, DSC

\# Find modules with a specific DscResource
Find-Module -DscResource xFirewall

\#Find modules with specific commands
Find-Module -Command Get-ScriptAnalyzerRule, Invoke-ScriptAnalyzer

\# Find all modules with Dsc resources
Find-Module -Includes DscResource

\# Find all modules with cmdlets
Find-Module -Includes Cmdlet

\# Find all modules with functions
Find-Module -Includes Function

\# Find all DSC resources
Find-DscResource

\# Find all DSC resources contained within a specific module
Find-DscResource -ModuleName xNetworking

\# Find all DSC resources in modules with DSCResourceKit or DesiredStateConfiguration
Find-DscResource -Tag DesiredStateConfiguration, DSCResourceKit

\# Find modules using -Filter parameter
\# Specified filter value is searched in Name and Description properties
Find-Module -Filter Cookbook -Repository PSGallery
Find-Module -Filter RBAC -Repository PSGallery
```

## <a name="new-features-in-powershellget"></a><span data-ttu-id="c2cf5-110">PowerShellGet의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="c2cf5-110">New features in PowerShellGet</span></span>
-   <span data-ttu-id="c2cf5-111">Windows PowerShell 5.0 이상에서 Side-by-side 버전 지원</span><span class="sxs-lookup"><span data-stu-id="c2cf5-111">Side-by-side version support on Windows PowerShell 5.0 or newer</span></span>
-   <span data-ttu-id="c2cf5-112">모듈 종속성 설치 지원</span><span class="sxs-lookup"><span data-stu-id="c2cf5-112">Module dependency installation support</span></span>
-   <span data-ttu-id="c2cf5-113">세 가지 새로운 cmdlet</span><span class="sxs-lookup"><span data-stu-id="c2cf5-113">Three new cmdlets</span></span>
    -   <span data-ttu-id="c2cf5-114">Get-InstalledModule</span><span class="sxs-lookup"><span data-stu-id="c2cf5-114">Get-InstalledModule</span></span>
    -   <span data-ttu-id="c2cf5-115">Uninstall-Module</span><span class="sxs-lookup"><span data-stu-id="c2cf5-115">Uninstall-Module</span></span>
    -   <span data-ttu-id="c2cf5-116">Save-Module</span><span class="sxs-lookup"><span data-stu-id="c2cf5-116">Save-Module</span></span>