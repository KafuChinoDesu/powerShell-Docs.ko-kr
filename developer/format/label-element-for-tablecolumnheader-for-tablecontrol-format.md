---
title: TableControl (형식)에 대 한 TableColumnHeader 요소 레이블에 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 7196f039-2f6a-41fd-b252-5b1623ebb9f9
caps.latest.revision: 11
ms.openlocfilehash: 59dfd40b95d5088a711eb89cf101eb31a4b159f5
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56856089"
---
# <a name="label-element-for-tablecolumnheader-for-tablecontrol-format"></a><span data-ttu-id="e0ef0-102">TableControl의 TableColumnHeader에 대한 Label 요소(형식)</span><span class="sxs-lookup"><span data-stu-id="e0ef0-102">Label Element for TableColumnHeader for TableControl (Format)</span></span>

<span data-ttu-id="e0ef0-103">열의 맨 위에 있는 표시 되는 레이블을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-103">Defines the label that is displayed at the top of a column.</span></span> <span data-ttu-id="e0ef0-104">이 요소는 테이블 뷰를 정의할 때 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-104">This element is used when defining a table view.</span></span>

<span data-ttu-id="e0ef0-105">구성 요소 (형식) ViewDefinitions 요소 (형식) 보기 (형식) TableControl 요소 (형식) TableHeaders 요소 TableHeaders TableControl (형식) 레이블 요소에 대 한 TableControl (형식) TableColumnHeader 요소에 TableColumnHeader TablControl (형식)에 대 한</span><span class="sxs-lookup"><span data-stu-id="e0ef0-105">Configuration Element (Format) ViewDefinitions Element (Format) View Element (Format) TableControl Element (Format) TableHeaders Element for TableControl (Format) TableColumnHeader Element for TableHeaders for TableControl (Format) Label Element  for TableColumnHeader for TablControl (Format)</span></span>

## <a name="syntax"></a><span data-ttu-id="e0ef0-106">구문</span><span class="sxs-lookup"><span data-stu-id="e0ef0-106">Syntax</span></span>

```xml
<Label>DisplayedLabel</Label>

```

## <a name="attributes-and-elements"></a><span data-ttu-id="e0ef0-107">특성 및 요소</span><span class="sxs-lookup"><span data-stu-id="e0ef0-107">Attributes and Elements</span></span>

<span data-ttu-id="e0ef0-108">다음 섹션에서는 특성, 자식 요소 및 부모 요소에는 `Label` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-108">The following sections describe the attributes, child elements, and the parent element of the `Label` element.</span></span> <span data-ttu-id="e0ef0-109">각 열에 대해 하나의 레이블만 허용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-109">Only one label is allowed for each column.</span></span>

### <a name="attributes"></a><span data-ttu-id="e0ef0-110">특성</span><span class="sxs-lookup"><span data-stu-id="e0ef0-110">Attributes</span></span>

<span data-ttu-id="e0ef0-111">없음</span><span class="sxs-lookup"><span data-stu-id="e0ef0-111">None.</span></span>

### <a name="child-elements"></a><span data-ttu-id="e0ef0-112">자식 요소</span><span class="sxs-lookup"><span data-stu-id="e0ef0-112">Child Elements</span></span>

<span data-ttu-id="e0ef0-113">없음</span><span class="sxs-lookup"><span data-stu-id="e0ef0-113">None.</span></span>

### <a name="parent-elements"></a><span data-ttu-id="e0ef0-114">부모 요소</span><span class="sxs-lookup"><span data-stu-id="e0ef0-114">Parent Elements</span></span>

|<span data-ttu-id="e0ef0-115">요소</span><span class="sxs-lookup"><span data-stu-id="e0ef0-115">Element</span></span>|<span data-ttu-id="e0ef0-116">설명</span><span class="sxs-lookup"><span data-stu-id="e0ef0-116">Description</span></span>|
|-------------|-----------------|
|[<span data-ttu-id="e0ef0-117">TableControl (형식)에 대 한 TableHeaders TableColumnHeader 요소</span><span class="sxs-lookup"><span data-stu-id="e0ef0-117">TableColumnHeader Element for TableHeaders for TableControl  (Format)</span></span>](./tablecolumnheader-element-format.md)|<span data-ttu-id="e0ef0-118">레이블, 너비 및 테이블의 열에 대 한 데이터의 맞춤을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-118">Defines a label, the width, and the alignment of the data for a column of the table.</span></span>|

## <a name="text-value"></a><span data-ttu-id="e0ef0-119">텍스트 값</span><span class="sxs-lookup"><span data-stu-id="e0ef0-119">Text Value</span></span>

<span data-ttu-id="e0ef0-120">테이블의 열 위쪽에 표시 되는 텍스트를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-120">Specify the text that is displayed at the top of the column of the table.</span></span> <span data-ttu-id="e0ef0-121">열 레이블에 대 한 제한 없는 문자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-121">There are no restricted characters for the column label.</span></span>

## <a name="remarks"></a><span data-ttu-id="e0ef0-122">설명</span><span class="sxs-lookup"><span data-stu-id="e0ef0-122">Remarks</span></span>

<span data-ttu-id="e0ef0-123">레이블이 없으면 지정 된 경우 값은 행에 표시 되는 속성의 이름을 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-123">If no label is specified, the name of the property whose value is displayed in the rows is used.</span></span>

<span data-ttu-id="e0ef0-124">테이블 보기의 구성 요소에 대 한 자세한 내용은 참조 [테이블 뷰를 만드는](./creating-a-table-view.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="e0ef0-124">For more information about the components of a table view, see [Creating a Table View](./creating-a-table-view.md).</span></span>

## <a name="example"></a><span data-ttu-id="e0ef0-125">예제</span><span class="sxs-lookup"><span data-stu-id="e0ef0-125">Example</span></span>

<span data-ttu-id="e0ef0-126">이 예제는 `TableColumnHeader` 요소 레이블을 열인지 "1".</span><span class="sxs-lookup"><span data-stu-id="e0ef0-126">This example shows a `TableColumnHeader` element whose label is "Column 1".</span></span>

```xml
<TableColumnHeader>
  <Label>Column 1</Label)
  <Width>16</Width>
  <Alignment>Left</Alignment>
</TableColumnHeader>
```

## <a name="see-also"></a><span data-ttu-id="e0ef0-127">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e0ef0-127">See Also</span></span>

[<span data-ttu-id="e0ef0-128">테이블 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="e0ef0-128">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="e0ef0-129">TableColumnHeader 요소 (형식)</span><span class="sxs-lookup"><span data-stu-id="e0ef0-129">TableColumnHeader Element (Format)</span></span>](./tablecolumnheader-element-format.md)

[<span data-ttu-id="e0ef0-130">서식 파일을 PowerShell 작성</span><span class="sxs-lookup"><span data-stu-id="e0ef0-130">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)