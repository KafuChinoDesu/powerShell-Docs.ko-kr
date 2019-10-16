---
title: 명령줄 입력을 처리 하는 매개 변수 추가 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- cmdlets [PowerShell Programmer's Guide], parameters
- Get-Proc cmdlet [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], command line input
- command line input [PowerShell Programmer's Guide]
- parameters [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], creating
ms.assetid: da0b32f8-7b51-440e-a061-3177b5759e0e
caps.latest.revision: 9
ms.openlocfilehash: 7db93af33717dc4802ed915793f6cd570cfb48f6
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72364632"
---
# <a name="adding-parameters-that-process-command-line-input"></a><span data-ttu-id="0de76-102">명령줄 입력을 처리하는 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="0de76-102">Adding Parameters That Process Command-Line Input</span></span>

<span data-ttu-id="0de76-103">Cmdlet에 대 한 입력의 한 소스는 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-103">One source of input for a cmdlet is the command line.</span></span> <span data-ttu-id="0de76-104">이 항목에서는 cmdlet이 cmdlet에 전달 된 명시적 개체를 기반으로 하 여 로컬 컴퓨터의 입력을 처리할 수 있도록 **Get Proc** cmdlet에 매개 변수를 추가 하는 방법에 대해 설명 합니다 .이 Cmdlet은 [첫 번째 cmdlet 만들기](./creating-a-cmdlet-without-parameters.md)에 설명 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-104">This topic describes how to add a parameter to the **Get-Proc** cmdlet (which is described in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md)) so that the cmdlet can process input from the local computer based on explicit objects passed to the cmdlet.</span></span> <span data-ttu-id="0de76-105">여기에 설명 된 **Get Proc** cmdlet은 이름에 따라 프로세스를 검색 한 다음 명령 프롬프트에서 프로세스에 대 한 정보를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-105">The **Get-Proc** cmdlet described here retrieves processes based on their names, and then displays information about the processes at a command prompt.</span></span>

## <a name="defining-the-cmdlet-class"></a><span data-ttu-id="0de76-106">Cmdlet 클래스 정의</span><span class="sxs-lookup"><span data-stu-id="0de76-106">Defining the Cmdlet Class</span></span>

<span data-ttu-id="0de76-107">Cmdlet 생성의 첫 번째 단계는 cmdlet 이름 및 cmdlet을 구현 하는 .NET Framework 클래스의 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-107">The first step in cmdlet creation is cmdlet naming and the declaration of the .NET Framework class that implements the cmdlet.</span></span> <span data-ttu-id="0de76-108">이 cmdlet은 프로세스 정보를 검색 하므로 여기서 선택한 동사 이름은 "Get"입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-108">This cmdlet retrieves process information, so the verb name chosen here is "Get."</span></span> <span data-ttu-id="0de76-109">정보를 검색할 수 있는 거의 모든 종류의 cmdlet은 명령줄 입력을 처리할 수 있습니다. 승인 된 cmdlet 동사에 대 한 자세한 내용은 [Cmdlet 동사 이름](./approved-verbs-for-windows-powershell-commands.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-109">(Almost any sort of cmdlet that is capable of retrieving information can process command-line input.) For more information about approved cmdlet verbs, see [Cmdlet Verb Names](./approved-verbs-for-windows-powershell-commands.md).</span></span>

<span data-ttu-id="0de76-110">다음은 **Get Proc** cmdlet에 대 한 클래스 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-110">Here's the class declaration for the **Get-Proc** cmdlet.</span></span> <span data-ttu-id="0de76-111">이 정의에 대 한 세부 정보는 [첫 번째 Cmdlet을 만들](./creating-a-cmdlet-without-parameters.md)때 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-111">Details about this definition are provided in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

```csharp
[Cmdlet(VerbsCommon.Get, "proc")]
public class GetProcCommand: Cmdlet
```

```vb
<Cmdlet(VerbsCommon.Get, "Proc")> _
Public Class GetProcCommand
    Inherits Cmdlet
```

## <a name="declaring-parameters"></a><span data-ttu-id="0de76-112">매개 변수 선언</span><span class="sxs-lookup"><span data-stu-id="0de76-112">Declaring Parameters</span></span>

<span data-ttu-id="0de76-113">Cmdlet 매개 변수를 사용 하면 사용자가 cmdlet에 입력을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-113">A cmdlet parameter enables the user to provide input to the cmdlet.</span></span> <span data-ttu-id="0de76-114">다음 예제에서 **Get-Proc** 및 `Get-Member`은 파이프라인 cmdlet의 이름이 고 `MemberType`는 `Get-Member` cmdlet에 대 한 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-114">In the following example, **Get-Proc** and `Get-Member` are the names of pipelined cmdlets, and `MemberType` is a parameter for the `Get-Member` cmdlet.</span></span> <span data-ttu-id="0de76-115">매개 변수의 인수는 "property"입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-115">The parameter has the argument "property."</span></span>

<span data-ttu-id="0de76-116">**PS > get-proc; @no__t-membertype 속성**</span><span class="sxs-lookup"><span data-stu-id="0de76-116">**PS> get-proc ; `get-member` -membertype property**</span></span>

<span data-ttu-id="0de76-117">Cmdlet에 대 한 매개 변수를 선언 하려면 먼저 매개 변수를 나타내는 속성을 정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-117">To declare parameters for a cmdlet, you must first define the properties that represent the parameters.</span></span> <span data-ttu-id="0de76-118">**Get-help** cmdlet에서 유일한 매개 변수는 `Name`입니다 .이 경우는 검색할 .NET Framework 프로세스 개체의 이름을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-118">In the **Get-Proc** cmdlet, the only parameter is `Name`, which in this case represents the name of the .NET Framework process object to retrieve.</span></span> <span data-ttu-id="0de76-119">따라서 cmdlet 클래스는 이름 배열을 허용 하는 문자열 형식의 속성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-119">Therefore, the cmdlet class defines a property of type string to accept an array of names.</span></span>

<span data-ttu-id="0de76-120">다음은 **Get Proc** cmdlet의 `Name` 매개 변수에 대 한 매개 변수 선언입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-120">Here's the parameter declaration for the `Name` parameter of the **Get-Proc** cmdlet.</span></span>

```csharp
/// <summary>
/// Specify the cmdlet Name parameter.
/// </summary>
  [Parameter(Position = 0)]
  [ValidateNotNullOrEmpty]
  public string[] Name
  {
    get { return processNames; }
    set { processNames = value; }
  }
  private string[] processNames;

  #endregion Parameters
```

```vb
<Parameter(Position:=0), ValidateNotNullOrEmpty()> _
Public Property Name() As String()
    Get
        Return processNames
    End Get

    Set(ByVal value As String())
        processNames = value
    End Set

End Property
```

<span data-ttu-id="0de76-121">Windows PowerShell 런타임에이 속성이 `Name` 매개 변수 임을 알리려면, 속성 정의에 [system.object](/dotnet/api/System.Management.Automation.ParameterAttribute) 를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-121">To inform the Windows PowerShell runtime that this property is the `Name` parameter, a [System.Management.Automation.Parameterattribute](/dotnet/api/System.Management.Automation.ParameterAttribute) attribute is added to the property definition.</span></span> <span data-ttu-id="0de76-122">이 특성을 선언 하는 기본 구문은 `[Parameter()]`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-122">The basic syntax for declaring this attribute is `[Parameter()]`.</span></span>

> [!NOTE]
> <span data-ttu-id="0de76-123">매개 변수는 명시적으로 public으로 표시 되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-123">A parameter must be explicitly marked as public.</span></span> <span data-ttu-id="0de76-124">공용으로 표시 되지 않는 매개 변수는 Windows PowerShell 런타임에서 찾을 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-124">Parameters that are not marked as public default to internal and are not found by the Windows PowerShell runtime.</span></span>

<span data-ttu-id="0de76-125">이 cmdlet은 `Name` 매개 변수에 대 한 문자열 배열을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-125">This cmdlet uses an array of strings for the `Name` parameter.</span></span> <span data-ttu-id="0de76-126">가능 하면 cmdlet은 매개 변수를 배열로도 정의 해야 합니다. 이렇게 하면 cmdlet이 둘 이상의 항목을 허용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-126">If possible, your cmdlet should also define a parameter as an array, because this allows the cmdlet to accept more than one item.</span></span>

#### <a name="things-to-remember-about-parameter-definitions"></a><span data-ttu-id="0de76-127">매개 변수 정의에 대해 기억할 사항</span><span class="sxs-lookup"><span data-stu-id="0de76-127">Things to Remember About Parameter Definitions</span></span>

- <span data-ttu-id="0de76-128">미리 정의 된 Windows PowerShell 매개 변수 이름 및 데이터 형식은 cmdlet이 Windows PowerShell cmdlet과 호환 되도록 가능한 한 많이 다시 사용 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-128">Predefined Windows PowerShell parameter names and data types should be reused as much as possible to ensure that your cmdlet is compatible with Windows PowerShell cmdlets.</span></span> <span data-ttu-id="0de76-129">예를 들어 모든 cmdlet이 미리 정의 된 `Id` 매개 변수 이름을 사용 하 여 리소스를 식별 하는 경우 사용자는 사용 중인 cmdlet에 관계 없이 매개 변수의 의미를 쉽게 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-129">For example, if all cmdlets use the predefined `Id` parameter name to identify a resource, user will easily understand the meaning of the parameter, regardless of what cmdlet they are using.</span></span> <span data-ttu-id="0de76-130">기본적으로 매개 변수 이름은 CLR (공용 언어 런타임)의 변수 이름에 사용 되는 것과 동일한 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-130">Basically, parameter names follow the same rules as those used for variable names in the common language runtime (CLR).</span></span> <span data-ttu-id="0de76-131">매개 변수 명명에 대 한 자세한 내용은 [Cmdlet 매개 변수 이름](https://msdn.microsoft.com/en-us/c4500737-0a05-4d01-911b-394424c65bfb)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-131">For more information about parameter naming, see [Cmdlet Parameter Names](https://msdn.microsoft.com/en-us/c4500737-0a05-4d01-911b-394424c65bfb).</span></span>

- <span data-ttu-id="0de76-132">Windows PowerShell은 일관 된 사용자 환경을 제공 하기 위해 몇 가지 매개 변수 이름을 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-132">Windows PowerShell reserves a few parameter names to provide a consistent user experience.</span></span> <span data-ttu-id="0de76-133">이러한 매개 변수 이름을 사용 하지 마세요. `WhatIf`, `Confirm`, `Verbose`, `Debug`, `Warn`, `ErrorAction`, `ErrorVariable`, `OutVariable` 및 `OutBuffer`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-133">Do not use these parameter names: `WhatIf`, `Confirm`, `Verbose`, `Debug`, `Warn`, `ErrorAction`, `ErrorVariable`, `OutVariable`, and `OutBuffer`.</span></span> <span data-ttu-id="0de76-134">또한 이러한 매개 변수 이름에 대 한 다음 별칭은 예약 되어 있습니다 (`vb`, `db`, `ea`, `ev`, `ov`, `ob`).</span><span class="sxs-lookup"><span data-stu-id="0de76-134">Additionally, the following aliases for these parameter names are reserved: `vb`, `db`, `ea`, `ev`, `ov`, and `ob`.</span></span>

- <span data-ttu-id="0de76-135">`Name`은 cmdlet에서 사용 하도록 권장 되는 단순 하 고 일반적인 매개 변수 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-135">`Name` is a simple and common parameter name, recommended for use in your cmdlets.</span></span> <span data-ttu-id="0de76-136">특정 cmdlet에 고유 하 고 기억할 수 없는 복잡 한 이름과 같은 매개 변수 이름을 선택 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-136">It is better to choose a parameter name like this than a complex name that is unique to a specific cmdlet and hard to remember.</span></span>

- <span data-ttu-id="0de76-137">매개 변수는 Windows PowerShell에서 대/소문자를 구분 하지 않지만 기본적으로 셸에서는 대/소문자를 유지 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-137">Parameters are case-insensitive in Windows PowerShell, although by default the shell preserves case.</span></span> <span data-ttu-id="0de76-138">인수에 대 한 대/소문자 구분은 cmdlet의 작업에 따라 달라 집니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-138">Case-sensitivity of the arguments depends on the operation of the cmdlet.</span></span> <span data-ttu-id="0de76-139">인수는 명령줄에서 지정 된 매개 변수로 전달 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-139">Arguments are passed to a parameter as specified at the command line.</span></span>

- <span data-ttu-id="0de76-140">다른 매개 변수 선언의 예는 [Cmdlet 매개 변수](./cmdlet-parameters.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-140">For examples of other parameter declarations, see [Cmdlet Parameters](./cmdlet-parameters.md).</span></span>

## <a name="declaring-parameters-as-positional-or-named"></a><span data-ttu-id="0de76-141">매개 변수를 위치 또는 이름으로 선언</span><span class="sxs-lookup"><span data-stu-id="0de76-141">Declaring Parameters as Positional or Named</span></span>

<span data-ttu-id="0de76-142">Cmdlet은 각 매개 변수를 위치 또는 명명 된 매개 변수로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-142">A cmdlet must set each parameter as either a positional or named parameter.</span></span> <span data-ttu-id="0de76-143">두 종류의 매개 변수 모두 단일 인수, 쉼표로 구분 된 여러 인수 및 부울 설정을 허용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-143">Both kinds of parameters accept single arguments, multiple arguments separated by commas, and Boolean settings.</span></span> <span data-ttu-id="0de76-144">부울 매개 변수 ( *스위치*라고도 함)는 부울 설정만 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-144">A Boolean parameter, also called a *switch*, handles only Boolean settings.</span></span> <span data-ttu-id="0de76-145">스위치는 매개 변수가 있는지 확인 하는 데 사용 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-145">The switch is used to determine the presence of the parameter.</span></span> <span data-ttu-id="0de76-146">권장 되는 기본값은 `false`입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-146">The recommended default is `false`.</span></span>

<span data-ttu-id="0de76-147">샘플 **Get Proc** cmdlet은 위치가 0 인 위치 매개 변수로 `Name` 매개 변수를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-147">The sample **Get-Proc** cmdlet defines the `Name` parameter as a positional parameter with position 0.</span></span> <span data-ttu-id="0de76-148">즉, 사용자가 명령줄에 입력 하는 첫 번째 인수가이 매개 변수에 대해 자동으로 삽입 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-148">This means that the first argument the user enters on the command line is automatically inserted for this parameter.</span></span> <span data-ttu-id="0de76-149">사용자가 명령줄에서 매개 변수 이름을 지정 해야 하는 명명 된 매개 변수를 정의 하려면 특성 선언에서 `Position` 키워드를 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-149">If you want to define a named parameter, for which the user must specify the parameter name from the command line, leave the `Position` keyword out of the attribute declaration.</span></span>

> [!NOTE]
> <span data-ttu-id="0de76-150">매개 변수 이름을 지정 하지 않는 한 사용자가 매개 변수 이름을 입력할 필요가 없도록 가장 많이 사용 하는 매개 변수 위치를 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-150">Unless parameters must be named, we recommend that you make the most-used parameters positional so that users will not have to type the parameter name.</span></span>

## <a name="declaring-parameters-as-mandatory-or-optional"></a><span data-ttu-id="0de76-151">매개 변수를 필수 또는 선택 사항으로 선언</span><span class="sxs-lookup"><span data-stu-id="0de76-151">Declaring Parameters as Mandatory or Optional</span></span>

<span data-ttu-id="0de76-152">Cmdlet은 각 매개 변수를 선택적 또는 필수 매개 변수로 설정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-152">A cmdlet must set each parameter as either an optional or a mandatory parameter.</span></span> <span data-ttu-id="0de76-153">샘플 **Get Proc** cmdlet에서 `Mandatory` 키워드가 특성 선언에 설정 되어 있지 않기 때문에 `Name` 매개 변수는 선택 사항으로 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-153">In the sample **Get-Proc** cmdlet, the `Name` parameter is defined as optional because the `Mandatory` keyword is not set in the attribute declaration.</span></span>

## <a name="supporting-parameter-validation"></a><span data-ttu-id="0de76-154">매개 변수 유효성 검사 지원</span><span class="sxs-lookup"><span data-stu-id="0de76-154">Supporting Parameter Validation</span></span>

<span data-ttu-id="0de76-155">**샘플** [Validatenotnulloremptyattribute](/dotnet/api/System.Management.Automation.ValidateNotNullOrEmptyAttribute)cmdlet은 입력 유효성 검사 특성을 `Name` 매개 변수에 추가 하 여 입력이-3 @no__t이 아니거나 비어 있지 않은 유효성 검사를 사용 하도록 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-155">The sample **Get-Proc** cmdlet adds an input validation attribute, [System.Management.Automation.Validatenotnulloremptyattribute](/dotnet/api/System.Management.Automation.ValidateNotNullOrEmptyAttribute), to the `Name` parameter to enable validation that the input is neither `null` nor empty.</span></span> <span data-ttu-id="0de76-156">이 특성은 Windows PowerShell에서 제공 하는 여러 유효성 검사 특성 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-156">This attribute is one of several validation attributes provided by Windows PowerShell.</span></span> <span data-ttu-id="0de76-157">다른 유효성 검사 특성의 예제는 [매개 변수 입력 유효성 검사](./validating-parameter-input.md)를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-157">For examples of other validation attributes, see [Validating Parameter Input](./validating-parameter-input.md).</span></span>

```
[Parameter(Position = 0)]
[ValidateNotNullOrEmpty]
public string[] Name
```

## <a name="overriding-an-input-processing-method"></a><span data-ttu-id="0de76-158">입력 처리 메서드 재정의</span><span class="sxs-lookup"><span data-stu-id="0de76-158">Overriding an Input Processing Method</span></span>

<span data-ttu-id="0de76-159">Cmdlet이 명령줄 입력을 처리 하려면 적절 한 입력 처리 메서드를 재정의 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-159">If your cmdlet is to handle command-line input, it must override the appropriate input processing methods.</span></span> <span data-ttu-id="0de76-160">기본 입력 처리 방법은 [첫 번째 Cmdlet을 만드는 데](./creating-a-cmdlet-without-parameters.md)도입 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-160">The basic input processing methods are introduced in [Creating Your First Cmdlet](./creating-a-cmdlet-without-parameters.md).</span></span>

<span data-ttu-id="0de76-161">[ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) 메서드를 재정의 **하 여 사용자** 또는 스크립트에서 제공 하는 @no__t 2 매개 변수 입력을 처리 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-161">The **Get-Proc** cmdlet overrides the [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord) method to handle the `Name` parameter input provided by the user or a script.</span></span> <span data-ttu-id="0de76-162">이 메서드는 요청 된 각 프로세스 이름에 대 한 프로세스를 가져오거나, 이름이 제공 되지 않은 경우에는 모든 프로세스에 대 한 프로세스를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-162">This method gets the processes for each requested process name, or all for processes if no name is provided.</span></span> <span data-ttu-id="0de76-163">[ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord)에서 [WriteObject% 28System% 2csystem %29](/dotnet/api/system.management.automation.cmdlet.writeobject?view=powershellsdk-1.1.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) 을 (를) 호출 하는 것은 출력 개체를로 전송 하는 출력 메커니즘입니다. 보유.</span><span class="sxs-lookup"><span data-stu-id="0de76-163">Notice that in [System.Management.Automation.Cmdlet.ProcessRecord](/dotnet/api/System.Management.Automation.Cmdlet.ProcessRecord), the call to [System.Management.Automation.Cmdlet.WriteObject%28System.Object%2CSystem.Boolean%29](/dotnet/api/system.management.automation.cmdlet.writeobject?view=powershellsdk-1.1.0#System_Management_Automation_Cmdlet_WriteObject_System_Object_System_Boolean_) is the output mechanism for sending output objects to the pipeline.</span></span> <span data-ttu-id="0de76-164">이 호출의 두 번째 매개 변수 `enumerateCollection`은 `true`로 설정 되어 프로세스 개체의 출력 배열을 열거 하 고 명령줄에 프로세스를 한 번에 하나씩 기록 하도록 Windows PowerShell 런타임에 알립니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-164">The second parameter of this call, `enumerateCollection`, is set to `true` to inform the Windows PowerShell runtime to enumerate the output array of process objects and write one process at a time to the command line.</span></span>

```csharp
protected override void ProcessRecord()
{
  // If no process names are passed to the cmdlet, get all processes.
  if (processNames == null)
  {
    // Write the processes to the pipeline making them available
    // to the next cmdlet. The second argument of this call tells
    // PowerShell to enumerate the array, and send one process at a
    // time to the pipeline.
    WriteObject(Process.GetProcesses(), true);
  }
  else
  {
    // If process names are passed to the cmdlet, get and write
    // the associated processes.
    foreach (string name in processNames)
    {
      WriteObject(Process.GetProcessesByName(name), true);
    }
  }
}
```

```vb
Protected Overrides Sub ProcessRecord()

    '/ If no process names are passed to the cmdlet, get all processes.
    If processNames Is Nothing Then
        Dim processes As Process()
        processes = Process.GetProcesses()
    End If

    '/ If process names are specified, write the processes to the
    '/ pipeline to display them or make them available to the next cmdlet.

    For Each name As String In processNames
        '/ The second parameter of this call tells PowerShell to enumerate the
        '/ array, and send one process at a time to the pipeline.
        WriteObject(Process.GetProcessesByName(name), True)
    Next

End Sub 'ProcessRecord
```

## <a name="code-sample"></a><span data-ttu-id="0de76-165">코드 샘플</span><span class="sxs-lookup"><span data-stu-id="0de76-165">Code Sample</span></span>

<span data-ttu-id="0de76-166">전체 C# 샘플 코드는 [GetProcessSample02 샘플](./getprocesssample02-sample.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-166">For the complete C# sample code, see [GetProcessSample02 Sample](./getprocesssample02-sample.md).</span></span>

## <a name="defining-object-types-and-formatting"></a><span data-ttu-id="0de76-167">개체 형식 및 서식 정의</span><span class="sxs-lookup"><span data-stu-id="0de76-167">Defining Object Types and Formatting</span></span>

<span data-ttu-id="0de76-168">Windows PowerShell은 .NET Framework 개체를 사용 하 여 cmdlet 간에 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-168">Windows PowerShell passes information between cmdlets by using .NET Framework objects.</span></span> <span data-ttu-id="0de76-169">따라서 cmdlet은 자체 형식을 정의 해야 할 수도 있고, 다른 cmdlet이 제공 하는 기존 형식을 cmdlet에서 확장 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-169">Consequently, a cmdlet might need to define its own type, or a cmdlet might need to extend an existing type provided by another cmdlet.</span></span> <span data-ttu-id="0de76-170">새 형식을 정의 하거나 기존 형식을 확장 하는 방법에 대 한 자세한 내용은 [개체 형식 확장 및 서식 지정](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-170">For more information about defining new types or extending existing types, see [Extending Object Types and Formatting](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351).</span></span>

## <a name="building-the-cmdlet"></a><span data-ttu-id="0de76-171">Cmdlet 빌드</span><span class="sxs-lookup"><span data-stu-id="0de76-171">Building the Cmdlet</span></span>

<span data-ttu-id="0de76-172">Cmdlet을 구현한 후 Windows PowerShell 스냅인을 사용 하 여 Windows PowerShell에 등록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-172">After you implement a cmdlet, you must register it with Windows PowerShell by using a Windows PowerShell snap-in.</span></span> <span data-ttu-id="0de76-173">Cmdlet을 등록 하는 방법에 대 한 자세한 내용은 [cmdlet, 공급자 및 호스트 응용 프로그램을 등록 하는 방법](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-173">For more information about registering cmdlets, see [How to Register Cmdlets, Providers, and Host Applications](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c).</span></span>

## <a name="testing-the-cmdlet"></a><span data-ttu-id="0de76-174">Cmdlet 테스트</span><span class="sxs-lookup"><span data-stu-id="0de76-174">Testing the Cmdlet</span></span>

<span data-ttu-id="0de76-175">Windows PowerShell을 사용 하 여 cmdlet을 등록 한 경우 명령줄에서 실행 하 여 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-175">When your cmdlet is registered with Windows PowerShell, you can test it by running it on the command line.</span></span> <span data-ttu-id="0de76-176">다음은 샘플 cmdlet에 대 한 코드를 테스트 하는 두 가지 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-176">Here are two ways to test the code for the sample cmdlet.</span></span> <span data-ttu-id="0de76-177">명령줄에서 cmdlet을 사용 하는 방법에 대 한 자세한 내용은 [Windows PowerShell 시작](/powershell/scripting/getting-started/getting-started-with-windows-powershell)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="0de76-177">For more information about using cmdlets from the command line, see [Getting Started with Windows PowerShell](/powershell/scripting/getting-started/getting-started-with-windows-powershell).</span></span>

- <span data-ttu-id="0de76-178">Windows PowerShell 프롬프트에서 다음 명령을 사용 하 여 "IEXPLORE.EXE" 라는 Internet Explorer 프로세스를 나열 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-178">At the Windows PowerShell prompt, use the following command to list the Internet Explorer process, which is named "IEXPLORE."</span></span>

    ```powershell
    PS> get-proc -name iexplore
    ```

<span data-ttu-id="0de76-179">다음 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-179">The following output appears.</span></span>

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
    -------  ------  -----   -----  -----   ------ --   -----------
        354      11  10036   18992    85   0.67   3284   iexplore
    ```

- <span data-ttu-id="0de76-180">"IEXPLORE.EXE", "OUTLOOK" 및 "NOTEPAD" 라는 Internet Explorer, Outlook 및 메모장 프로세스를 나열 하려면 다음 명령을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-180">To list the Internet Explorer, Outlook, and Notepad processes named "IEXPLORE," "OUTLOOK," and "NOTEPAD," use the following command.</span></span> <span data-ttu-id="0de76-181">여러 프로세스가 있는 경우 모든 프로세스가 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-181">If there are multiple processes, all of them are displayed.</span></span>

    ```powershell
    PS> get-proc -name iexplore, outlook, notepad
    ```

<span data-ttu-id="0de76-182">다음 출력이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0de76-182">The following output appears.</span></span>

    ```
    Handles  NPM(K)  PM(K)   WS(K)  VS(M)  CPU(s)   Id   ProcessName
    -------  ------  -----   -----  -----  ------   --    -----------
        732      21  24696    5000    138   2.25  2288   iexplore
        715      19  20556   14116    136   1.78  3860   iexplore
       3917      62  74096   58112    468 191.56  1848   OUTLOOK
         39       2   1024    3280     30   0.09  1444   notepad
         39       2   1024     356     30   0.08  3396   notepad
    ```

## <a name="see-also"></a><span data-ttu-id="0de76-183">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0de76-183">See Also</span></span>

[<span data-ttu-id="0de76-184">파이프라인 입력을 처리 하는 매개 변수 추가</span><span class="sxs-lookup"><span data-stu-id="0de76-184">Adding Parameters that Process Pipeline Input</span></span>](./adding-parameters-that-process-pipeline-input.md)

[<span data-ttu-id="0de76-185">첫 번째 Cmdlet 만들기</span><span class="sxs-lookup"><span data-stu-id="0de76-185">Creating Your First Cmdlet</span></span>](./creating-a-cmdlet-without-parameters.md)

[<span data-ttu-id="0de76-186">개체 형식 및 서식 확장</span><span class="sxs-lookup"><span data-stu-id="0de76-186">Extending Object Types and Formatting</span></span>](https://msdn.microsoft.com/en-us/da976d91-a3d6-44e8-affa-466b1e2bd351)

[<span data-ttu-id="0de76-187">Cmdlet, 공급자 및 호스트 응용 프로그램을 등록 하는 방법</span><span class="sxs-lookup"><span data-stu-id="0de76-187">How to Register Cmdlets, Providers, and Host Applications</span></span>](https://msdn.microsoft.com/en-us/a41e9054-29c8-40ab-bf2b-8ce4e7ec1c8c)

[<span data-ttu-id="0de76-188">Windows PowerShell 참조</span><span class="sxs-lookup"><span data-stu-id="0de76-188">Windows PowerShell Reference</span></span>](../windows-powershell-reference.md)

[<span data-ttu-id="0de76-189">Cmdlet 샘플</span><span class="sxs-lookup"><span data-stu-id="0de76-189">Cmdlet Samples</span></span>](./cmdlet-samples.md)