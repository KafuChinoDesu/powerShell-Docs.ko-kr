---
ms.date: 12/12/2018
keywords: dsc,powershell,리소스,갤러리,설정
title: 추가 DSC 리소스 설치
ms.openlocfilehash: ecaf176230ccd934b57b1c27d72ff83e6ba906e9
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954490"
---
# <a name="install-additional-dsc-resources"></a><span data-ttu-id="d86f5-103">추가 DSC 리소스 설치</span><span class="sxs-lookup"><span data-stu-id="d86f5-103">Install Additional DSC Resources</span></span>

<span data-ttu-id="d86f5-104">PowerShell에는 DSC(Desired State Configuration)의 여러 가지 기본 제공 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-104">PowerShell includes several Out-of-the-box resources for Desired State Configuration (DSC).</span></span> <span data-ttu-id="d86f5-105">**PSDesiredStateConfiguration** 모듈에는 특정 PowerShell 인스턴스에서 사용할 수 있는 모든 OOB DSC 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-105">The **PSDesiredStateConfiguration** module contains all of the OOB DSC resources available on your specific instance of PowerShell.</span></span>

<span data-ttu-id="d86f5-106">PowerShell 4.0에 포함된 OOB 리소스 및 리소스 기능에 대한 설명의 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-106">This is a list of the OOB resources included in PowerShell 4.0 and a description of the resource's capabilities.</span></span>

> [!NOTE]
> <span data-ttu-id="d86f5-107">OOB 리소스 수가 PowerShell의 각 버전과 함께 증가하므로 불완전한 목록입니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-107">This is an incomplete list, as the number of OOB resources has grown with each version of PowerShell.</span></span>

|<span data-ttu-id="d86f5-108">리소스</span><span class="sxs-lookup"><span data-stu-id="d86f5-108">Resource</span></span>  |<span data-ttu-id="d86f5-109">설명</span><span class="sxs-lookup"><span data-stu-id="d86f5-109">Description</span></span>  |
|---------|---------|
|<span data-ttu-id="d86f5-110">**File**</span><span class="sxs-lookup"><span data-stu-id="d86f5-110">**File**</span></span>|<span data-ttu-id="d86f5-111">파일 및 디렉터리의 상태를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-111">Controls the state of files and directories.</span></span> <span data-ttu-id="d86f5-112">**원본**에서 **대상**으로 파일을 복사하고 날짜, 체크섬 및 해시를 비교하여 **원본**이 변경되면 파일을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-112">Copies files from a **Source** to a **Destination** and updates them when the **Source** changes by comparing dates, checksums, and hashes.</span></span>|
|<span data-ttu-id="d86f5-113">**Archive**</span><span class="sxs-lookup"><span data-stu-id="d86f5-113">**Archive**</span></span>|<span data-ttu-id="d86f5-114">지정된 위치에 보관 파일의 압축을 풉니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-114">Unpacks archives and a specified location.</span></span> <span data-ttu-id="d86f5-115">지정된 **체크섬**을 사용하여 보관 파일의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-115">Validates the archives with a specified **Checksum**.</span></span>|
|<span data-ttu-id="d86f5-116">**Environment**</span><span class="sxs-lookup"><span data-stu-id="d86f5-116">**Environment**</span></span>|<span data-ttu-id="d86f5-117">환경 변수를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-117">Manages environment variables.</span></span>|
|<span data-ttu-id="d86f5-118">**그룹**</span><span class="sxs-lookup"><span data-stu-id="d86f5-118">**Group**</span></span>|<span data-ttu-id="d86f5-119">로컬 그룹을 관리하고 그룹 멤버 자격을 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-119">Manages local groups and controls group membership.</span></span>|
|<span data-ttu-id="d86f5-120">**Log**</span><span class="sxs-lookup"><span data-stu-id="d86f5-120">**Log**</span></span>|<span data-ttu-id="d86f5-121">`Microsoft-Windows-Desired State Configuration/Analytic` 이벤트 로그에 메시지를 씁니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-121">Writes messages to the `Microsoft-Windows-Desired State Configuration/Analytic` event log.</span></span>|
|<span data-ttu-id="d86f5-122">**패키지**</span><span class="sxs-lookup"><span data-stu-id="d86f5-122">**Package**</span></span>|<span data-ttu-id="d86f5-123">**Arguments**, **LogPath**, **ReturnCode**, 기타 설정을 사용하여 패키지를 설치하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-123">Installs or uninstalls packages using **Arguments**, **LogPath**, **ReturnCode**, other settings.</span></span>|
|<span data-ttu-id="d86f5-124">**Registry**</span><span class="sxs-lookup"><span data-stu-id="d86f5-124">**Registry**</span></span>|<span data-ttu-id="d86f5-125">레지스트리 키 및 값을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-125">Manages registry keys and values.</span></span>|
|<span data-ttu-id="d86f5-126">**Script**</span><span class="sxs-lookup"><span data-stu-id="d86f5-126">**Script**</span></span>|<span data-ttu-id="d86f5-127">고유한 [get-test-set](../resources/get-test-set.md) script 블록을 디자인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-127">Allows you to design your own [get-test-set](../resources/get-test-set.md) script blocks.</span></span>|
|<span data-ttu-id="d86f5-128">**Service**</span><span class="sxs-lookup"><span data-stu-id="d86f5-128">**Service**</span></span>|<span data-ttu-id="d86f5-129">Windows 서비스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-129">Configures Windows services.</span></span>|
|<span data-ttu-id="d86f5-130">**User**</span><span class="sxs-lookup"><span data-stu-id="d86f5-130">**User**</span></span> |<span data-ttu-id="d86f5-131">로컬 사용자 및 특성을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-131">Manages local users and attributes.</span></span>|
|<span data-ttu-id="d86f5-132">**WindowsFeature**</span><span class="sxs-lookup"><span data-stu-id="d86f5-132">**WindowsFeature**</span></span>|<span data-ttu-id="d86f5-133">역할 및 기능을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-133">Manages roles and features.</span></span>|
|<span data-ttu-id="d86f5-134">**WindowsProcess**</span><span class="sxs-lookup"><span data-stu-id="d86f5-134">**WindowsProcess**</span></span>|<span data-ttu-id="d86f5-135">Windows 프로세스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-135">Configures Windows processes.</span></span>|

