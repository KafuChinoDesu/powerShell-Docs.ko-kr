---
title: 뷰 (형식)에 대 한 GroupBy 요소 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 67a2b061-2a4a-4ad1-84f9-cdbefb64aaab
caps.latest.revision: 8
ms.openlocfilehash: abb8b91626128b3deaa2db24a9fd8b34a6563410
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72363632"
---
# <a name="groupby-element-for-view-format"></a>View에 대한 GroupBy 요소(형식)

새 개체 그룹을 표시 하는 방법을 정의 합니다. 이 요소는 테이블, 목록, 전체 또는 사용자 지정 컨트롤 뷰를 정의할 때 사용 됩니다.

Configuration 요소 (Format) ViewDefinitions 요소 (Format) View 요소 (format) GroupBy 요소 (형식)

## <a name="syntax"></a>구문

```xml
<GroupBy>
  <PropertyName>.NetTypeProperty</PropertyName>
  <ScriptBlock>ScriptToEvaluate</ScriptBlock>
  <Label>TextToDisplay</Label>
  <CustomControl>...</CustomControl>
  <CustomControlName>NameOfControl</CustomControlName>
</GroupBy>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 부모 요소에 대해 설명합니다.

### <a name="attributes"></a>특성

없음

### <a name="child-elements"></a>자식 요소

|요소|설명|
|-------------|-----------------|
|[GroupBy (형식)에 대 한 CustomControl 요소](./customcontrol-element-for-groupby-format.md)|선택적 요소입니다.<br /><br /> 새 그룹을 표시 하는 사용자 지정 컨트롤을 정의 합니다.|
|[GroupBy (형식)에 대 한 CustomControlName 요소](./customcontrolname-element-for-groupby-format.md)|선택적 요소입니다.<br /><br /> 새 그룹을 표시 하는 데 사용 되는 컨트롤의 이름을 지정 합니다.|
|[GroupBy (Format)의 Label 요소](./label-element-for-groupby-format.md)|선택적 요소입니다.<br /><br /> 새 그룹이 발견 될 때 표시 되는 레이블을 지정 합니다.|
|[GroupBy (형식)에 대 한 PropertyName 요소](./propertyname-element-for-groupby-format.md)|선택적 요소입니다.<br /><br /> 에서 값이 변경 될 때마다 새 그룹을 시작 하는 .NET 속성을 지정 합니다.|
|[GroupBy (형식)에 대 한 ScriptBlock 요소](./scriptblock-element-for-groupby-format.md)|선택적 요소입니다.<br /><br /> 값이 변경 될 때마다 새 그룹을 시작 하는 스크립트를 지정 합니다.|

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|[View 요소 (Format)](./view-element-format.md)|하나 이상의 .NET 개체를 표시 하는 뷰를 정의 합니다.|

## <a name="remarks"></a>설명

새 개체 그룹을 표시 하는 방법을 정의할 때 새 그룹을 시작 하는 속성 또는 스크립트를 지정 해야 합니다. 그러나 둘 다 지정할 수는 없습니다.

## <a name="see-also"></a>참고 항목

[GroupBy (형식)에 대 한 CustomControlName 요소](./customcontrolname-element-for-groupby-format.md)

[GroupBy (Format)의 Label 요소](./label-element-for-groupby-format.md)

[GroupBy (형식)에 대 한 PropertyName 요소](./propertyname-element-for-groupby-format.md)

[GroupBy (형식)에 대 한 ScriptBlock 요소](./scriptblock-element-for-groupby-format.md)

[View 요소 (Format)](./view-element-format.md)

[PowerShell 서식 파일 작성](./writing-a-powershell-formatting-file.md)
