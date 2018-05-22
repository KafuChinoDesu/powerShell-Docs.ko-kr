---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: DSC ProcessSet 리소스
ms.openlocfilehash: 412cf1076996126f0d9b7a9a8ebbc9bdb7ecf377
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="163af-103">DSC WindowsProcess 리소스</span><span class="sxs-lookup"><span data-stu-id="163af-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="163af-104">적용 대상: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="163af-104">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="163af-105">Windows PowerShell DSC(필요한 상태 구성)의 **ProcessSet** 리소스에서는 대상 노드에서 프로세스를 구성하는 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="163af-105">The **ProcessSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span> <span data-ttu-id="163af-106">이 리소스는 `GroupName` 매개 변수에 지정된 각 그룹에 대해 [WindowsProcess 리소스](windowsProcessResource.md)를 호출하는 [복합 리소스](authoringResourceComposite.md)입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-106">This resource is a [composite resource](authoringResourceComposite.md) that calls the [WindowsProcess resource](windowsProcessResource.md) for each group specified in the `GroupName` parameter.</span></span>

## <a name="syntax"></a><span data-ttu-id="163af-107">구문</span><span class="sxs-lookup"><span data-stu-id="163af-107">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ StandardOutputPath = [string] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ WorkingDirectory = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="163af-108">속성</span><span class="sxs-lookup"><span data-stu-id="163af-108">Properties</span></span>
|  <span data-ttu-id="163af-109">속성</span><span class="sxs-lookup"><span data-stu-id="163af-109">Property</span></span>  |  <span data-ttu-id="163af-110">설명</span><span class="sxs-lookup"><span data-stu-id="163af-110">Description</span></span>   |
|---|---|
| <span data-ttu-id="163af-111">인수</span><span class="sxs-lookup"><span data-stu-id="163af-111">Arguments</span></span>| <span data-ttu-id="163af-112">프로세스에 그대로 전달할 인수를 포함하는 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-112">A string that contains arguments to pass to the process as-is.</span></span> <span data-ttu-id="163af-113">몇 개의 인수를 전달해야 하는 경우 모두 이 문자열에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="163af-113">If you need to pass several arguments, put them all in this string.</span></span>|
| <span data-ttu-id="163af-114">경로</span><span class="sxs-lookup"><span data-stu-id="163af-114">Path</span></span>| <span data-ttu-id="163af-115">프로세스 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-115">The paths to the process executables.</span></span> <span data-ttu-id="163af-116">실행 파일의 정규화된 경로가 아니라 파일 이름인 경우 DSC 리소스는 환경 **Path** 변수(`$env:Path`)를 검색하여 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="163af-116">If these are the names of the executable files (not fully qualified paths), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the files.</span></span> <span data-ttu-id="163af-117">이 속성의 값이 정규화된 경로인 경우 DSC는 **Path** 환경 변수를 사용하여 파일을 찾지 않으며 경로가 없는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="163af-117">If the values of this property are fully qualified paths, DSC will not use the **Path** environment variable to find the files, and will throw an error if any of the paths do not exist.</span></span> <span data-ttu-id="163af-118">상대 경로는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="163af-118">Relative paths are not allowed.</span></span>|
| <span data-ttu-id="163af-119">자격 증명</span><span class="sxs-lookup"><span data-stu-id="163af-119">Credential</span></span>| <span data-ttu-id="163af-120">프로세스를 시작하기 위한 자격 증명을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="163af-120">Indicates the credentials for starting the process.</span></span>|
| <span data-ttu-id="163af-121">Ensure</span><span class="sxs-lookup"><span data-stu-id="163af-121">Ensure</span></span>| <span data-ttu-id="163af-122">프로세스가 존재하는지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="163af-122">Specifies whether the processes exists.</span></span> <span data-ttu-id="163af-123">프로세스가 존재하도록 하려면 이 속성을 "Present"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="163af-123">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="163af-124">그렇지 않으면, "Absent"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="163af-124">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="163af-125">기본값은 "Present"입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-125">The default is "Present".</span></span>|
| <span data-ttu-id="163af-126">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="163af-126">StandardErrorPath</span></span>| <span data-ttu-id="163af-127">프로세스가 표준 오류를 쓰는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-127">The path to which the processes write standard error.</span></span> <span data-ttu-id="163af-128">거기에 있던 기존 파일은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="163af-128">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="163af-129">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="163af-129">StandardInputPath</span></span>| <span data-ttu-id="163af-130">프로세스가 표준 입력을 받는 스트림입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-130">The stream from which the process receives standard input.</span></span>|
| <span data-ttu-id="163af-131">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="163af-131">StandardOutputPath</span></span>| <span data-ttu-id="163af-132">프로세스가 표준 출력을 쓰는 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-132">The path of the file to which the processes write standard output.</span></span> <span data-ttu-id="163af-133">거기에 있던 기존 파일은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="163af-133">Any existing file there will be overwritten.</span></span>|
| <span data-ttu-id="163af-134">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="163af-134">WorkingDirectory</span></span>| <span data-ttu-id="163af-135">프로세스에 대한 현재 작업 디렉터리로 사용되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-135">The location used as the current working directory for the processes.</span></span>|
| <span data-ttu-id="163af-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="163af-136">DependsOn</span></span> | <span data-ttu-id="163af-137">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="163af-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="163af-138">예를 들어 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 **ResourceName**이고 해당 형식이 **_ResourceType**일 경우, 이 속성을 사용하는 구문은 \`DependsOn = "[ResourceType]ResourceName"\`\`입니다.</span><span class="sxs-lookup"><span data-stu-id="163af-138">For example, if the ID of the resource configuration script block that you want to run first is **ResourceName** and its type is **_ResourceType**, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\` .</span></span>|