---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: 개체의 일부 선택(Select Object)
ms.assetid: 72e64b1a-d351-4500-9da3-24d8a71d7a92
ms.openlocfilehash: 323c57ba4462e20d9713fb74732989584f5a993f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403425"
---
# <a name="selecting-parts-of-objects-select-object"></a><span data-ttu-id="9a4c6-103">개체의 일부 선택(Select-Object)</span><span class="sxs-lookup"><span data-stu-id="9a4c6-103">Selecting Parts of Objects (Select-Object)</span></span>

<span data-ttu-id="9a4c6-104">**Select-Object** cmdlet을 사용하면 새 사용자 지정 Windows PowerShell 개체를 만들 수 있습니다. 이러한 개체에는 해당 개체를 만드는 데 사용된 개체에서 선택한 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c6-104">You can use the **Select-Object** cmdlet to create new, custom Windows PowerShell objects that contain properties selected from the objects you use to create them.</span></span> <span data-ttu-id="9a4c6-105">다음 명령을 입력하면 Win32_LogicalDisk WMI 클래스의 Name 및 FreeSpace 속성만 포함된 새 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c6-105">Type the following command to create a new object that includes only the Name and FreeSpace properties of the Win32_LogicalDisk WMI class:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace

Name                                    FreeSpace
----                                    ---------
C:                                      50664845312
```

<span data-ttu-id="9a4c6-106">이 명령을 실행해도 데이터 형식이 표시되지 않지만 다음과 같이 Select-Object 뒤에서 결과를 Get-Member에 파이프하면 새 유형의 개체인 PSCustomObject가 만들어지는 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c6-106">You cannot see the type of data after issuing that command, but if you pipe the result to Get-Member after the Select-Object, you can tell that you have a new type of object, a PSCustomObject:</span></span>

```
PS> Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace| Get-Member

   TypeName: System.Management.Automation.PSCustomObject

Name        MemberType   Definition
----        ----------   ----------
Equals      Method       System.Boolean Equals(Object obj)
GetHashCode Method       System.Int32 GetHashCode()
GetType     Method       System.Type GetType()
ToString    Method       System.String ToString()
FreeSpace   NoteProperty  FreeSpace=...
Name        NoteProperty System.String Name=C:
```

<span data-ttu-id="9a4c6-107">Select-Object는 다양한 용도로 사용할 수 있는데,</span><span class="sxs-lookup"><span data-stu-id="9a4c6-107">Select-Object has many uses.</span></span> <span data-ttu-id="9a4c6-108">그 중 하나는 데이터를 복제하는 것입니다(이러한 데이터는 나중에 수정할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="9a4c6-108">One of them is replicating data that you can then modify.</span></span> <span data-ttu-id="9a4c6-109">이렇게 하면 이전 섹션에서 설명한 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c6-109">We can now handle the problem we ran across in the previous section.</span></span> <span data-ttu-id="9a4c6-110">새로 만든 개체에서 FreeSpace 값을 업데이트하면 다음과 같이 설명이 포함된 레이블이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a4c6-110">We can update the value of FreeSpace in our newly-created objects and the output will include the descriptive label:</span></span>

```
Get-WmiObject -Class Win32_LogicalDisk | Select-Object -Property Name,FreeSpace | ForEach-Object -Process {$_.FreeSpace = ($_.FreeSpace)/1024.0/1024.0; $_}
Name                                                                  FreeSpace
----                                                                  ---------
C:                                                                48317.7265625
```