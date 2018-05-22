---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: DSC WindowsOptionalFeature 리소스
ms.openlocfilehash: 1866bc9cd2194a62de23eaabee8a9c5049a84946
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-windowsoptionalfeature-resource"></a><span data-ttu-id="532f2-103">DSC WindowsOptionalFeature 리소스</span><span class="sxs-lookup"><span data-stu-id="532f2-103">DSC WindowsOptionalFeature Resource</span></span>

> <span data-ttu-id="532f2-104">적용 대상: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="532f2-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="532f2-105">PowerShell DSC(필요한 상태 구성)의 **WindowsOptionalFeature** 리소스에서는 대상 노드에서 선택적 기능을 사용할 수 있도록 설정하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-105">The **WindowsOptionalFeature** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to ensure that optional features are enabled on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="532f2-106">구문</span><span class="sxs-lookup"><span data-stu-id="532f2-106">Syntax</span></span>

```
WindowsOptionalFeature [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Enable | Disable }  ]
    [ Source = [string] ]
    [ NoWindowsUpdateCheck = [bool] ]
    [ RemoveFilesOnDisable = [bool] ]
    [ LogLevel = [string] { ErrorsOnly | ErrorsAndWarning | ErrorsAndWarningAndInformation }  ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]

}
```

## <a name="properties"></a><span data-ttu-id="532f2-107">속성</span><span class="sxs-lookup"><span data-stu-id="532f2-107">Properties</span></span>

|  <span data-ttu-id="532f2-108">속성</span><span class="sxs-lookup"><span data-stu-id="532f2-108">Property</span></span>  |  <span data-ttu-id="532f2-109">설명</span><span class="sxs-lookup"><span data-stu-id="532f2-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="532f2-110">이름</span><span class="sxs-lookup"><span data-stu-id="532f2-110">Name</span></span>| <span data-ttu-id="532f2-111">사용 또는 사용하지 않도록 설정하려는 기능의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-111">Indicates the name of the feature that you want to ensure is enabled or disabled.</span></span>|
| <span data-ttu-id="532f2-112">Ensure</span><span class="sxs-lookup"><span data-stu-id="532f2-112">Ensure</span></span>| <span data-ttu-id="532f2-113">기능을 사용하도록 설정할지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-113">Specifies whether the feature is enabled.</span></span> <span data-ttu-id="532f2-114">기능을 사용하도록 설정하려면 이 속성을 "Enable"로 설정하고 기능을 사용하지 않도록 설정하려면 속성을 "Disable"로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-114">To ensure that the feature is enabled, set this property to "Enable" To ensure that the feature is disabled, set the property to "Disable".</span></span>|
| <span data-ttu-id="532f2-115">원본</span><span class="sxs-lookup"><span data-stu-id="532f2-115">Source</span></span>| <span data-ttu-id="532f2-116">구현되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-116">Not implemented.</span></span>|
| <span data-ttu-id="532f2-117">NoWindowsUpdateCheck</span><span class="sxs-lookup"><span data-stu-id="532f2-117">NoWindowsUpdateCheck</span></span>| <span data-ttu-id="532f2-118">기능을 사용하도록 설정하기 위해 원본 파일을 검색할 때 DISM에서 WU(Windows 업데이트)에 연결하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-118">Specifies whether DISM contacts Windows Update (WU) when searching for the source files to enable a feature.</span></span> <span data-ttu-id="532f2-119">$true이면 DISM에서 WU에 연결하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-119">If $true, DISM does not contact WU.</span></span>|
| <span data-ttu-id="532f2-120">RemoveFilesOnDisable</span><span class="sxs-lookup"><span data-stu-id="532f2-120">RemoveFilesOnDisable</span></span>| <span data-ttu-id="532f2-121">기능을 사용하지 않도록 설정할 때(즉, **Ensure**를 "Absent"로 설정할 때) 기능과 연결된 파일을 모두 제거하려면 **$true**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-121">Set to **$true** to remove all files associated with the feature when it is disabled (that is, when **Ensure** is set to "Absent").</span></span>|
| <span data-ttu-id="532f2-122">로그 수준</span><span class="sxs-lookup"><span data-stu-id="532f2-122">LogLevel</span></span>| <span data-ttu-id="532f2-123">로그에 표시되는 최대 출력 수준입니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-123">The maximum output level shown in the logs.</span></span> <span data-ttu-id="532f2-124">사용 가능한 값은 "ErrorsOnly"(오류만 기록), "ErrorsAndWarning"(오류와 경고 기록) 및 "ErrorsAndWarningAndInformation"(오류, 경고 및 디버그 정보 기록)입니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-124">The accepted values are: "ErrorsOnly" (only errors are logged), "ErrorsAndWarning" (errors and warnings are logged), and "ErrorsAndWarningAndInformation" (errors, warnings, and debug information are logged).</span></span>|
| <span data-ttu-id="532f2-125">LogPath</span><span class="sxs-lookup"><span data-stu-id="532f2-125">LogPath</span></span>| <span data-ttu-id="532f2-126">리소스 공급자가 작업을 기록할 로그 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-126">The path to a log file where you want the resource provider to log the operation.</span></span>|
| <span data-ttu-id="532f2-127">DependsOn</span><span class="sxs-lookup"><span data-stu-id="532f2-127">DependsOn</span></span>| <span data-ttu-id="532f2-128">이 리소스를 구성하기 전에 다른 리소스의 구성을 실행해야 함을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-128">Specifies that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="532f2-129">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="532f2-129">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|