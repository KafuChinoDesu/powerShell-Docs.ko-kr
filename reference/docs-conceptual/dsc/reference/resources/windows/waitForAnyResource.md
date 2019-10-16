---
ms.date: 09/20/2019
keywords: dsc,powershell,configuration,setup
title: DSC WaitForAny 리소스
ms.openlocfilehash: 61fee456d2652e08ed9bdbe64457627ff5b2e145
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71953000"
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="017d4-103">DSC WaitForAny 리소스</span><span class="sxs-lookup"><span data-stu-id="017d4-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="017d4-104">적용 대상: Windows PowerShell 5.1</span><span class="sxs-lookup"><span data-stu-id="017d4-104">Applies To: Windows PowerShell 5.1</span></span>

<span data-ttu-id="017d4-105">**WaitForAny** DSC(Desired State Configuration) 리소스를 [DSC 구성](../../../configurations/configurations.md)의 노드 블록 내에서 사용하면 다른 노드의 구성에 대한 종속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-105">The **WaitForAny** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](../../../configurations/configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="017d4-106">**ResourceName** 속성으로 지정된 리소스가 **NodeName** 속성으로 정의된 임의의 대상 노드에서 필요한 상태이면 이 리소스가 정상적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-106">This resource succeeds if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>

> [!NOTE]
> <span data-ttu-id="017d4-107">**WaitForAny** 리소스는 Windows 원격 관리를 사용하여 다른 노드의 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-107">**WaitForAny** resource uses Windows Remote Management to check the state of other Nodes.</span></span> <span data-ttu-id="017d4-108">WinRM에 대한 포트 및 보안 요구 사항에 대한 자세한 내용은 [PowerShell Remoting 보안 고려 사항](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="017d4-108">For more information about port and security requirements for WinRM, see [PowerShell Remoting Security Considerations](/powershell/scripting/learn/remoting/winrmsecurity?view=powershell-6).</span></span>

## <a name="syntax"></a><span data-ttu-id="017d4-109">구문</span><span class="sxs-lookup"><span data-stu-id="017d4-109">Syntax</span></span>

```Syntax
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string[]]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ]
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a><span data-ttu-id="017d4-110">속성</span><span class="sxs-lookup"><span data-stu-id="017d4-110">Properties</span></span>

|<span data-ttu-id="017d4-111">속성</span><span class="sxs-lookup"><span data-stu-id="017d4-111">Property</span></span> |<span data-ttu-id="017d4-112">설명</span><span class="sxs-lookup"><span data-stu-id="017d4-112">Description</span></span> |
|---|---|
|<span data-ttu-id="017d4-113">ResourceName</span><span class="sxs-lookup"><span data-stu-id="017d4-113">ResourceName</span></span> |<span data-ttu-id="017d4-114">사용할 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-114">The resource name to depend on.</span></span> <span data-ttu-id="017d4-115">이 리소스가 다른 구성에 속하면 `[ResourceType]ResourceName::[ConfigurationName]::[ConfigurationName]`으로 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-115">If this resource belongs to a different configuration, format the name as `[ResourceType]ResourceName::[ConfigurationName]::[ConfigurationName]`.</span></span> |
|<span data-ttu-id="017d4-116">NodeName</span><span class="sxs-lookup"><span data-stu-id="017d4-116">NodeName</span></span> |<span data-ttu-id="017d4-117">사용할 리소스의 대상 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-117">The target nodes of the resource to depend on.</span></span> |
|<span data-ttu-id="017d4-118">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="017d4-118">RetryIntervalSec</span></span> |<span data-ttu-id="017d4-119">다시 시도할 때까지의 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-119">The number of seconds before retrying.</span></span> <span data-ttu-id="017d4-120">최소값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-120">Minimum is 1.</span></span> |
|<span data-ttu-id="017d4-121">RetryCount</span><span class="sxs-lookup"><span data-stu-id="017d4-121">RetryCount</span></span> |<span data-ttu-id="017d4-122">최대 다시 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-122">The maximum number of times to retry.</span></span> |
|<span data-ttu-id="017d4-123">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="017d4-123">ThrottleLimit</span></span> |<span data-ttu-id="017d4-124">동시에 연결하는 컴퓨터의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-124">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="017d4-125">기본값은 `New-CimSession` 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-125">Default is `New-CimSession` default.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="017d4-126">공용 속성</span><span class="sxs-lookup"><span data-stu-id="017d4-126">Common properties</span></span>

|<span data-ttu-id="017d4-127">속성</span><span class="sxs-lookup"><span data-stu-id="017d4-127">Property</span></span> |<span data-ttu-id="017d4-128">설명</span><span class="sxs-lookup"><span data-stu-id="017d4-128">Description</span></span> |
|---|---|
|<span data-ttu-id="017d4-129">DependsOn</span><span class="sxs-lookup"><span data-stu-id="017d4-129">DependsOn</span></span> |<span data-ttu-id="017d4-130">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-130">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="017d4-131">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 ResourceName이고 해당 형식이 ResourceType일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-131">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |
|<span data-ttu-id="017d4-132">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="017d4-132">PsDscRunAsCredential</span></span> |<span data-ttu-id="017d4-133">전체 리소스를 실행하기 위한 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-133">Sets the credential for running the entire resource as.</span></span> |

> [!NOTE]
> <span data-ttu-id="017d4-134">**PsDscRunAsCredential** 공용 속성은 다른 자격 증명의 컨텍스트에서 DSC 리소스를 실행할 수 있도록 WMF 5.0에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="017d4-134">The **PsDscRunAsCredential** common property was added in WMF 5.0 to allow running any DSC resource in the context of other credentials.</span></span> <span data-ttu-id="017d4-135">자세한 내용은 [ DSC 리소스로 자격 증명 사용](../../../configurations/runasuser.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="017d4-135">For more information, see [Use Credentials with DSC Resources](../../../configurations/runasuser.md).</span></span>

## <a name="example"></a><span data-ttu-id="017d4-136">예제</span><span class="sxs-lookup"><span data-stu-id="017d4-136">Example</span></span>

<span data-ttu-id="017d4-137">이 리소스를 사용하는 방법의 예제를 보려면 [노드 간 종속성 지정](../../../configurations/crossNodeDependencies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="017d4-137">For an example of how to use this resource, see [Specifying cross-node dependencies](../../../configurations/crossNodeDependencies.md)</span></span>