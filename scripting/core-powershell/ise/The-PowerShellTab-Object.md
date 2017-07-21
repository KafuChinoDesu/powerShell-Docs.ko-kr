---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "PowerShellTab 개체"
ms.assetid: a9b58556-951b-4f48-b3ae-b351b7564360
ms.openlocfilehash: d4e9374202d352a30b3eb46bcf1e4e40dea49822
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2017
---
# <a name="the-powershelltab-object"></a><span data-ttu-id="93e59-103">PowerShellTab 개체</span><span class="sxs-lookup"><span data-stu-id="93e59-103">The PowerShellTab Object</span></span>
  <span data-ttu-id="93e59-104">**PowerShellTab** 개체는 Windows PowerShell 런타임 환경을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-104">The **PowerShellTab** object represents a Windows PowerShell runtime environment.</span></span>

## <a name="methods"></a><span data-ttu-id="93e59-105">메서드</span><span class="sxs-lookup"><span data-stu-id="93e59-105">Methods</span></span>

###  <span data-ttu-id="93e59-106"><a name="invoke"></a>Invoke\( Script \)</span><span class="sxs-lookup"><span data-stu-id="93e59-106"><a name="invoke"></a> Invoke\( Script \)</span></span>
  <span data-ttu-id="93e59-107">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-107">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-108">PowerShell 탭에서 지정된 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-108">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
>  <span data-ttu-id="93e59-109">이 메서드는 이 메서드가 실행되는 PowerShell 탭이 아닌, 다른 PowerShell 탭에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-109">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="93e59-110">개체 또는 값을 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-110">It does not return any object or value.</span></span> <span data-ttu-id="93e59-111">코드가 어떤 변수든 수정한다면, 해당 변경 내용은 해당 명령이 호출된 탭에서 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-111">If the code modifies any variable, then those changes persist on the tab against which the command was invoked.</span></span>

 <span data-ttu-id="93e59-112">**Script** - System.Management.Automation.ScriptBlock 또는 문자열. 실행할 스크립트 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-112">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

```
# Manually create a second PowerShell tab before running this script.
# Return to the first PowerShell tab and type the following command
$psise.PowerShellTabs[1].Invoke({dir})
```

### <a name="invokesynchronous-script-usenewscope-millisecondstimeout-"></a><span data-ttu-id="93e59-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span><span class="sxs-lookup"><span data-stu-id="93e59-113">InvokeSynchronous\( Script, \[useNewScope\], millisecondsTimeout \)</span></span>
  <span data-ttu-id="93e59-114">Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-114">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="93e59-115">PowerShell 탭에서 지정된 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-115">Runs the given script in the PowerShell tab.</span></span>

> [!NOTE]
>  <span data-ttu-id="93e59-116">이 메서드는 이 메서드가 실행되는 PowerShell 탭이 아닌, 다른 PowerShell 탭에 대해서만 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-116">This method only works on other PowerShell tabs, not the PowerShell tab from which it is run.</span></span> <span data-ttu-id="93e59-117">스크립트 블록이 실행되고, 스크립트에서 반환되는 모든 값은 명령을 호출한 실행 환경에 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-117">The script block is run and any value that is returned from the script is returned to the run environment from which you invoked the command.</span></span> <span data-ttu-id="93e59-118">**millesecondsTimeout** 값이 지정하는 시간보다 명령이 실행되는 데 더 오래 걸린다면 "작업 시간이 초과되었습니다."라는 예외와 함께 명령이 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-118">If the command takes longer to run than the **millesecondsTimeout** value specifies, then the command fails with an exception: "The operation has timed out."</span></span>

 <span data-ttu-id="93e59-119">**Script** - System.Management.Automation.ScriptBlock 또는 문자열. 실행할 스크립트 블록입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-119">**Script** - System.Management.Automation.ScriptBlock or String The script block to run.</span></span>

 <span data-ttu-id="93e59-120">**\[useNewScope\]** - 기본적으로 **$true**
로 설정되는 선택적 부울. **$true**로 설정된 경우 명령을 실행할 새 범위가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-120">**\[useNewScope\]** -  Optional Boolean that defaults to **$true**
 If set to **$true**, then a new scope is created within which to run the command.</span></span> <span data-ttu-id="93e59-121">명령으로 지정되는 PowerShell 탭의 런타임 환경을 수정하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-121">It does not modify the runtime environment of the PowerShell tab that is specified by the command.</span></span>

 <span data-ttu-id="93e59-122">**\[millisecondsTimeout\]** - 기본값이 **500**인 선택적 정수.</span><span class="sxs-lookup"><span data-stu-id="93e59-122">**\[millisecondsTimeout\]** -  Optional integer that defaults to **500**.</span></span>
