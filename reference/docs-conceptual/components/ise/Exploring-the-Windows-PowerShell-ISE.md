---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: Windows PowerShell ISE 탐색
ms.assetid: e0d2c6e8-5126-40e7-a1e1-d1cff29fe94a
ms.openlocfilehash: 059651f159fb2636a93167709134788e90d062b8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MTE95
ms.contentlocale: ko-KR
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403116"
---
# <a name="exploring-the-windows-powershell-ise"></a><span data-ttu-id="661ce-103">Windows PowerShell ISE 탐색</span><span class="sxs-lookup"><span data-stu-id="661ce-103">Exploring the Windows PowerShell ISE</span></span>

<span data-ttu-id="661ce-104">Windows PowerShell® ISE(통합 스크립팅 환경)를 사용하여 명령 및 스크립트를 만들고 실행하고 디버그할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-104">You can use the Windows PowerShell® Integrated Scripting Environment (ISE) to create, run, and debug commands and scripts.</span></span> <span data-ttu-id="661ce-105">Windows PowerShell ISE는 메뉴 모음, Windows PowerShell 탭, 도구 모음, 스크립트 탭, 스크립트 창, 콘솔 창, 상태 표시줄, 텍스트 크기 슬라이더, 상황에 맞는 도움말 등으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-105">The Windows PowerShell ISE consists of the menu bar, Windows PowerShell tabs, the toolbar, script tabs, a Script Pane, a Console Pane, a status bar, a text-size slider and context-sensitive Help.</span></span>

> [!NOTE]
> <span data-ttu-id="661ce-106">Windows PowerShell ISE 3.0부터는 명령 창과 출력 창이 단일 콘솔 창으로 결합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-106">Beginning with Windows PowerShell ISE 3.0 the Command and Output Panes were combined into a single Console Pane.</span></span>

## <a name="menu-bar"></a><span data-ttu-id="661ce-107">메뉴 모음</span><span class="sxs-lookup"><span data-stu-id="661ce-107">Menu Bar</span></span>

<span data-ttu-id="661ce-108">메뉴 모음에는 **파일**, **편집**, **보기**, **도구**, **디버그**, **추가 기능** 및 **도움말** 메뉴가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-108">The menu bar contains the **File**, **Edit**, **View**, **Tools**, **Debug**, **Add-ons**, and **Help** menus.</span></span> <span data-ttu-id="661ce-109">메뉴의 단추를 사용하여 Windows PowerShell ISE에서 스크립트를 작성 및 실행하고 명령을 실행하는 것과 관련된 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-109">The buttons on the menus allow you to perform tasks related to writing and running scripts and running commands in the Windows PowerShell ISE.</span></span> <span data-ttu-id="661ce-110">또한 [ISE 개체 모델 계층 구조](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md)를 사용하는 스크립트를 실행하여 메뉴 모음에 [추가 기능 도구](../../core-powershell/ise/The-ISEAddOnTool-Object.md)를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-110">Additionally, an [add-on tool](../../core-powershell/ise/The-ISEAddOnTool-Object.md) may be placed on the menu bar by running scripts that use the [The ISE Object Model Hierarchy](../../core-powershell/ise/The-ISE-Object-Model-Hierarchy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="661ce-111">Windows PowerShell ISE 2.0에는 **도구** 및 **추가 기능** 메뉴가 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-111">In Windows PowerShell ISE 2.0, The **Tools** and **Add-ons** menus were not present.</span></span>

## <a name="windows-powershell-tabs"></a><span data-ttu-id="661ce-112">Windows PowerShell 탭</span><span class="sxs-lookup"><span data-stu-id="661ce-112">Windows PowerShell Tabs</span></span>

<span data-ttu-id="661ce-113">Windows PowerShell 탭은 Windows PowerShell 스크립트가 실행되는 환경입니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-113">A Windows PowerShell tab is the environment in which a Windows PowerShell script runs.</span></span> <span data-ttu-id="661ce-114">Windows PowerShell ISE에서 새 Windows PowerShell 탭을 열어 로컬 컴퓨터나 원격 컴퓨터에 별도의 환경을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-114">You can open new Windows PowerShell tabs in the Windows PowerShell ISE to create separate environments on your local computer or on remote computers.</span></span> <span data-ttu-id="661ce-115">최대 8개의 PowerShell 탭을 동시에 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-115">You may have a maximum of eight PowerShell tabs simultaneously open.</span></span>

