---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.topic: conceptual
title: 알려진 문제 및 제한 사항 기록에 대한 예제 템플릿
ms.openlocfilehash: 453d4e40b906ebcab7314f04e138ded271338846
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/17/2018
ms.locfileid: "34221938"
---
><span data-ttu-id="ad964-103">참고: 제안된 설명이 포함된 제목과 간단한 설명을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="ad964-103">Note: provide a proposed descriptive title and a brief description</span></span>

## <a name="example-erroneous-executionpolicy-errors"></a><span data-ttu-id="ad964-104">예: 잘못된 ExecutionPolicy 오류</span><span class="sxs-lookup"><span data-stu-id="ad964-104">Example: Erroneous ExecutionPolicy errors</span></span> ##
<span data-ttu-id="ad964-105">Windows 7에서 PowerShell 모듈 및 DSC 리소스를 사용하면 ExecutionPolicy에 대해 오류가 보고될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ad964-105">On Windows 7, the use of PowerShell modules and DSC resources may result in errors reported about ExecutionPolicy.</span></span>

### <a name="resolution"></a><span data-ttu-id="ad964-106">해결 방법</span><span class="sxs-lookup"><span data-stu-id="ad964-106">Resolution</span></span>

<span data-ttu-id="ad964-107">해결하려면 다음 명령을 관리자 권한 PowerShell 세션에서 실행(관리자 권한으로 실행)하여 **ExecutionPolicy**를 **RemoteSigned**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="ad964-107">To resolve, set the **ExecutionPolicy** to **RemoteSigned** by running the following command in an elevated PowerShell session (Run as Administrator):</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```
