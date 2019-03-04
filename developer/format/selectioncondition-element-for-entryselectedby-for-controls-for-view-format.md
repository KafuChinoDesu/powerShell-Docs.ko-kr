---
title: 뷰 (형식)에 대 한 컨트롤에 대 한 EntrySelectedBy SelectionCondition 요소 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 2623407e-fa10-4d27-a804-204f6d50ef22
caps.latest.revision: 6
ms.openlocfilehash: ea15e647a9dd7a7064718a0c536c4a3178d62d95
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56858019"
---
# <a name="selectioncondition-element-for-entryselectedby-for-controls-for-view-format"></a><span data-ttu-id="cb3ee-102">View에 대한 Controls의 EntrySelectedBy에 대한 SelectionCondition 요소(형식)</span><span class="sxs-lookup"><span data-stu-id="cb3ee-102">SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>

<span data-ttu-id="cb3ee-103">사용할 컨트롤 정의에 있어야 하는 조건을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-103">Defines a condition that must exist for the control definition to be used.</span></span> <span data-ttu-id="cb3ee-104">이 요소는 뷰에서 사용할 수 있는 컨트롤을 정의할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-104">This element is used when defining controls that can be used by a view.</span></span>

<span data-ttu-id="cb3ee-105">구성 요소 (형식) ViewDefinitions 요소 (형식) 보기 (형식) 컨트롤 요소 (형식) 컨트롤 요소에 대 한 보기 (형식) CustomEntries 요소에 대 한 컨트롤에 대 한 컨트롤에 대 한 보기 (형식) CustomControl 요소에 대 한 컨트롤에 대 한 CustomControl CustomEntries CustomEntry EntrySelectedBy 보기 (컨트롤에 대 한 보기 (형식) SelectionCondition 요소에 대 한 컨트롤에 대 한 보기 (형식) EntrySelectedBy 요소에 대 한 컨트롤에 대 한 보기 (형식) CustomEntry 요소에 대 한 컨트롤에 대 한 형식)</span><span class="sxs-lookup"><span data-stu-id="cb3ee-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) Controls Element (Format) Control Element for Controls for View (Format) CustomControl Element for Control for Controls for View (Format) CustomEntries Element for CustomControl for Controls for View (Format) CustomEntry Element for CustomEntries for Controls for View (Format) EntrySelectedBy Element for CustomEntry for Controls for View (Format) SelectionCondition Element for EntrySelectedBy for Controls for View (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="cb3ee-106">구문</span><span class="sxs-lookup"><span data-stu-id="cb3ee-106">Syntax</span></span>

```xml
<SelectionCondition>
  <TypeName>Nameof.NetType</TypeName>
  <SelectionSetName>NameofSelectionSet</SelectionSetName>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
</SelectionCondition>
```

## <a name="attributes-and-elements"></a><span data-ttu-id="cb3ee-107">특성 및 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-107">Attributes and Elements</span></span>

<span data-ttu-id="cb3ee-108">다음 섹션에서는 특성, 자식 요소 및 부모 요소에는 `SelectionCondition` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-108">The following sections describe attributes, child elements, and the parent element of the `SelectionCondition` element.</span></span>

### <a name="attributes"></a><span data-ttu-id="cb3ee-109">특성</span><span class="sxs-lookup"><span data-stu-id="cb3ee-109">Attributes</span></span>

<span data-ttu-id="cb3ee-110">없음</span><span class="sxs-lookup"><span data-stu-id="cb3ee-110">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="cb3ee-111">자식 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-111">Child Elements</span></span>

