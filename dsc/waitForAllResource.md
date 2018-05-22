---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: DSC WaitForAll 리소스
ms.openlocfilehash: 4413220bb0b5eeef5fd1599f794cd551f15a2925
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
---
# <a name="dsc-waitforall-resource"></a>DSC WaitForAll 리소스

> 적용 대상: Windows PowerShell 5.0 이상

**WaitForAll** DSC(Desired State Configuration) 리소스를 [DSC 구성](configurations.md)의 노드 블록 내에서 사용하면 다른 노드의 구성에 대한 종속성을 지정할 수 있습니다.

**ResourceName** 속성으로 지정된 리소스가 **NodeName** 속성으로 정의된 모든 대상 노드에서 필요한 상태이면 이 리소스가 정상적으로 적용됩니다.


## <a name="syntax"></a>구문

```
WaitForAll [string] #ResourceName
{
    ResourceName = [string]
    NodeName = [string]
    [ RetryIntervalSec = [Uint64] ]
    [ RetryCount = [Uint32] ]
    [ ThrottleLimit = [Uint32]]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>속성

|  속성  |  설명   |
|---|---|
| ResourceName| 사용할 리소스 이름입니다. 이 리소스가 다른 구성에 속하는 경우 "[__ResourceType__]__ResourceName__::[__ConfigurationName__]::[__ConfigurationName__]"으로 이름의 형식을 지정합니다.|
| NodeName| 사용할 리소스의 대상 노드입니다.|
| RetryIntervalSec| 다시 시도할 때까지의 시간(초)입니다. 최소값은 1입니다.|
| RetryCount| 최대 다시 시도 횟수입니다.|
| ThrottleLimit| 동시에 연결하는 컴퓨터의 수입니다. 기본값은 new-cimsession 기본값입니다.|
| DependsOn | 이 리소스를 구성하려면 먼저 다른 리소스의 구성을 실행해야 함을 나타냅니다. 예를 들어, 먼저 실행하려는 리소스 구성 스크립트 블록의 ID가 __ResourceName__이고 해당 형식이 __ResourceType__일 경우, 이 속성을 사용하기 위한 구문은 `DependsOn = "[ResourceType]ResourceName"`입니다.|


## <a name="example"></a>예제

이 리소스를 사용하는 방법의 예제를 보려면 [노드 간 종속성 지정](crossNodeDependencies.md)을 참조하세요.