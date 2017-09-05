---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "Windows PowerShell ISE에서 스크립트를 디버깅하는 방법"
ms.assetid: 6dc6d8f9-8978-46e9-a92f-169af37e2817
ms.openlocfilehash: 2b8313c3f2ae1a8fb670099baa8950db49722330
ms.sourcegitcommit: 4102ecc35d473211f50a453f6ae3fbea31cb3428
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/31/2017
---
# <a name="how-to-debug-scripts-in-windows-powershell-ise"></a><span data-ttu-id="23f41-103">Windows PowerShell ISE에서 스크립트를 디버깅하는 방법</span><span class="sxs-lookup"><span data-stu-id="23f41-103">How to Debug Scripts in Windows PowerShell ISE</span></span>
<span data-ttu-id="23f41-104">이 항목에서는 Windows PowerShell® ISE(통합 스크립팅 환경) 시각적 디버깅 기능을 사용하여 로컬 컴퓨터에서 스크립트를 디버그하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-104">This topic describes how to debug scripts on a local computer by using the Windows PowerShell® Integrated Scripting Environment (ISE) visual debugging features.</span></span>

<span data-ttu-id="23f41-105">[중단점을 관리하는 방법]()
[디버깅 세션을 관리하는 방법]()
[디버그하는 동안 프로시저 단위 실행, 한 단계씩 코드 실행 및 프로시저 나가기를 수행하는 방법]()
[디버그하는 동안 변수 값을 표시하는 방법]()</span><span class="sxs-lookup"><span data-stu-id="23f41-105">[How to manage breakpoints]()
[How to manage a debugging session]()
[How to step over, step into, and step out while debugging]()
[How to display the values of variables while debugging]()</span></span>

## <span data-ttu-id="23f41-106"><a name="bkmk_1"></a>중단점을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="23f41-106"><a name="bkmk_1"></a>How to manage breakpoints</span></span>
<span data-ttu-id="23f41-107">중단점은 변수의 현재 상태와 스크립트를 실행하는 환경을 검사할 수 있도록 작업을 일시 중지하려는 스크립트의 지정된 지점입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-107">A breakpoint is a designated spot in a script where you would like operation to pause so that you can examine the current state of the variables and the environment in which your script is running.</span></span> <span data-ttu-id="23f41-108">스크립트가 중단점에서 일시 중지되면 콘솔 창에서 명령을 실행하여 스크립트 상태를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-108">Once your script is paused by a breakpoint, you can run commands in the Console Pane to examine the state of your script.</span></span>  <span data-ttu-id="23f41-109">변수를 출력하거나 다른 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-109">You can output variables or run other commands.</span></span> <span data-ttu-id="23f41-110">현재 실행 중인 스크립트의 컨텍스트에 표시되는 모든 변수의 값을 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-110">You can even modify the value of any variables that are visible to the context of the currently running script.</span></span> <span data-ttu-id="23f41-111">보려는 사항을 검사한 후 스크립트 작업을 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-111">After you have examined what you want to see, you can resume operation of the script.</span></span>

<span data-ttu-id="23f41-112">Windows PowerShell 디버깅 환경에서는 다음 세 가지 유형의 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-112">You can set three types of breakpoints in the Windows PowerShell debugging environment:</span></span>

1.  <span data-ttu-id="23f41-113">**줄 중단점**.</span><span class="sxs-lookup"><span data-stu-id="23f41-113">**Line breakpoint**.</span></span> <span data-ttu-id="23f41-114">스크립트 작업 중 지정된 줄에 도달하면 스크립트가 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-114">The script pauses when the designated line is reached during the operation of the script</span></span>

2.  <span data-ttu-id="23f41-115">**변수 중단점.**</span><span class="sxs-lookup"><span data-stu-id="23f41-115">**Variable breakpoint.**</span></span> <span data-ttu-id="23f41-116">지정된 변수의 값이 변경될 때마다 스크립트가 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-116">The script pauses whenever the designated variable’s value changes.</span></span>

