---
title: GroupBy (형식)에 대 한 ScriptBlock 요소 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 30183927-6f0e-4717-b6f5-f07a6e134cfb
caps.latest.revision: 6
ms.openlocfilehash: 41a6aaa24e5850bd390c8e3b6505cc88fc80b7b5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56856209"
---
# <a name="scriptblock-element-for-groupby-format"></a><span data-ttu-id="8ed95-102">GroupBy에 대한 ScriptBlock 요소(형식)</span><span class="sxs-lookup"><span data-stu-id="8ed95-102">ScriptBlock Element for GroupBy (Format)</span></span>

<span data-ttu-id="8ed95-103">해당 값이 변경 될 때마다 새 그룹을 시작 하는 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed95-103">Specifies the script that starts a new group whenever its value changes.</span></span>

<span data-ttu-id="8ed95-104">구성 요소 (형식) ViewDefinitions 요소 (형식) 보기 (형식) GroupBy 요소 GroupBy (형식)에 대 한 보기 (형식) ScriptBlock 요소에 대 한</span><span class="sxs-lookup"><span data-stu-id="8ed95-104">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) GroupBy Element for View (Format) ScriptBlock Element for GroupBy (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="8ed95-105">구문</span><span class="sxs-lookup"><span data-stu-id="8ed95-105">Syntax</span></span>

```xml
<ScriptBolck>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="8ed95-106">특성 및 요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-106">Attributes and Elements</span></span>

<span data-ttu-id="8ed95-107">다음 섹션에서는 특성, 자식 요소 및 부모 요소에는 `ScriptBlock` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="8ed95-107">The following sections describe attributes, child elements, and the parent element of the `ScriptBlock` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="8ed95-108">특성</span><span class="sxs-lookup"><span data-stu-id="8ed95-108">Attributes</span></span>

<span data-ttu-id="8ed95-109">없음</span><span class="sxs-lookup"><span data-stu-id="8ed95-109">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="8ed95-110">자식 요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-110">Child Elements</span></span>

<span data-ttu-id="8ed95-111">없음</span><span class="sxs-lookup"><span data-stu-id="8ed95-111">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="8ed95-112">부모 요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-112">Parent Elements</span></span>

|<span data-ttu-id="8ed95-113">요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-113">Element</span></span>|<span data-ttu-id="8ed95-114">설명</span><span class="sxs-lookup"><span data-stu-id="8ed95-114">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="8ed95-115">뷰 (형식)에 대 한 GroupBy 요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-115">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)|<span data-ttu-id="8ed95-116">.NET 개체 그룹에 표시 되는 방식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed95-116">Defines how a group of .NET objects is displayed.</span></span>|

## <a name="text-value"></a><span data-ttu-id="8ed95-117">텍스트 값</span><span class="sxs-lookup"><span data-stu-id="8ed95-117">Text Value</span></span>

<span data-ttu-id="8ed95-118">계산 되는 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed95-118">Specify the script that is evaluated.</span></span>

## <a name="remarks"></a><span data-ttu-id="8ed95-119">설명</span><span class="sxs-lookup"><span data-stu-id="8ed95-119">Remarks</span></span>

<span data-ttu-id="8ed95-120">Windows PowerShell이이 스크립트의 값이 변경 될 때마다 새 그룹을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed95-120">Windows PowerShell starts a new group whenever the value of this script changes.</span></span>

<span data-ttu-id="8ed95-121">이 요소를 지정 하는 경우 지정할 수 없습니다는 [PropertyName](http://msdn.microsoft.com/en-us/396dede0-039a-4a87-a5ef-3ecabb729676) 요소를 새 그룹을 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ed95-121">When this element is specified, you cannot specify the [PropertyName](http://msdn.microsoft.com/en-us/396dede0-039a-4a87-a5ef-3ecabb729676) element to start a new group.</span></span>

## <a name="see-also"></a><span data-ttu-id="8ed95-122">참고 항목</span><span class="sxs-lookup"><span data-stu-id="8ed95-122">See Also</span></span>

[<span data-ttu-id="8ed95-123">GroupBy (형식)에 대 한 PropertyName 요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-123">PropertyName Element for GroupBy (Format)</span></span>](./propertyname-element-for-groupby-format.md)

[<span data-ttu-id="8ed95-124">뷰 (형식)에 대 한 GroupBy 요소</span><span class="sxs-lookup"><span data-stu-id="8ed95-124">GroupBy Element for View (Format)</span></span>](./groupby-element-for-view-format.md)

[<span data-ttu-id="8ed95-125">서식 파일을 PowerShell 작성</span><span class="sxs-lookup"><span data-stu-id="8ed95-125">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)