---
title: 파일 서식 지정 개요 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: fe888fee-1fe9-459f-9d62-35732c19a7f8
caps.latest.revision: 13
ms.openlocfilehash: d418cff70c1197aa3c331eed909f49198da139e9
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72363692"
---
# <a name="formatting-file-overview"></a><span data-ttu-id="96537-102">형식 지정 파일 개요</span><span class="sxs-lookup"><span data-stu-id="96537-102">Formatting File Overview</span></span>

<span data-ttu-id="96537-103">명령 (cmdlet, 함수 및 스크립트)에서 반환 되는 개체에 대 한 표시 형식은 형식 지정 파일 (types.ps1xml 파일)을 사용 하 여 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-103">The display format for the objects that are returned by commands (cmdlets, functions, and scripts) are defined by using formatting files (format.ps1xml files).</span></span> <span data-ttu-id="96537-104">이러한 파일 중 일부는 powershell에서 제공 하는 명령 (예: `Get-Process` cmdlet에서 반환 된 [진단](/dotnet/api/System.Diagnostics.Process) 제공 명령에 의해 반환 되는 개체의 표시 형식을 정의 하기 위해 powershell에서 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-104">Several of these files are provided by PowerShell to define the display format for those objects returned by PowerShell-provided commands, such as the [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) object returned by the `Get-Process` cmdlet.</span></span> <span data-ttu-id="96537-105">그러나 사용자 고유의 사용자 지정 서식 파일을 만들어 기본 표시 형식을 덮어쓰거나 사용자 지정 서식 파일을 작성 하 여 사용자의 명령에서 반환 하는 개체의 표시를 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-105">However, you can also create your own custom formatting files to overwrite the default display formats or you can write a custom formatting file to define the display of objects returned by your own commands.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="96537-106">파일 서식 지정은 파이프라인에 반환 되는 개체의 요소를 결정 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-106">Formatting files do not determine the elements of an object that are returned to the pipeline.</span></span> <span data-ttu-id="96537-107">개체를 파이프라인으로 반환 하면 일부 표시 되지 않은 경우에도 해당 개체의 모든 멤버를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-107">When an object is returned to the pipeline, all members of that object are available even if some are not displayed.</span></span>

<span data-ttu-id="96537-108">PowerShell에서는 이러한 서식 파일의 데이터를 사용 하 여 표시 되는 내용과 표시 되는 데이터의 형식을 지정 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-108">PowerShell uses the data in these formatting files to determine what is displayed and how the displayed data is formatted.</span></span> <span data-ttu-id="96537-109">표시 되는 데이터에는 개체의 속성 또는 스크립트의 값이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-109">The displayed data can include the properties of an object or the value of a script.</span></span> <span data-ttu-id="96537-110">개체의 속성 값을 추가한 다음 합계를 데이터 조각으로 표시 하는 등 개체의 속성에서 직접 사용할 수 없는 일부 값을 표시 하려는 경우 스크립트를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-110">Scripts are used if you want to display some value that is not available directly from the properties of an object, such as adding the value of two properties of an object and then displaying the sum as a piece of data.</span></span> <span data-ttu-id="96537-111">표시 되는 데이터의 서식은 표시 하려는 개체에 대 한 뷰를 정의 하 여 수행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-111">Formatting of the displayed data is done by defining views for the objects that you want to display.</span></span> <span data-ttu-id="96537-112">각 개체에 대해 단일 뷰를 정의 하거나, 여러 개체에 대해 단일 뷰를 정의 하거나, 동일한 개체에 대해 여러 뷰를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-112">You can define a single view for each object, you can define a single view for multiple objects, or you can define multiple views for the same object.</span></span> <span data-ttu-id="96537-113">정의할 수 있는 뷰 수에는 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-113">There is no limit to the number of views that you can define.</span></span>

## <a name="common-features-of-formatting-files"></a><span data-ttu-id="96537-114">서식 파일의 일반적인 기능</span><span class="sxs-lookup"><span data-stu-id="96537-114">Common Features of Formatting Files</span></span>

<span data-ttu-id="96537-115">각 서식 파일은 파일에 정의 된 모든 보기에서 공유할 수 있는 다음 구성 요소를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-115">Each formatting file can define the following components that can be shared across all the views defined by the file:</span></span>

