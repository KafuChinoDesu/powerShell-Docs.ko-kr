---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "파이프라인에서 개체 제거(Where Object)"
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: 4140c4c3ebb26223d03ca139992fedf6e184a38b
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2017
---
# <a name="removing-objects-from-the-pipeline-where-object"></a><span data-ttu-id="bf220-103">파이프라인에서 개체 제거(Where-Object)</span><span class="sxs-lookup"><span data-stu-id="bf220-103">Removing Objects from the Pipeline (Where-Object)</span></span>
<span data-ttu-id="bf220-104">일반적으로 Windows PowerShell은 필요한 것보다 많은 개체를 만들어 파이프라인에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-104">In Windows PowerShell, you often generate and pass along more objects to a pipeline than you want.</span></span> <span data-ttu-id="bf220-105">**Format** cmdlet을 사용하면 표시할 특정 개체의 속성을 지정할 수 있지만 전체 개체를 표시하지 않는 문제에는 도움이 되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-105">You can specify the properties of particular objects to display by using the **Format** cmdlets, but this does not help with the problem of removing entire objects from the display.</span></span> <span data-ttu-id="bf220-106">파이프라인 끝에 도달하기 전에 개체를 필터링하여 처음 만들어진 개체의 하위 집합에 대해서만 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-106">You may want to filter objects before the end of a pipeline, so you can perform actions on only a subset of the initially-generated objects.</span></span>

<span data-ttu-id="bf220-107">Windows PowerShell에는 파이프라인에 있는 각 개체를 테스트하고 특정 테스트 조건을 통과하는 개체만 파이프라인을 통해 전달할 수 있는 **Where-Object** cmdlet이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-107">Windows PowerShell includes a **Where-Object** cmdlet that allows you to test each object in the pipeline and only pass it along the pipeline if it meets a particular test condition.</span></span> <span data-ttu-id="bf220-108">테스트를 통과하지 못한 개체는 파이프라인에서 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-108">Objects that do not pass the test are removed from the pipeline.</span></span> <span data-ttu-id="bf220-109">테스트 조건은 **Where-ObjectFilterScript** 매개 변수의 값으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-109">You supply the test condition as the value of the **Where-ObjectFilterScript** parameter.</span></span>

### <a name="performing-simple-tests-with-where-object"></a><span data-ttu-id="bf220-110">Where-Object를 사용하여 간단한 테스트 수행</span><span class="sxs-lookup"><span data-stu-id="bf220-110">Performing Simple Tests with Where-Object</span></span>
<span data-ttu-id="bf220-111">**FilterScript**의 값은 하나의 *스크립트 블록*, 즉 true 또는 false로 평가되는 하나 이상의 Windows PowerShell 명령이 중괄호({})로 묶여 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-111">The value of **FilterScript** is a *script block* -  one or more Windows PowerShell commands surrounded by braces {} - that evaluates to true or false.</span></span> <span data-ttu-id="bf220-112">이러한 스크립트 블록은 매우 간단할 수 있지만 비교 연산자와 같은 다른 Windows PowerShell 개념을 알고 있어야 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-112">These script blocks can be very simple, but creating them requires knowing about another Windows PowerShell concept, comparison operators.</span></span> <span data-ttu-id="bf220-113">비교 연산자는 자신을 중심으로 양쪽에 표시되는 두 항목을 비교합니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-113">A comparison operator compares the items that appear on each side of it.</span></span> <span data-ttu-id="bf220-114">비교 연산자의 이름은 '-' 문자로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-114">Comparison operators begin with a '-' character and are followed by a name.</span></span> <span data-ttu-id="bf220-115">기본 비교 연산자는 거의 모든 유형의 개체에서 작동하지만</span><span class="sxs-lookup"><span data-stu-id="bf220-115">Basic comparison operators work on almost any kind of object.</span></span> <span data-ttu-id="bf220-116">고급 비교 연산자는 텍스트나 배열에서만 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-116">The more advanced comparison operators might only work on text or arrays.</span></span>

> [!NOTE]
> <span data-ttu-id="bf220-117">기본적으로 Windows PowerShell 비교 연산자는 텍스트를 비교할 때 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-117">By default, when working with text, Windows PowerShell comparison operators are case-insensitive.</span></span>

