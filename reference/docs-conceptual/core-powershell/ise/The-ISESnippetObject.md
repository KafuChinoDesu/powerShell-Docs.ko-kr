---
ms.date: 2017-06-05T00:00:00.000Z
keywords: powershell,cmdlet
title: "ISESnippet 개체"
ms.assetid: 98bc8113-c3cd-4201-bdb9-9d9bdb7e266c
ms.openlocfilehash: 5cc49cd504a1343a5737f78eb886bb41591d087d
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/03/2017
---
# <a name="the-isesnippetobject"></a>ISESnippet 개체
  **ISESnippet** 개체는 Microsoft.PowerShell.Host.ISE.ISESnippet 클래스의 인스턴스입니다. **$psISE.CurrentPowerShellTab.Snippets** 컬렉션의 멤버는 모두 **ISESnippet** 개체의 예입니다. 코드 조각을 만드는 가장 쉬운 방법은 [New-IseSnippet&#91;PSITPro5_ISE&#93;](https://technet.microsoft.com/en-us/library/0a6339a3-2683-4a8e-8929-90ad9a95c3e0) cmdlet을 사용하는 것입니다.

## <a name="properties"></a>속성

###  <a name="DisplayName"></a> Author
  Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다. 

 코드 조각 작성자의 이름을 가져오는 읽기 전용 속성입니다.

```
# Get the author of the first snippet item
$psISE.CurrentPowerShellTab.Snippets.Item(0).Author

```

###  <a name="Action"></a> CodeFragment
  Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다. 

 편집기에 삽입할 코드 조각을 가져오는 읽기 전용 속성입니다.

```
# Get the code fragment associated with the first snippet item.
$psISE.CurrentPowerShellTab.Snippets.Item(0).CodeFragment

```

###  <a name="Shortcut"></a> Shortcut
  Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다. 

 메뉴 항목에 대한 Windows 바로 가기 키를 가져오는 읽기 전용 속성입니다.

```
# Get the shortcut for the first submenu item.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P")
$psISE.CurrentPowerShellTab.AddOnsMenu.Submenus[0].Shortcut
```

## <a name="see-also"></a>참고 항목
- [ISESnippetCollection 개체](The-ISESnippetCollection-Object.md) 
- [Windows PowerShell ISE 스크립팅 개체 모델](The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [Windows PowerShell ISE 개체 모델 참조](Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [ISE 개체 모델 계층 구조](The-ISE-Object-Model-Hierarchy.md)

  
