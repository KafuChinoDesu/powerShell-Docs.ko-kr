---
title: Runspace01 샘플 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 42c1c59c-6da5-4cda-9562-e8059177fee1
caps.latest.revision: 11
ms.openlocfilehash: c33044fde4456513b5b07b998cc8db389b318e8e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56855719"
---
# <a name="runspace01-sample"></a><span data-ttu-id="07c97-102">Runspace01 샘플</span><span class="sxs-lookup"><span data-stu-id="07c97-102">Runspace01 Sample</span></span>

<span data-ttu-id="07c97-103">이 샘플에 사용 하는 방법을 보여 줍니다 합니다 [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) 실행 하는 클래스는 [Get-process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet 동기적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-103">This sample shows how to use the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) class to run the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet synchronously.</span></span> <span data-ttu-id="07c97-104">합니다 [Get-process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) 반환 [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) 로컬 컴퓨터에서 실행 중인 각 프로세스에 대 한 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-104">The [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet returns [System.Diagnostics.Process](/dotnet/api/System.Diagnostics.Process) objects for each process running on the local computer.</span></span> <span data-ttu-id="07c97-105">값을 [System.Diagnostics.Process.Processname\*](/dotnet/api/System.Diagnostics.Process.ProcessName) 하 고 [System.Diagnostics.Process.Handlecount\*](/dotnet/api/System.Diagnostics.Process.Handlecount) 속성 다음 반환된 된 개체에서 추출 되 고 콘솔에 표시 창입니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-105">The values of the [System.Diagnostics.Process.Processname\*](/dotnet/api/System.Diagnostics.Process.ProcessName) and [System.Diagnostics.Process.Handlecount\*](/dotnet/api/System.Diagnostics.Process.Handlecount) properties are then extracted from the returned objects and displayed in a console window.</span></span>

## <a name="requirements"></a><span data-ttu-id="07c97-106">요구 사항</span><span class="sxs-lookup"><span data-stu-id="07c97-106">Requirements</span></span>

 <span data-ttu-id="07c97-107">이 샘플 Windows PowerShell 2.0이 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-107">This sample requires Windows PowerShell 2.0.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="07c97-108">시연</span><span class="sxs-lookup"><span data-stu-id="07c97-108">Demonstrates</span></span>

- <span data-ttu-id="07c97-109">만들기는 [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) 명령을 실행 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-109">Creating a [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object to run a command.</span></span>

- <span data-ttu-id="07c97-110">파이프라인에 명령을 추가 합니다 [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-110">Adding a command to the pipeline of the [System.Management.Automation.Powershell](/dotnet/api/system.management.automation.powershell) object.</span></span>

- <span data-ttu-id="07c97-111">동기적으로 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-111">Running the command synchronously.</span></span>

- <span data-ttu-id="07c97-112">사용 하 여 [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) 명령에 의해 반환 된 개체에서 속성을 추출 하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-112">Using [System.Management.Automation.Psobject](/dotnet/api/System.Management.Automation.PSObject) objects to extract properties from the objects returned by the command.</span></span>

## <a name="example"></a><span data-ttu-id="07c97-113">예제</span><span class="sxs-lookup"><span data-stu-id="07c97-113">Example</span></span>

 <span data-ttu-id="07c97-114">이 샘플을 실행 합니다 [Get-process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet Windows PowerShell에서 제공 하는 기본 runspace에 동기적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="07c97-114">This sample runs the [Get-Process](/powershell/module/Microsoft.PowerShell.Management/Get-Process) cmdlet synchronously in the default runspace provided by Windows PowerShell.</span></span>

```csharp
namespace Microsoft.Samples.PowerShell.Runspaces
{
  using System;
  using System.Management.Automation;
  using PowerShell = System.Management.Automation.PowerShell;

  /// <summary>
  /// This class contains the Main entry point for this host application.
  /// </summary>
  internal class Runspace01
  {
    /// <summary>
    /// This sample uses the PowerShell class to execute
    /// the get-process cmdlet synchronously. The name and
    /// handlecount are then extracted from the PSObjects
    /// returned and displayed.
    /// </summary>
    /// <param name="args">Parameter not used.</param>
    /// <remarks>
    /// This sample demonstrates the following:
    /// 1. Creating a PowerShell object to run a command.
    /// 2. Adding a command to the pipeline of the PowerShell object.
    /// 3. Running the command synchronously.
    /// 4. Using PSObject objects to extract properties from the objects
    ///    returned by the command.
    /// </remarks>
    private static void Main(string[] args)
    {
      // Create a PowerShell object. Creating this object takes care of
      // building all of the other data structures needed to run the command.
      using (PowerShell powershell = PowerShell.Create().AddCommand("get-process"))
      {
        Console.WriteLine("Process              HandleCount");
        Console.WriteLine("--------------------------------");

        // Invoke the command synchronously and display the
        // ProcessName and HandleCount properties of the
        // objects that are returned.
        foreach (PSObject result in powershell.Invoke())
        {
          Console.WriteLine(
                      "{0,-20} {1}",
                      result.Members["ProcessName"].Value,
                      result.Members["HandleCount"].Value);
        }
      }

      System.Console.WriteLine("Hit any key to exit...");
      System.Console.ReadKey();
    }
  }
}
```

## <a name="see-also"></a><span data-ttu-id="07c97-115">참고 항목</span><span class="sxs-lookup"><span data-stu-id="07c97-115">See Also</span></span>