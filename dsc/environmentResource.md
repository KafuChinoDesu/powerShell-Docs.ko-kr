---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "DSC 환경 리소스"
ms.openlocfilehash: 7c98798fa0e8fc865798ea30530e41ac87b2dadc
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
<a id="dsc-environment-resource" class="xliff"></a>
# DSC 환경 리소스

> 적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0

PowerShell DSC(필요한 상태 구성)의 __Environment__ 리소스에서는 시스템 환경 변수를 관리하는 메커니즘을 제공합니다.

<a id="syntax" class="xliff"></a>
## 구문
``` mof
Environment [string] #ResourceName
{
    Name = [string]
    [ Ensure = [string] { Absent | Present }  ]
    [ Path = [bool] ]
    [ DependsOn = [string[]] ]
    [ Value = [string] ]
}
```

<a id="properties" class="xliff"></a>
## 속성

|  속성  |  설명   | 
|---|---| 
| 이름| 특정 상태를 확인하려는 환경 변수의 이름을 나타냅니다.| 
| Ensure| 변수가 있는지 여부를 나타냅니다. 변수가 없는 경우 환경 변수를 만들거나 변수가 이미 있는 경우 그 값이 __Value__ 속성을 통해 제공된 값과 일치하는지 확인하려면 이 속성을 __있음__으로 설정합니다. 변수가 존재하는 경우 변수를 삭제하려면 이 속성을 __없음__으로 설정합니다.| 
| 경로| 구성 중인 환경 변수를 정의합니다. 변수가 __Path__ 변수이면 이 속성을 __$true__로 설정하고, 그렇지 않으면 __$false__로 설정합니다. 기본값은 __$false__입니다. 구성되고 있는 변수가 __Path__ 변수라면, __Value__ 속성을 통해 제공된 값은 기존 값에 추가됩니다.| 
| DependsOn | 이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다. 예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.| 
| Value| 환경 변수에 할당할 값입니다.| 

<a id="example" class="xliff"></a>
## 예제

다음 예제에서는 __TestEnvironmentVariable__이 있고 그 값이 __TestValue__인지 확인합니다. 없을 경우 만듭니다.

```powershell
Environment EnvironmentExample
{
    Ensure = "Present"  # You can also set Ensure to "Absent"
    Name = "TestEnvironmentVariable"
    Value = "TestValue"
}
```

