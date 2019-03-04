---
title: Runspace01 (VB.NET) 코드 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 12ee5382-95ba-41c7-8291-7f69a6f63514
caps.latest.revision: 7
ms.openlocfilehash: fbc90a6736d841fe184b86ab143809ad23c7977a
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56856059"
---
# <a name="runspace01-vbnet-code-sample"></a><span data-ttu-id="e2519-102">Runspace01(VB.NET) 코드 샘플</span><span class="sxs-lookup"><span data-stu-id="e2519-102">Runspace01 (VB.NET) Code Sample</span></span>

<span data-ttu-id="e2519-103">에 설명 된 runspace에 대 한 코드 예제는 다음과 같습니다 [콘솔 응용 프로그램을 실행 지정 명령 만들기](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2519-103">Here are the code samples for the runspace described in [Creating a Console Application That Runs a Specified Command](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).</span></span> <span data-ttu-id="e2519-104">이렇게 하려면 응용 프로그램 runspace를 호출 하 고 명령을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2519-104">To do this, the application invokes a runspace, and then invokes a command.</span></span> <span data-ttu-id="e2519-105">(이 응용 프로그램에서 runspace 구성 정보를 지정 하지도 않습니다이 명시적으로 파이프라인 만들기는 note). 호출 되는 명령입니다는 `Get-Process` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2519-105">(Note that this application does not specify runspace configuration information, nor does it explicitly create a pipeline.) The command that is invoked is the `Get-Process` cmdlet.</span></span>
<span data-ttu-id="e2519-106">에 설명 된 runspace에 대 한 코드 예제는 다음과 같습니다 [콘솔 응용 프로그램을 실행 지정 명령 만들기](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e)합니다.</span><span class="sxs-lookup"><span data-stu-id="e2519-106">Here are the code samples for the runspace described in [Creating a Console Application That Runs a Specified Command](http://msdn.microsoft.com/en-us/793a6570-a072-4799-840b-172f28ce620e).</span></span> <span data-ttu-id="e2519-107">이렇게 하려면 응용 프로그램 runspace를 호출 하 고 명령을 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="e2519-107">To do this, the application invokes a runspace, and then invokes a command.</span></span> <span data-ttu-id="e2519-108">(이 응용 프로그램에서 runspace 구성 정보를 지정 하지도 않습니다이 명시적으로 파이프라인 만들기는 note). 호출 되는 명령입니다는 `Get-Process` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2519-108">(Note that this application does not specify runspace configuration information, nor does it explicitly create a pipeline.) The command that is invoked is the `Get-Process` cmdlet.</span></span>

## <a name="code-sample"></a><span data-ttu-id="e2519-109">코드 예제</span><span class="sxs-lookup"><span data-stu-id="e2519-109">Code Sample</span></span>

```vb
Imports System
Imports System.Collections.Generic
Imports System.Text
Imports System.Management.Automation
Imports System.Management.Automation.Host
Imports System.Management.Automation.Runspaces

Namespace Microsoft.Samples.PowerShell.Runspaces

    Module Runspace01
        ' <summary>
        ' This sample uses the RunspaceInvoke class to execute
        ' the get-process cmdlet synchronously. The name and
        ' handlecount are then extracted from  the PSObjects
        ' returned and displayed.
        ' </summary>
        ' <param name="args">Unused</param>
        ' <remarks>
        ' This sample demonstrates the following:
        ' 1. Creating an instance of the RunspaceInvoke class.
        ' 2. Using this instance to invoke a PowerShell command.
        ' 3. Using PSObject to extract properties from the objects
        '    returned by this command.
        ' </remarks>
        Sub Main()
            ' Create an instance of the RunspaceInvoke class.
            ' This takes care of all building all of the other
            ' data structures needed...
            Dim invoker As RunspaceInvoke = New RunspaceInvoke()

            Console.WriteLine("Process              HandleCount")
            Console.WriteLine("--------------------------------")

            ' Now invoke the runspace and display the objects that are
            ' returned...
            For Each result As PSObject In invoker.Invoke("get-process")
                Console.WriteLine("{0,-20} {1}", _
                    result.Members("ProcessName").Value, _
                    result.Members("HandleCount").Value)
            Next
            System.Console.WriteLine("Hit any key to exit...")
            System.Console.ReadKey()
        End Sub
    End Module
End Namespace
```

<!-- TODO!!!: [!code-csharp[Runspace01.vb](../../powershell-sdk-samples/SDK-2.0/vb/Runspace01/Runspace01.vb#L09-L53 "Runspace01.vb")] -->

## <a name="see-also"></a><span data-ttu-id="e2519-110">참고 항목</span><span class="sxs-lookup"><span data-stu-id="e2519-110">See Also</span></span>

[<span data-ttu-id="e2519-111">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="e2519-111">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)