3.  <span data-ttu-id="23f41-117">**명령 중단점.**</span><span class="sxs-lookup"><span data-stu-id="23f41-117">**Command breakpoint.**</span></span> <span data-ttu-id="23f41-118">스크립트 작업 중 지정된 명령을 실행하려 할 때마다 스크립트가 일시 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-118">The script pauses whenever the designated command is about to be run during the operation of the script.</span></span> <span data-ttu-id="23f41-119">매개 변수를 포함하여 중단점을 원하는 작업으로만 추가로 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-119">It can include parameters to further filter the breakpoint to only the operation you want.</span></span> <span data-ttu-id="23f41-120">명령은 사용자가 만든 함수일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-120">The command can also be a function you created.</span></span>

<span data-ttu-id="23f41-121">Windows PowerShell ISE 디버깅 환경에서는 이 중에서 줄 중단점만 메뉴 또는 바로 가기 키를 통해 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-121">Of these, in the Windows PowerShell ISE debugging environment, only line breakpoints can be set by using the menu or the keyboard shortcuts.</span></span> <span data-ttu-id="23f41-122">다른 두 유형의 중단점도 설정할 수 있지만 콘솔 창에서 [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet을 통해 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-122">The other two types of breakpoints can be set, but they are set from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/88d2d9ad-17dc-44ae-99aa-f841125b9dc8) cmdlet.</span></span> <span data-ttu-id="23f41-123">이 섹션에서는 Windows PowerShell ISE에서 메뉴(사용할 수 있을 경우)를 사용하여 디버깅 작업을 수행하는 방법과 콘솔 창에서 스크립팅을 사용하여 보다 다양한 명령을 수행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-123">This section describes how you can perform debugging tasks in Windows PowerShell ISE by using the menus where available, and perform a wider range of commands from the Console Pane by using scripting.</span></span>

### <a name="to-set-a-breakpoint"></a><span data-ttu-id="23f41-124">중단점을 설정하려면</span><span class="sxs-lookup"><span data-stu-id="23f41-124">To set a breakpoint</span></span>
<span data-ttu-id="23f41-125">스크립트를 저장한 후에만 스크립트에 중단점을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-125">A breakpoint can be set in a script only after it has been saved.</span></span> <span data-ttu-id="23f41-126">줄 중단점을 설정할 줄을 마우스 오른쪽 단추로 클릭한 다음 **중단점 설정/해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-126">Right-click the line where you want to set a line breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="23f41-127">또는 줄 중단점을 설정할 줄을 클릭한 다음 **F9** 키를 누르거나 **디버그** 메뉴에서 **중단점 설정/해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-127">Or, click the line where you want to set a line breakpoint, and press **F9** or, on the **Debug** menu, click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="23f41-128">다음 스크립트는 [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet을 사용하여 콘솔 창에서 변수 중단점을 설정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-128">The following script is an example of how you can set a variable breakpoint from the Console Pane by using the [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420) cmdlet.</span></span>

``` PowerShell
# This command sets a breakpoint on the Server variable in the Sample.ps1 script.
Set-PSBreakpoint -Script sample.ps1 -Variable Server
```

### <a name="list-all-breakpoints"></a><span data-ttu-id="23f41-129">모든 중단점 표시</span><span class="sxs-lookup"><span data-stu-id="23f41-129">List all breakpoints</span></span>
<span data-ttu-id="23f41-130">현재 Windows PowerShell® 세션에 있는 중단점을 모두 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-130">Displays all breakpoints in the current Windows PowerShell® session.</span></span>