- <span data-ttu-id="96537-116">데이터가 열의 너비 보다 길면 다음 줄에 테이블 행에 표시 되는 데이터를 표시할지 여부와 같은 기본 구성 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="96537-116">Default configuration setting, such as whether the data displayed in the rows of tables will be displayed on the next line if the data is longer than the width of the column.</span></span> <span data-ttu-id="96537-117">이러한 설정에 대 한 자세한 내용은 [공통 구성 설정 정의](./defining-common-configuration-features.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-117">For more information about these settings, see [Defining Common Configuration Settings](./defining-common-configuration-features.md).</span></span>

- <span data-ttu-id="96537-118">서식 파일의 모든 보기에서 표시할 수 있는 개체 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="96537-118">Sets of objects that can be displayed by any of the views of the formatting file.</span></span> <span data-ttu-id="96537-119">이러한 집합 ( *선택 집합*이라고 함)에 대 한 자세한 내용은 [개체 집합 정의](./defining-selection-sets.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-119">For more information about these sets (referred to as *selection sets*), see [Defining Sets of Objects](./defining-selection-sets.md).</span></span>

- <span data-ttu-id="96537-120">서식 파일의 모든 뷰에서 사용할 수 있는 공용 컨트롤입니다.</span><span class="sxs-lookup"><span data-stu-id="96537-120">Common controls that can be used by all the views of the formatting file.</span></span> <span data-ttu-id="96537-121">컨트롤을 통해 데이터가 표시 되는 방법을 보다 세밀 하 게 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-121">Controls give you finer control on how data is displayed.</span></span> <span data-ttu-id="96537-122">컨트롤에 대 한 자세한 내용은 [사용자 지정 컨트롤 정의](./creating-custom-controls.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-122">For more information about controls, see [Defining Custom Controls](./creating-custom-controls.md).</span></span>

## <a name="formatting-views"></a><span data-ttu-id="96537-123">보기 서식 지정</span><span class="sxs-lookup"><span data-stu-id="96537-123">Formatting Views</span></span>

<span data-ttu-id="96537-124">서식 보기에서는 개체를 테이블 형식, 목록 형식, 넓은 형식 및 사용자 지정 형식으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-124">Formatting views can display objects in a table format, list format, wide format, and custom format.</span></span> <span data-ttu-id="96537-125">대부분의 경우 각 서식 지정 정의는 뷰를 설명 하는 XML 태그 집합으로 설명 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-125">For the most part, each formatting definition is described by a set of XML tags that describe the view.</span></span> <span data-ttu-id="96537-126">각 뷰에는 뷰 이름, 뷰를 사용 하는 개체 및 뷰의 요소 (예: 테이블 뷰의 열 및 행 정보)가 포함 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-126">Each view contains the name of the view, the objects that use the view, and the elements of the view, such as the column and row information for a table view.</span></span>

<span data-ttu-id="96537-127">테이블 뷰 하나 이상의 열에 있는 개체 또는 스크립트 블록 값의 속성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-127">Table View Lists the properties of an object or a script block value in one or more columns.</span></span> <span data-ttu-id="96537-128">각 열은 개체의 단일 속성 또는 스크립트 값을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="96537-128">Each column represents a single property of the object or a script value.</span></span> <span data-ttu-id="96537-129">개체의 모든 속성, 개체 속성의 하위 집합 또는 속성 및 스크립트 값의 조합을 표시 하는 테이블 뷰를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-129">You can define a table view that displays all the properties of an object, a subset of the properties of an object, or a combination of properties and script values.</span></span> <span data-ttu-id="96537-130">테이블의 각 행은 반환 된 개체를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="96537-130">Each row of the table represents a returned object.</span></span> <span data-ttu-id="96537-131">개체를 `Format-Table` cmdlet으로 파이프 하는 경우와 매우 유사 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-131">Creating a table view is very similar to when you pipe an object to the `Format-Table` cmdlet.</span></span> <span data-ttu-id="96537-132">이 보기에 대 한 자세한 내용은 [테이블 뷰](./creating-a-table-view.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-132">For more information about this view, see [Table View](./creating-a-table-view.md).</span></span>

<span data-ttu-id="96537-133">목록 뷰 단일 열에 있는 개체 또는 스크립트 값의 속성을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-133">List View Lists the properties of an object or a script value in a single column.</span></span> <span data-ttu-id="96537-134">목록의 각 행에는 선택적 레이블 또는 속성 이름과 속성 또는 스크립트의 값이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-134">Each row of the list displays an optional label or the property name followed by the value of the property or script.</span></span> <span data-ttu-id="96537-135">목록 뷰를 만드는 것은 개체를 `Format-List` cmdlet으로 파이프 하는 것과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-135">Creating a list view is very similar to piping an object to the `Format-List` cmdlet.</span></span> <span data-ttu-id="96537-136">이 보기에 대 한 자세한 내용은 [목록 뷰](./creating-a-list-view.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-136">For more information about this view, see [List View](./creating-a-list-view.md).</span></span>

<span data-ttu-id="96537-137">넓은 뷰 하나 이상의 열에 있는 단일 개체 속성 또는 스크립트 값을 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-137">Wide View Lists a single property of an object or a script value in one or more columns.</span></span> <span data-ttu-id="96537-138">이 보기에 대 한 레이블이나 머리글이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-138">There is no label or header for this view.</span></span> <span data-ttu-id="96537-139">넓은 뷰를 만드는 것은 개체를 `Format-Wide` cmdlet으로 파이프 하는 것과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-139">Creating a wide view is very similar to piping an object to the `Format-Wide` cmdlet.</span></span> <span data-ttu-id="96537-140">이 보기에 대 한 자세한 내용은 [Wide view](./creating-a-wide-view.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-140">For more information about this view, see [Wide View](./creating-a-wide-view.md).</span></span>

<span data-ttu-id="96537-141">사용자 지정 보기에는 테이블 뷰, 목록 뷰 또는 넓은 보기의 고정 구조를 준수 하지 않는 개체 속성 또는 스크립트 값을 사용자 지정할 수 있는 뷰가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="96537-141">Custom View Displays a customizable view of object properties or script values that does not adhere to the rigid structure of table views, list views, or wide views.</span></span> <span data-ttu-id="96537-142">독립 실행형 사용자 지정 뷰를 정의 하거나 다른 보기에서 사용 되는 사용자 지정 보기 (예: 테이블 뷰 또는 목록 보기)를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-142">You can define a stand-alone custom view, or you can define a custom view that is used by another view, such as a table view or list view.</span></span> <span data-ttu-id="96537-143">사용자 지정 뷰를 만드는 것은 개체를 `Format-Custom` cmdlet으로 파이프 하는 것과 매우 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-143">Creating a custom view is very similar to piping an object to the `Format-Custom` cmdlet.</span></span> <span data-ttu-id="96537-144">이 보기에 대 한 자세한 내용은 [사용자 지정 뷰](./creating-custom-controls.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="96537-144">For more information about this view, see [Custom View](./creating-custom-controls.md).</span></span>

## <a name="components-of-a-view"></a><span data-ttu-id="96537-145">뷰의 구성 요소</span><span class="sxs-lookup"><span data-stu-id="96537-145">Components of a View</span></span>

<span data-ttu-id="96537-146">다음 XML 예제에서는 뷰의 기본 XML 구성 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96537-146">The following XML examples show the basic XML components of a view.</span></span> <span data-ttu-id="96537-147">개별 XML 요소는 만들려는 뷰에 따라 다르지만 뷰의 기본 구성 요소는 모두 동일 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-147">The individual XML elements vary depending on which view you want to create, but the basic components of the views are all the same.</span></span>

<span data-ttu-id="96537-148">부터 각 뷰에는 뷰를 참조 하는 데 사용 되는 사용자에 게 친숙 한 이름을 지정 하는 `Name` 요소가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-148">To start with, each view has a `Name` element that specifies a user friendly name that is used to reference the view.</span></span> <span data-ttu-id="96537-149">뷰가 표시 하는 .NET 개체와 뷰를 정의 하는 *컨트롤* 요소를 정의 하는 `ViewSelectedBy` 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="96537-149">a `ViewSelectedBy` element that defines which .NET objects are displayed by the view, and a *control* element that defines the view.</span></span>

```xml
<ViewDefinitions>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <TableControl>...</TableControl>
  </View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <ListControl>...</ListControl>
  <View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <WideControl>...</WideControl>
  <View>
  <View>
    <Name>NameOfView</Name>
    <ViewSelectedBy>...</ViewSelectedBy>
    <CustomControl>...</CustomControl>
  </View>
</ViewDefinitions>

```

<span data-ttu-id="96537-150">컨트롤 요소 내에서 하나 이상의 *항목* 요소를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-150">Within the control element, you can define one or more *entry* elements.</span></span> <span data-ttu-id="96537-151">여러 정의를 사용 하는 경우 각 정의를 사용 하는 .NET 개체를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-151">If you use multiple definitions, you must specify which .NET objects use each definition.</span></span> <span data-ttu-id="96537-152">일반적으로 각 컨트롤에는 하나의 정의만 있는 항목이 하나만 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-152">Typically only one entry, with only one definition, is needed for each control.</span></span>

```xml
<ListControl>
  <ListEntries>
    <ListEntry>
      <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
    <ListEntry>
        <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
    <ListEntry>
        <EntrySelectedBy>...</EntrySelectedBy>
      <ListItems>...</ListItems>
    <ListEntry>
  </ListEntries>
</ListControl>

```

<span data-ttu-id="96537-153">뷰의 각 entry 요소 내에서 해당 보기에 표시 되는 .NET 속성 또는 스크립트를 정의 하는 *항목* 요소를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-153">Within each entry element of a view, you specify the *item* elements that define the .NET properties or scripts that are displayed by that view.</span></span>

```xml

<ListItems>
  <ListItem>...</ListItem>
  <ListItem>...</ListItem>
  <ListItem>...</ListItem>
</ListItems>

```

<span data-ttu-id="96537-154">앞의 예제에서 볼 수 있듯이 서식 파일에는 여러 뷰가 포함 될 수 있으며, 뷰에는 여러 개의 정의가 포함 될 수 있으며 각 정의에는 여러 항목이 포함 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="96537-154">As shown in the preceding examples, the formatting file can contain multiple views, a view can contain multiple definitions, and each definition can contain multiple items.</span></span>

## <a name="example-of-a-table-view"></a><span data-ttu-id="96537-155">테이블 뷰의 예</span><span class="sxs-lookup"><span data-stu-id="96537-155">Example of a Table View</span></span>

<span data-ttu-id="96537-156">다음 예에서는 두 개의 열이 포함 된 테이블 뷰를 정의 하는 데 사용 되는 XML 태그를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="96537-156">The following example shows the XML tags used to define a table view that contains two columns.</span></span> <span data-ttu-id="96537-157">[Viewdefinitions](./viewdefinitions-element-format.md) 요소는 서식 파일에 정의 된 모든 뷰에 대 한 컨테이너 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="96537-157">The [ViewDefinitions](./viewdefinitions-element-format.md) element is the container element for all the views defined in the formatting file.</span></span> <span data-ttu-id="96537-158">[View](./view-element-format.md) 요소는 특정 테이블, 목록, 전체 또는 사용자 지정 뷰를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-158">The [View](./view-element-format.md) element defines the specific table, list, wide, or custom view.</span></span> <span data-ttu-id="96537-159">각 [뷰](./view-element-format.md) 요소 내에서 [name](./name-element-for-view-format.md) 요소는 뷰의 이름을 지정 하 고 [viewselectedby](./viewselectedby-element-format.md) 요소는 뷰를 사용 하는 개체와 다음에 표시 되는 `TableControl` 요소와 같은 다양 한 컨트롤 요소를 정의 합니다. 예) 보기의 유형을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="96537-159">Within each [View](./view-element-format.md) element, the [Name](./name-element-for-view-format.md) element specifies the name of the view, the [ViewSelectedBy](./viewselectedby-element-format.md) element defines the objects that use the view, and the different control elements (such as the `TableControl` element shown in the following example) define the type of the view.</span></span>

```xml
<ViewDefinitions>
  <View>
    <Name>Name of View</Name>
    <ViewSelectedBy>
      <TypeName>Object to display using this view</TypeName>
      <TypeName>Object to display using this view</TypeName>
    </ViewSelectedBy>
    <TableControl>
      <TableHeaders>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
        <TableColumnHeader>
          <Width></Width>
        </TableColumnHeader>
      </TableHeaders>
      <TableRowEntries>
        <TableRowEntry>
          <TableColumnItems>
            <TableColumnItem>
              <PropertyName>Header for column 1</PropertyName>
            </TableColumnItem>
            <TableColumnItem>
              <PropertyName>Header for column 2</PropertyName>
            </TableColumnItem>
          </TableColumnItems>
        </TableRowEntry>
      </TableRowEntries>
    </TableControl)
  </View>
</ViewDefinitions>

```

## <a name="see-also"></a><span data-ttu-id="96537-160">참고 항목</span><span class="sxs-lookup"><span data-stu-id="96537-160">See Also</span></span>

[<span data-ttu-id="96537-161">목록 보기 만들기</span><span class="sxs-lookup"><span data-stu-id="96537-161">Creating a List View</span></span>](./creating-a-list-view.md)

[<span data-ttu-id="96537-162">테이블 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="96537-162">Creating a Table View</span></span>](./creating-a-table-view.md)

[<span data-ttu-id="96537-163">넓은 뷰 만들기</span><span class="sxs-lookup"><span data-stu-id="96537-163">Creating a Wide View</span></span>](./creating-a-wide-view.md)

[<span data-ttu-id="96537-164">사용자 지정 컨트롤 만들기</span><span class="sxs-lookup"><span data-stu-id="96537-164">Creating Custom Controls</span></span>](./creating-custom-controls.md)

[<span data-ttu-id="96537-165">PowerShell 서식 지정 및 형식 파일 작성</span><span class="sxs-lookup"><span data-stu-id="96537-165">Writing a PowerShell Formatting and Types File</span></span>](./writing-a-powershell-formatting-file.md)