<span data-ttu-id="bf220-118">구문 오류가 발생할 수 있으므로 <, >, = 등의 기호는 비교 연산자로 사용할 수 없고</span><span class="sxs-lookup"><span data-stu-id="bf220-118">Due to parsing considerations, symbols such as <,>, and = are not used as comparison operators.</span></span> <span data-ttu-id="bf220-119">문자만 비교 연산자로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-119">Instead, comparison operators are comprised of letters.</span></span> <span data-ttu-id="bf220-120">다음 표에는 기본 비교 연산자가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-120">The basic comparison operators are listed in the following table.</span></span>

|<span data-ttu-id="bf220-121">비교 연산자</span><span class="sxs-lookup"><span data-stu-id="bf220-121">Comparison Operator</span></span>|<span data-ttu-id="bf220-122">의미</span><span class="sxs-lookup"><span data-stu-id="bf220-122">Meaning</span></span>|<span data-ttu-id="bf220-123">예제(true 반환)</span><span class="sxs-lookup"><span data-stu-id="bf220-123">Example (returns true)</span></span>|
|-----------------------|-----------|--------------------------|
|<span data-ttu-id="bf220-124">-eq</span><span class="sxs-lookup"><span data-stu-id="bf220-124">-eq</span></span>|<span data-ttu-id="bf220-125">같음</span><span class="sxs-lookup"><span data-stu-id="bf220-125">is equal to</span></span>|<span data-ttu-id="bf220-126">1 -eq 1</span><span class="sxs-lookup"><span data-stu-id="bf220-126">1 -eq 1</span></span>|
|<span data-ttu-id="bf220-127">-ne</span><span class="sxs-lookup"><span data-stu-id="bf220-127">-ne</span></span>|<span data-ttu-id="bf220-128">같지 않음</span><span class="sxs-lookup"><span data-stu-id="bf220-128">Is not equal to</span></span>|<span data-ttu-id="bf220-129">1 -ne 2</span><span class="sxs-lookup"><span data-stu-id="bf220-129">1 -ne 2</span></span>|
|<span data-ttu-id="bf220-130">-lt</span><span class="sxs-lookup"><span data-stu-id="bf220-130">-lt</span></span>|<span data-ttu-id="bf220-131">보다 작음</span><span class="sxs-lookup"><span data-stu-id="bf220-131">Is less than</span></span>|<span data-ttu-id="bf220-132">1 -lt 2</span><span class="sxs-lookup"><span data-stu-id="bf220-132">1 -lt 2</span></span>|
|<span data-ttu-id="bf220-133">-le</span><span class="sxs-lookup"><span data-stu-id="bf220-133">-le</span></span>|<span data-ttu-id="bf220-134">작거나 같음</span><span class="sxs-lookup"><span data-stu-id="bf220-134">Is less than or equal to</span></span>|<span data-ttu-id="bf220-135">1 -le 2</span><span class="sxs-lookup"><span data-stu-id="bf220-135">1 -le 2</span></span>|
|<span data-ttu-id="bf220-136">-gt</span><span class="sxs-lookup"><span data-stu-id="bf220-136">-gt</span></span>|<span data-ttu-id="bf220-137">보다 큼</span><span class="sxs-lookup"><span data-stu-id="bf220-137">Is greater than</span></span>|<span data-ttu-id="bf220-138">2 -gt 1</span><span class="sxs-lookup"><span data-stu-id="bf220-138">2 -gt 1</span></span>|
|<span data-ttu-id="bf220-139">-ge</span><span class="sxs-lookup"><span data-stu-id="bf220-139">-ge</span></span>|<span data-ttu-id="bf220-140">크거나 같음</span><span class="sxs-lookup"><span data-stu-id="bf220-140">Is greater than or equal to</span></span>|<span data-ttu-id="bf220-141">2 -ge 1</span><span class="sxs-lookup"><span data-stu-id="bf220-141">2 -ge 1</span></span>|
|<span data-ttu-id="bf220-142">-like</span><span class="sxs-lookup"><span data-stu-id="bf220-142">-like</span></span>|<span data-ttu-id="bf220-143">비슷함(텍스트의 와일드카드 비교)</span><span class="sxs-lookup"><span data-stu-id="bf220-143">Is like (wildcard comparison for text)</span></span>|<span data-ttu-id="bf220-144">"file.doc" -like "f\*.do?"</span><span class="sxs-lookup"><span data-stu-id="bf220-144">"file.doc" -like "f\*.do?"</span></span>|
|<span data-ttu-id="bf220-145">-notlike</span><span class="sxs-lookup"><span data-stu-id="bf220-145">-notlike</span></span>|<span data-ttu-id="bf220-146">비슷하지 않음(텍스트의 와일드카드 비교)</span><span class="sxs-lookup"><span data-stu-id="bf220-146">Is not like (wildcard comparison for text)</span></span>|<span data-ttu-id="bf220-147">"file.doc" -notlike "p\*.doc"</span><span class="sxs-lookup"><span data-stu-id="bf220-147">"file.doc" -notlike "p\*.doc"</span></span>|
|<span data-ttu-id="bf220-148">-contains</span><span class="sxs-lookup"><span data-stu-id="bf220-148">-contains</span></span>|<span data-ttu-id="bf220-149">포함</span><span class="sxs-lookup"><span data-stu-id="bf220-149">Contains</span></span>|<span data-ttu-id="bf220-150">1,2,3 -contains 1</span><span class="sxs-lookup"><span data-stu-id="bf220-150">1,2,3 -contains 1</span></span>|
|<span data-ttu-id="bf220-151">-notcontains</span><span class="sxs-lookup"><span data-stu-id="bf220-151">-notcontains</span></span>|<span data-ttu-id="bf220-152">포함 안 함</span><span class="sxs-lookup"><span data-stu-id="bf220-152">Does not contain</span></span>|<span data-ttu-id="bf220-153">1,2,3 -notcontains 4</span><span class="sxs-lookup"><span data-stu-id="bf220-153">1,2,3 -notcontains 4</span></span>|