## <a name="toolbar"></a><span data-ttu-id="661ce-116">도구 모음</span><span class="sxs-lookup"><span data-stu-id="661ce-116">Toolbar</span></span>

<span data-ttu-id="661ce-117">도구 모음에는 다음과 같은 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-117">The following buttons are located on the toolbar.</span></span>

|<span data-ttu-id="661ce-118">단추</span><span class="sxs-lookup"><span data-stu-id="661ce-118">Button</span></span>|<span data-ttu-id="661ce-119">기능</span><span class="sxs-lookup"><span data-stu-id="661ce-119">Function</span></span>|
|----------|------------|
|<span data-ttu-id="661ce-120">**새로 만들기**</span><span class="sxs-lookup"><span data-stu-id="661ce-120">**New**</span></span>|<span data-ttu-id="661ce-121">새 스크립트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-121">Opens a new script.</span></span>|
|<span data-ttu-id="661ce-122">**열기**</span><span class="sxs-lookup"><span data-stu-id="661ce-122">**Open**</span></span>|<span data-ttu-id="661ce-123">기존 스크립트 또는 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-123">Opens an existing script or file.</span></span>|
|<span data-ttu-id="661ce-124">**저장**</span><span class="sxs-lookup"><span data-stu-id="661ce-124">**Save**</span></span>|<span data-ttu-id="661ce-125">스크립트 또는 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-125">Saves a script or file.</span></span>|
|<span data-ttu-id="661ce-126">**잘라내기**</span><span class="sxs-lookup"><span data-stu-id="661ce-126">**Cut**</span></span>|<span data-ttu-id="661ce-127">선택한 텍스트를 잘라내어 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-127">Cuts the selected text and copies it to the clipboard.</span></span>|
|<span data-ttu-id="661ce-128">**복사**</span><span class="sxs-lookup"><span data-stu-id="661ce-128">**Copy**</span></span>|<span data-ttu-id="661ce-129">선택한 텍스트를 클립보드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-129">Copies the selected text to the clipboard.</span></span>|
|<span data-ttu-id="661ce-130">**붙여넣기**</span><span class="sxs-lookup"><span data-stu-id="661ce-130">**Paste**</span></span>|<span data-ttu-id="661ce-131">클립보드의 내용을 커서 위치에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-131">Pastes the contents of the clipboard at the cursor location.</span></span>|
|<span data-ttu-id="661ce-132">**출력 창 지우기**</span><span class="sxs-lookup"><span data-stu-id="661ce-132">**Clear Output Pane**</span></span>|<span data-ttu-id="661ce-133">출력 창에서 모든 내용을 지웁니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-133">Clears all content in the Output Pane.</span></span>|
|<span data-ttu-id="661ce-134">**실행 취소**</span><span class="sxs-lookup"><span data-stu-id="661ce-134">**Undo**</span></span>|<span data-ttu-id="661ce-135">방금 수행한 작업을 취소합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-135">Reverses the action that was just performed.</span></span>|
|<span data-ttu-id="661ce-136">**다시 실행**</span><span class="sxs-lookup"><span data-stu-id="661ce-136">**Redo**</span></span>|<span data-ttu-id="661ce-137">방금 실행 취소한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-137">Performs the action that was just undone.</span></span>|
|<span data-ttu-id="661ce-138">**스크립트 실행**</span><span class="sxs-lookup"><span data-stu-id="661ce-138">**Run Script**</span></span>|<span data-ttu-id="661ce-139">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-139">Runs a script.</span></span>|
|<span data-ttu-id="661ce-140">**선택 항목 실행**</span><span class="sxs-lookup"><span data-stu-id="661ce-140">**Run Selection**</span></span>|<span data-ttu-id="661ce-141">선택한 스크립트 부분을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-141">Runs a selected portion of a script.</span></span>|
|<span data-ttu-id="661ce-142">**실행 중지**</span><span class="sxs-lookup"><span data-stu-id="661ce-142">**Stop Execution**</span></span>|<span data-ttu-id="661ce-143">실행 중인 스크립트를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-143">Stops a script that is running.</span></span>|
|<span data-ttu-id="661ce-144">**새 원격 PowerShell 탭**</span><span class="sxs-lookup"><span data-stu-id="661ce-144">**New Remote PowerShell Tab**</span></span>|<span data-ttu-id="661ce-145">원격 컴퓨터에서 세션을 설정하는 새 PowerShell 탭을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-145">Creates a new PowerShell Tab that establishes a session on a remote computer.</span></span> <span data-ttu-id="661ce-146">대화 상자가 나타나고 원격 연결을 설정하는 데 필요한 세부 정보를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-146">A dialog box appears and prompts you to enter details required to establish the remote connection.</span></span>|
|<span data-ttu-id="661ce-147">**PowerShell.exe 시작**</span><span class="sxs-lookup"><span data-stu-id="661ce-147">**Start PowerShell.exe**</span></span>|<span data-ttu-id="661ce-148">PowerShell 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-148">Opens a PowerShell Console.</span></span>|
|<span data-ttu-id="661ce-149">**스크립트 창 위쪽에 표시**</span><span class="sxs-lookup"><span data-stu-id="661ce-149">**Show Script Pane Top**</span></span>|<span data-ttu-id="661ce-150">표시에서 스크립트 창을 맨 위로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-150">Moves the Script Pane to the top in the display.</span></span>|
|<span data-ttu-id="661ce-151">**스크립트 창 오른쪽에 표시**</span><span class="sxs-lookup"><span data-stu-id="661ce-151">**Show Script Pane Right**</span></span>|<span data-ttu-id="661ce-152">표시에서 스크립트 창을 오른쪽으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-152">Moves the Script Pane to the right in the display.</span></span>|
|<span data-ttu-id="661ce-153">**스크립트 창 최대 표시**</span><span class="sxs-lookup"><span data-stu-id="661ce-153">**Show Script Pane Maximized**</span></span>|<span data-ttu-id="661ce-154">스크립트 창을 최대화합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-154">Maximizes the Script Pane.</span></span>|

