---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: MSFT_DSCLocalConfigurationManager 클래스의 DisableDebugConfiguration 메서드
ms.openlocfilehash: ec5a401de4cb93f302f8572c0408e3f32d8876ad
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892215"
---
# <a name="disabledebugconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a>MSFT_DSCLocalConfigurationManager 클래스의 DisableDebugConfiguration 메서드

DSC 리소스 디버깅을 사용하지 않도록 설정합니다.

## <a name="syntax"></a>구문

```mof
uint32 DisableDebugConfiguration();
```

## <a name="parameters"></a>매개 변수

이 메서드에는 매개 변수가 없습니다.

## <a name="return-value"></a>반환 값

성공하면 0을 반환하고 그렇지 않으면 오류 코드를 반환합니다.

## <a name="remarks"></a>설명

정적 메서드입니다.

## <a name="requirements"></a>요구 사항

**MOF:** DscCore.mof

**네임스페이스**: Root\Microsoft\Windows\DesiredStateConfiguration

## <a name="see-also"></a>참고 항목

[**MSFT_DSCLocalConfigurationManager**](msft-dsclocalconfigurationmanager.md)