<span data-ttu-id="23f41-131">**디버그** 메뉴에서 **중단점 목록**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-131">On the **Debug** menu, click **List Breakpoints**.</span></span> <span data-ttu-id="23f41-132">다음 스크립트는 [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet을 사용하여 콘솔 창에서 모든 중단점을 표시하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-132">The following script is an example of how you can list all breakpoints from the Console Pane by using the [Get-PSBreakpoint](https://technet.microsoft.com/library/0bf48936-00ab-411c-b5e0-9b10a812a3c6) cmdlet.</span></span>

``` PowerShell
# This command lists all breakpoints in the current session. 
Get-PSBreakpoint
```

### <a name="remove-a-breakpoint"></a><span data-ttu-id="23f41-133">중단점 제거</span><span class="sxs-lookup"><span data-stu-id="23f41-133">Remove a breakpoint</span></span>
<span data-ttu-id="23f41-134">중단점을 제거하면 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-134">Removing a breakpoint deletes it.</span></span>  <span data-ttu-id="23f41-135">나중에 다시 사용할 수도 있는 경우 대신 [사용하지 않도록 설정]()하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-135">If you think you might want to use it again later, consider [disabling]() it instead.</span></span>  <span data-ttu-id="23f41-136">중단점을 제거할 줄을 마우스 오른쪽 단추로 클릭한 다음 **중단점 설정/해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-136">Right-click the line where you want to remove a breakpoint, and then click **Toggle Breakpoint**.</span></span> <span data-ttu-id="23f41-137">또는 중단점을 제거할 줄을 클릭한 다음 **디버그** 메뉴에서 **중단점 설정/해제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-137">Or, click the line where you want to remove a breakpoint, and on the **Debug** menu, click **Toggle Breakpoint**.</span></span> <span data-ttu-id="23f41-138">다음 스크립트는 [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet을 사용하여 콘솔 창에서 지정된 ID의 중단점을 제거하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-138">The following script is an example of how to remove a breakpoint with a specified ID from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

``` PowerShell
# This command deletes the breakpoint with breakpoint ID 2.
Remove-PSBreakpoint -Id 2
```

### <a name="remove-all-breakpoints"></a><span data-ttu-id="23f41-139">모든 중단점 제거</span><span class="sxs-lookup"><span data-stu-id="23f41-139">Remove All Breakpoints</span></span>
<span data-ttu-id="23f41-140">현재 세션에서 정의된 모든 중단점을 제거하려면 **디버그** 메뉴에서 **모든 중단점 제거**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-140">To remove all breakpoints defined in the current session, on the **Debug** menu, click **Remove All Breakpoints**.</span></span>

<span data-ttu-id="23f41-141">다음 스크립트는 [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet을 사용하여 콘솔 창에서 모든 중단점을 제거하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-141">The following script is an example of how to remove all breakpoints from the Console Pane by using the [Remove-PSBreakpoint](https://technet.microsoft.com/library/4c877a80-0ea0-4790-9281-88c08ef0ddd6) cmdlet.</span></span>

``` PowerShell
# This command deletes all of the breakpoints in the current session.
Get-PSBreakpoint | Remove-PSBreakpoint
```

### <span data-ttu-id="23f41-142"><a name="bkmk_disable"></a>중단점 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="23f41-142"><a name="bkmk_disable"></a>Disable a Breakpoint</span></span>
<span data-ttu-id="23f41-143">중단점을 사용하지 않도록 설정할 경우 중단점이 제거되지 않고, 사용하도록 설정할 때까지 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-143">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="23f41-144">특정 줄 중단점을 사용하지 않도록 설정하려면 중단점을 사용하지 않도록 설정할 줄을 마우스 오른쪽 단추로 클릭한 다음 **중단점 사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-144">To disable a specific line breakpoint, right-click the line where you want to disable a breakpoint, and then click **Disable Breakpoint**.</span></span> <span data-ttu-id="23f41-145">또는 중단점을 사용하지 않도록 설정할 줄을 클릭한 다음 **F9** 키를 누르거나 **디버그** 메뉴에서 **중단점 사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-145">Or, click the line where you want to disable a breakpoint, and press **F9** or, on the **Debug** menu, click **Disable Breakpoint**.</span></span> <span data-ttu-id="23f41-146">다음 스크립트는 [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet을 사용하여 콘솔 창에서 지정된 ID의 중단점을 제거하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-146">The following script is an example of how you can remove a breakpoint with a specified ID from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

``` PowerShell
# This command disables the breakpoint with breakpoint ID 0.
Disable-PSBreakpoint -Id 0
```

### <a name="disable-all-breakpoints"></a><span data-ttu-id="23f41-147">모든 중단점 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="23f41-147">Disable All Breakpoints</span></span>
<span data-ttu-id="23f41-148">중단점을 사용하지 않도록 설정할 경우 중단점이 제거되지 않고, 사용하도록 설정할 때까지 해제됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-148">Disabling a breakpoint does not remove it; it turns it off until it is enabled.</span></span>  <span data-ttu-id="23f41-149">현재 세션의 모든 중단점을 사용하지 않도록 설정하려면 **디버그** 메뉴에서 **모든 중단점 사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-149">To disable all breakpoints in the current session, on the **Debug** menu, click **Disable all Breakpoints**.</span></span> <span data-ttu-id="23f41-150">다음 스크립트는 [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet을 사용하여 콘솔 창에서 모든 중단점을 사용하지 않도록 설정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-150">The following script is an example of how you can disable all breakpoints from the Console Pane by using the [Disable-PSBreakpoint](https://technet.microsoft.com/library/d4974e9b-0aaa-4e20-b87f-f599a413e4e8) cmdlet.</span></span>

``` PowerShell
# This command disables all breakpoints in the current session. 
# You can abbreviate this command as: "gbp | dbp".
Get-PSBreakpoint | Disable-PSBreakpoint
```

### <a name="enable-a-breakpoint"></a><span data-ttu-id="23f41-151">중단점 사용</span><span class="sxs-lookup"><span data-stu-id="23f41-151">Enable a Breakpoint</span></span>
<span data-ttu-id="23f41-152">특정 중단점을 사용하도록 설정하려면 중단점을 사용하도록 설정할 줄을 마우스 오른쪽 단추로 클릭한 다음 **중단점 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-152">To enable a specific breakpoint, right-click the line where you want to enable a breakpoint, and then click **Enable Breakpoint**.</span></span> <span data-ttu-id="23f41-153">또는 중단점을 사용하도록 설정할 줄을 클릭한 다음 **F9** 키를 누르거나 **디버그** 메뉴에서 **중단점 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-153">Or, click the line where you want to enable a breakpoint, and then press **F9** or, on the **Debug** menu, click **Enable Breakpoint**.</span></span> <span data-ttu-id="23f41-154">다음 스크립트는 [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet을 사용하여 콘솔 창에서 특정 중단점을 사용하도록 설정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-154">The following script is an example of how you can enable specific breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

``` PowerShell
# This command enables breakpoints with breakpoint IDs 0, 1, and 5.
Enable-PSBreakpoint -Id 0, 1, 5
```

### <a name="enable-all-breakpoints"></a><span data-ttu-id="23f41-155">모든 중단점 사용</span><span class="sxs-lookup"><span data-stu-id="23f41-155">Enable All Breakpoints</span></span>
<span data-ttu-id="23f41-156">현재 세션에서 정의된 모든 중단점을 사용하도록 설정하려면 **디버그** 메뉴에서 **모든 중단점 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-156">To enable all breakpoints defined in the current session, on the **Debug** menu, click **Enable all Breakpoints**.</span></span> <span data-ttu-id="23f41-157">다음 스크립트는 [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet을 사용하여 콘솔 창에서 모든 중단점을 사용하도록 설정하는 방법의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-157">The following script is an example of how you can enable all breakpoints from the Console Pane by using the [Enable-PSBreakpoint](https://technet.microsoft.com/library/739e1091-3b3f-405f-a428-bec7543e5df0) cmdlet.</span></span>

``` PowerShell
# This command enables all breakpoints in the current session. 
# You can abbreviate the command by using their aliases: "gbp | ebp".
Get-PSBreakpoint | Enable-PSBreakpoint
```

## <span data-ttu-id="23f41-158"><a name="bkmk_2"></a>디버깅 세션을 관리하는 방법</span><span class="sxs-lookup"><span data-stu-id="23f41-158"><a name="bkmk_2"></a>How to manage a debugging session</span></span>
<span data-ttu-id="23f41-159">디버깅을 시작하기 전에 중단점을 하나 이상 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-159">Before you start debugging, you must set one or more breakpoints.</span></span> <span data-ttu-id="23f41-160">디버그하려는 스크립트를 저장하지 않은 경우 중단점을 설정할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-160">You cannot set a breakpoint unless the script that you want to debug is saved.</span></span> <span data-ttu-id="23f41-161">중단점을 설정하는 방법에 대한 지침은 [중단점을 관리하는 방법]() 또는 [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="23f41-161">For directions on of how to set a breakpoint, see [How to manage breakpoints]() or [Set-PSBreakpoint](https://technet.microsoft.com/library/6afd5d2c-a285-4796-8607-3cbf49471420).</span></span> <span data-ttu-id="23f41-162">디버깅을 시작한 후에는 디버깅을 중지할 때까지 스크립트를 편집할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-162">After you start debugging, you cannot edit a script until you stop debugging.</span></span> <span data-ttu-id="23f41-163">중단점이 하나 이상 설정되어 있는 스크립트는 실행되기 전에 자동으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-163">A script that has one or more breakpoints set is automatically saved before it is run.</span></span>

### <a name="to-start-debugging"></a><span data-ttu-id="23f41-164">디버깅을 시작하려면</span><span class="sxs-lookup"><span data-stu-id="23f41-164">To start debugging</span></span>
<span data-ttu-id="23f41-165">**F5** 키를 누르거나, 도구 모음에서 **스크립트 실행** 아이콘을 클릭하거나, **디버그** 메뉴에서 **실행/계속**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-165">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu click **Run/Continue**.</span></span> <span data-ttu-id="23f41-166">스크립트가 첫 번째 중단점에 도달할 때까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-166">The script runs until it encounters the first breakpoint.</span></span> <span data-ttu-id="23f41-167">여기서 작업이 일시 중지되고, 일시 중지된 줄이 강조 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-167">It pauses operation there and highlights the line on which it paused.</span></span>

### <a name="to-continue-debugging"></a><span data-ttu-id="23f41-168">디버깅을 계속하려면</span><span class="sxs-lookup"><span data-stu-id="23f41-168">To continue debugging</span></span>
<span data-ttu-id="23f41-169">**F5** 키를 누르거나, 도구 모음에서 **스크립트 실행** 아이콘을 클릭하거나, **디버그** 메뉴에서 **실행/계속**을 클릭하거나, 콘솔 창에서 **C**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-169">Press **F5** or, on the toolbar, click the **Run Script** icon, or on the **Debug** menu, click **Run/Continue** or, in the Console Pane, type **C** and then press **ENTER**.</span></span> <span data-ttu-id="23f41-170">이렇게 하면 스크립트가 다음 중단점이나 더 이상 중단점이 없는 경우 스크립트의 끝까지 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-170">This causes the script to continue running to the next breakpoint or to the end of the script if no further breakpoints are encountered.</span></span>

### <a name="to-view-the-call-stack"></a><span data-ttu-id="23f41-171">호출 스택을 보려면</span><span class="sxs-lookup"><span data-stu-id="23f41-171">To view the call stack</span></span>
<span data-ttu-id="23f41-172">호출 스택은 스크립트에서 현재 실행 위치를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-172">The call stack displays the current run location in the script.</span></span> <span data-ttu-id="23f41-173">다른 함수에 의해 호출된 함수에서 스크립트를 실행하는 경우 출력에서 추가 행으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-173">If the script is running in a function that was called by a different function, then that is represented in the display by additional rows in the output.</span></span> <span data-ttu-id="23f41-174">맨 아래에 있는 행은 원래 스크립트와 함수가 호출된 스크립트의 줄을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-174">The bottom-most row displays the original script and the line in it in which a function was called.</span></span> <span data-ttu-id="23f41-175">위에 있는 다음 줄은 해당 함수와 다른 함수가 호출되었을 수 있는 함수의 줄을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-175">The next line up shows that function and the line in it in which another function might have been called.</span></span>  <span data-ttu-id="23f41-176">맨 위에 있는 행은 중단점이 설정된 현재 줄의 현재 컨텍스트를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-176">The top-most row shows the current context of the current line on which the breakpoint is set.</span></span>

<span data-ttu-id="23f41-177">일시 중지된 동안 현재 호출 스택을 보려면 **Ctrl+Shift+D**를 누르거나, **디버그** 메뉴에서 **호출 스택 표시**를 클릭하거나, 콘솔 창에서 **K**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-177">While paused, to see the current call stack, press **CTRL+SHIFT+D** or, on the **Debug** menu, click **Display Call Stack** or, in the Console Pane, type **K** and then press **ENTER**.</span></span>

### <a name="to-stop-debugging"></a><span data-ttu-id="23f41-178">디버깅을 중지하려면</span><span class="sxs-lookup"><span data-stu-id="23f41-178">To stop debugging</span></span>
<span data-ttu-id="23f41-179">**Shift-F5**를 누르거나, **디버그** 메뉴에서 **디버거 중지**를 클릭하거나, 콘솔 창에서 **Q**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-179">Press **SHIFT-F5** or, on the **Debug** menu, click **Stop Debugger**, or, in the Console Pane, type **Q** and then press **ENTER**.</span></span>

## <span data-ttu-id="23f41-180"><a name="bkmk_3"></a>디버그하는 동안 프로시저 단위 실행, 한 단계씩 코드 실행 및 프로시저 나가기를 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="23f41-180"><a name="bkmk_3"></a>How to step over, step into, and step out while debugging</span></span>
<span data-ttu-id="23f41-181">한 단계씩 코드 실행은 한 번에 하나씩 문을 실행하는 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-181">Stepping is the process of running one statement at a time.</span></span> <span data-ttu-id="23f41-182">코드 줄에서 중지하고 변수 값과 시스템 상태를 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-182">You can stop on a line of code, and examine the values of variables and the state of the system.</span></span> <span data-ttu-id="23f41-183">다음 표에서는 프로시저 단위 실행, 한 단계씩 코드 실행, 프로시저 나가기 등의 일반적인 디버깅 작업에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-183">The following table describes common debugging tasks such as stepping over, stepping into, and stepping out.</span></span>

| <span data-ttu-id="23f41-184">디버깅 작업</span><span class="sxs-lookup"><span data-stu-id="23f41-184">Debugging Task</span></span> | <span data-ttu-id="23f41-185">설명</span><span class="sxs-lookup"><span data-stu-id="23f41-185">Description</span></span> | <span data-ttu-id="23f41-186">PowerShell ISE에서 작업을 수행하는 방법</span><span class="sxs-lookup"><span data-stu-id="23f41-186">How to accomplish it in PowerShell ISE</span></span> |
| --- | --- | --- |
| <span data-ttu-id="23f41-187">**한 단계씩 코드 실행**</span><span class="sxs-lookup"><span data-stu-id="23f41-187">**Step Into**</span></span> | <span data-ttu-id="23f41-188">현재 문을 실행하고 다음 문에서 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-188">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="23f41-189">현재 문이 함수 또는 스크립트 호출이면 디버거가 해당 함수나 스크립트로 한 단계씩 코드를 실행하고, 그렇지 않으면 다음 문에서 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-189">If the current statement is a function or script call, then the debugger steps into that function or script, otherwise it stops at the next statement.</span></span> | <span data-ttu-id="23f41-190">**F11** 키를 누르거나, **디버그** 메뉴에서 **한 단계씩 코드 실행**을 클릭하거나, 콘솔 창에서 **S**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-190">Press **F11** or, on the **Debug** menu, click **Step Into**, or in the Console Pane, type **S** and press **ENTER**.</span></span> |
| <span data-ttu-id="23f41-191">**프로시저 단위 실행**</span><span class="sxs-lookup"><span data-stu-id="23f41-191">**Step Over**</span></span> | <span data-ttu-id="23f41-192">현재 문을 실행하고 다음 문에서 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-192">Executes the current statement and then stops at the next statement.</span></span> <span data-ttu-id="23f41-193">현재 문이 함수 또는 스크립트 호출이면 디버거가 전체 함수나 스크립트를 실행하고, 함수 호출 후 다음 문에서 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-193">If the current statement is a function or script call then the debugger executes the whole function or script, and it stops at the next statement after the function call.</span></span> | <span data-ttu-id="23f41-194">**F10** 키를 누르거나, **디버그** 메뉴에서 **프로시저 단위 실행**을 클릭하거나, 콘솔 창에서 **V**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-194">Press **F10** or, on the **Debug** menu, click **Step Over**, or in the Console Pane, type **V** and press **ENTER**.</span></span> |
| <span data-ttu-id="23f41-195">**프로시저 나가기**</span><span class="sxs-lookup"><span data-stu-id="23f41-195">**Step Out**</span></span> | <span data-ttu-id="23f41-196">현재 함수에서 나가고, 함수가 중첩된 경우에는 한 수준 위로 올라갑니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-196">Steps out of the current function and up one level if the function is nested.</span></span> <span data-ttu-id="23f41-197">본문에 있는 경우 스크립트가 끝 또는 다음 중단점까지 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-197">If in the main body, the script is executed to the end, or to the next breakpoint.</span></span> <span data-ttu-id="23f41-198">건너뛴 문은 실행되지만 단계별로 실행되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-198">The skipped statements are executed, but not stepped through.</span></span> | <span data-ttu-id="23f41-199">**Shift+F11**을 누르거나, **디버그** 메뉴에서 **프로시저 나가기**를 클릭하거나, 콘솔 창에서 **O**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-199">Press **SHIFT+F11**, or on the **Debug** menu, click **Step Out**, or in the Console Pane, type **O** and press **ENTER**.</span></span> |
| <span data-ttu-id="23f41-200">**계속**</span><span class="sxs-lookup"><span data-stu-id="23f41-200">**Continue**</span></span> | <span data-ttu-id="23f41-201">끝이나 다음 중단점까지 실행을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-201">Continues execution to the end, or to the next breakpoint.</span></span> <span data-ttu-id="23f41-202">건너뛴 함수 및 호출은 실행되지만 단계별로 실행되지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-202">The skipped functions and invocations are executed, but not stepped through.</span></span> | <span data-ttu-id="23f41-203">**F5** 키를 누르거나, **디버그** 메뉴에서 **실행/계속**을 클릭하거나, 콘솔 창에서 **C**를 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-203">Press **F5** or, on the **Debug** menu, click **Run/Continue**, or in the Console Pane, type **C** and press **ENTER**.</span></span> |

## <span data-ttu-id="23f41-204"><a name="bkmk_4"></a>디버그하는 동안 변수 값을 표시하는 방법</span><span class="sxs-lookup"><span data-stu-id="23f41-204"><a name="bkmk_4"></a>How to display the values of variables while debugging</span></span>
<span data-ttu-id="23f41-205">코드를 단계별로 실행할 때 스크립트에서 변수의 현재 값을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-205">You can display the current values of variables in the script as you step through the code.</span></span>

### <a name="to-display-the-values-of-standard-variables"></a><span data-ttu-id="23f41-206">표준 변수의 값을 표시하려면</span><span class="sxs-lookup"><span data-stu-id="23f41-206">To display the values of standard variables</span></span>
<span data-ttu-id="23f41-207">다음 방법 중 하나를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-207">Use one of the following methods:</span></span>

-   <span data-ttu-id="23f41-208">스크립트 창에서 변수를 마우스로 가리켜 해당 값을 도구 설명으로 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-208">In the Script Pane, hover over the variable to display its value as a tool tip.</span></span>

-   <span data-ttu-id="23f41-209">콘솔 창에서 변수 이름을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-209">In the Console Pane, type the variable name and press **ENTER**.</span></span>

<span data-ttu-id="23f41-210">ISE에서 모든 창은 항상 동일한 범위입니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-210">All panes in ISE are always in the same scope.</span></span> <span data-ttu-id="23f41-211">따라서 스크립트를 디버그하는 동안 콘솔 창에 입력한 명령은 스크립트 범위에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-211">Therefore, while you are debugging a script, the commands that you type in the Console Pane run in script scope.</span></span> <span data-ttu-id="23f41-212">따라서 콘솔 창을 사용하여 변수 값을 찾고 스크립트에만 정의되어 있는 함수를 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-212">This allows you to use the Console Pane to find the values of variables and call functions that are defined only in the script.</span></span>

### <a name="to-display-the-values-of-automatic-variables"></a><span data-ttu-id="23f41-213">자동 변수의 값을 표시하려면</span><span class="sxs-lookup"><span data-stu-id="23f41-213">To display the values of automatic variables</span></span>
<span data-ttu-id="23f41-214">앞에서 설명한 방법을 사용하면 스크립트를 디버그하는 동안 거의 모든 변수의 값을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-214">You can use the preceding method to display the value of almost all variables while you are debugging a script.</span></span> <span data-ttu-id="23f41-215">그러나 다음과 같은 자동 변수에는 이러한 방법을 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-215">However, these methods do not work for the following automatic variables.</span></span>

-   <span data-ttu-id="23f41-216">$_</span><span class="sxs-lookup"><span data-stu-id="23f41-216">$_</span></span>

-   <span data-ttu-id="23f41-217">$Input</span><span class="sxs-lookup"><span data-stu-id="23f41-217">$Input</span></span>

-   <span data-ttu-id="23f41-218">$MyInvocation</span><span class="sxs-lookup"><span data-stu-id="23f41-218">$MyInvocation</span></span>

-   <span data-ttu-id="23f41-219">$PSBoundParameters</span><span class="sxs-lookup"><span data-stu-id="23f41-219">$PSBoundParameters</span></span>

-   <span data-ttu-id="23f41-220">$Args</span><span class="sxs-lookup"><span data-stu-id="23f41-220">$Args</span></span>

<span data-ttu-id="23f41-221">이러한 변수의 값을 표시하려는 경우 스크립트의 변수 값이 아니라 디버거가 사용하는 내부 파이프라인의 해당 변수 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-221">If you try to display the value of any of these variables, you get the value of that variable for in an internal pipeline the debugger uses, not the value of the variable in the script.</span></span> <span data-ttu-id="23f41-222">몇 가지 변수($_, $Input, $MyInvocation, $PSBoundParameters 및 $Args)의 경우 다음과 같은 방법으로 이 문제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-222">You can work around this for a few variables ($_, $Input, $MyInvocation, $PSBoundParameters, and $Args) by using the following method:</span></span>

1.  <span data-ttu-id="23f41-223">스크립트에서 자동 변수의 값을 새 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-223">In the script, assign the value of the automatic variable to a new variable.</span></span>

2.  <span data-ttu-id="23f41-224">스크립트 창에서 새 변수를 마우스로 가리키거나 콘솔 창에서 새 변수를 입력하여 새 변수의 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-224">Display the value of the new variable, either by hovering over the new variable in the Script Pane, or by typing the new variable in the Console Pane.</span></span>

<span data-ttu-id="23f41-225">예를 들어 $MyInvocation 변수의 값을 표시하려면 스크립트에서 $scriptname 등의 새 변수에 값을 할당한 다음 $scriptname 변수를 마우스로 가리키거나 입력하여 해당 값을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="23f41-225">For example, to display the value of the $MyInvocation variable, in the script, assign the value to a new variable, such as $scriptname, and then hover over or type the $scriptname variable to display its value.</span></span>

``` PowerShell
#In MyScript.ps1
$scriptname = $MyInvocation.MyCommand.Path

#In the Console Pane:
C:\ps-test> $scriptname
C:\ps-test\MyScript.ps1
```

## <a name="see-also"></a><span data-ttu-id="23f41-226">참고 항목</span><span class="sxs-lookup"><span data-stu-id="23f41-226">See Also</span></span>
- [<span data-ttu-id="23f41-227">Windows PowerShell ISE 사용</span><span class="sxs-lookup"><span data-stu-id="23f41-227">Using the Windows PowerShell ISE</span></span>](Using-the-Windows-PowerShell-ISE.md)

