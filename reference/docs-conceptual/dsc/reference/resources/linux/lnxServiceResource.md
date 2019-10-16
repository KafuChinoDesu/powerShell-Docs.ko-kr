---
ms.date: 09/20/2019
keywords: dsc,powershell,configuration,setup
title: Linux용 DSC nxService 리소스
ms.openlocfilehash: 6bb58796c4deff1153f932f61c328d84f8c4d2ca
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954840"
---
# <a name="dsc-for-linux-nxservice-resource"></a><span data-ttu-id="0bfff-103">Linux용 DSC nxService 리소스</span><span class="sxs-lookup"><span data-stu-id="0bfff-103">DSC for Linux nxService Resource</span></span>

<span data-ttu-id="0bfff-104">PowerShell DSC(필요한 상태 구성)의 **nxService** 리소스에서는 Linux 노드에 있는 서비스를 관리하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-104">The **nxService** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage services on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="0bfff-105">구문</span><span class="sxs-lookup"><span data-stu-id="0bfff-105">Syntax</span></span>

```Syntax
nxService <string> #ResourceName
{
    Name = <string>
    [ Controller = <string> { init | upstart | systemd } ]
    [ Enabled = <bool> ]
    [ State = <string> { Running | Stopped } ]
    [ DependsOn = <string[]> ]
}
```

## <a name="properties"></a><span data-ttu-id="0bfff-106">속성</span><span class="sxs-lookup"><span data-stu-id="0bfff-106">Properties</span></span>

|<span data-ttu-id="0bfff-107">속성</span><span class="sxs-lookup"><span data-stu-id="0bfff-107">Property</span></span> |<span data-ttu-id="0bfff-108">설명</span><span class="sxs-lookup"><span data-stu-id="0bfff-108">Description</span></span> |
|---|---|
|<span data-ttu-id="0bfff-109">이름</span><span class="sxs-lookup"><span data-stu-id="0bfff-109">Name</span></span> |<span data-ttu-id="0bfff-110">구성할 서비스/데몬의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-110">The name of the service/daemon to configure.</span></span> |
|<span data-ttu-id="0bfff-111">컨트롤러</span><span class="sxs-lookup"><span data-stu-id="0bfff-111">Controller</span></span> |<span data-ttu-id="0bfff-112">서비스를 구성할 때 사용할 서비스 컨트롤러의 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-112">The type of service controller to use when configuring the service.</span></span> |
|<span data-ttu-id="0bfff-113">사용</span><span class="sxs-lookup"><span data-stu-id="0bfff-113">Enabled</span></span> |<span data-ttu-id="0bfff-114">부팅 시 서비스가 시작되는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-114">Indicates whether the service starts on boot.</span></span> |
|<span data-ttu-id="0bfff-115">State</span><span class="sxs-lookup"><span data-stu-id="0bfff-115">State</span></span> |<span data-ttu-id="0bfff-116">서비스가 실행되고 있는지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-116">Indicates whether the service is running.</span></span> <span data-ttu-id="0bfff-117">서비스가 실행 중이 아니도록 설정하려면 이 속성을 **Stopped**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-117">Set this property to **Stopped** to ensure that the service is not running.</span></span> <span data-ttu-id="0bfff-118">서비스가 실행 중이도록 하려면 이 속성을 **Running**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-118">Set it to **Running** to ensure that the service is running.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="0bfff-119">공용 속성</span><span class="sxs-lookup"><span data-stu-id="0bfff-119">Common properties</span></span>

|<span data-ttu-id="0bfff-120">속성</span><span class="sxs-lookup"><span data-stu-id="0bfff-120">Property</span></span> |<span data-ttu-id="0bfff-121">설명</span><span class="sxs-lookup"><span data-stu-id="0bfff-121">Description</span></span> |
|---|---|
|<span data-ttu-id="0bfff-122">DependsOn</span><span class="sxs-lookup"><span data-stu-id="0bfff-122">DependsOn</span></span> |<span data-ttu-id="0bfff-123">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-123">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0bfff-124">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 ResourceName이고 해당 형식이 ResourceType일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-124">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |

## <a name="additional-information"></a><span data-ttu-id="0bfff-125">추가 정보</span><span class="sxs-lookup"><span data-stu-id="0bfff-125">Additional Information</span></span>

<span data-ttu-id="0bfff-126">**nxService** 리소스는 서비스 정의나 서비스에 대한 스크립트가 존재하지 않는 경우 만들지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-126">The **nxService** resource will not create a service definition or script for the service if it does not exist.</span></span> <span data-ttu-id="0bfff-127">PowerShell 필요한 상태 구성 **nxFile** 리소스를 사용하여 서비스 정의 파일 또는 스크립트의 존재 또는 내용을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-127">You can use the PowerShell Desired State Configuration **nxFile** Resource resource to manage the existence or contents of the service definition file or script.</span></span>

## <a name="example"></a><span data-ttu-id="0bfff-128">예제</span><span class="sxs-lookup"><span data-stu-id="0bfff-128">Example</span></span>

<span data-ttu-id="0bfff-129">다음 예에서는 **SystemD** 서비스 컨트롤러로 등록된 ‘httpd’ 서비스(Apache HTTP Server용)의 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="0bfff-129">The following example shows configuration of the 'httpd' service (for Apache HTTP Server), registered with the **SystemD** service controller.</span></span>

```powershell
Import-DSCResource -Module nx

Node $node
{
    #Apache Service
    nxService ApacheService {
        Name = 'httpd'
        State = 'running'
        Enabled = $true
        Controller = 'systemd'
    }
}
```