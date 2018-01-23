---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "DSC WindowsProcess 리소스"
ms.openlocfilehash: ec77209637d574a0e530f4cce283e1ad98701cdb
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-windowsprocess-resource"></a><span data-ttu-id="b4859-103">DSC WindowsProcess 리소스</span><span class="sxs-lookup"><span data-stu-id="b4859-103">DSC WindowsProcess Resource</span></span>

> <span data-ttu-id="b4859-104">적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="b4859-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="b4859-105">Windows PowerShell DSC(필요한 상태 구성)의 **WindowsProcess** 리소스에서는 대상 노드에서 프로세스를 구성하는 메커니즘을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-105">The **WindowsProcess** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to configure processes on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="b4859-106">구문</span><span class="sxs-lookup"><span data-stu-id="b4859-106">Syntax</span></span>

```
WindowsProcess [string] #ResourceName
{
    Arguments = [string]
    Path = [string]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ DependsOn = [string[]] ]
    [ StandardErrorPath = [string] ]
    [ StandardInputPath = [string] ]
    [ StandardOutputPath = [string] ]
    [ WorkingDirectory = [string] ]
}
```

## <a name="properties"></a><span data-ttu-id="b4859-107">속성</span><span class="sxs-lookup"><span data-stu-id="b4859-107">Properties</span></span>
|  <span data-ttu-id="b4859-108">속성</span><span class="sxs-lookup"><span data-stu-id="b4859-108">Property</span></span>  |  <span data-ttu-id="b4859-109">설명</span><span class="sxs-lookup"><span data-stu-id="b4859-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="b4859-110">인수</span><span class="sxs-lookup"><span data-stu-id="b4859-110">Arguments</span></span>| <span data-ttu-id="b4859-111">프로세스에 그대로 전달할 인수의 문자열을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-111">Indicates a string of arguments to pass to the process as-is.</span></span> <span data-ttu-id="b4859-112">몇 개의 인수를 전달해야 하는 경우 모두 이 문자열에 넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-112">If you need to pass several arguments, put them all in this string.</span></span>| 
| <span data-ttu-id="b4859-113">경로</span><span class="sxs-lookup"><span data-stu-id="b4859-113">Path</span></span>| <span data-ttu-id="b4859-114">프로세스 실행 파일의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-114">The path to the process executable.</span></span> <span data-ttu-id="b4859-115">실행 파일의 정규화된 경로가 아니라 파일 이름인 경우 DSC 리소스는 환경 **Path** 변수(`$env:Path`)를 검색하여 실행 파일을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-115">If this the file name of the executable (not the fully qualified path), the DSC resource will search the environment **Path** variable (`$env:Path`) to find the executable file.</span></span> <span data-ttu-id="b4859-116">이 속성의 값이 정규화된 경로인 경우 DSC는 **Path** 환경 변수를 사용하여 파일을 찾지 않으며 경로가 없는 경우 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-116">If the value of this property is a fully qualified path, DSC will not use the **Path** environment variable to find the file, and will throw an error if the path does not exist.</span></span> <span data-ttu-id="b4859-117">상대 경로는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-117">Relative paths are not allowed.</span></span>| 
| <span data-ttu-id="b4859-118">자격 증명</span><span class="sxs-lookup"><span data-stu-id="b4859-118">Credential</span></span>| <span data-ttu-id="b4859-119">프로세스를 시작하기 위한 자격 증명을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-119">Indicates the credentials for starting the process.</span></span>| 
| <span data-ttu-id="b4859-120">Ensure</span><span class="sxs-lookup"><span data-stu-id="b4859-120">Ensure</span></span>| <span data-ttu-id="b4859-121">프로세스가 존재하는지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-121">Indicates if the process exists.</span></span> <span data-ttu-id="b4859-122">프로세스가 존재하도록 하려면 이 속성을 "Present"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-122">Set this property to "Present" to ensure that the process exists.</span></span> <span data-ttu-id="b4859-123">그렇지 않으면, "Absent"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-123">Otherwise, set it to "Absent".</span></span> <span data-ttu-id="b4859-124">기본값은 "Present"입니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-124">The default is "Present".</span></span>| 
| <span data-ttu-id="b4859-125">DependsOn</span><span class="sxs-lookup"><span data-stu-id="b4859-125">DependsOn</span></span> | <span data-ttu-id="b4859-126">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-126">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="b4859-127">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 \`DependsOn = "[ResourceType]ResourceName"\`\`입니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-127">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\` .</span></span>| 
| <span data-ttu-id="b4859-128">StandardErrorPath</span><span class="sxs-lookup"><span data-stu-id="b4859-128">StandardErrorPath</span></span>| <span data-ttu-id="b4859-129">표준 오류를 쓸 디렉터리 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-129">Indicates the directory path to write the standard error.</span></span> <span data-ttu-id="b4859-130">거기에 있던 기존 파일은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-130">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="b4859-131">StandardInputPath</span><span class="sxs-lookup"><span data-stu-id="b4859-131">StandardInputPath</span></span>| <span data-ttu-id="b4859-132">표준 입력 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-132">Indicates the standard input location.</span></span>| 
| <span data-ttu-id="b4859-133">StandardOutputPath</span><span class="sxs-lookup"><span data-stu-id="b4859-133">StandardOutputPath</span></span>| <span data-ttu-id="b4859-134">표준 출력을 쓸 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-134">Indicates the location to write the standard output.</span></span> <span data-ttu-id="b4859-135">거기에 있던 기존 파일은 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-135">Any existing file there will be overwritten.</span></span>| 
| <span data-ttu-id="b4859-136">WorkingDirectory</span><span class="sxs-lookup"><span data-stu-id="b4859-136">WorkingDirectory</span></span>| <span data-ttu-id="b4859-137">프로세스에 대한 현재 작업 디렉터리로 사용할 위치를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="b4859-137">Indicates the location that will be used as the current working directory for the process.</span></span>| 

