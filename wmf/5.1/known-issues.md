---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: "WMF 5.1의 알려진 문제"
ms.openlocfilehash: 93113962781f1cc84a80f8f97f56ffd7622fec6b
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
# <a name="known-issues-in-wmf-51"></a><span data-ttu-id="11714-103">WMF 5.1의 알려진 문제</span><span class="sxs-lookup"><span data-stu-id="11714-103">Known Issues in WMF 5.1</span></span> #

> <span data-ttu-id="11714-104">참고: 이 정보는 변경될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-104">Note: This information is subject to change.</span></span>

## <a name="starting-powershell-shortcut-as-administrator"></a><span data-ttu-id="11714-105">관리자 권한으로 PowerShell 바로 가기 시작</span><span class="sxs-lookup"><span data-stu-id="11714-105">Starting PowerShell shortcut as Administrator</span></span>
<span data-ttu-id="11714-106">WMF를 설치할 때, 바로 가기에서 관리자 권한으로 PowerShell을 시작하려고 하면 "지정되지 않은 오류" 메시지가 발생할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-106">Upon installing WMF, if you try to start PowerShell as administrator from the shortcut, you may get an "Unspecified error" message.</span></span>
<span data-ttu-id="11714-107">관리자가 아닌 사용자로 바로 가기를 다시 열면 관리자 권한으로도 바로 가기가 작동됩니다.</span><span class="sxs-lookup"><span data-stu-id="11714-107">Reopen the shortcut as non-administrator and the shortcut now works even as administrator.</span></span>

## <a name="pester"></a><span data-ttu-id="11714-108">Pester</span><span class="sxs-lookup"><span data-stu-id="11714-108">Pester</span></span>
<span data-ttu-id="11714-109">이 릴리스에는 Nano Server의 Pester를 사용할 때 알아야 하는 두 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-109">In this release, there are two issues you should be aware of when using Pester on Nano Server:</span></span>

* <span data-ttu-id="11714-110">Pester 자체에 대한 테스트를 실행하면 FULL CLR 및 CORE CLR 간의 차이로 인해 몇 가지 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-110">Running tests against Pester itself can result in some failures because of differences between FULL CLR and CORE CLR.</span></span> <span data-ttu-id="11714-111">특히 XmlDocument 형식에는 Validate 메서드를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-111">In particular, the Validate method is not available on the XmlDocument type.</span></span> <span data-ttu-id="11714-112">NUnit 출력 로그의 스키마 유효성 검사를 시도하는 여섯 가지 테스트에서 오류가 발생하는 것으로 알려져 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-112">Six tests which attempt to validate the schema of the NUnit output logs are known to fail.</span></span> 
* <span data-ttu-id="11714-113">*WindowsFeature* DSC 리소스가 Nano Server에 없기 때문에 하나의 코드 검사 테스트에서 현재 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="11714-113">One Code Coverage test fails currently because the *WindowsFeature* DSC Resource does not exist in Nano Server.</span></span> <span data-ttu-id="11714-114">그러나 이러한 오류는 일반적으로 심각하지 않으며 무시해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11714-114">However, these failures are generally benign and can safely be ignored.</span></span>

## <a name="operation-validation"></a><span data-ttu-id="11714-115">작업 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="11714-115">Operation Validation</span></span> 

* <span data-ttu-id="11714-116">작동하지 않는 도움말 URI로 인해 Microsoft.PowerShell.Operation.Validation 모듈에 대해 Update-Help가 실패함</span><span class="sxs-lookup"><span data-stu-id="11714-116">Update-Help fails for Microsoft.PowerShell.Operation.Validation module due to non-working help URI</span></span>

## <a name="dsc-after-uninstall-wmf"></a><span data-ttu-id="11714-117">WMF 제거 후 DSC</span><span class="sxs-lookup"><span data-stu-id="11714-117">DSC after uninstall WMF</span></span> 
* <span data-ttu-id="11714-118">WMF를 제거해도 DSC MOF 문서가 구성 폴더에서 삭제되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-118">Uninstalling WMF does not delete DSC MOF documents from the configuration folder.</span></span> <span data-ttu-id="11714-119">MOF 문서에 이전 시스템에서 사용할 수 없는 최신 속성이 포함되어 있는 경우 DSC가 제대로 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-119">DSC won't work properly if the MOF documents contain newer properties which are not available on the older systems.</span></span> <span data-ttu-id="11714-120">이 경우 관리자 권한 PowerShell 콘솔에서 다음 스크립트를 실행하여 DSC 상태를 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="11714-120">In this case, run the following script from elevated PowerShell console to to clean up the DSC states.</span></span>
 ```PowerShell
    $PreviousDSCStates = @("$env:windir\system32\configuration\*.mof",
            "$env:windir\system32\configuration\*.mof.checksum",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof",
            "$env:windir\system32\configuration\PartialConfiguration\*.mof.checksum"
           )

    $PreviousDSCStates | Remove-Item -ErrorAction SilentlyContinue -Verbose
 ```  

## <a name="jea-virtual-accounts"></a><span data-ttu-id="11714-121">JEA 가상 계정</span><span class="sxs-lookup"><span data-stu-id="11714-121">JEA Virtual Accounts</span></span>
<span data-ttu-id="11714-122">WMF 5.0에서 가상 계정을 사용하도록 구성된 JEA 끝점 및 세션 구성은 WMF 5.1로 업그레이드한 후 가상 계정을 사용하도록 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11714-122">JEA endpoints and session configurations configured to use virtual accounts in WMF 5.0 will not be configured to use a virtual account after upgrading to WMF 5.1.</span></span>
<span data-ttu-id="11714-123">즉, JEA 세션에서 실행되는 명령은 임시 관리자 계정 대신 연결하는 사용자의 ID로 실행되어 잠재적으로 사용자가 상승된 권한이 필요한 명령을 실행하지 못하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="11714-123">This means that commands run in JEA sessions will run under the connecting user's identity instead of a temporary administrator account, potentially preventing the user from running commands which require elevated privileges.</span></span>
<span data-ttu-id="11714-124">가상 계정을 복원하려면 가상 계정을 사용하는 모든 세션 구성을 등록 취소한 후 다시 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="11714-124">To restore the virtual accounts, you need to unregister and re-register any session configurations that use virtual accounts.</span></span>

```powershell
# Find the JEA endpoint by its name
$jea = Get-PSSessionConfiguration -Name MyJeaEndpoint

# Copy the cached PSSC file so it can be re-registered
$pssc = Copy-Item $jea.ConfigFilePath $env:temp -PassThru

# Unregister the current PSSC
Unregister-PSSessionConfiguration -Name $jea.Name

# Re-register the PSSC
Register-PSSessionConfiguration -Name $jea.Name -Path $pssc.FullName -Force

# Ensure the access policies remain the same
Set-PSSessionConfiguration -Name $newjea.Name -SecurityDescriptorSddl $jea.SecurityDescriptorSddl
```

