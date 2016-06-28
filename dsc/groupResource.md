---
title: "DSC 그룹 리소스"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: f6e33f82f495a89a4aa28c64b7974c170d50cfe1
ms.openlocfilehash: 446c9036989c47c03664d978a1dea4e0234ada8d

---

# DSC 그룹 리소스

> 적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0

Windows PowerShell DSC(필요한 상태 구성)의 그룹 리소스에서는 대상 노드에 있는 로컬 그룹을 관리하는 메커니즘을 제공합니다.

##구문##
```
Group [string] #ResourceName
{
    GroupName = [string]
    [ Credential = [PSCredential] ]
    [ Description = [string[]] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ Members = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn = [string[]] ]
}
```

## 속성

|  속성  |  설명   | 
|---|---| 
| GroupName| 상태를 확인하려는 그룹의 이름입니다.| 
| 자격 증명| 원격 리소스에 액세스하는 데 필요한 자격 증명입니다. **참고**: 이 계정에 로컬이 아닌 모든 계정을 그룹에 추가할 수 있는 Active Directory 권한이 있어야 합니다. 그렇지 않으면 오류가 발생합니다.
| 설명| 그룹에 대한 설명입니다.| 
| Ensure| 그룹이 존재하는지 여부를 나타냅니다. 그룹이 존재하지 않도록 하려면 이 속성을 "Absent"으로 설정합니다. 그룹이 존재하도록 하려면 이 속성을 "Present"(기본값)으로 설정합니다.| 
| 구성원| 현재 그룹 구성원 자격을 지정된 구성원으로 바꾸려면 이 속성을 사용합니다. 이 속성의 값은 폼의 문자열 배열을 *Domain*\\*UserName* 형식의 문자열 배열입니다. 구성에서 이 속성을 설정하는 경우 **MembersToExclude** 또는 **MembersToInclude** 속성을 사용하지 마세요. 사용할 경우 오류가 발생합니다.| 
| MembersToExclude| 그룹의 기존 구성원 자격에서 구성원을 제거하려면 이 속성을 사용합니다. 이 속성의 값은 폼의 문자열 배열을 *Domain*\\*UserName* 형식의 문자열 배열입니다. 구성에서 이 속성을 설정하는 경우 **Members** 속성을 사용하지 마세요. 사용할 경우 오류가 발생합니다.| 
| MembersToInclude| 그룹의 기존 구성원 자격에 구성원을 추가하려면 이 속성을 사용합니다. 이 속성의 값은 폼의 문자열 배열을 *Domain*\\*UserName* 형식의 문자열 배열입니다. 구성에서 이 속성을 설정하는 경우 **Members** 속성을 사용하지 마세요. 사용할 경우 오류가 발생합니다.| 
| DependsOn | 이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다. 예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하는 구문은 `DependsOn = "[ResourceType]ResourceName"``입니다.| 

## 예제 1

다음 예제에서는 “TestGroup”이라는 그룹이 없음을 확인하는 방법을 보여 줍니다. 

```powershell
Group GroupExample
{
    # This will remove TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```
## 예 2
다음 예제에서는 Active Directory 사용자를 로컬 관리자 그룹에 다중 컴퓨터 랩 빌드의 일부로 추가하는 방법을 보여줍니다. 이 빌드에서 사용자는 이미 로컬 관리자 계정에 대해 PSCredential을 사용하고 있습니다. 이것은 또한 도메인 승급 후 도메인 관리자 계정에도 사용되므로, 기존 PSCredential을 도메인 자격 증명으로 전환하여 구성원 서버에서 도메인 사용자가 로컬 관리자 그룹에 추가되도록 설정할 수 있습니다.

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
     @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'   
      }    
    )
}
                  
$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup
        {
            GroupName='Administrators'   
            Ensure= 'Present'             
            MembersToInclude= "$domain\$($Node.AdminAccount)"
            Credential = $dCredential    
            PsDscRunAsCredential = $DCredential
        }
```




<!--HONumber=Jun16_HO4-->


