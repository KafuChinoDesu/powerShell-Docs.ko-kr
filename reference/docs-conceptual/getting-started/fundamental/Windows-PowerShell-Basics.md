---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "Windows PowerShell 기본 사항"
ms.assetid: 6b3cbbc8-060c-4877-b00b-7300dbbe4e28
ms.openlocfilehash: 7b5cdfce876aa7d5559fe772379829011b275a02
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2017
---
# <a name="windows-powershell-basics"></a>Windows PowerShell 기본 사항
그래픽 사용자 인터페이스는 대부분의 컴퓨터 사용자에게 잘 알려진 몇 가지 기본 개념을 사용합니다. 사용자는 이러한 친숙한 인터페이스를 사용하여 손쉽게 작업을 수행할 수 있습니다. 운영 체제는 대개 특정 기능에 액세스하기 위한 드롭다운 메뉴와 특정 상황에 맞는 기능에 액세스하기 위한 상황에 맞는 메뉴를 사용하여 검색 가능한 항목을 그래픽 방식으로 표시합니다.

그러나 Windows PowerShell과 같은 CLI(명령줄 인터페이스)는 메뉴나 그래픽 시스템을 사용하지 않으므로 이와 다른 방식으로 정보를 표시해야 합니다. 명령을 사용하려면 먼저 명령 이름을 알아야 합니다. GUI 환경의 기능에 해당하는 복잡한 명령을 입력할 수 있더라도 일반적으로 사용되는 명령과 명령 매개 변수에 대해 잘 알고 있어야 합니다.

대부분의 CLI에는 인터페이스를 쉽게 익힐 수 있는 일정한 패턴이 없습니다. CLI는 최초 운영 체제 셸이기 때문에 많은 명령 이름과 매개 변수 이름이 임의로 선택되었습니다. 대개 이러한 이름은 정확성보다는 간결성을 고려하여 만들어졌습니다. 도움말 시스템 및 명령 설계 표준은 대부분의 CLI에 통합되어 있지만 대개 최초 명령과의 호환성을 고려해 설계되었으므로 명령 집합의 모양이 계속 이전에 결정된 모양을 따릅니다.

Windows PowerShell은 사용자가 CLI에 대해 오랫동안 쌓은 지식을 활용하도록 설계되었습니다. 이 장에서는 Windows PowerShell을 빠르게 익히는 데 사용할 수 있는 몇 가지 기본 도구와 개념에 대해 설명합니다. 해당 기능은 아래와 같습니다.

- Get-Command 사용

- Cmd.exe 및 UNIX 명령 사용

- 외부 명령 사용

- 탭 완성 기능 사용

- Get-Help 사용