<span data-ttu-id="d86f5-136">OOB 리소스는 일반적인 작업을 위한 좋은 시작점입니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-136">The OOB resources allow a good starting point for common operations.</span></span> <span data-ttu-id="d86f5-137">OOB 리소스가 필요에 맞지 않으면 고유한 [사용자 지정 리소스](../resources/authoringResource.md)를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-137">If the OOB resources do not meet your needs, you can write your own [Custom Resource](../resources/authoringResource.md).</span></span> <span data-ttu-id="d86f5-138">문제를 해결하기 위한 사용자 지정 리소스를 작성하기 전에 Microsoft 및 PowerShell 커뮤니티에서 이미 만들어진 수많은 DSC 리소스를 살펴보아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-138">Before you write a custom resource to solve your problem, you should look through the vast number of DSC resources that have already been created by both Microsoft and the PowerShell community.</span></span>

<span data-ttu-id="d86f5-139">[PowerShell 갤러리](https://www.powershellgallery.com/) 및 [GitHub](https://github.com/)에서 DSC 리소스를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-139">You can find DSC resources in both the [PowerShell Gallery](https://www.powershellgallery.com/) and [GitHub](https://github.com/).</span></span> <span data-ttu-id="d86f5-140">[PowerShellGet](/powershell/module/powershellget/)을 사용하여 PowerShell 콘솔에서 직접 DSC 리소스를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-140">You can also install DSC resources directly from the PowerShell console using [PowerShellGet](/powershell/module/powershellget/).</span></span>

## <a name="installing-powershellget"></a><span data-ttu-id="d86f5-141">PowerShellGet 설치</span><span class="sxs-lookup"><span data-stu-id="d86f5-141">Installing PowerShellGet</span></span>

<span data-ttu-id="d86f5-142">**PowerShell**을 이미 다운로드했는지 확인하거나 설치하는 데 도움이 필요하면 다음 가이드를 참조하세요. [PowerShellGet 설치](/powershell/gallery/installing-psget).</span><span class="sxs-lookup"><span data-stu-id="d86f5-142">To determine if you already have **PowerShell** get, or to get help installing it, see the following guide: [Installing PowerShellGet](/powershell/gallery/installing-psget).</span></span>

## <a name="finding-dsc-resources-using-powershellget"></a><span data-ttu-id="d86f5-143">PowerShellGet을 사용하여 DSC 리소스 찾기</span><span class="sxs-lookup"><span data-stu-id="d86f5-143">Finding DSC resources using PowerShellGet</span></span>

<span data-ttu-id="d86f5-144">**PowerShellGet**이 시스템에 설치되면 [PowerShell 갤러리](https://www.powershellgallery.com/)에서 호스트되는 DSC 리소스를 찾고 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-144">Once **PowerShellGet** is installed on your system, you can find and install DSC resources hosted in the [PowerShell Gallery](https://www.powershellgallery.com/).</span></span>

<span data-ttu-id="d86f5-145">먼저, [Find-DSCResource](/powershell/module/powershellget/find-dscresource) cmdlet을 사용하여 DSC 리소스를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-145">First, use the [Find-DSCResource](/powershell/module/powershellget/find-dscresource) cmdlet to find DSC resources.</span></span> <span data-ttu-id="d86f5-146">`Find-DSCResource`를 처음 실행하면 “NuGet 공급자”를 설치하라는 다음 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-146">When you run `Find-DSCResource` for the first time, you see the following prompt to install the "NuGet provider".</span></span>

```
PS> Find-DSCResource

NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The
NuGet provider must be available in 'C:\Program Files\PackageManagement\ProviderAssemblies' or
'C:\Users\xAdministrator\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider
 by running 'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to
install and import the NuGet provider now?
[Y] Yes  [N] No  [?] Help (default is "Y"):
```

<span data-ttu-id="d86f5-147">‘y’를 누른 후 “NuGet” 공급자가 설치되고, PowerShell 갤러리에서 설치할 수 있는 DSC 리소스 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-147">After pressing 'y', the "NuGet" provider is installed, you see a list of DSC resources that you can install from the PowerShell Gallery.</span></span>

> [!NOTE]
> <span data-ttu-id="d86f5-148">목록이 매우 크기 때문에 표시되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-148">List is not shown because it is very large.</span></span>

<span data-ttu-id="d86f5-149">와일드카드를 사용하여 `-Name` 매개 변수를 지정하거나 와일드카드 없이 `-Filter` 매개 변수를 지정하여 검색 범위를 좁힐 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-149">You can also specify the `-Name` parameter using wildcards, or `-Filter` parameter without wildcards to narrow down your search.</span></span> <span data-ttu-id="d86f5-150">이 예제에서는 와일드카드를 사용하여 “TimeZone” DSC 리소스를 찾겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-150">This example attempts to find a "TimeZone" DSC resource using the wildcards.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d86f5-151">현재 `Find-DSCResource` cmdlet에는 `-Name` 및 `-Filter` 매개 변수에서 와일드카드를 사용할 수 없는 버그가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-151">Currently there is a bug in the `Find-DSCResource` cmdlet that prevents using wildcards in both the `-Name` and `-Filter` parameters.</span></span> <span data-ttu-id="d86f5-152">아래 두 번째 예제에서는 `Where-Object`를 사용하여 해결 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-152">The second example below shows a workaround using `Where-Object`.</span></span>

```
PS> Find-DSCResource -Name *Time*

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
Carbon_EnvironmentVariable          2.6.0      Carbon                              PSGallery
Carbon_FirewallRule                 2.6.0      Carbon                              PSGallery
Carbon_Group                        2.6.0      Carbon                              PSGallery
Carbon_IniFile                      2.6.0      Carbon                              PSGallery
Carbon_Permission                   2.6.0      Carbon                              PSGallery
Carbon_Privilege                    2.6.0      Carbon                              PSGallery
Carbon_ScheduledTask                2.6.0      Carbon                              PSGallery
Carbon_Service                      2.6.0      Carbon                              PSGallery
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
xTimeZone                           1.8.0.0    xTimeZone                           PSGallery
xSqlServerDefaultDir                1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerMoveDatabaseFiles         1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerSQLDataRoot               1.0.0      mlSqlServerDSC                      PSGallery
xSqlServerStartupParam              1.0.0      mlSqlServerDSC                      PSGallery
```

<span data-ttu-id="d86f5-153">`Where-Object`를 사용하여 더 세분화된 필터링을 통해 DSC 리소스를 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-153">You can also use `Where-Object` to find DSC resources with more granular filtering.</span></span> <span data-ttu-id="d86f5-154">이 방법은 기본 제공 필터링 매개 변수를 사용하는 것보다 느립니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-154">This approach will be slower than using built in filtering parameters.</span></span>

```
PS> Find-DSCResource | Where-Object {$_.Name -like "Time*"}

Name                                Version    ModuleName                          Repository
----                                -------    ----------                          ----------
TimeZone                            6.0.0.0    ComputerManagementDsc               PSGallery
```

<span data-ttu-id="d86f5-155">필터링에 대한 자세한 내용은 [Where-Object](/powershell/module/microsoft.powershell.core/where-object)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="d86f5-155">For more information on filtering, see [Where-Object](/powershell/module/microsoft.powershell.core/where-object).</span></span>

## <a name="installing-dsc-resources-using-powershellget"></a><span data-ttu-id="d86f5-156">PowerShellGet을 사용하여 DSC 리소스 설치</span><span class="sxs-lookup"><span data-stu-id="d86f5-156">Installing DSC Resources using PowerShellGet</span></span>

<span data-ttu-id="d86f5-157">DSC 리소스를 설치하려면 [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet을 사용하여 검색 결과에서 **모듈** 이름 아래에 표시되는 모듈 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-157">To install a DSC resource, use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet, specifying the name of the module shown under **Module** name in your search results.</span></span>

<span data-ttu-id="d86f5-158">“TimeZone” 리소스는 이 예제에서 설치하는 “ComputerManagementDSC” 모듈에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-158">The "TimeZone" resource exists in the "ComputerManagementDSC" module, so that is the module this example installs.</span></span>

> [!NOTE]
> <span data-ttu-id="d86f5-159">PowerShell 갤러리를 신뢰하지 않은 경우에는 확인 여부를 묻고 설치 관련 후속 프롬프트를 표시하지 않는 방법을 알려주는 아래 경고가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-159">If you have not trusted the PowerShell gallery, you see the warning below asking for confirmation, and instructing you how to avoid subsequent prompts on installs.</span></span>

```
PS> Install-Module -Name ComputerManagementDSC

Untrusted repository
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"):
```

<span data-ttu-id="d86f5-160">‘y’를 눌러 모듈을 계속 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-160">Press 'y' to continue installing the module.</span></span> <span data-ttu-id="d86f5-161">설치한 후 새 리소스가 [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)를 사용하여 설치되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-161">After install, you can verify that your new resource is installed using [Get-DSCResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource).</span></span>

```
PS> Get-DSCResource -Name TimeZone -Syntax

TimeZone [String] #ResourceName
{
    IsSingleInstance = [string]{ Yes }
    TimeZone = [string]
    [DependsOn = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

<span data-ttu-id="d86f5-162">`-ModuleName` 매개 변수를 지정하여 새로 설치된 모듈에서 다른 리소스를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d86f5-162">You can also view other resources in your newly installed module, by specifying the `-ModuleName` parameter.</span></span>

```
PS> Get-DSCResource -Module ComputerManagementDSC

ImplementedAs   Name                      ModuleName                     Version    Properties
-------------   ----                      ----------                     -------    ----------
PowerShell      Computer                  ComputerManagementDsc          6.0.0.0    {Name, Credential, DependsOn, ...
PowerShell      OfflineDomainJoin         ComputerManagementDsc          6.0.0.0    {IsSingleInstance, RequestFile...
PowerShell      PowerPlan                 ComputerManagementDsc          6.0.0.0    {IsSingleInstance, Name, Depen...
PowerShell      PowerShellExecutionPolicy ComputerManagementDsc          6.0.0.0    {ExecutionPolicy, ExecutionPol...
PowerShell      ScheduledTask             ComputerManagementDsc          6.0.0.0    {TaskName, ActionArguments, Ac...
PowerShell      TimeZone                  ComputerManagementDsc          6.0.0.0    {IsSingleInstance, TimeZone, D...
PowerShell      VirtualMemory             ComputerManagementDsc          6.0.0.0    {Drive, Type, DependsOn, Initi...
```

## <a name="see-also"></a><span data-ttu-id="d86f5-163">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d86f5-163">See also</span></span>

- [<span data-ttu-id="d86f5-164">리소스란?</span><span class="sxs-lookup"><span data-stu-id="d86f5-164">What are Resources?</span></span>](../resources/resources.md)