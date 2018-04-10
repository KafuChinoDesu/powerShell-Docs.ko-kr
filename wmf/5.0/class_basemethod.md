---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: eeafdd8d7a50e0bfc5ebd0ca8e9852c3d7405bf0
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
---
# <a name="call-base-class-method"></a>기본 클래스 메서드 호출

하위 클래스에서 기존 메서드를 재정의할 수 있습니다. 이렇게 하려면 동일한 이름과 서명을 사용하여 메서드를 선언합니다.

```powershell
class baseClass
{
    [int]foo() {return 100500}
}

class childClass1 : baseClass
{
    [int]foo() {return 200600}
}

[childClass1]::new().foo() # return 200600
```

재정의된 구현에서 기본 클래스 메서드를 호출하려면 호출할 때 기본 클래스([baseClass]$this)로 캐스팅합니다.

```powershell
class childClass2 : baseClass
{
    [int]foo()
    {
        return 3 * ([baseClass]$this).foo()
    }
}

[childClass2]::new().foo() # return 301500
```

모든 PowerShell 메서드는 가상입니다. 재정의에 사용한 것과 동일한 구문을 사용하여 하위 클래스에서 비가상 .NET 메서드를 숨길 수 있습니다. 동일한 이름과 서명으로 메서드를 선언하면 됩니다.

```powershell
class MyIntList : system.collections.generic.list[int]
{
    # Add is final in system.collections.generic.list
    [void] Add([int]$arg)
    {
        ([system.collections.generic.list[int]]$this).Add($arg * 2)
    }
}

$list = [MyIntList]::new()
$list.Add(100)
$list[0] # return 200
```