---
title: "Windows PowerShell ISE 스크립팅 개체 모델의 용도"
ms.date: 2016-05-11
keywords: powershell,cmdlet
description: 
ms.topic: article
author: jpjofre
manager: dongill
ms.prod: powershell
ms.assetid: d176a131-ab0c-43ee-80c1-f824ab8e4a05
translationtype: Human Translation
ms.sourcegitcommit: 3222a0ba54e87b214c5ebf64e587f920d531956a
ms.openlocfilehash: 16bd9de4e5636431a192dc3d49e3310c816b997f

---

# Windows PowerShell ISE 스크립팅 개체 모델의 용도
  개체는 Windows PowerShell ISE(통합 스크립팅 환경)의 형식 및 함수와 연결되어 있습니다. 개체 모델 참조에서는 이러한 개체를 노출하는 멤버 속성 및 메서드에 대한 세부 정보를 제공합니다. 스크립트를 사용하여 이러한 메서드와 속성에 직접 액세스하는 방법을 보여 주기 위해 예제가 제공되었습니다. 스크립팅 개체 모델은 다음 범위의 작업을 보다 쉽게 해줍니다.

## Windows PowerShell ISE의 모양 사용자 지정
 개체 모델을 사용하여 응용 프로그램 설정 및 옵션을 수정할 수 있습니다. 예를 들어, 다음과 같이 수정할 수 있습니다.

-   오류, 경고, 자세한 정보 출력 및 디버그 출력의 색을 변경할 수 있습니다.

-   명령 창, 출력 창 및 스크립트 창의 배경색을 가져오거나 설정할 수 있습니다.

-   출력 창의 전경색을 설정할 수 있습니다.

-   Windows PowerShell ISE의 글꼴 이름 및 글꼴 크기를 설정할 수 있습니다.

-   경고를 구성할 수 있습니다. 이 설정에는 파일이 여러 PowerShell 탭에 열려 있거나, 파일에 있는 스크립트가 파일이 저장되기 전에 실행되는 경우 발생하는 경고가 포함됩니다.

-   스크립트 창과 출력 창이 나란히 있는 보기와 스크립트 창이 출력 창 위에 있는 보기 간에 전환할 수 있습니다. 명령 창을 출력 창의 맨 아래 또는 위에 도킹할 수 있습니다.

## Windows PowerShell ISE의 기능 향상
 개체 모델을 사용하여 Windows PowerShell ISE의 기능을 향상시킬 수 있습니다. 예를 들어, 다음을 수행할 수 있습니다.

-   Windows PowerShell ISE 자체의 인스턴스를 추가 및 수정할 수 있습니다. 예를 들어 메뉴를 변경하려면 새 메뉴 항목을 추가하고 이 새 메뉴 항목을 스크립트에 매핑할 수 있습니다.

-   Windows PowerShell ISE의 메뉴 명령 및 단추를 사용하여 수행할 수 있는 작업 중 일부를 수행하는 스크립트를 만들 수 있습니다. 예를 들어 PowerShell 탭을 추가, 제거 또는 선택할 수 있습니다.

-   메뉴 명령 및 단추를 사용하여 수행할 수 있는 작업을 보완합니다. 예를 들어 PowerShell 탭의 이름을 바꿀 수 있습니다.

-   파일과 한 연결된 명령 창, 출력 창 및 스크립트 창용의 텍스트 버퍼를 조작할 수 있습니다. 예를 들어, 다음을 수행할 수 있습니다.

    -   모든 텍스트를 가져오거나 설정할 수 있습니다.

    -   텍스트 선택 내용을 가져오거나 설정할 수 있습니다.

    -   스크립트를 실행하거나 스크립트에서 선택된 부분을 실행할 수 있습니다.

    -   줄을 스크롤하여 볼 수 있습니다.

    -   캐럿 위치에 텍스트를 삽입할 수 있습니다.

    -   텍스트 블록을 선택할 수 있습니다.

    -   마지막 줄 번호를 가져올 수 있습니다.

-   파일 작업을 수행할 수 있습니다. 예를 들어, 다음을 수행할 수 있습니다.

    -   파일을 열거나, 파일을 저장하거나, 다른 이름을 사용하여 파일을 저장할 수 있습니다.

    -   파일이 마지막으로 저장된 후 변경되었는지 여부를 결정할 수 있습니다.

    -   파일 이름을 가져올 수 있습니다.

    -   파일을 선택할 수 있습니다.

## 작업 자동화
 스크립팅 개체 모델을 사용하여 자주 수행하는 작업에 대한 바로 가기 키를 만들 수 있습니다.

## 참고 항목
 [ISE 개체 모델 계층 구조](The-ISE-Object-Model-Hierarchy.md) 
 [Windows PowerShell ISE 개체 모델 참조](Windows-PowerShell-ISE-Object-Model-Reference.md) 
 [Windows PowerShell ISE 스크립팅 개체 모델](The-Windows-PowerShell-ISE-Scripting-Object-Model.md)

  



<!--HONumber=Aug16_HO4-->


