---
title: "DSC WindowsFeatureSet 리소스"
ms.date: 2016-05-24
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 1bb0e73a1aae6926040373e017494c2ef5e5fd3e
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="dsc-windowsfeatureset-resource"></a>DSC WindowsFeatureSet 리소스

> 적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0

PowerShell DSC(필요한 상태 구성)의 **WindowsFeatureSet** 리소스에서는 대상 노드에서 역할 및 기능을 추가 또는 제거하는 메커니즘을 제공합니다.
이 리소스는 `Name` 속성에 지정된 각 기능에 대해 [WindowsFeature 리소스](windowsfeatureResource.md)를 호출하는 [복합 리소스](authoringResourceComposite.md)입니다.

여러 Windows 기능을 동일한 상태로 구성하려는 경우 이 리소스를 사용합니다.

## <a name="syntax"></a>구문

```
WindowsFeatureSet [string] #ResourceName
{
    Name = [string[]] 
    [ Ensure = [string] { Absent | Present }  ]
    [ Source = [string] ]
    [ IncludeAllSubFeature = [bool] ]
    [ Credential = [PSCredential] ]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
    
}
```

## <a name="properties"></a>속성

|  속성  |  설명   | 
|---|---| 
| 이름| 추가 또는 제거하려는 역할이나 기능의 이름입니다. 이것은 [Get-WindowsFeature](https://technet.microsoft.com/en-us/library/jj205469.aspx) cmdlet의 **Name** 속성과 동일하며, 역할이나 기능의 표시 이름은 아닙니다.| 
| 자격 증명| 역할 또는 기능을 추가 또는 제거하는 데 사용할 자격 증명입니다.| 
| Ensure| 역할이나 기능이 추가되는지 여부를 지정합니다. 역할이나 기능이 추가되도록 하려면 이 속성을 "Present"로 설정하고, 역할이나 기능이 제거되도록 하려면 이 속성을 "Absent"로 설정합니다.| 
| IncludeAllSubFeature| **Name** 속성에 지정하는 기능과 함께 모든 필수 하위 기능을 포함하려면 이 속성을 **$true**로 설정합니다.| 
| LogPath| 리소스 공급자가 작업을 기록할 로그 파일의 경로입니다.| 
| DependsOn| 이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다. 예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.| 
| 원본| 필요한 경우 설치에 사용할 소스 파일의 위치를 나타냅니다.| 

## <a name="example"></a>예제

다음 구성을 사용하면 **Web-Server**(IIS) 및 **SMTP 서버** 기능과 각각의 모든 하위 기능이 설치됩니다.

```powershell
configuration FeatureSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        WindowsFeatureSet WindowsFeatureSetExample
        {
            Name                    = @("SMTP-Server", "Web-Server")
            Ensure                  = 'Present'
            IncludeAllSubFeature    = $true
        } 
    }
}
```

