---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: MSFT_DSCLocalConfigurationManager 클래스의 EnableDebugConfiguration 메서드
ms.openlocfilehash: b2eaebfa901cb5d93fd0183287073e6b31f975d1
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892402"
---
# <a name="enabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a9024-103">MSFT_DSCLocalConfigurationManager 클래스의 EnableDebugConfiguration 메서드</span><span class="sxs-lookup"><span data-stu-id="a9024-103">EnableDebugConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a9024-104">DSC 리소스 디버깅을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9024-104">Enables DSC resource debugging.</span></span>

## <a name="syntax"></a><span data-ttu-id="a9024-105">구문</span><span class="sxs-lookup"><span data-stu-id="a9024-105">Syntax</span></span>

```mof
uint32 EnableDebugConfiguration(
  [in] boolean BreakAll
);
```

## <a name="parameters"></a><span data-ttu-id="a9024-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="a9024-106">Parameters</span></span>

<span data-ttu-id="a9024-107">*BreakAll* \[in\] 리소스 스크립트의 모든 줄에 중단점을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a9024-107">*BreakAll* \[in\] Sets a breakpoint at every line in the resource script.</span></span>

## <a name="return-value"></a><span data-ttu-id="a9024-108">반환 값</span><span class="sxs-lookup"><span data-stu-id="a9024-108">Return value</span></span>

<span data-ttu-id="a9024-109">성공하면 0을 반환하고 그렇지 않으면 오류 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a9024-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a9024-110">설명</span><span class="sxs-lookup"><span data-stu-id="a9024-110">Remarks</span></span>

<span data-ttu-id="a9024-111">정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="a9024-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a9024-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="a9024-112">Requirements</span></span>

<span data-ttu-id="a9024-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a9024-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="a9024-114">**네임스페이스**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a9024-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="a9024-115">참고 항목</span><span class="sxs-lookup"><span data-stu-id="a9024-115">See also</span></span>

[<span data-ttu-id="a9024-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a9024-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)