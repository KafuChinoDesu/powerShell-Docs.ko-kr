---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: "WMF 5.1 릴리스 정보"
ms.openlocfilehash: f80c1ec5886578e3e43f2c96981f40152db000d1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
# <a name="windows-management-framework-wmf-51-release-notes"></a><span data-ttu-id="f80ae-103">WMF(Windows Management Framework) 5.1 릴리스 정보</span><span class="sxs-lookup"><span data-stu-id="f80ae-103">Windows Management Framework (WMF) 5.1 Release Notes</span></span> #

<span data-ttu-id="f80ae-104">WMF 5.1에는 Windows Server 2016과 함께 릴리스된 PowerShell, WMI, WinRM 및 SIL(소프트웨어 인벤토리 및 라이선스) 구성 요소가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-104">WMF 5.1 includes the PowerShell, WMI, WinRM, and Software Inventory and Licensing (SIL) components that were released with Windows Server 2016.</span></span>
<span data-ttu-id="f80ae-105">WMF 5.1은 Windows 7, Windows 8.1, Windows Server 2008 R2, 2012 및 2012 R2에 설치할 수 있으며 WMF 5.0 RTM보다 개선된 많은 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-105">WMF 5.1 can be installed on Windows 7, Windows 8.1, Windows Server 2008 R2, 2012, and 2012 R2, and provides a number of improvements over WMF 5.0 RTM including:</span></span>

- <span data-ttu-id="f80ae-106">새 cmdlet: 로컬 사용자 및 그룹; Get-ComputerInfo</span><span class="sxs-lookup"><span data-stu-id="f80ae-106">New cmdlets: local users and groups; Get-ComputerInfo</span></span>
- <span data-ttu-id="f80ae-107">서명된 모듈, JEA 모듈 설치 등의 PowerShellGet 개선 사항</span><span class="sxs-lookup"><span data-stu-id="f80ae-107">PowerShellGet improvements include enforcing signed modules, and installing JEA modules</span></span>
- <span data-ttu-id="f80ae-108">PackageManagement에서 컨테이너, CBS 설치, EXE 기반 설치, CAB 패키지에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="f80ae-108">PackageManagement added support for Containers, CBS Setup, EXE-based setup, CAB packages</span></span>
- <span data-ttu-id="f80ae-109">DSC 및 PowerShell 클래스에 대한 디버깅 개선 사항</span><span class="sxs-lookup"><span data-stu-id="f80ae-109">Debugging improvements for DSC and PowerShell classes</span></span>
- <span data-ttu-id="f80ae-110">끌어오기 서버에서 나오는 카탈로그 서명 모듈 적용 및 PowerShellGet cmdlet을 사용할 경우를 비롯한 보안 향상</span><span class="sxs-lookup"><span data-stu-id="f80ae-110">Security enhancements including enforcement of catalog-signed modules coming from the Pull Server and when using PowerShellGet cmdlets</span></span>
- <span data-ttu-id="f80ae-111">다양한 사용자 요청 및 문제에 대한 응답</span><span class="sxs-lookup"><span data-stu-id="f80ae-111">Responses to a number of user requests and issues</span></span>

<span data-ttu-id="f80ae-112">**중요:**</span><span class="sxs-lookup"><span data-stu-id="f80ae-112">**Important notes:**</span></span>

- <span data-ttu-id="f80ae-113">**WMF 5.1을 사용하려면 .NET Framework 4.5.2가 필요합니다**.</span><span class="sxs-lookup"><span data-stu-id="f80ae-113">**WMF 5.1 requires the .NET Framework 4.5.2**.</span></span> <span data-ttu-id="f80ae-114">.NET 4.5.2가 설치되어 있지 않은 경우 설치는 되지만 주요 기능이 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-114">Installation will succeed, but key features will fail if .NET 4.5.2 is not installed.</span></span> <span data-ttu-id="f80ae-115">지침은 [WMF 5.1 설치 및 구성](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure) 항목에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-115">Instructions are available in the [Install and Configure WMF 5.1 ](https://msdn.microsoft.com/en-us/powershell/wmf/5.1/install-configure) topic.</span></span>
- <span data-ttu-id="f80ae-116">WMF 5.1 RTM을 설치하기 전에 먼저 WMF 5.1 Preview를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-116">WMF 5.1 Preview must be uninstalled before installing WMF 5.1 RTM.</span></span>
- <span data-ttu-id="f80ae-117">WMF 5.1은 WMF 5.0 또는 WMF 4.0 위에 바로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-117">WMF 5.1 may be installed directly over WMF 5.0 or WMF 4.0.</span></span>
- <span data-ttu-id="f80ae-118">Windows 7 및 Windows Server 2008 R2에서는 WMF 5.1을 설치하기 전에 먼저 WMF 4.0을 설치할 __필요가 없습니다__.</span><span class="sxs-lookup"><span data-stu-id="f80ae-118">It is __not required__ to install WMF 4.0 prior to installing WMF 5.1 on Windows 7 and Windows Server 2008 R2.</span></span> <span data-ttu-id="f80ae-119">이는 WMF 5.1 Preview 릴리스의 문제였으며 해결되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f80ae-119">That was an issue for the WMF 5.1 Preview release, and has been resolved.</span></span>  


