---
title: "DSC 서비스 리소스"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: bda348e6597f31b8dfa2014e5c34c5d3bc7bca15
ms.openlocfilehash: 10123359213df7180388d9251e032c2bbb673143

---

# DSC 서비스 리소스

> 적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0


Windows PowerShell DSC(필요한 상태 구성)의 **서비스** 리소스에서는 대상 노드에 있는 서비스를 관리하는 메커니즘을 제공합니다.

## 구문

```
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Path = [string] ]
}
```

## 속성

|  속성  |  설명   | 
|---|---| 
| 이름| 서비스 이름을 나타냅니다. 이 속성은 경우에 따라 표시 이름과 다릅니다. Get-Service cmdlet으로 서비스 목록과 현재 상태를 가져올 수 있습니다.| 
| BuiltInAccount| 서비스에 사용할 로그인 계정을 나타냅니다. 이 속성에 허용된 값은 **LocalService**, **LocalSystem**, 및 **NetworkService**입니다.| 
| 자격 증명| 서비스가 실행되는 계정에 대한 자격 증명을 나타냅니다. 이 속성과 __BuiltinAccount__ 속성은 함께 사용할 수 없습니다.| 
| DependsOn| 이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다. 예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.| 
| StartupType| 서비스의 시작 유형을 나타냅니다. 이 속성에 허용된 값은 **Automatic**, **Disabled** 및 **Manual**입니다.| 
| State| 서비스에 대해 확인하려는 상태를 나타냅니다.| 
| 설명 | 대상 서비스에 대한 설명을 나타냅니다.| 
| DisplayName | 대상 서비스에 대한 표시 이름을 나타냅니다.| 
| Ensure | 대상 서비스가 시스템에 있는지 여부를 지정합니다. 대상 서비스가 존재하지 않도록 하려면 이 속성을 **Absent**로 설정합니다. 대상 서비스가 존재하도록 하려면 이 속성을 **Present**(기본값)로 설정합니다.|
| 경로 | 새 서비스에 대한 이진 파일의 경로를 나타냅니다.| 

## 예제

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        } 
    }
}
```




<!--HONumber=Aug16_HO3-->