## <a name="script-tab"></a><span data-ttu-id="661ce-155">스크립트 탭</span><span class="sxs-lookup"><span data-stu-id="661ce-155">Script Tab</span></span>

<span data-ttu-id="661ce-156">편집 중인 스크립트의 이름을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-156">Displays the name of the script you are editing.</span></span> <span data-ttu-id="661ce-157">스크립트 탭을 클릭하여 편집할 스크립트를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-157">You can click a script tab to select the script you want to edit.</span></span>

<span data-ttu-id="661ce-158">스크립트 탭을 가리키면 스크립트 파일의 정규화된 경로가 도구 설명에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-158">When you point to the script tab, the fully qualified path to the script file appears in a tooltip.</span></span>

## <a name="script-pane"></a><span data-ttu-id="661ce-159">스크립트 창</span><span class="sxs-lookup"><span data-stu-id="661ce-159">Script Pane</span></span>

<span data-ttu-id="661ce-160">스크립트를 만들고 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-160">Allows you to create and run scripts.</span></span> <span data-ttu-id="661ce-161">스크립트 창에서 기존 스크립트를 열고, 편집하고, 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-161">You can open, edit and run existing scripts in the Script Pane.</span></span>

## <a name="output-pane"></a><span data-ttu-id="661ce-162">출력 창</span><span class="sxs-lookup"><span data-stu-id="661ce-162">Output Pane</span></span>

<span data-ttu-id="661ce-163">실행한 명령 및 스크립트의 결과를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-163">Displays the results of the commands and scripts you have run.</span></span> <span data-ttu-id="661ce-164">출력 창에서 내용을 복사하고 지울 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-164">You can also copy and clear the contents in the Output Pane.</span></span>

