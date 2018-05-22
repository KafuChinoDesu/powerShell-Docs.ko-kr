---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: DSC 레지스트리 리소스
ms.openlocfilehash: 8819b3704fa1a61d2be5ce11c974542f48177e09
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-registry-resource"></a><span data-ttu-id="66e2b-103">DSC 레지스트리 리소스</span><span class="sxs-lookup"><span data-stu-id="66e2b-103">DSC Registry Resource</span></span>

> <span data-ttu-id="66e2b-104">적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="66e2b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="66e2b-105">PowerShell DSC(필요한 상태 구성)의 **레지스트리** 리소스에서는 대상 노드에 있는 레지스트리 키와 값을 관리하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-105">The **Registry** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage registry keys and values on a target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="66e2b-106">구문</span><span class="sxs-lookup"><span data-stu-id="66e2b-106">Syntax</span></span>

```
Registry [string] #ResourceName
{
    Key = [string]
    ValueName = [string]
    [ Ensure = [string] { Present | Absent }  ]
    [ Force =  [bool]   ]
    [ Hex = [bool] ]
    [ DependsOn = [string[]] ]
    [ ValueData = [string[]] ]
    [ ValueType = [string] { Binary | Dword | ExpandString | MultiString | Qword | String }  ]
}
```

## <a name="properties"></a><span data-ttu-id="66e2b-107">속성</span><span class="sxs-lookup"><span data-stu-id="66e2b-107">Properties</span></span>
|  <span data-ttu-id="66e2b-108">속성</span><span class="sxs-lookup"><span data-stu-id="66e2b-108">Property</span></span>  |  <span data-ttu-id="66e2b-109">설명</span><span class="sxs-lookup"><span data-stu-id="66e2b-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="66e2b-110">키</span><span class="sxs-lookup"><span data-stu-id="66e2b-110">Key</span></span>| <span data-ttu-id="66e2b-111">특정 상태를 확인하려는 레지스트리 키의 경로를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-111">Indicates the path of the registry key for which you want to ensure a specific state.</span></span> <span data-ttu-id="66e2b-112">이 경로는 하이브를 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-112">This path must include the hive.</span></span>|
| <span data-ttu-id="66e2b-113">ValueName</span><span class="sxs-lookup"><span data-stu-id="66e2b-113">ValueName</span></span>| <span data-ttu-id="66e2b-114">레지스트리 값의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-114">Indicates the name of the registry value.</span></span> <span data-ttu-id="66e2b-115">레지스트리 키를 추가하거나 제거하려면 ValueType 또는 ValueData를 지정하지 않고 이 속성을 빈 문자열로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-115">To add or remove a registry key, specify this property as an empty string without specifying ValueType or ValueData.</span></span> <span data-ttu-id="66e2b-116">레지스트리 키의 기본값을 수정하거나 제거하려면 ValueType 또는 ValueData도 지정하고 이 속성을 빈 문자열로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-116">To modify or remove the default value of a registry key, specify this property as an empty string while also specifying ValueType or ValueData.</span></span>|
| <span data-ttu-id="66e2b-117">Ensure</span><span class="sxs-lookup"><span data-stu-id="66e2b-117">Ensure</span></span>| <span data-ttu-id="66e2b-118">키와 값의 존재 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-118">Indicates if the key and value exist.</span></span> <span data-ttu-id="66e2b-119">존재하도록 하려면 이 속성을 "Present"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-119">To ensure that they do, set this property to "Present".</span></span> <span data-ttu-id="66e2b-120">존재하지 않도록 하려면 이 속성을 "Absent"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-120">To ensure that they do not exist, set the property to "Absent".</span></span> <span data-ttu-id="66e2b-121">기본값은 "Present"입니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-121">The default value is "Present".</span></span>|
| <span data-ttu-id="66e2b-122">Force</span><span class="sxs-lookup"><span data-stu-id="66e2b-122">Force</span></span>| <span data-ttu-id="66e2b-123">지정된 레지스트리 키가 있을 경우, __Force__를 사용하면 새 값으로 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-123">If the specified registry key is present, __Force__ overwrites it with the new value.</span></span> <span data-ttu-id="66e2b-124">하위 키가 포함된 레지스트리 키를 삭제하는 경우에는 이 속성을 __$true__로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-124">If deleting a registry key with subkeys, this needs to be __$true__</span></span>|
| <span data-ttu-id="66e2b-125">Hex</span><span class="sxs-lookup"><span data-stu-id="66e2b-125">Hex</span></span>| <span data-ttu-id="66e2b-126">데이터가 16진수 형식으로 표현될 것인지 여부를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-126">Indicates if data will be expressed in hexadecimal format.</span></span> <span data-ttu-id="66e2b-127">지정하는 경우 DWORD/QWORD 값 데이터가 16진수 형식으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-127">If specified, the DWORD/QWORD value data is presented in hexadecimal format.</span></span> <span data-ttu-id="66e2b-128">다른 형식에 대해서는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-128">Not valid for other types.</span></span> <span data-ttu-id="66e2b-129">기본값은 __$false__입니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-129">The default value is __$false__.</span></span>|
| <span data-ttu-id="66e2b-130">DependsOn</span><span class="sxs-lookup"><span data-stu-id="66e2b-130">DependsOn</span></span>| <span data-ttu-id="66e2b-131">이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-131">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="66e2b-132">예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-132">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="66e2b-133">ValueData</span><span class="sxs-lookup"><span data-stu-id="66e2b-133">ValueData</span></span>| <span data-ttu-id="66e2b-134">레지스트리 값에 대한 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-134">The data for the registry value.</span></span>|
| <span data-ttu-id="66e2b-135">ValueType</span><span class="sxs-lookup"><span data-stu-id="66e2b-135">ValueType</span></span>| <span data-ttu-id="66e2b-136">값의 형식을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-136">Indicates the type of the value.</span></span> <span data-ttu-id="66e2b-137">지원되는 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-137">The supported types are:</span></span>
<ul><li><span data-ttu-id="66e2b-138">문자열(REG_SZ)</span><span class="sxs-lookup"><span data-stu-id="66e2b-138">String (REG_SZ)</span></span></li>


