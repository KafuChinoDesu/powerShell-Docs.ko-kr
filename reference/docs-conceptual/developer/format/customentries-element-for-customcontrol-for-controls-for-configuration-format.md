---
title: 구성 (형식)에 대 한 CustomControl의 CustomEntries 요소 Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 80fc4de2-208f-4506-9a6a-c2675bb83be4
caps.latest.revision: 11
ms.openlocfilehash: abef6c91500f665c2366f221496d4cfd6444f5c9
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72368822"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-configuration-format"></a>Configuration에 대한 Controls의 CustomControl에 대한 CustomEntries 요소(형식)

공용 컨트롤의 정의를 제공 합니다. 이 요소는 서식 파일의 모든 뷰에서 사용할 수 있는 공용 컨트롤을 정의 하는 데 사용 됩니다.

구성 요소 (format) 컨트롤 요소의 구성 (format) CustomControl 요소에 대 한 Control 요소 구성의 CustomControl에 대 한 구성 (형식) CustomEntries 요소 형식과

## <a name="syntax"></a>구문

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>

```

## <a name="attributes-and-elements"></a>특성 및 요소

다음 섹션에서는 특성, 자식 요소 및 `CustomEntries` 요소의 부모 요소에 대해 설명 합니다. 하나 이상의 자식 요소를 지정 해야 합니다.

### <a name="attributes"></a>특성

없음

### <a name="child-elements"></a>자식 요소

|요소|설명|
|-------------|-----------------|
|[구성에 대 한 CustomControl의 CustomEntry 요소 (형식)](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|공용 컨트롤의 정의를 제공 합니다.|

### <a name="parent-elements"></a>부모 요소

|요소|설명|
|-------------|-----------------|
|[구성 (형식)의 컨트롤에 대 한 CustomControl 요소](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|공용 컨트롤을 정의 합니다.|

## <a name="remarks"></a>설명

대부분의 경우 컨트롤에는 단일 `CustomEntry` 요소에 정의 된 정의가 하나만 있습니다. 그러나 같은 컨트롤을 사용 하 여 서로 다른 .NET 개체를 표시 하려는 경우에는 여러 정의를 사용할 수 있습니다. 이러한 경우 각 개체 또는 개체 집합에 대 한 `CustomEntry` 요소를 정의할 수 있습니다.

## <a name="see-also"></a>참고 항목

[구성 (형식)의 컨트롤에 대 한 CustomControl 요소](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[구성에 대 한 CustomControl의 CustomEntry 요소 (형식)](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[PowerShell 서식 파일 작성](./writing-a-powershell-formatting-file.md)
