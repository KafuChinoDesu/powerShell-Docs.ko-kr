---
title: 구성 (형식)의 컨트롤에 대 한 ExpressionBinding의 CustomControlName 요소 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c5242935-2782-4d23-84f5-2446b2b7ba83
caps.latest.revision: 8
ms.openlocfilehash: c9abd9f22907b87323c16d603a9f75bb3d375a03
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364122"
---
# <a name="customcontrolname-element-for-expressionbinding-for-controls-for-configuration-format"></a>Configuration에 대한 Controls의 ExpressionBinding에 대한 CustomControlName 요소(형식)

공용 컨트롤의 이름을 지정 합니다. 이 요소는 서식 파일의 모든 뷰에서 사용할 수 있는 공용 컨트롤을 정의 하는 데 사용 됩니다.

구성 요소 (format) 컨트롤 요소의 구성 (format) CustomControl 요소에 대 한 Control 요소 구성의 CustomControl에 대 한 구성 (형식) CustomEntries 요소 Format) CustomControl에 대 한 컨트롤의 CustomEntry 요소 구성 (형식) Customentry 요소 구성 요소에 대 한 컨트롤의 customentry에 대 한 컨트롤의 Customentry에 대 한 customentry 요소 구성 (형식) CustomControlName 구성에 대 한 컨트롤의 ExpressionBinding 요소 (형식)

## <a name="syntax"></a>구문

```xml
<CustomControlName>NameofCustomControl</CustomControlName>
```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 `CustomControlName` 요소의 특성, 자식 요소 및 부모 요소에 대해 설명 합니다.

### <a name="attributes"></a>특성

없음

### <a name="child-elements"></a>자식 요소

없음

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|[구성에 대 한 컨트롤 CustomItem의 ExpressionBinding 요소 (형식)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)|컨트롤에 표시 되는 데이터를 정의 합니다.|

## <a name="text-value"></a>텍스트 값

컨트롤의 이름을 지정 합니다.

## <a name="remarks"></a>설명

서식 파일의 모든 보기에서 사용할 수 있는 공용 컨트롤을 만들 수 있으며, 특정 뷰에서 사용할 수 있는 뷰 컨트롤을 만들 수 있습니다. 다음 요소는 이러한 컨트롤의 이름을 지정 합니다.

- [구성 컨트롤에 대 한 컨트롤의 Name 요소 (형식)](./name-element-for-control-for-controls-for-configuration-format.md)

- [View 컨트롤의 컨트롤에 대 한 Name 요소 (Format)](./name-element-for-control-for-controls-for-view-format.md)

## <a name="see-also"></a>참고 항목

[구성 컨트롤에 대 한 컨트롤의 Name 요소 (형식)](./name-element-for-control-for-controls-for-configuration-format.md)

[View 컨트롤의 컨트롤에 대 한 Name 요소 (Format)](./name-element-for-control-for-controls-for-view-format.md)

[구성에 대 한 컨트롤 CustomItem의 ExpressionBinding 요소 (형식)](./expressionbinding-element-for-customitem-for-controls-for-configuration-format.md)

[PowerShell 서식 파일 작성](./writing-a-powershell-formatting-file.md)