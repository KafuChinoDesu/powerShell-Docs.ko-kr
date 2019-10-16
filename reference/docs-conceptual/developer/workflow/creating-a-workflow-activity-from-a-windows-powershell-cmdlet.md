---
title: Windows PowerShell Cmdlet에서 워크플로 작업 만들기 | Microsoft Docs
ms.custom: ''
ms.date: 09/12/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 4174e84f-d516-4aca-b418-273047dcfb07
caps.latest.revision: 7
ms.openlocfilehash: 5761ed2168a46d6ed9a2e50554d459f5b93223ee
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359662"
---
# <a name="creating-a-workflow-activity-from-a-windows-powershell-cmdlet"></a><span data-ttu-id="34f9c-102">Windows PowerShell Cmdlet에서 워크플로 활동 만들기</span><span class="sxs-lookup"><span data-stu-id="34f9c-102">Creating a Workflow Activity from a Windows PowerShell Cmdlet</span></span>

<span data-ttu-id="34f9c-103">모든 Windows PowerShell 모듈 또는 cmdlet을 워크플로 작업으로 패키지할 수 [있습니다 .이 클래스의](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator) 메서드를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="34f9c-103">Any Windows PowerShell module or cmdlet can be packaged as a Workflow activity by using the methods of the [Microsoft.Powershell.Activities.Activitygenerator](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator) class.</span></span> <span data-ttu-id="34f9c-104">Microsoft. m a. a. a. a y. a g [Frommoduleinfo \*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromModuleInfo), [microsoft](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromCommandInfo) [powershell. ](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromName)활동을 나타내는 코드를 생성 C# 하는 [데 해당 하](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator) 는 Microsoft. Powershell. Activitygenerator. generatefromname \* 메서드.</span><span class="sxs-lookup"><span data-stu-id="34f9c-104">Use the [Microsoft.Powershell.Activities.Activitygenerator.Generatefrommoduleinfo\*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromModuleInfo), [Microsoft.Powershell.Activities.Activitygenerator.Generatefromcommandinfo\*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromCommandInfo), and [Microsoft.Powershell.Activities.Activitygenerator.Generatefromname\*](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator.GenerateFromName) methods of the [Microsoft.Powershell.Activities.Activitygenerator](/dotnet/api/Microsoft.PowerShell.Activities.ActivityGenerator) class to generate C# code that represents an activity.</span></span> <span data-ttu-id="34f9c-105">그런 다음 결과 C# 코드를 프로젝트에 활동으로 추가할 수 있는 어셈블리로 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f9c-105">You can then compile the resulting C# code into an assembly that can be added to a project as an activity.</span></span>

<span data-ttu-id="34f9c-106">그러면 결과 C# 코드를 다음 형식의 명령줄을 사용 하 여 프로젝트에 작업으로 추가할 수 있는 어셈블리로 컴파일할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="34f9c-106">You can then compile the resulting C# code into an assembly that can be added to a project as an activity by using a command line with the following form.</span></span>

<span data-ttu-id="34f9c-107">**csc/nologo/out: AssemblyName/target: library/reference: codefile.cs/reference: Microsoft. 작업**</span><span class="sxs-lookup"><span data-stu-id="34f9c-107">**csc /nologo /out:AssemblyName /target:library /reference:System.Activities.Activity /reference:Microsoft.PowerShell.Activities codefile.cs**</span></span>

## <a name="example"></a><span data-ttu-id="34f9c-108">예제</span><span class="sxs-lookup"><span data-stu-id="34f9c-108">Example</span></span>

<span data-ttu-id="34f9c-109">다음 예제에서는 Windows PowerShell 모듈에서 C# 활동에 대 한 코드를 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34f9c-109">The following example demonstrates how to generate C# code for an activity from a Windows PowerShell module.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using System.Management.Automation;
using System.Collections.ObjectModel;
using Microsoft.PowerShell.Activities;

namespace MakeActivity
{
    class Program
    {
        static void Main(string[] args)

        {
            StreamWriter CodeFile = new StreamWriter("c:\\\\testmodule\\codefile.cs");
            Collection<PSModuleInfo> ModuleInfos = new Collection<PSModuleInfo> { };
            PSModuleInfo ModuleInfo;
            string ActivityCode = "";
            string ModulePath = "";
            Console.Write("Type the full path and filename of the module to process:");
            ModulePath = Console.ReadLine();

            PowerShell ps = PowerShell.Create();

            ps.AddCommand("Import-Module").AddArgument(ModulePath);
            ps.AddParameter("PassThru");
            ModuleInfos = ps.Invoke<PSModuleInfo>();

            ModuleInfo = (PSModuleInfo)ModuleInfos[0];

            ActivityCode = ActivityGenerator.GenerateFromModuleInfo(ModuleInfo, "MyNamespace").First<String>();

           CodeFile.Write(ActivityCode);
            Console.ReadLine();

        }
    }
}

```

## <a name="example"></a><span data-ttu-id="34f9c-110">예제</span><span class="sxs-lookup"><span data-stu-id="34f9c-110">Example</span></span>

<span data-ttu-id="34f9c-111">다음 예제에서는 Windows PowerShell cmdlet에서 C# 작업에 대 한 코드를 생성 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="34f9c-111">The following example demonstrates how to generate C# code for an activity from a Windows PowerShell cmdlet.</span></span>

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;
using System.Management.Automation;
using System.Collections.ObjectModel;
using Microsoft.PowerShell.Activities;

namespace MakeActivity
{
    class Program
    {
        static void Main(string[] args)

        {
            StreamWriter CodeFile = new StreamWriter("c:\\\\testmodule\\codefile.cs");
            Collection<PSModuleInfo> ModuleInfos = new Collection<PSModuleInfo> { };
            PSModuleInfo ModuleInfo;
            Collection<CommandInfo> CommandInfos = new Collection<CommandInfo> { };
            CommandInfo MyCommand;
            string ActivityCode = "";
            string ModulePath = "";
            Console.Write("Type the full path and filename of the module to process:");
            ModulePath = Console.ReadLine();

            PowerShell ps = PowerShell.Create();

            ps.AddCommand("Import-Module").AddArgument(ModulePath);
            ps.AddParameter("PassThru");
            ModuleInfos = ps.Invoke<PSModuleInfo>();

            ModuleInfo = (PSModuleInfo)ModuleInfos[0];

            ps.AddCommand("Get-Command").AddArgument(ModuleInfo);
            CommandInfos = ps.Invoke<CommandInfo>();

            MyCommand = CommandInfos[0];

            ActivityCode = ActivityGenerator.GenerateFromCommandInfo(MyCommand, "MyNamespace");

           CodeFile.Write(ActivityCode);
            Console.ReadLine();

        }
    }
}

```