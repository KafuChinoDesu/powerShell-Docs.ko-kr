---
manager: carmonm
ms.topic: article
author: rpsqrd
ms.author: ryanpu
ms.prod: powershell
keywords: powershell,cmdlet,jea
ms.date: 2016-12-05
title: "JEA 세션 구성"
ms.technology: powershell
ms.openlocfilehash: 1d410e345ff31a5f8149810fb9c3b07e92b27e05
ms.sourcegitcommit: b88151841dd44c8ee9296d0855d8b322cbf16076
translationtype: HT
---
# <a name="jea-session-configurations"></a>JEA 세션 구성

> 적용 대상: Windows PowerShell 5.0

JEA 끝점은 특정한 방법으로 PowerShell 세션 구성 파일을 만들고 등록하여 시스템에 등록합니다.
세션 구성은 JEA 끝점을 사용할 수 있는 *사용자* 및 해당 사용자가 액세스할 수 있는 역할을 결정합니다.
또한 JEA 세션에서 모든 역할의 사용자에게 적용되는 전역 설정을 정의합니다.

이 항목에서는 PowerShell 세션 구성 파일을 만들고 JEA 끝점을 등록하는 방법을 설명합니다.

## <a name="create-a-session-configuration-file"></a>세션 구성 파일 만들기

JEA 끝점을 등록하려면 해당 끝점이 구성되는 방법을 지정해야 합니다.
여기서 고려해야 할 옵션은 많지만, 그중 가장 중요한 옵션은 JEA 끝점에 대한 액세스 권한을 가져야 하는 사용자, 해당 사용자에게 할당할 역할, JEA를 사용할 ID 및 JEA 끝점의 이름입니다.
이러한 내용은 모두 PowerShell 세션 구성 파일(확장명 .pssc로 끝나는 PowerShell 데이터 파일)에 정의됩니다.

JEA 끝점에 대한 기본 세션 구성 파일을 만들려면 다음 명령을 실행합니다.

```powershell
New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\MyJEAEndpoint.pssc
```

> [!TIP]
> 가장 일반적인 구성 옵션만 기본 파일에 기본적으로 포함됩니다.
> 생성된 PSSC에 적용 가능한 모든 설정을 포함하려면 `-Full` 스위치를 사용하세요.