|<span data-ttu-id="cb3ee-112">요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-112">Element</span></span>|<span data-ttu-id="cb3ee-113">설명</span><span class="sxs-lookup"><span data-stu-id="cb3ee-113">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cb3ee-114">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition PropertyName 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-114">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="cb3ee-115">선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-115">Optional element.</span></span><br /><br /> <span data-ttu-id="cb3ee-116">조건이 트리거하는.NET 속성을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-116">Specifies a .NET property that triggers the condition.</span></span>|
|[<span data-ttu-id="cb3ee-117">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition ScriptBlock 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-117">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="cb3ee-118">선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-118">Optional element.</span></span><br /><br /> <span data-ttu-id="cb3ee-119">조건이 트리거하는 스크립트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-119">Specifies the script that triggers the condition.</span></span>|
|[<span data-ttu-id="cb3ee-120">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition SelectionSetName 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-120">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="cb3ee-121">선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-121">Optional element.</span></span><br /><br /> <span data-ttu-id="cb3ee-122">조건이 트리거하는.NET 형식의 집합을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-122">Specifies the set of .NET types that triggers the condition.</span></span>|
|[<span data-ttu-id="cb3ee-123">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition TypeName 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-123">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-view-format.md)|<span data-ttu-id="cb3ee-124">선택적 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-124">Optional element.</span></span><br /><br /> <span data-ttu-id="cb3ee-125">조건이 트리거하는.NET 형식을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-125">Specifies a .NET type that triggers the condition.</span></span>|

### <a name="parent-elements"></a><span data-ttu-id="cb3ee-126">부모 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-126">Parent Elements</span></span>

|<span data-ttu-id="cb3ee-127">요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-127">Element</span></span>|<span data-ttu-id="cb3ee-128">설명</span><span class="sxs-lookup"><span data-stu-id="cb3ee-128">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="cb3ee-129">뷰 (형식)에 대 한 컨트롤에 대 한 CustomEntry EntrySelectedBy 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-129">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)|<span data-ttu-id="cb3ee-130">이 컨트롤 정의 또는이 정의를 사용할 수 있어야 하는 조건을 사용 하는.NET 형식을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-130">Defines the .NET types that use this control definition or the condition that must exist for this definition to be used.</span></span>|

## <a name="remarks"></a><span data-ttu-id="cb3ee-131">설명</span><span class="sxs-lookup"><span data-stu-id="cb3ee-131">Remarks</span></span>

<span data-ttu-id="cb3ee-132">선택 조건을 정의 하는 경우 다음 요구 사항을 적용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-132">When you are defining a selection condition, the following requirements apply:</span></span>

- <span data-ttu-id="cb3ee-133">선택 조건 최소 하나의 속성 이름 또는 스크립트 블록을 지정 해야 하지만 둘 다 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-133">The selection condition must specify a least one property name or a script block, but cannot specify both.</span></span>

- <span data-ttu-id="cb3ee-134">선택 조건.NET 형식의 숫자를 지정할 수 또는 선택 영역 집합을 모두 지정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-134">The selection condition can specify any number of .NET types or selection sets, but cannot specify both.</span></span>

<span data-ttu-id="cb3ee-135">선택 조건을 사용 하는 방법에 대 한 자세한 내용은 참조 하세요. [데이터를 표시 하는 경우에 대 한 조건을 정의](./defining-conditions-for-displaying-data.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="cb3ee-135">For more information about how to use selection conditions, see [Defining Conditions for when Data is Displayed](./defining-conditions-for-displaying-data.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="cb3ee-136">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cb3ee-136">See Also</span></span>

[<span data-ttu-id="cb3ee-137">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition PropertyName 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-137">PropertyName Element for SelectionCondition for Controls for View (Format)</span></span>](./propertyname-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="cb3ee-138">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition ScriptBlock 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-138">ScriptBlock Element for SelectionCondition for Controls for View (Format)</span></span>](./scriptblock-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="cb3ee-139">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition SelectionSetName 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-139">SelectionSetName Element for SelectionCondition for Controls for View (Format)</span></span>](./selectionsetname-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="cb3ee-140">뷰 (형식)에 대 한 컨트롤에 대 한 SelectionCondition TypeName 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-140">TypeName Element for SelectionCondition for Controls for View (Format)</span></span>](./typename-element-for-selectioncondition-for-controls-for-view-format.md)

[<span data-ttu-id="cb3ee-141">뷰 (형식)에 대 한 컨트롤에 대 한 CustomEntry EntrySelectedBy 요소</span><span class="sxs-lookup"><span data-stu-id="cb3ee-141">EntrySelectedBy Element for CustomEntry for Controls for View (Format)</span></span>](./entryselectedby-element-for-customentry-for-controls-for-view-format.md)

[<span data-ttu-id="cb3ee-142">서식 파일을 PowerShell 작성</span><span class="sxs-lookup"><span data-stu-id="cb3ee-142">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)