<span data-ttu-id="93e59-123">이 명령이 지정된 시간 안에 완료되지 않으면 이 명령은 "작업 시간이 초과되었습니다"라는 메시지와 함께 **TimeoutException**을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-123">If the command does not finish within the specified time, then the command generates a **TimeoutException** with the message "The operation has timed out."</span></span>

```
# create a new PowerShell tab and then switch back to the first
$PSise.PowerShellTabs.Add()
$psISE.PowerShellTabs.SetSelectedPowerShellTab($psISE.PowerShellTabs[0]) 

# Invoke a simple command on the other tab, in its own scope
$psISE.PowerShellTabs[1].InvokeSynchronous('$x=1',$false)
# You can switch to the other tab and type “$x” to see that the value is saved there.

# This example sets a value in the other tab (in a different scope) 
# and returns it through the pipeline to this tab to store in $a
$a=$psISE.PowerShellTabs[1].InvokeSynchronous('$z=3;$z') 
$a

# This example runs a command that takes longer than the allowed timeout value
# and measures how long it runs so that you can see the impact
measure-command {$psISE.PowerShellTabs[1].InvokeSynchronous("sleep 10",$false,5000)}

```

## <a name="properties"></a><span data-ttu-id="93e59-124">속성</span><span class="sxs-lookup"><span data-stu-id="93e59-124">Properties</span></span>

###  <span data-ttu-id="93e59-125"><a name="AddOnsMenu"></a> AddOnsMenu</span><span class="sxs-lookup"><span data-stu-id="93e59-125"><a name="AddOnsMenu"></a> AddOnsMenu</span></span>
  <span data-ttu-id="93e59-126">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-126">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-127">PowerShell 탭에 대한 추가 기능 메뉴를 가져오는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-127">The read-only property that gets the Add-ons menu for the PowerShell tab.</span></span>

```
# Clear the Add-ons menu if one exists.
$psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Clear()
# Create an AddOns menu with an accessor.
# Note the use of "_"  as opposed to the "&" for mapping to the fast key letter for the menu item.
$menuAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("_Process",{get-process},"Alt+P") 
# Add a nested menu. 
$parentAdded = $psISE.CurrentPowerShellTab.AddOnsMenu.SubMenus.Add("Parent",$null,$null) 
$parentAdded.SubMenus.Add("_Dir",{dir},"Alt+D")
# Show the Add-ons menu on the current PowerShell tab.
$psISE.CurrentPowerShellTab.AddOnsMenu
```

