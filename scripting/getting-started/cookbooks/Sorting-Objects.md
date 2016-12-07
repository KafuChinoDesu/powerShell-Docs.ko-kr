---
title: "개체 정렬"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: 8530caa8-3ed4-4c56-aed7-1295dd9ba199
ms.openlocfilehash: 99ca62261f8302673f886149a7715ce06efa16cb
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="sorting-objects"></a>개체 정렬
**Sort-Object** cmdlet을 사용하여 표시된 데이터를 검색하기 쉽게 구성할 수 있습니다. **Sort-Object**는 정렬 기준으로 사용할 하나 이상의 속성 이름을 선택하고 이러한 속성의 값을 기준으로 정렬된 데이터를 반환합니다.

예를 들어 Win32_SystemDriver 인스턴스를 표시할 때 정렬 기준으로 **State**와 **Name**을 차례로 사용하여 정렬하려면 다음과 같이 입력하면 됩니다.

```
Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap
```

이 목록에는 필요한 것보다 많은 항목이 포함되어 있지만 다음과 같이 상태가 동일한 항목이 그룹화되어 표시됩니다.

```
Name           State   Started DisplayName
----           -----   ------- -----------
ACPI           Running    True Microsoft ACPI Driver
AFD            Running    True AFD
AmdK7          Running    True AMD K7 Processor Driver
AsyncMac       Running    True RAS Asynchronous Media Driver
...
Abiosdsk       Stopped   False Abiosdsk
ACPIEC         Stopped   False ACPIEC
aec            Stopped   False Microsoft Kernel Acoustic Echo Canceller
...
```

또한 **Descending** 매개 변수를 지정하여 개체를 반대 순서로 정렬할 수도 있습니다. 이렇게 하면 이름은 사전 반대순으로 정렬되고 번호는 내림차순으로 정렬됩니다.

```
PS> Get-WmiObject -Class Win32_SystemDriver | Sort-Object -Property State,Name -Descending | Format-Table -Property Name,State,Started,DisplayName -AutoSize -Wrap

Name           State   Started DisplayName
----           -----   ------- -----------
WS2IFSL        Stopped   False Windows Socket 2.0 Non-IFS Service Provider Supp
                               ort Environment
wceusbsh       Stopped   False Windows CE USB Serial Host Driver...
...
wdmaud         Running    True Microsoft WINMM WDM Audio Compatibility Driver
Wanarp         Running    True Remote Access IP ARP Driver
...
```

