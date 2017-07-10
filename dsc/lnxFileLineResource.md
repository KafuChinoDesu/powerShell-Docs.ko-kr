---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "Linux nxFileLine 리소스용 DSC"
ms.openlocfilehash: bde42bbe217fc9acf5a3f2ee0136d30e2b5f2415
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
<a id="dsc-for-linux-nxfileline-resource" class="xliff"></a>
# Linux nxFileLine 리소스용 DSC

PowerShell DSC(필요한 상태 구성)의 **nxFileLine** 리소스에서는 Linux 노드 상의 구성 파일 내 줄을 관리하는 메커니즘을 제공합니다.

<a id="syntax" class="xliff"></a>
## 구문

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

<a id="properties" class="xliff"></a>
## 속성

|  속성 |  설명 | 
|---|---|
| FilePath| 대상 노드에서 줄을 관리하는 파일의 전체 경로입니다.| 
| ContainsLine| 파일에 존재하도록 할 줄입니다. 이 줄은 파일에 존재하지 않는 경우 파일에 추가됩니다. **ContainsLine**은 필수지만 필요하지 않은 경우 빈 문자열(`ContainsLine = ‘’``)로 설정할 수 있습니다.| 
| DoesNotContainPattern| 파일에 존재할 수 없는 줄에 대한 정규식 패턴입니다. 파일에 존재하고 이 정규식과 일치하는 모든 줄의 경우 파일에서 제거됩니다.| 
| DependsOn | 이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다. 예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 **ID**가 **ResourceName**이고 해당 형식이 **ResourceType**일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.| 

<a id="example" class="xliff"></a>
## 예제

다음 예제에서는 **nxFileLine** 리소스를 사용하여 사용자: monuser가 not requiretty로 구성되도록 `/etc/sudoers` 파일을 구성하는 것을 보여 줍니다.

```
Import-DSCResource -Module nx 

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
} 
```

