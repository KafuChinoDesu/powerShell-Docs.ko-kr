---
title: 입력 처리 메서드를 재정의 하는 방법 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 1a1ad921-5816-4937-acf1-ed4760fae740
caps.latest.revision: 8
ms.openlocfilehash: cfee55576518cf9ce38501192872ce94054f5213
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364472"
---
# <a name="how-to-override-input-processing-methods"></a><span data-ttu-id="cd3e9-102">입력 처리 메서드를 재정의하는 방법</span><span class="sxs-lookup"><span data-stu-id="cd3e9-102">How to Override Input Processing Methods</span></span>

<span data-ttu-id="cd3e9-103">다음 예에서는 cmdlet 내에서 입력 처리 메서드를 덮어쓰는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-103">These examples show how to overwrite the input processing methods within a cmdlet.</span></span> <span data-ttu-id="cd3e9-104">이러한 메서드는 다음 작업을 수행 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-104">These methods are used to perform the following operations:</span></span>

- <span data-ttu-id="cd3e9-105">Cmdlet에서 처리 하는 모든 개체에 유효한 일회성 시작 작업을 수행 하는 데에는 [system.object](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-105">The [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method is used to perform one-time startup operations that are valid for all the objects processed by the cmdlet.</span></span> <span data-ttu-id="cd3e9-106">Windows PowerShell 런타임은이 메서드를 한 번만 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-106">The Windows PowerShell runtime calls this method only once.</span></span>

- <span data-ttu-id="cd3e9-107">[ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) 메서드는 Cmdlet에 전달 된 개체를 처리 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-107">The [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method is used to process the objects passed to the cmdlet.</span></span> <span data-ttu-id="cd3e9-108">Windows PowerShell 런타임은 cmdlet에 전달 된 각 개체에 대해이 메서드를 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-108">The Windows PowerShell runtime calls this method for each object passed to the cmdlet.</span></span>

- <span data-ttu-id="cd3e9-109">일회성 사후 처리 작업을 수행 하는 데에는 [system.object](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) 를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-109">The [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method is used to perform one-time post processing operations.</span></span> <span data-ttu-id="cd3e9-110">Windows PowerShell 런타임은이 메서드를 한 번만 호출 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-110">The Windows PowerShell runtime calls this method only once.</span></span>

## <a name="to-override-the-beginprocessing-method"></a><span data-ttu-id="cd3e9-111">BeginProcessing 메서드를 재정의 하려면</span><span class="sxs-lookup"><span data-stu-id="cd3e9-111">To override the BeginProcessing method</span></span>

- <span data-ttu-id="cd3e9-112">보호 된 재정의를 [system.object](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) 의 재정의 메서드로 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-112">Declare a protected override of the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method.</span></span>

<span data-ttu-id="cd3e9-113">다음 클래스는 샘플 메시지를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-113">The following class prints a sample message.</span></span> <span data-ttu-id="cd3e9-114">이 클래스를 사용 하려면 Cmdlet 특성에서 동사 및 명사를 변경 하 고, 새 동사 및 명사를 반영 하도록 클래스의 이름을 변경한 다음, 필요한 기능을 System.object의 재정의에 추가 합니다 [.](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) 방법이.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-114">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.BeginProcessing](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "BeginProcessingClass")]
public class TestBeginProcessingClassTemplate : Cmdlet
{
  // Override the BeginProcessing method to add preprocessing
  //operations to the cmdlet.
  protected override void BeginProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the BeginProcessing template.");
  }
}
```

## <a name="to-override-the-processrecord-method"></a><span data-ttu-id="cd3e9-115">ProcessRecord 메서드를 재정의 하려면</span><span class="sxs-lookup"><span data-stu-id="cd3e9-115">To override the ProcessRecord method</span></span>

- <span data-ttu-id="cd3e9-116">[ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) 메서드의 보호 된 재정의를 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-116">Declare a protected override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

<span data-ttu-id="cd3e9-117">다음 클래스는 샘플 메시지를 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-117">The following class prints a sample message.</span></span> <span data-ttu-id="cd3e9-118">이 클래스를 사용 하려면 Cmdlet 특성에서 동사 및 명사를 변경 하 고, 새 동사 및 명사를 반영 하도록 클래스의 이름을 변경한 다음, 필요한 기능을 [ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) 메서드의 재정의에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-118">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "ProcessRecordClass")]
public class TestProcessRecordClassTemplate : Cmdlet
{
    // Override the ProcessRecord method to add processing
    //operations to the cmdlet.
    protected override void ProcessRecord()
    {
        // Replace the WriteObject method with the logic required
        // by your cmdlet. It is used here to generate the following
        // output:
        // "This is a test of the ProcessRecord template."
        WriteObject("This is a test of the ProcessRecord template.");
    }
}

```

## <a name="to-override-the-endprocessing-method"></a><span data-ttu-id="cd3e9-119">EndProcessing 메서드를 재정의 하려면</span><span class="sxs-lookup"><span data-stu-id="cd3e9-119">To override the EndProcessing method</span></span>

- <span data-ttu-id="cd3e9-120">보호 된 재정의를 [system.object](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) 로 선언 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-120">Declare a protected override of the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span>

<span data-ttu-id="cd3e9-121">다음 클래스는 샘플을 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-121">The following class prints a sample.</span></span> <span data-ttu-id="cd3e9-122">이 클래스를 사용 하려면 Cmdlet 특성에서 동사 및 명사를 변경 하 고, 새 동사 및 명사를 반영 하도록 클래스의 이름을 변경한 다음, 필요한 기능을 [system.object](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) 의 재정의에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-122">To use this class, change the verb and noun in the Cmdlet attribute, change the name of the class to reflect the new verb and noun, and then add the functionality you require to the override of the [System.Management.Automation.Cmdlet.EndProcessing](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing) method.</span></span>

```csharp
[Cmdlet(VerbsDiagnostic.Test, "EndProcessingClass")]
public class TestEndProcessingClassTemplate : Cmdlet
{
  // Override the EndProcessing method to add postprocessing
  //operations to the cmdlet.
  protected override void EndProcessing()
  {
    // Replace the WriteObject method with the logic required
    // by your cmdlet. It is used here to generate the following
    // output:
    // "This is a test of the BeginProcessing template."
    WriteObject("This is a test of the EndProcessing template.");
  }
}
```

## <a name="see-also"></a><span data-ttu-id="cd3e9-123">참고 항목</span><span class="sxs-lookup"><span data-stu-id="cd3e9-123">See Also</span></span>

[<span data-ttu-id="cd3e9-124">System.object를 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-124">System.Management.Automation.Cmdlet.BeginProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.BeginProcessing)

[<span data-ttu-id="cd3e9-125">System.object..</span><span class="sxs-lookup"><span data-stu-id="cd3e9-125">System.Management.Automation.Cmdlet.EndProcessing</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.EndProcessing)

[<span data-ttu-id="cd3e9-126">ProcessRecord입니다.</span><span class="sxs-lookup"><span data-stu-id="cd3e9-126">System.Management.Automation.Cmdlet.ProcessRecord</span></span>](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)

<span data-ttu-id="cd3e9-127">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)(Windows PowerShell Cmdlet 작성)</span><span class="sxs-lookup"><span data-stu-id="cd3e9-127">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>