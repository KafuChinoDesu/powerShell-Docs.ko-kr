---
title: 이 listcontrol (형식)의 경우 EntrySelectedBy의 SelectionCondition에 대 한 ScriptBlock 요소 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4a1adad7-e864-4892-9d26-a6476a9698d2
caps.latest.revision: 7
ms.openlocfilehash: b65d953169f6daf15fb617ce4d0303cf4cb584ee
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72368592"
---
# <a name="scriptblock-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format"></a>ListControl에 대한 EntrySelectedBy의 SelectionCondition에 대한 ScriptBlock 요소(형식)

조건을 트리거하는 스크립트를 지정 합니다. 이 스크립트가 `true`평가 되 면 조건이 충족 되 고 목록 항목이 사용 됩니다.

Configuration 요소 (Format) ViewDefinitions 요소 (format)이 listcontrol Element (format) ListEntries Element (format) ListEntry Element (format) EntrySelectedBy 요소에 대 한 ListEntry (Format) SelectionCondition 요소 ListEntry (형식)에 대 한 EntrySelectedBy에 대 한 ListEntry (Format) ScriptBlock 요소의 EntrySelectedBy

## <a name="syntax"></a>구문

```xml
<ScriptBlock>ScriptToEvaluate</ScriptBlock>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 `ScriptBlock` 요소의 부모 요소에 대해 설명 합니다.

### <a name="attributes"></a>특성

없음

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|[ListEntry (형식)에 대 한 EntrySelectedBy의 SelectionCondition 요소](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)|이 목록 항목을 사용 하기 위해 있어야 하는 조건을 정의 합니다.|

## <a name="text-value"></a>텍스트 값

평가 되는 스크립트를 지정 합니다.

## <a name="remarks"></a>설명

선택 조건은 평가할 스크립트나 속성 이름을 하나 이상 지정 해야 하지만 둘 다 지정할 수는 없습니다. 선택 조건을 사용할 수 있는 방법에 대 한 자세한 내용은 [뷰 항목이 나 항목을 사용 하는 경우에 대 한 조건 정의](./defining-conditions-for-displaying-data.md)를 참조 하세요.

목록 뷰의 다른 구성 요소에 대 한 자세한 내용은 [목록 뷰](./creating-a-list-view.md)를 참조 하세요.

## <a name="see-also"></a>참고 항목

[ListEntry 요소 (Format)](./listentry-element-for-listcontrol-format.md)

[ListEntry (형식)의 경우 EntrySelectedBy에 대 한 SelectionCondition의 PropertyName 요소](./propertyname-element-for-selectioncondition-for-entryselectedby-for-listcontrol-format.md)

[ListEntry (형식)에 대 한 EntrySelectedBy의 SelectionCondition 요소](./selectioncondition-element-for-entryselectedby-for-listcontrol-format.md)

[목록 보기](./creating-a-list-view.md)

[뷰 항목이 나 항목을 사용 하는 경우 조건 정의](./defining-conditions-for-displaying-data.md)

[Windows PowerShell 서식 지정 및 형식 파일 작성](./writing-a-powershell-formatting-file.md)
