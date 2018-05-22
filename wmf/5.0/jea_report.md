---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 7982acc111e95b4167f948314f176d53f39d3620
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="reporting-on-jea"></a>JEA에 대한 보고
JEA 구성의 상태를 보고하려면 다음을 사용할 수 있습니다.
1.  **Get-PSSessionConfiguration** - 지정된 컴퓨터에서 등록된 모든 끝점 목록을 반환합니다.
2.  **Get-PSSessionCapability** - 특정 끝점에 대해 지정된 사용자에게 제공되는 기능을 보고합니다.

다음은 **Get-PSSessionCapability**의 예제입니다.
```powershell
Get-PSSessionCapability -ConfigurationName Maintenance -Username "CONTOSO\JohnDoe"

CommandType     Name                                               Version    Source
-----------     ----                                               -------    ------
Alias           clear -> Clear-Host
Alias           cls -> Clear-Host
Alias           exsn -> Exit-PSSession
Alias           gcm -> Get-Command
Alias           measure -> Measure-Object
Alias           select -> Select-Object
Function        Clear-Host
Function        Exit-PSSession
Function        Get-Command
Function        Get-FormatData
Function        Get-Help
Function        Get-UserInfo
Function        Measure-Object
Function        Out-Default
Function        Select-Object
Cmdlet          Restart-Service                                    3.0.0.0 Microsof...


```

JEA 세션 중 사용자가 수행한 _작업_을 보고하려면 다음을 수행할 수 있습니다.
1. 해당 JEA 끝점에 대해 “자격 증명 입력” 기록을 사용하고 기록 디렉터리에서 각 사용자의 작업에 대한 전체 로그를 참조합니다.
2. PowerShell 모듈 로깅을 켜고 PowerShell 이벤트 로그를 검사합니다.
