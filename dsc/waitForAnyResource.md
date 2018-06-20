---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: DSC WaitForAny 리소스
ms.openlocfilehash: c9700c908f8601db85f9c922445969a34b59d453
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2018
ms.locfileid: "34186714"
---
# <a name="dsc-waitforany-resource"></a><span data-ttu-id="27645-103">DSC WaitForAny 리소스</span><span class="sxs-lookup"><span data-stu-id="27645-103">DSC WaitForAny Resource</span></span>

> <span data-ttu-id="27645-104">적용 대상: Windows PowerShell 5.1 이상</span><span class="sxs-lookup"><span data-stu-id="27645-104">Applies To: Windows PowerShell 5.1 and later</span></span>

<span data-ttu-id="27645-105">**WaitForSome** DSC(Desired State Configuration) 리소스를 [DSC 구성](configurations.md)의 노드 블록 내에서 사용하면 다른 노드의 구성에 대한 종속성을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="27645-105">The **WaitForSome** Desired State Configuration (DSC) resource can be used within a node block in a [DSC configuration](configurations.md) to specify dependencies on configurations on other nodes.</span></span>

<span data-ttu-id="27645-106">**ResourceName** 속성으로 지정된 리소스가 **NodeName** 속성으로 정의된 임의의 대상 노드에서 필요한 상태이면 이 리소스가 정상적으로 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="27645-106">This resource succeeds if if the resource specified by the **ResourceName** property is in the desired state on any target nodes defined in the **NodeName** property.</span></span>


## <a name="syntax"></a><span data-ttu-id="27645-107">구문</span><span class="sxs-lookup"><span data-stu-id="27645-107">Syntax</span></span>

```
WaitForAny [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ]
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="27645-108">속성</span><span class="sxs-lookup"><span data-stu-id="27645-108">Properties</span></span>

|  <span data-ttu-id="27645-109">속성</span><span class="sxs-lookup"><span data-stu-id="27645-109">Property</span></span>  |  <span data-ttu-id="27645-110">설명</span><span class="sxs-lookup"><span data-stu-id="27645-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="27645-111">ResourceName</span><span class="sxs-lookup"><span data-stu-id="27645-111">ResourceName</span></span>| <span data-ttu-id="27645-112">사용할 리소스 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-112">The resource name to depend on.</span></span> <span data-ttu-id="27645-113">이 리소스가 다른 구성에 속하는 경우 "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"으로 이름의 형식을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="27645-113">If this resource belongs to a different configuration, format the name as "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"</span></span>|
| <span data-ttu-id="27645-114">NodeName</span><span class="sxs-lookup"><span data-stu-id="27645-114">NodeName</span></span>| <span data-ttu-id="27645-115">사용할 리소스의 대상 노드입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-115">The target nodes of the resource to depend on.</span></span>|
| <span data-ttu-id="27645-116">RetryIntervalSec</span><span class="sxs-lookup"><span data-stu-id="27645-116">RetryIntervalSec</span></span>| <span data-ttu-id="27645-117">다시 시도할 때까지의 시간(초)입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-117">The number of seconds before retrying.</span></span> <span data-ttu-id="27645-118">최소값은 1입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-118">Minimum is 1.</span></span>|
| <span data-ttu-id="27645-119">RetryCount</span><span class="sxs-lookup"><span data-stu-id="27645-119">RetryCount</span></span>| <span data-ttu-id="27645-120">최대 다시 시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-120">The maximum number of times to retry.</span></span>|
| <span data-ttu-id="27645-121">ThrottleLimit</span><span class="sxs-lookup"><span data-stu-id="27645-121">ThrottleLimit</span></span>| <span data-ttu-id="27645-122">동시에 연결하는 컴퓨터의 수입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-122">Number of machines to connect simultaneously.</span></span> <span data-ttu-id="27645-123">기본값은 new-cimsession 기본값입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-123">Default is new-cimsession default.</span></span>|
| <span data-ttu-id="27645-124">DependsOn</span><span class="sxs-lookup"><span data-stu-id="27645-124">DependsOn</span></span> | <span data-ttu-id="27645-125">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="27645-125">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="27645-126">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="27645-126">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|


## <a name="example"></a><span data-ttu-id="27645-127">예제</span><span class="sxs-lookup"><span data-stu-id="27645-127">Example</span></span>

<span data-ttu-id="27645-128">이 리소스를 사용하는 방법의 예제를 보려면 [노드 간 종속성 지정](crossNodeDependencies.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="27645-128">For an example of how to use this resource, see [Specifying cross-node dependencies](crossNodeDependencies.md)</span></span>