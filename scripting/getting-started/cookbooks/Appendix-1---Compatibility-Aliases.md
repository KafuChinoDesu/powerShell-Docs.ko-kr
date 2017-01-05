---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: powershell,cmdlet
ms.date: 2016-12-12
title: "부록 1 호환성 별칭"
ms.technology: powershell
ms.assetid: 96ad921e-1a57-463e-8e60-424faf8b6ef8
ms.openlocfilehash: 126c124bd9bd4aa7c724fc0ef0b075a649d66f44
ms.sourcegitcommit: 8acbf9827ad8f4ef9753f826ecaff58495ca51b0
translationtype: HT
---
# <a name="appendix-1---compatibility-aliases"></a>부록 1 - 호환성 별칭
Windows PowerShell에는 UNIX 및 Cmd 사용자가 Windows PowerShell에서 친숙한 명령 이름을 사용할 수 있게 해주는 여러 전환 별칭이 있습니다. 아래 표에는 가장 일반적인 별칭이 나와 있으며, 별칭 뒤에 Windows PowerShell 명령과 표준 Windows PowerShell 별칭(있는 경우)이 표시됩니다.

Get-Alias cmdlet을 사용하면 Windows PowerShell 내에서 별칭이 가리키는 Windows PowerShell 명령을 찾을 수 있습니다. 예를 들어 **get-alias cls**를 입력합니다.

```
CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

|CMD 명령|UNIX 명령|PS 명령|PS 별칭|
|---------------|----------------|--------------|------------|
|**dir**|**ls**|**Get-ChildItem**|**gci**|
|**cls**|**clear**|**Clear-Host**(함수)|**cls**|
|**del, erase, rmdir**|**rm**|**Remove-Item**|**ri**|
|**copy**|**cp**|**Copy-Item**|**ci**|
|**move**|**mv**|**Move-Item**|**mi**|
|**rename**|**mv**|**Rename-Item**|**rni**|
|**type**|**cat**|**Get-Content**|**gc**|
|**cd**|**cd**|**Set-Location**|**sl**|
|**md**|**mkdir**|**New-Item**|**ni**|
|**pushd**|**pushd**|**Push-Location**|**pushd**|
|**popd**|**popd**|**Pop-Location**|**popd**|