## <a name="command-pane"></a><span data-ttu-id="661ce-165">명령 창</span><span class="sxs-lookup"><span data-stu-id="661ce-165">Command Pane</span></span>

<span data-ttu-id="661ce-166">명령을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-166">Allows you to write commands.</span></span> <span data-ttu-id="661ce-167">명령 창에서 한 줄 명령이나 여러 줄 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-167">You can run a one line command or a multiline command in the Command Pane.</span></span> <span data-ttu-id="661ce-168">Shift+Enter를 눌러 여러 줄 명령의 각 줄을 입력하고 마지막 줄 다음에 Enter 키를 눌러 여러 줄 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-168">Press SHIFT+ENTER to enter each line of a multiline command, and press ENTER after the last line to execute the multiline command.</span></span> <span data-ttu-id="661ce-169">명령 창 맨 위에 표시된 프롬프트에는 현재 작업 디렉터리의 경로가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-169">The prompt displayed on top of the Command Pane shows the path to the current working directory.</span></span>

## <a name="status-bar"></a><span data-ttu-id="661ce-170">상태 표시줄</span><span class="sxs-lookup"><span data-stu-id="661ce-170">Status Bar</span></span>

<span data-ttu-id="661ce-171">실행하는 명령 및 스크립트가 완료되었는지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-171">Allows you to see whether the commands and scripts that you run are complete.</span></span> <span data-ttu-id="661ce-172">상태 표시줄은 맨 아래에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-172">The status bar is at the very bottom of the display.</span></span> <span data-ttu-id="661ce-173">오류 메시지의 선택한 부분이 상태 표시줄에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-173">Selected portions of error messages are displayed on the status bar.</span></span>

## <a name="text-size-slider"></a><span data-ttu-id="661ce-174">텍스트 크기 슬라이더</span><span class="sxs-lookup"><span data-stu-id="661ce-174">Text-Size Slider</span></span>

<span data-ttu-id="661ce-175">화면에서 텍스트 크기를 크게 하거나 작게 합니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-175">Increases or decreases the size of the text on the screen.</span></span>

## <a name="help"></a><span data-ttu-id="661ce-176">도움말</span><span class="sxs-lookup"><span data-stu-id="661ce-176">Help</span></span>

<span data-ttu-id="661ce-177">Windows PowerShell ISE에 대한 도움말을 웹의 TechNet 라이브러리에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-177">Help for Windows PowerShell ISE is available on the Web in the TechNet Library.</span></span> <span data-ttu-id="661ce-178">**도움말** 메뉴에서 **Windows PowerShell ISE 도움말**을 클릭하거나 스크립트 창이나 콘솔 창에서 커서가 cmdlet 이름에 있는 경우를 제외하고 아무 곳에서나 F1 키를 누르면 도움말을 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-178">You can open the Help by clicking **Windows PowerShell ISE Help** on the **Help** menu or by pressing the F1 key anywhere except when the cursor is on a cmdlet name in either the Script Pane or the Console Pane.</span></span> <span data-ttu-id="661ce-179">**도움말** 메뉴에서 Update-Help cmdlet을 실행하여 cmdlet에 대한 모든 매개 변수를 표시하고 사용하기 쉬운 형태로 매개 변수를 입력할 수 있게 하여 명령 생성을 지원하는 명령 창을 표시할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="661ce-179">From the **Help** menu you can also run the Update-Help cmdlet, and display the Command Window which assists you in constructing commands by showing you all of the parameters for a cmdlet and enabling you to fill in the parameters in an easy-to-use form.</span></span>

## <a name="see-also"></a><span data-ttu-id="661ce-180">참고 항목</span><span class="sxs-lookup"><span data-stu-id="661ce-180">See Also</span></span>

- [<span data-ttu-id="661ce-181">Windows PowerShell ISE 소개</span><span class="sxs-lookup"><span data-stu-id="661ce-181">Introducing the Windows PowerShell ISE</span></span>](../../core-powershell/ise/Introducing-the-Windows-PowerShell-ISE.md)