###  <span data-ttu-id="93e59-128"><a name="CanExecute"></a> CanInvoke</span><span class="sxs-lookup"><span data-stu-id="93e59-128"><a name="CanExecute"></a> CanInvoke</span></span>
  <span data-ttu-id="93e59-129">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-129">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-130">스크립트를 [Invoke( Script )](#invoke) 메서드로 호출할 수 있으면 **$true** 값을 반환하는 읽기 전용 부울 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-130">The read-only Boolean property that returns a **$true** value if a script can be invoked with the [Invoke( Script )](#invoke) method.</span></span>

```
# CanInvoke will be false if the PowerShell
# tab is running a script that takes a while, and you
# check its properties from another PowerShell tab. It is
# always false if checked on the current PowerShell tab. 
# Manually create a second PowerShell tab before running this script.
# Return to the first tab and type
$secondTab = $psise.PowerShellTabs[1] 
$secondTab.CanInvoke 
$secondTab.Invoke({sleep 20})
$secondTab.CanInvoke

```

###  <span data-ttu-id="93e59-131"><a name="Commandpane"></a> Consolepane</span><span class="sxs-lookup"><span data-stu-id="93e59-131"><a name="Commandpane"></a> Consolepane</span></span>
  <span data-ttu-id="93e59-132">Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-132">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span>  <span data-ttu-id="93e59-133">Windows PowerShell ISE 2.0에서는 이 속성의 이름이 **CommandPane**이었습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-133">In Windows PowerShell ISE 2.0 this was named **CommandPane**.</span></span>

 <span data-ttu-id="93e59-134">콘솔 창 [editor](../ise/The-ISEEditor-Object.md) 개체를 가져오는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-134">The read-only property that gets the Console pane [editor](../ise/The-ISEEditor-Object.md) object.</span></span>

```
# Gets the Console Pane editor.
$psISE.CurrentPowerShellTab.ConsolePane

```

###  <span data-ttu-id="93e59-135"><a name="Displayname"></a> DisplayName</span><span class="sxs-lookup"><span data-stu-id="93e59-135"><a name="Displayname"></a> DisplayName</span></span>
  <span data-ttu-id="93e59-136">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-136">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-137">PowerShell 탭에 표시되는 텍스트를 가져오거나 설정하는 읽기-쓰기 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-137">The read-write property that gets or sets the text that is displayed on the PowerShell tab.</span></span> <span data-ttu-id="93e59-138">기본적으로 탭 이름은 "PowerShell #"이며, 여기서 #은 숫자를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-138">By default, tabs are named "PowerShell #", where the # represents a number.</span></span>

```
$newTab = $psise.PowerShellTabs.Add()
# Change the DisplayName of the new PowerShell tab. 
$newTab.DisplayName="Brand New Tab"
```

###  <span data-ttu-id="93e59-139"><a name="ExpandedScript"></a> ExpandedScript</span><span class="sxs-lookup"><span data-stu-id="93e59-139"><a name="ExpandedScript"></a> ExpandedScript</span></span>
  <span data-ttu-id="93e59-140">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-140">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-141">스크립트 창이 확장 또는 숨겨져 있는지 여부를 결정하는 읽기-쓰기를 부울 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-141">The read-write Boolean property that determines whether the Script pane is expanded or hidden.</span></span>

```
# Toggle the expanded script property to see its effect.
$PSise.CurrentPowerShellTab.ExpandedScript=!$PSise.CurrentPowerShellTab.ExpandedScript

```

###  <span data-ttu-id="93e59-142"><a name="Files"></a> Files</span><span class="sxs-lookup"><span data-stu-id="93e59-142"><a name="Files"></a> Files</span></span>
  <span data-ttu-id="93e59-143">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-143">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-144">PowerShell 탭에 열려 있는 [스크립트 파일 컬렉션](../ise/The-ISEFileCollection-Object.md)을 가져오는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-144">The read-only property that gets the [collection of script files](../ise/The-ISEFileCollection-Object.md) that are open in the PowerShell tab.</span></span>

```
$newFile = $psISE.CurrentPowerShellTab.Files.Add()
$newFile.Editor.Text = "a`r`nb" 
# Gets the line count
$newFile.Editor.LineCount
```

###  <span data-ttu-id="93e59-145"><a name="Output"></a> Output</span><span class="sxs-lookup"><span data-stu-id="93e59-145"><a name="Output"></a> Output</span></span>
  <span data-ttu-id="93e59-146">이 기능은 Windows PowerShell ISE 2.0에는 있었지만 그 이후 버전의 ISE에서 제거되었거나 이름이 바뀌었습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-146">This feature is present in Windows PowerShell ISE 2.0, but was removed or renamed in later versions of the ISE.</span></span>  <span data-ttu-id="93e59-147">Windows PowerShell ISE의 이후 버전에서는 동일한 용도로 **ConsolePane** 개체를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-147">In later versions of Windows PowerShell ISE, you can use the **ConsolePane** object for the same purposes.</span></span>

 <span data-ttu-id="93e59-148">현재 [편집기](../ise/The-ISEEditor-Object.md)의 출력 창을 가져오는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-148">The read-only property that gets the Output pane of the current [editor](../ise/The-ISEEditor-Object.md).</span></span>

```
# Clears the text in the Output pane.
$psise.CurrentPowerShellTab.output.clear()
```

###  <span data-ttu-id="93e59-149"><a name="Prompt"></a> Prompt</span><span class="sxs-lookup"><span data-stu-id="93e59-149"><a name="Prompt"></a> Prompt</span></span>
  <span data-ttu-id="93e59-150">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-150">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-151">현재 프롬프트 텍스트를 가져오는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-151">The read-only property that gets the current prompt text.</span></span> <span data-ttu-id="93e59-152">참고: **Prompt** 함수는 사용자의 프로필로 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-152">Note: the **Prompt** function can be overridden by the user’s profile.</span></span> <span data-ttu-id="93e59-153">결과가 단순 문자열이 아니라면 이 속성은 아무 것도 반환하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-153">If the result is other than a simple string, then this property returns nothing.</span></span>

```
# Gets the current prompt text.
$psISE.CurrentPowerShellTab.Prompt
```

###  <span data-ttu-id="93e59-154"><a name="ShowCommands"></a> ShowCommands</span><span class="sxs-lookup"><span data-stu-id="93e59-154"><a name="ShowCommands"></a> ShowCommands</span></span>
  <span data-ttu-id="93e59-155">Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-155">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="93e59-156">현재 명령 창이 표시되어 있는지 여부를 나타내는 읽기-쓰기 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-156">The read-write property that indicates if the Commands pane is currently displayed.</span></span>

```
# Gets the current status of the Commands pane and stores it in the $a variable
$a = $psISE.CurrentPowerShellTab.ShowCommands
# if $a is $false, then turn the Commands pane on by changing the value to $True
if (!$a) {$psISE.CurrentPowerShellTab.ShowCommands=$True}
```

###  <span data-ttu-id="93e59-157"><a name="StatusText"></a> StatusText</span><span class="sxs-lookup"><span data-stu-id="93e59-157"><a name="StatusText"></a> StatusText</span></span>
  <span data-ttu-id="93e59-158">Windows PowerShell ISE 2.0 이상에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-158">Supported in Windows PowerShell ISE 2.0 and later.</span></span> 

 <span data-ttu-id="93e59-159">**PowerShellTab** 상태 텍스트를 가져오는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-159">The read-only property that gets the **PowerShellTab** status text.</span></span>

```
# Gets the current status text,
$psISE.CurrentPowerShellTab.StatusText
```

###  <span data-ttu-id="93e59-160"><a name="HorizontalAddOnToolsPaneOpened"></a> HorizontalAddOnToolsPaneOpened</span><span class="sxs-lookup"><span data-stu-id="93e59-160"><a name="HorizontalAddOnToolsPaneOpened"></a> HorizontalAddOnToolsPaneOpened</span></span>
  <span data-ttu-id="93e59-161">Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-161">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="93e59-162">가로 추가 기능 도구 창이 현재 열려 있는지 여부를 나타내는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-162">The read-only property that indicates whether the horizontal Add-Ons tool pane is currently open.</span></span>

```
# Gets the current state of the horizontal Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

###  <span data-ttu-id="93e59-163"><a name="VerticalAddOnToolsPaneOpened"></a> **VerticalAddOnToolsPaneOpened**</span><span class="sxs-lookup"><span data-stu-id="93e59-163"><a name="VerticalAddOnToolsPaneOpened"></a> **VerticalAddOnToolsPaneOpened**</span></span>
  <span data-ttu-id="93e59-164">Windows PowerShell ISE 3.0 이상에서 지원되며, 이전 버전에는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-164">Supported in Windows PowerShell ISE 3.0 and later, and not present in earlier versions.</span></span> 

 <span data-ttu-id="93e59-165">세로 추가 기능 도구 창이 현재 열려 있는지 여부를 나타내는 읽기 전용 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="93e59-165">The read-only property that indicates whether the vertical Add-Ons tool pane is currently open.</span></span>

```
# Turns on the Commands pane
$psISE.CurrentPowerShellTab.ShowCommands=$True
# Gets the current state of the vertical Add-ons tool pane. 
$psISE.CurrentPowerShellTab.HorizontalAddOnToolsPaneOpened
```

## <a name="see-also"></a><span data-ttu-id="93e59-166">참고 항목</span><span class="sxs-lookup"><span data-stu-id="93e59-166">See Also</span></span>
- [<span data-ttu-id="93e59-167">PowerShellTabCollection 개체</span><span class="sxs-lookup"><span data-stu-id="93e59-167">The PowerShellTabCollection Object</span></span>](The-PowerShellTabCollection-Object.md) 
- [<span data-ttu-id="93e59-168">Windows PowerShell ISE 스크립팅 개체 모델</span><span class="sxs-lookup"><span data-stu-id="93e59-168">The Windows PowerShell ISE Scripting Object Model</span></span>](../ise/The-Windows-PowerShell-ISE-Scripting-Object-Model.md) 
- [<span data-ttu-id="93e59-169">Windows PowerShell ISE 개체 모델 참조</span><span class="sxs-lookup"><span data-stu-id="93e59-169">Windows PowerShell ISE Object Model Reference</span></span>](../ise/Windows-PowerShell-ISE-Object-Model-Reference.md) 
- [<span data-ttu-id="93e59-170">ISE 개체 모델 계층 구조</span><span class="sxs-lookup"><span data-stu-id="93e59-170">The ISE Object Model Hierarchy</span></span>](../ise/The-ISE-Object-Model-Hierarchy.md)

  