<span data-ttu-id="bf220-154">Where-Object 스크립트 블록은 특수 변수 '$_'를 사용하여 파이프라인에 있는 현재 개체를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-154">Where-Object script blocks use the special variable '$_' to refer to the current object in the pipeline.</span></span> <span data-ttu-id="bf220-155">다음은 이러한 동작을 보여 주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-155">Here is an example of how it works.</span></span> <span data-ttu-id="bf220-156">일련의 숫자 중에서 3보다 작은 숫자만 반환하려면 다음과 같이 Where-Object를 사용하여 숫자를 필터링하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-156">If you have a list of numbers, and only want to return the ones that are less than 3, you can use Where-Object to filter the numbers by typing:</span></span>

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a><span data-ttu-id="bf220-157">개체 속성을 기반으로 필터링</span><span class="sxs-lookup"><span data-stu-id="bf220-157">Filtering Based on Object Properties</span></span>
<span data-ttu-id="bf220-158">$_가 현재 파이프라인 개체를 참조하므로 테스트를 위해 이 개체의 속성에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-158">Since $_ refers to the current pipeline object, we can access its properties for our tests.</span></span>

<span data-ttu-id="bf220-159">예를 들어 WMI에서 Win32_SystemDriver 클래스를 살펴보면</span><span class="sxs-lookup"><span data-stu-id="bf220-159">As an example, we can look at the Win32_SystemDriver class in WMI.</span></span> <span data-ttu-id="bf220-160">특정 시스템에 수백 개의 시스템 드라이버가 있을 수 있지만 현재 실행 중인 드라이버와 같은 특정 시스템 드라이버 집합만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-160">There might be hundreds of system drivers on a particular system, but you might only be interested in a particular set of the system drivers, such as those which are currently running.</span></span> <span data-ttu-id="bf220-161">Get-Member를 사용하여 Win32_SystemDriver 멤버(**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**)를 보면 관련 속성이 State이고 드라이버가 실행 중일 때 해당 값이 "Running"인 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-161">If you use Get-Member to view Win32_SystemDriver members (**Get-WmiObject -Class Win32_SystemDriver | Get-Member -MemberType Property**) you will see that the relevant property is State, and that it has a value of "Running" when the driver is running.</span></span> <span data-ttu-id="bf220-162">다음과 같이 입력하면 시스템 드라이버를 필터링하여 실행 중인 드라이버만 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-162">You can filter the system drivers, selecting only the running ones by typing:</span></span>

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"}
```

<span data-ttu-id="bf220-163">그러나 이 목록에는 아직도 필요한 것보다 많은 항목이 포함되어 있으므로</span><span class="sxs-lookup"><span data-stu-id="bf220-163">This still produces a long list.</span></span> <span data-ttu-id="bf220-164">다음과 같이 StartMode 값도 테스트하여 자동으로 시작되도록 설정된 드라이버만 선택하도록 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-164">You may want to filter to only select the drivers set to start automatically by testing the StartMode value as well:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

<span data-ttu-id="bf220-165">드라이버가 실행 중이라는 것을 앞에서 확인했기 때문에 이 목록에는 아직도 불필요한 정보가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-165">This gives us a lot of information we no longer need because we know that the drivers are running.</span></span> <span data-ttu-id="bf220-166">사실 이 시점에서 필요한 정보는 이름과 표시 이름뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-166">In fact, the only information we probably need at this point are the name and the display name.</span></span> <span data-ttu-id="bf220-167">다음 명령은 목록에 이러한 두 속성만 포함하여 출력을 훨씬 더 간단하게 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-167">The following command includes only those two properties, resulting in much simpler output:</span></span>

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

<span data-ttu-id="bf220-168">위의 명령에는 두 개의 Where-Object 요소가 있지만 다음과 같이 -and 논리 연산자를 사용하여 단일 Where-Object 요소로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-168">There are two Where-Object elements in the above command, but they can be expressed in a single Where-Object element by using the -and logical operator, like this:</span></span>

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq "Running") -and ($_.StartMode -eq "Manual") } | Format-Table -Property Name,DisplayName
```

