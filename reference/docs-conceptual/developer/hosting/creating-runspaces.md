---
title: Runspace 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 17f323c3-e873-449e-8a28-477f1c6b5e12
caps.latest.revision: 6
ms.openlocfilehash: b4e61600f68521e4e7ab56ceae3349381e88a70a
ms.sourcegitcommit: debd2b38fb8070a7357bf1a4bf9cc736f3702f31
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2019
ms.locfileid: "72367582"
---
# <a name="creating-runspaces"></a>runspace 만들기

Runspace는 호스트 응용 프로그램에서 호출 하는 명령에 대 한 운영 환경입니다. 이 환경에는 현재 존재 하는 명령 및 데이터와 현재 적용 되는 모든 언어 제한이 포함 됩니다.

 호스트 응용 프로그램은 사용 가능한 모든 핵심 명령을 포함 하는 Windows PowerShell에서 제공 하는 기본 runspace를 사용 하거나 사용 가능한 명령의 하위 집합만 포함 하는 사용자 지정 runspace를 만들 수 있습니다. 사용자 지정 runspace를 만들려면 [runspace](/dotnet/api/System.Management.Automation.Runspaces.InitialSessionState) 개체를 만들고이 개체를 runspace에 할당 합니다.

## <a name="runspace-tasks"></a>Runspace 작업

1. [InitialSessionState 만들기](./creating-an-initialsessionstate.md)

2. [제한 된 runspace 만들기](./creating-a-constrained-runspace.md)

3. [여러 runspace 만들기](./creating-multiple-runspaces.md)

## <a name="see-also"></a>참고 항목
