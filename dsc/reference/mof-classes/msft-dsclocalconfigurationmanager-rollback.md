---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: MSFT_DSCLocalConfigurationManager 클래스의 RollBack 메서드
ms.openlocfilehash: 4956900ecd2c9cb7f2e2b5bcab94616f9f5d5565
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MTE95
ms.contentlocale: ko-KR
ms.lasthandoff: 01/04/2019
ms.locfileid: "54047733"
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="d2422-103">MSFT_DSCLocalConfigurationManager 클래스의 RollBack 메서드</span><span class="sxs-lookup"><span data-stu-id="d2422-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="d2422-104">이전 버전으로 구성을 롤백합니다.</span><span class="sxs-lookup"><span data-stu-id="d2422-104">Rolls back the configuration to a previous version.</span></span>

## <a name="syntax"></a><span data-ttu-id="d2422-105">구문</span><span class="sxs-lookup"><span data-stu-id="d2422-105">Syntax</span></span>

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

## <a name="parameters"></a><span data-ttu-id="d2422-106">매개 변수</span><span class="sxs-lookup"><span data-stu-id="d2422-106">Parameters</span></span>

<span data-ttu-id="d2422-107">*configurationNumber* \[in\] 요청된 구성을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d2422-107">*configurationNumber* \[in\] Specifies the requested configuration.</span></span>

## <a name="return-value"></a><span data-ttu-id="d2422-108">반환 값</span><span class="sxs-lookup"><span data-stu-id="d2422-108">Return value</span></span>

<span data-ttu-id="d2422-109">성공하면 0을 반환하고 그렇지 않으면 오류 코드를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d2422-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="d2422-110">설명</span><span class="sxs-lookup"><span data-stu-id="d2422-110">Remarks</span></span>

<span data-ttu-id="d2422-111">정적 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="d2422-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="d2422-112">요구 사항</span><span class="sxs-lookup"><span data-stu-id="d2422-112">Requirements</span></span>

<span data-ttu-id="d2422-113">MOF\*\* DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="d2422-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="d2422-114">{0} 네임스페이스 Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="d2422-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="d2422-115">참고 항목</span><span class="sxs-lookup"><span data-stu-id="d2422-115">See also</span></span>

[<span data-ttu-id="d2422-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="d2422-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)