<span data-ttu-id="bf220-169">다음 표에는 기본 논리 연산자가 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf220-169">The standard logical operators are listed in the following table.</span></span>

|<span data-ttu-id="bf220-170">논리 연산자</span><span class="sxs-lookup"><span data-stu-id="bf220-170">Logical Operator</span></span>|<span data-ttu-id="bf220-171">의미</span><span class="sxs-lookup"><span data-stu-id="bf220-171">Meaning</span></span>|<span data-ttu-id="bf220-172">예제(true 반환)</span><span class="sxs-lookup"><span data-stu-id="bf220-172">Example (returns true)</span></span>|
|--------------------|-----------|--------------------------|
|<span data-ttu-id="bf220-173">-and</span><span class="sxs-lookup"><span data-stu-id="bf220-173">-and</span></span>|<span data-ttu-id="bf220-174">논리곱(둘 다 true일 경우 true임)</span><span class="sxs-lookup"><span data-stu-id="bf220-174">Logical and; true if both sides are true</span></span>|<span data-ttu-id="bf220-175">(1 -eq 1) -and (2 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="bf220-175">(1 -eq 1) -and (2 -eq 2)</span></span>|
|<span data-ttu-id="bf220-176">-or</span><span class="sxs-lookup"><span data-stu-id="bf220-176">-or</span></span>|<span data-ttu-id="bf220-177">논리합(둘 중 하나만 true여도 true임)</span><span class="sxs-lookup"><span data-stu-id="bf220-177">Logical or; true if either side is true</span></span>|<span data-ttu-id="bf220-178">(1 -eq 1) -or (1 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="bf220-178">(1 -eq 1) -or (1 -eq 2)</span></span>|
|<span data-ttu-id="bf220-179">-not</span><span class="sxs-lookup"><span data-stu-id="bf220-179">-not</span></span>|<span data-ttu-id="bf220-180">논리 부정(true와 false를 반대로 바꿈)</span><span class="sxs-lookup"><span data-stu-id="bf220-180">Logical not; reverses true and false</span></span>|<span data-ttu-id="bf220-181">-not (1 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="bf220-181">-not (1 -eq 2)</span></span>|
|\!|<span data-ttu-id="bf220-182">논리 부정(true와 false를 반대로 바꿈)</span><span class="sxs-lookup"><span data-stu-id="bf220-182">Logical not; reverses true and false</span></span>|<span data-ttu-id="bf220-183">\!(1 -eq 2)</span><span class="sxs-lookup"><span data-stu-id="bf220-183">\!(1 -eq 2)</span></span>|

