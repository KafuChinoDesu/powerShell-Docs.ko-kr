---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "MSFT_DSCLocalConfigurationManager 클래스의 ResourceTest 메서드"
ms.openlocfilehash: 3c88f74c5f623502e8cbe0d7aa7390fca75569a9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="resourcetest-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9d6dd-103">MSFT_DSCLocalConfigurationManager 클래스의 ResourceTest 메서드</span><span class="sxs-lookup"><span data-stu-id="9d6dd-103">ResourceTest method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9d6dd-104">DSC 리소스의 **Test** 메서드를 직접 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-104">Directly calls the **Test** method of a DSC resource.</span></span>

<a name="syntax"></a><span data-ttu-id="9d6dd-105">구문</span><span class="sxs-lookup"><span data-stu-id="9d6dd-105">Syntax</span></span>
------

```mof
uint32 ResourceTest(
  [in]  string  ResourceType,
  [in]  string  ModuleName,
  [in]  uint8   resourceProperty[],
  [out] boolean InDesiredState
);
```

<a name="parameters"></a><span data-ttu-id="9d6dd-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="9d6dd-106">Parameters</span></span>
----------

<span data-ttu-id="9d6dd-107">*ResourceType* \[in\]</span><span class="sxs-lookup"><span data-stu-id="9d6dd-107">*ResourceType* \[in\]</span></span>  
<span data-ttu-id="9d6dd-108">호출할 리소스의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-108">The name of the resource to call.</span></span>

<span data-ttu-id="9d6dd-109">*ModuleName* \[in\]</span><span class="sxs-lookup"><span data-stu-id="9d6dd-109">*ModuleName* \[in\]</span></span>  
<span data-ttu-id="9d6dd-110">호출할 리소스를 포함하는 모듈의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-110">The name of the module that contains the resource to call.</span></span>

<span data-ttu-id="9d6dd-111">*resourceProperty* \[in\]</span><span class="sxs-lookup"><span data-stu-id="9d6dd-111">*resourceProperty* \[in\]</span></span>  
<span data-ttu-id="9d6dd-112">해시 테이블의 리소스 속성 이름 및 해당 값을 키와 값으로 각각 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-112">Specifies the resource property name and its value in a hash table as key and value, respectively.</span></span> <span data-ttu-id="9d6dd-113">[Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet을 사용하여 리소스 속성 및 해당 종류를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-113">Use the [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet to discover resource properties and their types.</span></span>

<span data-ttu-id="9d6dd-114">*InDesiredState* \[out\]</span><span class="sxs-lookup"><span data-stu-id="9d6dd-114">*InDesiredState* \[out\]</span></span>  
<span data-ttu-id="9d6dd-115">반환 시, 대상 노드가 원하는 상태이면 이 속성이 **true**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-115">On return, this property is set to **true** if the target node is in the desired state.</span></span>

## <a name="return-value"></a><span data-ttu-id="9d6dd-116">반환 값</span><span class="sxs-lookup"><span data-stu-id="9d6dd-116">Return value</span></span>
------------

<span data-ttu-id="9d6dd-117">성공하면 0을 반환하고 그렇지 않으면 오류 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-117">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9d6dd-118">설명</span><span class="sxs-lookup"><span data-stu-id="9d6dd-118">Remarks</span></span>

<span data-ttu-id="9d6dd-119">정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="9d6dd-119">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9d6dd-120">요구 사항</span><span class="sxs-lookup"><span data-stu-id="9d6dd-120">Requirements</span></span>
------------
><span data-ttu-id="9d6dd-121">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9d6dd-121">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="9d6dd-122">**네임스페이스**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9d6dd-122">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="9d6dd-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="9d6dd-123">See also</span></span>


[<span data-ttu-id="9d6dd-124">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9d6dd-124">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



