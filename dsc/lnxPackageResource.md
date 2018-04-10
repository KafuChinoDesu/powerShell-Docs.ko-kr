---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: Linux용 DSC nxPackage 리소스
ms.openlocfilehash: 0a62bb01c2daa57bd5d6f1ef131ec8ae6d6f81ee
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxpackage-resource"></a><span data-ttu-id="2199e-103">Linux용 DSC nxPackage 리소스</span><span class="sxs-lookup"><span data-stu-id="2199e-103">DSC for Linux nxPackage Resource</span></span>

<span data-ttu-id="2199e-104">PowerShell DSC(필요한 상태 구성)의 **nxPackage** 리소스에서는 Linux 노드에 있는 패키지를 관리하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-104">The **nxPackage** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage packages on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="2199e-105">구문</span><span class="sxs-lookup"><span data-stu-id="2199e-105">Syntax</span></span>

```
nxPackage <string> #ResourceName
{
    Name = <string>
    [ Ensure = <string> { Absent | Present }  ]
    [ PackageManager = <string> { Yum | Apt | Zypper } ]
    [ PackageGroup = <bool>]
    [ Arguments = <string> ]
    [ ReturnCode = <uint32> ]
    [ LogPath = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="2199e-106">속성</span><span class="sxs-lookup"><span data-stu-id="2199e-106">Properties</span></span>

|  <span data-ttu-id="2199e-107">속성</span><span class="sxs-lookup"><span data-stu-id="2199e-107">Property</span></span> |  <span data-ttu-id="2199e-108">설명</span><span class="sxs-lookup"><span data-stu-id="2199e-108">Description</span></span> |
|---|---|
| <span data-ttu-id="2199e-109">이름</span><span class="sxs-lookup"><span data-stu-id="2199e-109">Name</span></span>| <span data-ttu-id="2199e-110">특정 상태를 확인하려는 패키지의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-110">The name of the package for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="2199e-111">Ensure</span><span class="sxs-lookup"><span data-stu-id="2199e-111">Ensure</span></span>| <span data-ttu-id="2199e-112">해당 패키지가 존재하는지를 확인할지 여부를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-112">Determines whether to check if the package exists.</span></span> <span data-ttu-id="2199e-113">해당 패키지가 존재하도록 하려면 이 속성을 "Present"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-113">Set this property to "Present" to ensure the package exists.</span></span> <span data-ttu-id="2199e-114">해당 패키지가 존재하지 않도록 하려면 이 속성을 "Absent"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-114">Set it to "Absent" to ensure the package does not exist.</span></span> <span data-ttu-id="2199e-115">기본값은 "Present"입니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-115">The default value is "Present".</span></span>|
| <span data-ttu-id="2199e-116">PackageManager</span><span class="sxs-lookup"><span data-stu-id="2199e-116">PackageManager</span></span>| <span data-ttu-id="2199e-117">지원되는 값은 "yum", "apt" 및 "zypper"입니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-117">Supported values are "yum", "apt", and "zypper".</span></span> <span data-ttu-id="2199e-118">패키지를 설치할 때 사용할 패키지 관리자를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-118">Specifies the package manager to use when installing packages.</span></span> <span data-ttu-id="2199e-119">**FilePath**가 지정되면, 제공된 경로가 패키지를 설치하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-119">If **FilePath** is specified, the provided path will be used to install the package.</span></span> <span data-ttu-id="2199e-120">지정되지 않으면 패키지 관리자를 사용하여 미리 구성된 리포지토리에서 패키지를 설치하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-120">Otherwise, a Package Manager will be used to install the package from a pre-configured repository.</span></span> <span data-ttu-id="2199e-121">**PackageManager**와 **FilePath**가 모두 제공되지 않으면, 시스템에 대한 기본 패키지 관리자가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-121">If neither **PackageManager** nor **FilePath** are provided, the default package manager for the system will be used.</span></span>|
| <span data-ttu-id="2199e-122">FilePath</span><span class="sxs-lookup"><span data-stu-id="2199e-122">FilePath</span></span>| <span data-ttu-id="2199e-123">패키지가 있는 파일 경로</span><span class="sxs-lookup"><span data-stu-id="2199e-123">The file path where the package resides</span></span>|
| <span data-ttu-id="2199e-124">PackageGroup</span><span class="sxs-lookup"><span data-stu-id="2199e-124">PackageGroup</span></span>| <span data-ttu-id="2199e-125">**$true**일 경우, **Name**은 **PackageManager**와 함께 사용할 패키지 그룹의 이름이 될 것으로 예상됩니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-125">If **$true**, the **Name** is expected to be the name of a package group for use with a **PackageManager**.</span></span> <span data-ttu-id="2199e-126">**FilePath**를 제공하면 **PacakgeGroup**이 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-126">**PacakgeGroup** is not valid when providing a **FilePath**.</span></span>|
| <span data-ttu-id="2199e-127">인수</span><span class="sxs-lookup"><span data-stu-id="2199e-127">Arguments</span></span>| <span data-ttu-id="2199e-128">제공된 그대로 패키지에 전달되는 인수 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-128">A string of arguments that will be passed to the package exactly as provided.</span></span>|
| <span data-ttu-id="2199e-129">ReturnCode</span><span class="sxs-lookup"><span data-stu-id="2199e-129">ReturnCode</span></span>| <span data-ttu-id="2199e-130">예상된 반환 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-130">The expected return code.</span></span> <span data-ttu-id="2199e-131">실제 반환 코드가 여기에 제공된 예상 값과 일치하지 않는 경우 구성에서 오류를 반환하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-131">If the actual return code does not match the expected value provided here, the configuration will return an error.</span></span>|
| <span data-ttu-id="2199e-132">DependsOn</span><span class="sxs-lookup"><span data-stu-id="2199e-132">DependsOn</span></span> | <span data-ttu-id="2199e-133">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="2199e-134">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 **ID**가 **ResourceName**이고 해당 형식이 **ResourceType**일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="2199e-135">예제</span><span class="sxs-lookup"><span data-stu-id="2199e-135">Example</span></span>

<span data-ttu-id="2199e-136">다음 예제에서는 "Yum" 패키지 관리자를 사용하여 "httpd"라는 패키지가 Linux 컴퓨터에 설치되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2199e-136">The following example ensures that the package named "httpd" is installed on a Linux computer, using the “Yum” package manager.</span></span>

```
Import-DSCResource -Module nx

Node $node {
nxPackage httpd
{
    Name = "httpd"
    Ensure = "Present"
    PackageManager = "Yum"
}
}
```