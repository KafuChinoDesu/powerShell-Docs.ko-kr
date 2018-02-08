---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: gallery,powershell,cmdlet,psgallery
title: psgallery_items_tab
ms.openlocfilehash: 8704091542de5c19817ab0b4f77fd98987084b5d
ms.sourcegitcommit: 1a0a0928c1e3cae4e8df8d79b0737bd7ed6b4e47
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="items-tab"></a>항목 탭

[항목 탭](https://www.powershellgallery.com/items)에는 PowerShell 갤러리에서 사용 가능한 모든 항목이 표시됩니다.

항목을 필터링, 정렬 및 검색하는 방법에는 여러 가지가 있습니다.
특정 항목에 대한 자세한 정보를 보려면 해당 항목을 클릭합니다.

## <a name="filter-by"></a>필터 기준

“필터 기준” 아래의 드롭다운에서는 다음을 기준으로 결과를 필터링할 수 있습니다.
* 시험판 포함
* 안정적인 항목만

“시험판” 및 “안정적인 항목”에 대한 내용은 PowerShell 팀 블로그의 [Prerelease Versioning Added to PowerShellGet and PowerShell Gallery](https://blogs.msdn.microsoft.com/powershell/2017/12/05/prerelease-versioning-added-to-powershellget-and-powershell-gallery/)(PowerShellGet 및 PowerShell 갤러리에 추가된 시험판 버전)를 참조하세요.

드롭다운의 확인란을 사용하여 다음을 기준으로 결과를 필터링할 수 있습니다.
* 항목 종류
  - 모듈
  - 스크립트
* 범주
  - Cmdlet
  - DSC 리소스
  - 기능
  - 역할 기능
  - Workflow

PowerShell 갤러리의 모듈만 보려면 [항목 종류]에서 [모듈]을 선택합니다.
마찬가지로 PowerShell 갤러리에서 스크립트만 보려면 [항목 종류]에서 [스크립트]를 선택합니다.

> [!NOTE]
> 필터가 포함됩니다.
> 예: cmdlet과 함수를 둘 다 포함하는 항목은 [Cmdlet] 또는 [함수] \(또는 둘 다)를 선택한 경우에 표시됩니다.
> 둘 다 선택하지 않으면 항목이 표시되지 않습니다.
> 마찬가지로, 모든 범주를 선택하면 이러한 범주 중 하나를 포함하는 항목만 표시됩니다.
> **이러한 범주에 속하지 않는 항목은 표시되지 않습니다.**

## <a name="sort-by"></a>정렬 기준

[정렬 기준] 드롭다운에서 다음을 기준으로 결과를 정렬할 수 있습니다.
* 인기도 - 인기도는 다운로드 횟수에 따라 결정됩니다.
* A-Z - 항목 이름을 기준으로 사전순으로 정렬됩니다.
* 최근 - 게시 날짜순으로 항목이 표시됩니다.

## <a name="search-box"></a>검색 상자

검색 상자에서 키워드로 항목을 검색할 수 있습니다.
자세한 내용은 [갤러리 검색 구문](psgallery_search_syntax.md)을 참조하세요.
