---
title: GetProc03 (C#) 샘플 코드 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: ebc0d538-69ac-43d5-837d-b6f47344fc6a
caps.latest.revision: 5
ms.openlocfilehash: 10c41ffd03e9adae82813bfe79d3e15030087953
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72360342"
---
# <a name="getproc03-c-sample-code"></a><span data-ttu-id="66071-102">GetProc03(C#) 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="66071-102">GetProc03 (C#) Sample Code</span></span>

<span data-ttu-id="66071-103">다음 코드는 파이프라인 입력을 수락할 수 있는 `Get-Process` cmdlet의 구현을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="66071-103">The following code shows the implementation of a `Get-Process` cmdlet that can accept pipelined input.</span></span> <span data-ttu-id="66071-104">이 구현은 파이프라인 입력을 허용 하 고, 제공 된 이름에 따라 로컬 컴퓨터에서 프로세스 정보를 검색 하 고, [WriteObject (system.string, system.string)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) 메서드를 출력으로 사용 하는 `Name` 매개 변수를 정의 합니다. 파이프라인에 개체를 보내기 위한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="66071-104">This implementation defines a `Name` parameter that accepts pipeline input, retrieves process information from the local computer based on the supplied names, and then uses the [WriteObject(System.Object,System.Boolean)](/dotnet/api/system.management.automation.cmdlet.writeobject?view=pscore-6.2.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) method as the output mechanism for sending objects to the pipeline.</span></span>

> [!NOTE]
> <span data-ttu-id="66071-105">Windows Vista 용 Microsoft C# Windows 소프트웨어 개발 키트 및 .NET Framework 3.0 런타임 구성 요소를 사용 하 여이 getprov03.cs cmdlet에 대 한 원본 파일 ()을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66071-105">You can download the C# source file (getprov03.cs) for this Get-Proc cmdlet using the Microsoft Windows Software Development Kit for Windows Vista and .NET Framework 3.0 Runtime Components.</span></span> <span data-ttu-id="66071-106">다운로드 지침은 [Windows powershell을 설치 하 고 Windows POWERSHELL SDK를 다운로드 하는 방법](/powershell/developer/installing-the-windows-powershell-sdk)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="66071-106">For download instructions, see [How to Install Windows PowerShell and Download the Windows PowerShell SDK](/powershell/developer/installing-the-windows-powershell-sdk).</span></span>
>
> <span data-ttu-id="66071-107">다운로드 된 원본 파일은 **\<PowerShell 샘플 >** 디렉터리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66071-107">The downloaded source files are available in the **\<PowerShell Samples>** directory.</span></span>

## <a name="code-sample"></a><span data-ttu-id="66071-108">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="66071-108">Code Sample</span></span>

[!code-csharp[GetProcessSample03.cs](../../../../powershell-sdk-samples/SDK-2.0/csharp/GetProcessSample03/GetProcessSample03.cs#L11-L78 "GetProcessSample03.cs")]

## <a name="see-also"></a><span data-ttu-id="66071-109">참고 항목</span><span class="sxs-lookup"><span data-stu-id="66071-109">See Also</span></span>

[<span data-ttu-id="66071-110">Windows PowerShell 프로그래머 가이드</span><span class="sxs-lookup"><span data-stu-id="66071-110">Windows PowerShell Programmer's Guide</span></span>](./windows-powershell-programmer-s-guide.md)

[<span data-ttu-id="66071-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="66071-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)