<li><span data-ttu-id="66e2b-139">이진수(REG-BINARY)</span><span class="sxs-lookup"><span data-stu-id="66e2b-139">Binary (REG-BINARY)</span></span></li>


<li><span data-ttu-id="66e2b-140">Dword 32비트(REG_DWORD)</span><span class="sxs-lookup"><span data-stu-id="66e2b-140">Dword 32-bit (REG_DWORD)</span></span></li>


<li><span data-ttu-id="66e2b-141">Qword 64비트(REG_QWORD)</span><span class="sxs-lookup"><span data-stu-id="66e2b-141">Qword 64-bit (REG_QWORD)</span></span></li>


<li><span data-ttu-id="66e2b-142">다중 문자열(REG_MULTI_SZ)</span><span class="sxs-lookup"><span data-stu-id="66e2b-142">Multi-string (REG_MULTI_SZ)</span></span></li>


<li><span data-ttu-id="66e2b-143">확장 가능한 문자열(REG_EXPAND_SZ)</span><span class="sxs-lookup"><span data-stu-id="66e2b-143">Expandable string (REG_EXPAND_SZ)</span></span></li></ul>

## <a name="example"></a><span data-ttu-id="66e2b-144">예제</span><span class="sxs-lookup"><span data-stu-id="66e2b-144">Example</span></span>
<span data-ttu-id="66e2b-145">이 예제에서는 "ExampleKey"라는 키가 **HKEY\_LOCAL\_MACHINE** 하이브에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-145">This example ensures that a key named "ExampleKey" is present in the **HKEY\_LOCAL\_MACHINE** hive.</span></span>
```powershell
Configuration RegistryTest
{
    Registry RegistryExample
    {
        Ensure      = "Present"  # You can also set Ensure to "Absent"
        Key         = "HKEY_LOCAL_MACHINE\SOFTWARE\ExampleKey"
        ValueName   = "TestValue"
        ValueData   = "TestData"
    }
}
```

><span data-ttu-id="66e2b-146">**참고:** **HKEY\_CURRENT\_USER** 하이브에서 레지스트리 설정을 변경하려면 구성이 시스템이 아닌 사용자 자격 증명을 사용하여 실행되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-146">**Note:** Changing a registry setting in the **HKEY\_CURRENT\_USER** hive requires that the configuration runs with user credentials, rather than as the system.</span></span>
><span data-ttu-id="66e2b-147">**PsDscRunAsCredential** 속성을 사용하여 구성에 대한 사용자 자격 증명을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66e2b-147">You can use the **PsDscRunAsCredential** property to specify user credentials for the configuration.</span></span> <span data-ttu-id="66e2b-148">예제는 [사용자 자격 증명을 사용하여 DSC 실행](runAsUser.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="66e2b-148">For an example, see [Running DSC with user credentials](runAsUser.md)</span></span>