세션 구성 파일은 모든 텍스트 편집기에서 열 수 있습니다.
`-SessionType RestrictedRemoteServer` 필드는 세션 구성이 안전한 관리를 위해 JEA에서 사용됨을 나타냅니다.
이 방법으로 구성된 세션은 [NoLanguage 모드](https://technet.microsoft.com/en-us/library/dn433292.aspx)에서 작동하며 다음과 같은 8가지 기본 cmdlet(및 별칭)만 사용할 수 있습니다.

- Clear-Host(cls, clear)
- Exit-PSSession(exsn, exit)
- Get-Command(gcm)
- Get-FormatData
- Get-Help
- Measure-Object(measure)
- Out-Default
- Select-Object(select): PowerShell 공급자와 외부 프로그램(실행 파일, 스크립트 등)은 모두 사용할 수 없습니다.

JEA 세션에 대해 구성할 다른 여러 가지 필드도 있습니다.
이러한 필드는 다음 섹션에 설명되어 있습니다.

### <a name="choose-the-jea-identity"></a>JEA ID 선택

백그라운드에서 JEA에는 연결된 사용자의 명령을 실행할 때 사용할 ID(계정)가 필요합니다.
세션 구성 파일에서 JEA가 사용할 ID를 결정합니다.

#### <a name="local-virtual-account"></a>로컬 가상 계정

이 JEA 끝점에서 지원하는 역할이 모두 로컬 컴퓨터를 관리하는 데 사용되고 명령을 실행하는 데 로컬 관리자 계정으로 충분하다면 로컬 가상 계정을 사용하도록 JEA를 구성해야 합니다.
가상 계정은 특정 사용자에게 고유하고 해당 PowerShell 세션 기간 동안만 지속하는 임시 계정입니다.
구성원 서버 또는 워크스테이션에서 가상 계정은 로컬 컴퓨터의 **Administrators** 그룹에 속하고 대부분의 시스템 리소스에 액세스할 수 있습니다.
Active Directory 도메인 컨트롤러에서 가상 계정은 도메인의 **Domain Admins** 그룹에 속합니다.

```powershell
# Setting the session to use a virtual account
RunAsVirtualAccount = $true
```

세션 구성에서 지원하는 역할에 광범위한 권한이 필요하지 않으면 필요에 따라 가상 계정이 속할 보안 그룹을 지정할 수 있습니다.
구성원 서버 또는 워크스테이션에서 지정된 보안 그룹은 도메인의 그룹이 아니라 로컬 그룹이어야 합니다.

하나 이상의 보안 그룹을 지정한 경우 가상 계정은 더 이상 로컬 또는 도메인 관리자 그룹에 속하지 않게 됩니다.

```powershell
# Setting the session to use a virtual account that only belongs to the NetworkOperator and NetworkAuditor local groups
RunAsVirtualAccount = $true
RunAsVirtualAccountGroups = 'NetworkOperator', 'NetworkAuditor'
```

#### <a name="group-managed-service-account"></a>그룹 관리 서비스 계정


JEA 사용자가 다른 컴퓨터 또는 웹 서비스와 같은 네트워크 리소스에 액세스해야 하는 시나리오의 경우 gMSA(그룹 관리 서비스 계정)가 사용하기 더 적합한 ID입니다.
gMSA 계정은 도메인 내의 모든 컴퓨터에 있는 리소스에 대해 인증하는 데 사용할 수 있는 도메인 ID를 제공합니다.
gMSA 계정이 제공하는 권한은 액세스하는 리소스에 의해 결정됩니다.
컴퓨터/서비스 관리자가 명시적으로 gMSA 계정 관리자 권한을 부여하지 않은 한, 자동으로 컴퓨터 또는 서비스에 대한 관리자 권한이 부여되지는 않습니다.

```powershell
# Configure JEA sessions to use the gMSA account in the local computer's domain with the sAMAccountName of 'MyJEAgMSA'
GroupManagedServiceAccount = 'MyJEAgMSA'
```

gMSA 계정은 다음과 같은 몇 가지 이유로 네트워크 리소스에 액세스해야 하는 경우에만 사용되어야 합니다.

- 모든 사용자가 같은 실행 ID를 공유하므로 gMSA 계정을 사용할 경우 사용자까지 거슬러 올라가 작업을 추적하기가 어렵습니다. PowerShell 세션 기록 및 로그를 확인하여 사용자와 해당 작업의 상관 관계를 지정해야 합니다.

- gMSA 계정은 연결하는 사용자가 액세스할 필요가 없는 많은 네트워크 리소스에 대한 액세스 권한을 가질 수 있습니다. 항상 JEA 세션에서 유효 권한을 제한하여 최소 권한 원칙을 따르도록 합니다.

> [!NOTE]
> 그룹 관리 서비스 계정은 Windows PowerShell 5.1 이상 및 도메인에 가입된 컴퓨터에서만 사용할 수 있습니다.


#### <a name="more-information-about-run-as-users"></a>실행 사용자에 대한 자세한 내용

실행 ID 및 실행 ID가 JEA 세션의 보안에 어떤 영향을 주는지에 대한 자세한 내용은 [보안 고려 사항](security-considerations.md) 문서에서 확인할 수 있습니다.

### <a name="session-transcripts"></a>세션 기록

사용자의 세션 기록을 자동으로 기록하려면 JEA 세션 구성 파일을 구성하는 것이 좋습니다.
PowerShell 세션 기록은 연결하는 사용자, 사용자에게 할당된 실행 ID 및 사용자가 실행한 명령에 대한 정보를 포함합니다.
이러한 기록은 시스템에 대한 특정 변경 내용을 수행한 사용자를 파악해야 하는 감사 팀에 유용할 수 있습니다.

세션 구성 파일에서 자동 기록을 구성하려면 기록이 저장되는 폴더의 경로를 제공합니다.

```powershell
TranscriptDirectory = 'C:\ProgramData\JEAConfiguration\Transcripts'
```

지정된 폴더는 사용자가 폴더 내의 데이터를 수정하거나 삭제하지 못하도록 구성되어야 합니다.
기록은 디렉터리에 대한 읽기 및 쓰기 권한이 필요한 로컬 시스템 계정에 의해 폴더에 기록됩니다.
표준 사용자는 폴더에 대한 액세스 권한이 없어야 하고, 제한된 보안 관리자 집합은 기록을 감사하기 위한 액세스 권한이 있어야 합니다.

### <a name="user-drive"></a>사용자 드라이브

연결하는 사용자가 명령을 실행하기 위해 JEA 끝점으로/에서 파일을 복사해야 할 경우 세션 구성 파일에서 사용자 드라이브를 사용하도록 설정할 수 있습니다.
사용자 드라이브는 각 연결하는 사용자에 대해 고유한 폴더에 매핑되는 [PSDrive](https://msdn.microsoft.com/en-us/powershell/scripting/getting-started/cookbooks/managing-windows-powershell-drives)입니다.
이 폴더는 전체 파일 시스템에 대한 액세스 권한을 제공하거나 FileSystem 공급자를 노출하지 않고 각 연결하는 사용자가 시스템으로/에서 파일을 복사할 수 있는 공간 역할을 합니다.
사용자 드라이브 콘텐츠는 세션 전체에서 유지되어 네트워크 연결이 중단될 수 있는 상황을 수용합니다.

```powershell
MountUserDrive = $true
```

기본적으로 사용자 드라이브를 사용하여 사용자당 최대 50MB의 데이터를 저장할 수 있습니다.
*UserDriveMaxmimumSize* 필드를 사용하여 사용자가 사용할 수 있는 데이터의 양을 제한할 수 있습니다.

```powershell
# Enables the user drive with a per-user limit of 500MB (524288000 bytes)
MountUserDrive = $true
UserDriveMaximumSize = 524288000
```

사용자 드라이브의 데이터가 유지되지 않게 하려는 경우 매일 밤 자동으로 폴더를 정리하도록 시스템에 대한 예약된 작업을 구성할 수 있습니다.

> [!NOTE]
> 사용자 드라이브는 Windows PowerShell 5.1 이상에서만 사용할 수 있습니다.

### <a name="role-definitions"></a>역할 정의

세션 구성 파일의 역할 정의는 *역할*에 대한 *사용자*의 매핑을 정의합니다.
JEA 끝점이 등록되면 이 필드에 포함된 모든 사용자 또는 그룹에 자동으로 해당 JEA 끝점에 대한 사용 권한이 부여됩니다.
각 사용자 또는 그룹은 해시 테이블의 키로 한 번만 포함될 수 있지만, 역할은 여러 개가 할당될 수 있습니다.
역할 기능의 이름은 .psrc 확장명이 없는 역할 기능 파일의 이름이어야 합니다.

```powershell
RoleDefinitions = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}
```

사용자가 역할 정의에서 둘 이상의 그룹에 속하는 경우 각 역할에 대한 액세스 권한을 얻게 됩니다.
두 역할이 같은 cmdlet에 대한 액세스 권한을 부여하는 경우 사용자에게 최대로 허용되는 매개 변수 집합이 부여됩니다.

### <a name="role-capability-search-order"></a>역할 기능 검색 순서
위의 예제에 표시된 것처럼 역할 기능은 역할 기능 파일의 일반 이름(확장명이 없는 파일 이름)으로 참조됩니다.
시스템에서 일반 이름이 같은 역할 기능을 여러 개 사용할 수 있는 경우 PowerShell에서는 암시적 검색 순서를 사용하여 유효 역할 기능 파일을 선택합니다.
이름이 같은 모든 역할 기능 파일에 대한 액세스 권한을 부여하지는 **않습니다**.

JEA 역할 기능에 대한 검색 순서는 `$env:PSModulePath`의 경로 순서 지정 및 부모 모듈의 이름에 의해 결정됩니다.
PowerShell의 기본 모듈 경로는 다음과 같습니다.

```powershell
PS C:\> $env:PSModulePath


C:\Users\Alice\Documents\WindowsPowerShell\Modules;C:\Program Files\WindowsPowerShell\Modules;C:\WINDOWS\system32\WindowsPowerShell\v1.0\Modules\
```

PSModulePath 목록에서 앞에(왼쪽에) 나타나는 경로는 오른쪽에 있는 경로보다 우선 순위가 높습니다.

각 경로 내에는 0개 이상의 PowerShell 모듈이 있을 수 있습니다.
역할 기능은 원하는 이름과 일치하는 역할 기능 파일을 포함하는 첫 번째 모듈에서 사전순으로 선택됩니다.

이 절차를 이해하는 데 도움이 되도록 여기서는 더하기 기호(+)가 폴더를 나타내고 빼기 기호(-)가 파일을 나타내는 다음 예제를 살펴봅니다.

```
+ C:\Program Files\WindowsPowerShell\Modules
    + ContosoMaintenance
        - ContosoMaintenance.psd1
        + RoleCapabilities
            - DnsAdmin.psrc
            - DnsOperator.psrc
            - DnsAuditor.psrc
    + FabrikamModule
        - FabrikamModule.psd1
        + RoleCapabilities
            - DnsAdmin.psrc
            - FileServerAdmin.psrc

+ C:\Windows\System32\WindowsPowerShell\v1.0\Modules
    + BuiltInModule
        - BuiltInModule.psd1
        + RoleCapabilities
            - DnsAdmin.psrc
            - OtherBuiltinRole.psrc
```

이 시스템에 설치된 역할 기능 파일은 여러 개가 있습니다.
세션 구성 파일에서 사용자에게 "DnsAdmin" 역할에 대한 액세스 권한을 제공하면 어떻게 되나요?


유효 역할 기능 파일은 "C:\\Program Files\\WindowsPowerShell\\Modules\\ContosoMaintenance\\RoleCapabilities\\DnsAdmin.psrc"에 있습니다.

이유가 궁금한 경우 다음과 같은 우선 순위의 2가지 순서를 기억하세요.

1. `$env:PSModulePath` 변수는 System32 폴더 앞에 나열된 Program Files 폴더를 포함하므로 Program Files 폴더의 파일을 선호합니다.
2. 사전순으로 ContosoMaintenance 모듈은 FabrikamModule 앞에 오므로 ContosoMaintenance에서 DnsAdmin 역할을 선택합니다.

### <a name="conditional-access-rules"></a>조건부 액세스 규칙

RoleDefinitions 필드에 포함된 모든 사용자 및 그룹에는 자동으로 JEA 끝점에 대한 액세스 권한이 부여됩니다.
조건부 액세스 규칙을 사용하여 이 액세스 권한을 구체화하고 사용자가 사용자에게 할당된 역할에 영향을 주지 않는 추가 보안 그룹에 속해야 하도록 할 수 있습니다.
이 기능은 "Just In Time" 권한 있는 액세스 권한 관리 솔루션, 스마트 카드 인증 또는 다른 다단계 인증 솔루션을 JEA와 통합하려는 경우 유용할 수 있습니다.

조건부 액세스 규칙은 세션 구성 파일에서 RequiredGroups 필드에 정의됩니다.
여기서 'And' 및 'Or' 키를 사용하여 규칙을 구성하는 해시 테이블(필요에 따라 중첩됨)을 제공할 수 있습니다.
다음은 이 필드를 사용하는 방법의 몇 가지 예입니다.

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

> [!NOTE]
> 조건부 액세스 규칙은 Windows PowerShell 5.1 이상에서만 사용할 수 있습니다.

### <a name="other-properties"></a>기타 속성
세션 구성 파일도 역할 기능 파일이 수행할 수 있는 모든 작업을 수행할 수 있지만, 연결하는 사용자에게 다른 명령에 대한 액세스 권한을 부여하는 기능은 제외됩니다.
모든 사용자가 특정 cmdlet, 함수 또는 공급자에 액세스할 수 있게 하려는 경우 세션 구성 파일에서 직접 이렇게 할 수 있습니다.
세션 구성 파일에서 지원되는 속성의 전체 목록을 보려면 `Get-Help New-PSSessionConfigurationFile -Full`을 실행합니다.

## <a name="testing-a-session-configuration-file"></a>세션 구성 파일 테스트

[Test-PSSessionConfigurationFile](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/test-pssessionconfigurationfile) cmdlet을 사용하여 세션 구성 파일을 테스트할 수 있습니다.
구문이 올바른지 확인하기 위해 텍스트 편집기를 사용하여 수동으로 pssc 파일을 편집한 경우 세션 구성 파일을 테스트하는 것이 좋습니다.
세션 구성 파일이 이 테스트를 통과하지 못하면 시스템에 등록될 수 없습니다.

## <a name="sample-session-configuration-file"></a>샘플 세션 구성 파일

다음은 JEA에 대한 세션 구성을 만들고 유효성을 검사하는 방법을 보여 주는 전체 예제입니다.
역할 정의는 편의성과 가독성을 위해 생성되어 `$roles` 변수에 저장되어 있습니다.
이는 작업을 수행하기 위한 요구 사항은 아닙니다.

```powershell
$roles = @{
    'CONTOSO\JEA_DNS_ADMINS'    = @{ RoleCapabilities = 'DnsAdmin', 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_OPERATORS' = @{ RoleCapabilities = 'DnsOperator', 'DnsAuditor' }
    'CONTOSO\JEA_DNS_AUDITORS'  = @{ RoleCapabilities = 'DnsAuditor' }
}

New-PSSessionConfigurationFile -SessionType RestrictedRemoteServer -Path .\JEAConfig.pssc -RunAsVirtualAccount -TranscriptDirectory 'C:\ProgramData\JEAConfiguration\Transcripts' -RoleDefinitions $roles -RequiredGroups @{ Or = '2FA-logon', 'smartcard-logon' }
Test-PSSessionConfigurationFile -Path .\JEAConfig.pssc # should yield True
```

## <a name="updating-session-configuration-files"></a>세션 구성 파일 업데이트

역할에 대한 사용자의 매핑을 비롯한 JEA 세션 구성의 속성을 변경해야 하는 경우 JEA 세션 구성을 [등록 취소](register-jea.md#unregistering-jea-configurations)한 후 [다시 등록](register-jea.md)해야 합니다.
JEA 세션 구성을 다시 등록할 때 원하는 변경 내용을 포함하는 업데이트된 PowerShell 세션 구성 파일을 사용합니다.

## <a name="next-steps"></a>다음 단계

- [JEA 구성 등록](register-jea.md)
- [JEA 역할 작성](role-capabilities.md)