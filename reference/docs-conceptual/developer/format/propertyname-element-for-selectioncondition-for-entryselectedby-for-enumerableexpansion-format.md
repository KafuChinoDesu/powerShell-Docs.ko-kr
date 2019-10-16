---
title: EnumerableExpansion (형식)의 경우 EntrySelectedBy의 SelectionCondition에 대 한 PropertyName 요소 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9ae11924-0072-451e-bf70-c5ffb25dccc0
caps.latest.revision: 13
ms.openlocfilehash: 0c20512e660c8d2b61d063dbd7078b55b23efeb8
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72362322"
---
# <a name="propertyname-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format"></a><span data-ttu-id="fad1d-102">EnumerableExpansion에 대한 EntrySelectedBy의 SelectionCondition에 대한 PropertyName 요소(형식)</span><span class="sxs-lookup"><span data-stu-id="fad1d-102">PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

<span data-ttu-id="fad1d-103">조건을 트리거하는 .NET 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad1d-103">Specifies the .NET property that triggers the condition.</span></span> <span data-ttu-id="fad1d-104">이 속성이 있거나 `true`으로 평가 되 면 조건이 충족 되 고 정의가 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fad1d-104">When this property is present or when it evaluates to `true`, the condition is met, and the definition is used.</span></span>

<span data-ttu-id="fad1d-105">Configuration 요소 (Format) DefaultSettings 요소 (format) EnumerableExpansions element (format) enumerableexpansions 요소 (format)에 대 한 EntrySelectedBy 요소에 대 한 EnumerableExpansion (Format) PropertyName 요소는 EnumerableExpansion (형식)에 대해 EntrySelectedBy</span><span class="sxs-lookup"><span data-stu-id="fad1d-105">Configuration Element (Format) DefaultSettings Element (Format) EnumerableExpansions Element (Format) EnumerableExpansion Element (Format) EntrySelectedBy Element for EnumerableExpansion (Format) SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format) PropertyName Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="fad1d-106">구문</span><span class="sxs-lookup"><span data-stu-id="fad1d-106">Syntax</span></span>

```xml
<PropertyName>.NetTypeProperty</PropertyName>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="fad1d-107">특성 및 요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-107">Attributes and Elements</span></span>

<span data-ttu-id="fad1d-108">다음 섹션에서는 `PropertyName` 요소의 특성, 자식 요소 및 부모 요소에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad1d-108">The following sections describe attributes, child elements, and the parent element of the `PropertyName` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="fad1d-109">특성</span><span class="sxs-lookup"><span data-stu-id="fad1d-109">Attributes</span></span>

<span data-ttu-id="fad1d-110">없음</span><span class="sxs-lookup"><span data-stu-id="fad1d-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="fad1d-111">자식 요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-111">Child Elements</span></span>

<span data-ttu-id="fad1d-112">없음</span><span class="sxs-lookup"><span data-stu-id="fad1d-112">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="fad1d-113">부모 요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-113">Parent Elements</span></span>

|<span data-ttu-id="fad1d-114">요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-114">Element</span></span>|<span data-ttu-id="fad1d-115">설명</span><span class="sxs-lookup"><span data-stu-id="fad1d-115">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="fad1d-116">EnumerableExpansion (형식)에 대 한 EntrySelectedBy의 SelectionCondition 요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-116">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)|<span data-ttu-id="fad1d-117">이 정의의 컬렉션 개체를 확장 하기 위해 있어야 하는 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad1d-117">Defines the condition that must exist to expand the collection objects of this definition.</span></span>|

## <a name="text-value"></a><span data-ttu-id="fad1d-118">텍스트 값</span><span class="sxs-lookup"><span data-stu-id="fad1d-118">Text Value</span></span>

<span data-ttu-id="fad1d-119">.NET 속성 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="fad1d-119">Specify the .NET property name.</span></span>

## <a name="remarks"></a><span data-ttu-id="fad1d-120">설명</span><span class="sxs-lookup"><span data-stu-id="fad1d-120">Remarks</span></span>

<span data-ttu-id="fad1d-121">선택 조건은 평가할 하나 이상의 속성 이름 또는 스크립트를 지정 해야 하지만 둘 다 지정할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fad1d-121">The selection condition must specify at least one property name or a script to evaluate, but cannot specify both.</span></span> <span data-ttu-id="fad1d-122">선택 조건을 사용 하는 방법에 대 한 자세한 내용은 [데이터 표시 시기에 대 한 조건 정의](./defining-conditions-for-displaying-data.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="fad1d-122">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="fad1d-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="fad1d-123">See Also</span></span>

[<span data-ttu-id="fad1d-124">데이터가 표시 되는 시점에 대 한 조건 정의</span><span class="sxs-lookup"><span data-stu-id="fad1d-124">Defining Conditions for When Data is Displayed</span></span>](./defining-conditions-for-displaying-data.md)

[<span data-ttu-id="fad1d-125">EnumerableExpansion (형식)에 대 한 EntrySelectedBy의 SelectionCondition 요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-125">ScriptBlock Element for SelectionCondition for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="fad1d-126">EnumerableExpansion (형식)에 대 한 EntrySelectedBy의 SelectionCondition 요소</span><span class="sxs-lookup"><span data-stu-id="fad1d-126">SelectionCondition Element for EntrySelectedBy for EnumerableExpansion (Format)</span></span>](./selectioncondition-element-for-entryselectedby-for-enumerableexpansion-format.md)

[<span data-ttu-id="fad1d-127">PowerShell 서식 파일 작성</span><span class="sxs-lookup"><span data-stu-id="fad1d-127">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)