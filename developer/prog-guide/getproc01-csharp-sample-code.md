---
title: GetProc01 (C#) 코드 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 65094bb7-1972-44b3-b8b0-5f639860b58c
caps.latest.revision: 5
ms.openlocfilehash: 56ce7080e24cc12de6d43ac607ffd5d3f0a3b17c
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56856889"
---
# <a name="getproc01-c-sample-code"></a><span data-ttu-id="de03c-102">GetProc01(C#) 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="de03c-102">GetProc01 (C#) Sample Code</span></span>

<span data-ttu-id="de03c-103">다음 코드는 GetProc01 샘플 cmdlet의 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="de03c-103">The following code shows the implementation of the GetProc01 sample cmdlet.</span></span> <span data-ttu-id="de03c-104">Cmdlet에 검색 프로세스의 실제 작업을 두어 간단를 확인 합니다 [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) 메서드.</span><span class="sxs-lookup"><span data-stu-id="de03c-104">Notice that the cmdlet is simplified by leaving the actual work of process retrieval to the [System.Diagnostics.Process.Getprocesses\*](/dotnet/api/System.Diagnostics.Process.GetProcesses) method.</span></span>

> [!NOTE]
> <span data-ttu-id="de03c-105">다운로드할 수 있습니다는 C# Microsoft Windows 소프트웨어 개발 키트에 대 한 Windows Vista 및.NET Framework 3.0 런타임 구성 요소를 사용 하 여이 Get-proc cmdlet에 대 한 소스 파일 (getproc01.cs).</span><span class="sxs-lookup"><span data-stu-id="de03c-105">You can download the C# source file (getproc01.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="de03c-106">다운로드 지침에 대해서 [Windows PowerShell 설치 및 Windows PowerShell SDK를 다운로드 하는 방법을](/powershell/developer/installing-the-windows-powershell-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="de03c-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
> <span data-ttu-id="de03c-107">다운로드할 수 있습니다는 C# Microsoft Windows 소프트웨어 개발 키트에 대 한 Windows Vista 및.NET Framework 3.0 런타임 구성 요소를 사용 하 여이 Get-proc cmdlet에 대 한 소스 파일 (getproc01.cs).</span><span class="sxs-lookup"><span data-stu-id="de03c-107">You can download the C# source file (getproc01.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="de03c-108">다운로드 지침에 대해서 [Windows PowerShell 설치 및 Windows PowerShell SDK를 다운로드 하는 방법을](/powershell/developer/installing-the-windows-powershell-sdk)합니다.</span><span class="sxs-lookup"><span data-stu-id="de03c-108">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="de03c-109">다운로드 한 소스 파일에서 사용할 수는  **\<PowerShell 샘플 >** 디렉터리입니다.</span><span class="sxs-lookup"><span data-stu-id="de03c-109">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="de03c-110">코드 예제</span><span class="sxs-lookup"><span data-stu-id="de03c-110">Code Sample</span></span>

[!code-csharp[GetProcessSample01.cs](../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample01/GetProcessSample01.cs#L11-L126 "GetProcessSample01.cs")]

## <a name="see-also"></a><span data-ttu-id="de03c-111">참고 항목</span><span class="sxs-lookup"><span data-stu-id="de03c-111">See Also</span></span>

[<span data-ttu-id="de03c-112">Windows PowerShell 프로그래머 가이드</span><span class="sxs-lookup"><span data-stu-id="de03c-112">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="de03c-113">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="de03c-113">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)