---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: PowerShell 스크립팅
ms.openlocfilehash: c6ba3abc2544834e2cbec16a524f79399a1d2599
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094054"
---
# <a name="powershell"></a>PowerShell

.NET Framework를 기반으로 하는 PowerShell은 작업 기반 명령줄 셸 및 스크립트 언어입니다. 시스템 관리자와 고급 사용자가 여러 운영 체제(Linux, macOS, Unix 및 Windows) 및 해당 운영 체제에서 실행되는 응용 프로그램과 관련된 프로세스의 관리를 신속하게 자동화할 수 있도록 특별히 설계되었습니다.

## <a name="powershell-is-open-source"></a>PowerShell이 오픈 소스로 제공됨

이제 GitHub에서 PowerShell 기본 소스 코드를 사용할 수 있으며 커뮤니티 참여가 개방됩니다.
[GitHub의 PowerShell 소스](https://github.com/powershell/powershell)를 참조하세요.

[Get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell)(PowerShell 다운로드)에서 필요한 비트로 시작할 수 있습니다.
또는 [시작](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)에서 둘러보기로 시작합니다.

## <a name="powershell-design-goals"></a>PowerShell 디자인 목표
PowerShell은 장기적인 문제를 제거하고 새로운 기능을 추가하여 명령줄 및 스크립팅 환경을 개선하도록 설계되었습니다.

### <a name="discoverability"></a>검색 기능
PowerShell을 사용하면 해당 기능을 쉽게 검색할 수 있습니다. 예를 들어 Windows 서비스를 보고 변경하는 cmdlet 목록을 찾으려면 다음과 같이 입력합니다.

```powershell
Get-Command *-Service
```

작업을 수행하는 cmdlet을 검색한 후 `Get-Help` cmdlet을 사용하여 cmdlet에 대해 자세히 알아볼 수 있습니다.
예를 들어 `Get-Service` cmdlet에 대한 도움말을 표시하려면 다음과 같이 입력합니다.

```powershell
Get-Help Get-Service
```
대부분의 cmdlet은 조작한 다음 텍스트로 렌더링하여 표시할 수 있는 개체를 내보냅니다.
해당 cmdlet의 출력을 완벽하게 이해하려면 출력을 `Get-Member` cmdlet에 파이프합니다.
예를 들어 다음 명령은 `Get-Service` cmdlet에 의한 개체 출력의 멤버에 대한 정보를 표시합니다.

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a>Consistency
시스템 관리는 내재된 복잡성을 제어하는 데 도움이 되는 일관된 인터페이스가 있는 도구 및 복잡한 노력일 수 있습니다.
일관성으로 알려진 명령줄 도구 및 스크립트 가능한 COM 개체는 없습니다.

PowerShell의 일관성은 기본 자산 중 하나입니다.
예를 들어 `Sort-Object` cmdlet을 사용하는 방법을 배운 경우 해당 지식을 사용하여 모든 cmdlet의 출력을 정렬할 수 있습니다.
각 cmdlet의 다른 정렬 루틴을 배울 필요가 없습니다.

또한 cmdlet 개발자는 해당 cmdlet의 정렬 기능을 디자인할 필요가 없습니다.
PowerShell에서 기본 기능을 지원하는 프레임워크를 제공하며 인터페이스의 여러 측면에서 강제로 일관성을 유지하도록 합니다.
프레임워크는 일반적으로 개발자가 선택하는 몇 가지 사항을 제거하지만, 그 대신 강력하고 사용하기 쉬운 cmdlet을 훨씬 더 간단하게 개발할 수 있게 합니다.

### <a name="interactive-and-scripting-environments"></a>대화형 및 스크립팅 환경
PowerShell은 명령줄 도구와 COM 개체에 대한 액세스를 제공하고 .NET FCL(Framework 클래스 라이브러리)의 기능을 사용할 수 있게 해주는 결합된 대화형 및 스크립팅 환경입니다.

이 환경은 대화형 환경에 여러 명령줄 도구를 제공하는 Windows 명령 프롬프트를 개선합니다.
또한 여러 명령줄 도구와 COM 자동화 개체를 사용할 수 있게 하지만 대화형 환경을 제공하지 않는 WSH(Windows 스크립트 호스트) 스크립트를 개선합니다.

PowerShell은 이러한 모든 기능에 대한 액세스를 결합하여 대화형 사용자와 스크립트 작성자의 능력을 확장하고 시스템 관리를 보다 관리가 용이하게 합니다.

### <a name="object-orientation"></a>개체 방향
텍스트로 명령을 입력하여 PowerShell을 조작하지만 PowerShell은 텍스트가 아니라 개체를 기반으로 합니다.
명령의 출력은 개체입니다.
출력 개체를 다른 명령에 입력으로 보낼 수 있습니다.
결과적으로, PowerShell은 다른 셸에 익숙한 사용자에게 친숙한 인터페이스를 제공하는 동시에 새롭고 강력한 명령줄 패러다임을 소개합니다.
텍스트 대신 개체를 보낼 수 있게 함으로써 명령 간에 데이터를 보내는 개념을 확장합니다.

### <a name="easy-transition-to-scripting"></a>스크립팅으로 쉽게 전환
PowerShell을 사용하면 대화형 명령 입력에서 스크립트 생성 및 실행으로 쉽게 전환할 수 있습니다.
PowerShell 명령 프롬프트에서 명령을 입력하여 작업을 수행하는 명령을 검색할 수 있습니다.
그런 다음 스크립트로 사용하기 위해 파일에 복사하기 전에 해당 명령을 기록에 저장할 수 있습니다.
