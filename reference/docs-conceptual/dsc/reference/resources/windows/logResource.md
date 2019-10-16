---
ms.date: 09/20/2019
keywords: dsc,powershell,configuration,setup
title: DSC 로그 리소스
ms.openlocfilehash: a1b7bf44fbaf36a3adaf0666e9f0a754fa3f6ee1
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71954670"
---
# <a name="dsc-log-resource"></a><span data-ttu-id="321e0-103">DSC 로그 리소스</span><span class="sxs-lookup"><span data-stu-id="321e0-103">DSC Log Resource</span></span>

> <span data-ttu-id="321e0-104">적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.x</span><span class="sxs-lookup"><span data-stu-id="321e0-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.x</span></span>

<span data-ttu-id="321e0-105">Windows PowerShell DSC(필요한 상태 구성)의 **Log** 리소스에서는 메시지를 Microsoft-Windows-필요한 상태 구성/분석 이벤트 로그에 쓰는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-105">The **Log** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to write messages to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

## <a name="syntax"></a><span data-ttu-id="321e0-106">구문</span><span class="sxs-lookup"><span data-stu-id="321e0-106">Syntax</span></span>

```Syntax
Log [string] #ResourceName
{
    Message = [string]
    [ DependsOn = [string[]] ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

> [!NOTE]
> <span data-ttu-id="321e0-107">기본적으로 DSC에 대한 작업 로그만 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-107">By default only the Operational logs for DSC are enabled.</span></span> <span data-ttu-id="321e0-108">분석 로그를 사용할 수 있거나 볼 수 있으려면 먼저 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-108">Before the Analytic log will be available or visible, it must be enabled.</span></span> <span data-ttu-id="321e0-109">자세한 내용은 [DSC 이벤트 로그는 어디에 있나요?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="321e0-109">For more information, see [Where are DSC Event Logs?](../../../troubleshooting/troubleshooting.md#where-are-dsc-event-logs).</span></span>

## <a name="properties"></a><span data-ttu-id="321e0-110">속성</span><span class="sxs-lookup"><span data-stu-id="321e0-110">Properties</span></span>

|<span data-ttu-id="321e0-111">속성</span><span class="sxs-lookup"><span data-stu-id="321e0-111">Property</span></span> |<span data-ttu-id="321e0-112">설명</span><span class="sxs-lookup"><span data-stu-id="321e0-112">Description</span></span> |
|---|---|
|<span data-ttu-id="321e0-113">메시지</span><span class="sxs-lookup"><span data-stu-id="321e0-113">Message</span></span> |<span data-ttu-id="321e0-114">Microsoft-Windows-필요한 상태 구성/분석 이벤트 로그에 쓸 메시지를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-114">Indicates the message you want to write to the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span> |

## <a name="common-properties"></a><span data-ttu-id="321e0-115">공용 속성</span><span class="sxs-lookup"><span data-stu-id="321e0-115">Common properties</span></span>

|<span data-ttu-id="321e0-116">속성</span><span class="sxs-lookup"><span data-stu-id="321e0-116">Property</span></span> |<span data-ttu-id="321e0-117">설명</span><span class="sxs-lookup"><span data-stu-id="321e0-117">Description</span></span> |
|---|---|
|<span data-ttu-id="321e0-118">DependsOn</span><span class="sxs-lookup"><span data-stu-id="321e0-118">DependsOn</span></span> |<span data-ttu-id="321e0-119">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-119">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="321e0-120">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 ResourceName이고 해당 형식이 ResourceType일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-120">For example, if the ID of the resource configuration script block that you want to run first is ResourceName and its type is ResourceType, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span> |
|<span data-ttu-id="321e0-121">PsDscRunAsCredential</span><span class="sxs-lookup"><span data-stu-id="321e0-121">PsDscRunAsCredential</span></span> |<span data-ttu-id="321e0-122">전체 리소스를 실행하기 위한 자격 증명을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-122">Sets the credential for running the entire resource as.</span></span> |

> [!NOTE]
> <span data-ttu-id="321e0-123">**PsDscRunAsCredential** 공용 속성은 다른 자격 증명의 컨텍스트에서 DSC 리소스를 실행할 수 있도록 WMF 5.0에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-123">The **PsDscRunAsCredential** common property was added in WMF 5.0 to allow running any DSC resource in the context of other credentials.</span></span> <span data-ttu-id="321e0-124">자세한 내용은 [ DSC 리소스로 자격 증명 사용](../../../configurations/runasuser.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="321e0-124">For more information, see [Use Credentials with DSC Resources](../../../configurations/runasuser.md).</span></span>

## <a name="example"></a><span data-ttu-id="321e0-125">예제</span><span class="sxs-lookup"><span data-stu-id="321e0-125">Example</span></span>

<span data-ttu-id="321e0-126">다음 예제에서는 Microsoft-Windows-필요한 상태 구성/분석 이벤트 로그에 메시지를 포함하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-126">The following example shows how to include a message in the Microsoft-Windows-Desired State Configuration/Analytic event log.</span></span>

> [!NOTE]
> <span data-ttu-id="321e0-127">이 리소스를 구성한 상태에서 [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx)을 실행하는 경우 항상 **$false**를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="321e0-127">If you run [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) with this resource configured, it will always return **$false**.</span></span>

```powershell
Configuration logResourceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node localhost
    {
        Log LogExample
        {
            Message = 'This message will appear in the Microsoft-Windows-Desired State Configuration/Analytic event log.'
        }
    }
}
```