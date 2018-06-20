---
ms.date: 06/05/2017
keywords: powershell,cmdlet
title: PowerShell 50 ISE의 새로운 기능
ms.assetid: 38648d47-7c27-4b37-a40e-ad29948519c2
ms.openlocfilehash: 35b825cfa6ea720d0af3537c5d1b16c5ececb701
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
ms.locfileid: "30953585"
---
# <a name="what39s-new-in-the-windows-powershell-ise"></a><span data-ttu-id="6d5cb-103">Windows PowerShell ISE의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="6d5cb-103">What&#39;s New in the Windows PowerShell ISE</span></span>
<span data-ttu-id="6d5cb-104">이 항목에서는 Windows PowerShell  ISE(통합 스크립팅 환경) 버전에서 도입된 새로운 기능과 업데이트된 기능에 대해 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-104">This topic explains the new and updated features that have been introduced in versions of Windows PowerShell  Integrated Scripting Environment (ISE).</span></span>

## <a name="feature-description"></a><span data-ttu-id="6d5cb-105">기능 설명</span><span class="sxs-lookup"><span data-stu-id="6d5cb-105">Feature description</span></span>
<span data-ttu-id="6d5cb-106">Windows PowerShell ISE는 그래픽 환경 및 직관적인 환경에서 스크립트 및 모듈을 작성, 실행 및 테스트할 수 있는 호스트 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-106">The Windows PowerShell ISE is a host application that enables you to write, run, and test scripts and modules in a graphical and intuitive environment.</span></span> <span data-ttu-id="6d5cb-107">구문 색 지정, 탭 완성, 시각적 디버깅, 유니코드 규정 준수 및 상황에 맞는 도움말과 같은 주요 기능을 통해 풍부한 스크립팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-107">Key features such as syntax-coloring, tab completion, visual debugging, Unicode compliance, and context-sensitive Help provide a rich scripting experience.</span></span>

<span data-ttu-id="6d5cb-108">Windows PowerShell ISE의 개요는 [Windows PowerShell 통합 스크립팅 환경 개요](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-108">For an overview of Windows PowerShell ISE, see [Windows PowerShell Integrated Scripting Environment overview](https://technet.microsoft.com/library/3c1892c2-bf84-4cb6-af26-1f453be9e671).</span></span>

## <a name="new-and-changed-functionality-in-windows-powershell-ise"></a><span data-ttu-id="6d5cb-109">Windows PowerShell ISE의 새로운 기능 및 변경된 기능</span><span class="sxs-lookup"><span data-stu-id="6d5cb-109">New and changed functionality in Windows PowerShell ISE</span></span>
<span data-ttu-id="6d5cb-110">다음 표에는 Windows PowerShell에 있는 이 Windows PowerShell ISE 릴리스용의 새로운 기능과 변경된 기능이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-110">The following table lists the new and changed features for this release of Windows PowerShell ISE in Windows PowerShell.</span></span>

|<span data-ttu-id="6d5cb-111">기능</span><span class="sxs-lookup"><span data-stu-id="6d5cb-111">Feature/functionality</span></span>|<span data-ttu-id="6d5cb-112">Windows PowerShell ISE 4.0</span><span class="sxs-lookup"><span data-stu-id="6d5cb-112">Windows PowerShell ISE 4.0</span></span>|<span data-ttu-id="6d5cb-113">Windows PowerShell ISE 3.0</span><span class="sxs-lookup"><span data-stu-id="6d5cb-113">Windows PowerShell ISE 3.0</span></span>|<span data-ttu-id="6d5cb-114">Windows PowerShell ISE 2.0</span><span class="sxs-lookup"><span data-stu-id="6d5cb-114">Windows PowerShell ISE 2.0</span></span>|
|--------------------------|-----------------------------------------------|-----------------------------------------------|-----------------------------------------------|
|<span data-ttu-id="6d5cb-115">**[IntelliSense](#intellisense)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-115">**[IntelliSense](#intellisense)**</span></span>|<span data-ttu-id="6d5cb-116">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-116">X</span></span>|<span data-ttu-id="6d5cb-117">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-117">X</span></span>||
|<span data-ttu-id="6d5cb-118">**[코드 조각](#snippets)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-118">**[Snippets](#snippets)**</span></span>|<span data-ttu-id="6d5cb-119">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-119">X</span></span>|<span data-ttu-id="6d5cb-120">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-120">X</span></span>||
|<span data-ttu-id="6d5cb-121">**[추가 기능 도구](#add-on-tools)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-121">**[Add-on Tools](#add-on-tools)**</span></span>|<span data-ttu-id="6d5cb-122">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-122">X</span></span>|<span data-ttu-id="6d5cb-123">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-123">X</span></span>||
|<span data-ttu-id="6d5cb-124">**[관리자 다시 시작 및 자동 저장](#restart-manager-and-auto-save)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-124">**[Restart Manager and Auto-save](#restart-manager-and-auto-save)**</span></span>|<span data-ttu-id="6d5cb-125">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-125">X</span></span>|<span data-ttu-id="6d5cb-126">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-126">X</span></span>||
|<span data-ttu-id="6d5cb-127">**[가장 최근에 사용한 목록](#most-recently-used-list)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-127">**[Most-recently used list](#most-recently-used-list)**</span></span>|<span data-ttu-id="6d5cb-128">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-128">X</span></span>|<span data-ttu-id="6d5cb-129">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-129">X</span></span>||
|<span data-ttu-id="6d5cb-130">**[콘솔 창](#console-pane)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-130">**[Console Pane](#console-pane)**</span></span>|<span data-ttu-id="6d5cb-131">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-131">X</span></span>|<span data-ttu-id="6d5cb-132">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-132">X</span></span>||
|<span data-ttu-id="6d5cb-133">**[명령줄 스위치](#command-line-switches)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-133">**[Command-line switches](#command-line-switches)**</span></span>|<span data-ttu-id="6d5cb-134">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-134">X</span></span>|<span data-ttu-id="6d5cb-135">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-135">X</span></span>||
|<span data-ttu-id="6d5cb-136">**[새 편집기 기능](#new-editor-features)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-136">**[New editor features](#new-editor-features)**</span></span>|<span data-ttu-id="6d5cb-137">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-137">X</span></span>|<span data-ttu-id="6d5cb-138">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-138">X</span></span>||
|<span data-ttu-id="6d5cb-139">**[새 도움말 뷰어 창](#new-help-viewer-window)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-139">**[New Help viewer window](#new-help-viewer-window)**</span></span>|<span data-ttu-id="6d5cb-140">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-140">X</span></span>|<span data-ttu-id="6d5cb-141">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-141">X</span></span>||
|<span data-ttu-id="6d5cb-142">**[Show-Command cmdlet](#show-command-cmdlet)**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-142">**[Show-Command cmdlet](#show-command-cmdlet)**</span></span>|<span data-ttu-id="6d5cb-143">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-143">X</span></span>|<span data-ttu-id="6d5cb-144">X</span><span class="sxs-lookup"><span data-stu-id="6d5cb-144">X</span></span>||

### <a name="intellisense"></a><span data-ttu-id="6d5cb-145">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6d5cb-145">IntelliSense</span></span>
<span data-ttu-id="6d5cb-146">**ISE 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-146">**Added in ISE 3.0**</span></span>

<span data-ttu-id="6d5cb-147">IntelliSense는 Windows PowerShell ISE의 일부인 자동 완성 지원 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-147">IntelliSense is an automatic-completion assistance feature that is part of Windows PowerShell ISE.</span></span> <span data-ttu-id="6d5cb-148">IntelliSense는 입력하는 동안 잠재적으로 일치하는 cmdlet, 매개 변수, 매개 변수 값, 파일 또는 폴더가 포함된 클릭 가능한 메뉴를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-148">IntelliSense displays clickable menus of potentially matching cmdlets, parameters, parameter values, files, or folders as you type.</span></span>

<span data-ttu-id="6d5cb-149">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-149">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-150">IntelliSense를 추가하면 Windows PowerShell ISE를 사용하여 스크립트를 작성할 때 cmdlet과 구문을 더 쉽게 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-150">With the addition of IntelliSense, it is easier to discover cmdlets and syntax when you use Windows PowerShell ISE to create scripts.</span></span> <span data-ttu-id="6d5cb-151">새 스크립트를 만드는 동안 Windows PowerShell ISE를 사용하여 Windows PowerShell에 대해 알아볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-151">You can also use Windows PowerShell ISE to learn Windows PowerShell while you create new scripts.</span></span>

<span data-ttu-id="6d5cb-152">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-152">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-153">Windows PowerShell ISE 3.0 이상에서 cmdlet을 입력하면 스크롤 및 클릭 가능한 메뉴가 표시되므로 적절한 명령을 찾아서 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-153">When you type cmdlets in the Windows PowerShell ISE 3.0 or later, a scrollable and clickable menu displays, allowing you to browse and select the appropriate commands.</span></span>

### <a name="snippets"></a><span data-ttu-id="6d5cb-154">코드 조각</span><span class="sxs-lookup"><span data-stu-id="6d5cb-154">Snippets</span></span>
<span data-ttu-id="6d5cb-155">**ISE 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-155">**Added in ISE 3.0**</span></span>

<span data-ttu-id="6d5cb-156">*코드 조각*은 Windows PowerShell ISE에서 만든 스크립트에 삽입할 수 있는 Windows PowerShell 코드의 짧은 부분입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-156">*Snippets* are short sections of Windows PowerShell code that you can insert into the scripts you create in Windows PowerShell ISE.</span></span> <span data-ttu-id="6d5cb-157">Windows PowerShell ISE에는 기본 코드 조각 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-157">Windows PowerShell ISE comes with a default set of snippets.</span></span> <span data-ttu-id="6d5cb-158">Windows PowerShell ISE에서 작업하는 동안 **New-Snippet** cmdlet을 사용하여 코드 조각을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-158">You can add snippets by using the **New-Snippet** cmdlet while working in Windows PowerShell ISE.</span></span>

<span data-ttu-id="6d5cb-159">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-159">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-160">코드 조각을 사용하면 빠르게 스크립트를 조합하고 만들어 사용자 환경을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-160">By using snippets, you can quickly assemble and create scripts to automate your environment.</span></span>

<span data-ttu-id="6d5cb-161">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-161">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-162">Windows PowerShell 3.0 이상에서 코드 조각을 사용하려면 **편집** 메뉴에서 **조각 시작**을 클릭하거나 **Ctrl-J**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-162">To use snippets in Windows PowerShell 3.0 or later, on the **Edit** menu, click **Start Snippets**, or press **Ctrl-J**.</span></span>

### <a name="add-on-tools"></a><span data-ttu-id="6d5cb-163">추가 기능 도구</span><span class="sxs-lookup"><span data-stu-id="6d5cb-163">Add-on tools</span></span>
<span data-ttu-id="6d5cb-164">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-164">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-165">이제 Windows PowerShell ISE에서 개체 모델을 사용하여 추가된 WPF(Windows Presentation Foundation) 컨트롤인 추가 기능 도구를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-165">Windows PowerShell ISE now supports add-on tools, which are Windows Presentation Foundation (WPF) controls that are added by using the object model.</span></span> <span data-ttu-id="6d5cb-166">추가 기능 도구는 콘솔의 세로 창이나 가로 창으로 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-166">Add-on tools can be displayed as a vertical or horizontal pane in the console.</span></span> <span data-ttu-id="6d5cb-167">하나의 창에 있는 여러 가지 추가 기능 도구는 탭 컨트롤로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-167">Multiple add-on tools in a pane are displayed as a tabbed control.</span></span> <span data-ttu-id="6d5cb-168">타사에서 만든 추가 기능 도구를 추가하거나 제거할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-168">You can also add or remove add-on tools that are produced by non-Microsoft parties.</span></span> <span data-ttu-id="6d5cb-169">추가 기능 도구를 가져오거나 제거하는 방법에 대한 자세한 내용은 [Windows PowerShell ISE 작업](http://technet.microsoft.com/library/cc732148.aspx)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-169">For more information about how to import or remove add-on tools, see [Windows PowerShell ISE Operations](http://technet.microsoft.com/library/cc732148.aspx).</span></span>

<span data-ttu-id="6d5cb-170">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-170">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-171">추가 기능을 사용하면 스크립팅 환경을 향상하거나 Windows PowerShell ISE에 기능을 추가할 수 있는 도구로 Windows PowerShell ISE를 확장하고 사용자 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-171">Add-ons allow you to extend and customize Windows PowerShell ISE with tools that can enhance your scripting experience or add functionality to Windows PowerShell ISE.</span></span>

<span data-ttu-id="6d5cb-172">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-172">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-173">Windows PowerShell ISE 3.0 이상에는 **Commands** 추가 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-173">Windows PowerShell ISE 3.0 and later come with the **Commands** add-on.</span></span> <span data-ttu-id="6d5cb-174">**Commands** 추가 기능을 사용하면 cmdlet을 찾고 **스크립트** 창과 **콘솔** 창에서 cmdlet에 대한 도움말을 나란히 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-174">The **Commands** add-on allows you to browse cmdlets, and access help about the cmdlets side-by-side with the **Script** and **Console** Panes.</span></span>

<span data-ttu-id="6d5cb-175">**추가 기능** 메뉴의 **추가 기능 도구 웹 사이트 열기** 명령을 사용하여 추가 기능을 더 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-175">Additional add-ons can be found by using the **Open Add-on Tools Website** command on the **Add-ons** menu.</span></span>

### <a name="restart-manager-and-auto-save"></a><span data-ttu-id="6d5cb-176">관리자 다시 시작 및 자동 저장</span><span class="sxs-lookup"><span data-stu-id="6d5cb-176">Restart manager and auto-save</span></span>
<span data-ttu-id="6d5cb-177">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-177">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-178">이제 Windows PowerShell ISE에서 열려 있는 스크립트를 2분마다 개별 위치에 자동으로 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-178">Windows PowerShell ISE now automatically saves your open scripts every two minutes, in a separate location.</span></span>  <span data-ttu-id="6d5cb-179">Windows PowerShell ISE의 작동이 중지되거나 운영 체제가 다시 시작되는 경우 Windows PowerShell ISE를 다시 시작하면 스크립트를 저장하지 않은 경우에도 마지막 세션에 열려 있던 스크립트가 복구됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-179">If Windows PowerShell ISE stops working, or if the operating system is restarted, after Windows PowerShell ISE restarts, it recovers scripts that were open in the last session, even if the scripts were not saved.</span></span>

<span data-ttu-id="6d5cb-180">자동 저장 간격을 변경하려면 콘솔 창에서 **$psise.Options.AutoSaveMinuteInterval** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-180">To change the automatic saving interval, run the following command in the Console pane: **$psise.Options.AutoSaveMinuteInterval**.</span></span>

<span data-ttu-id="6d5cb-181">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-181">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-182">이제 예상치 않게 다시 시작될 경우 열려 있는 스크립트가 자동으로 저장된다는 것을 알고 Windows PowerShell ISE 내에서 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-182">You can now work within Windows PowerShell ISE knowing that your open scripts are automatically saved in the event of an unexpected restart.</span></span>

<span data-ttu-id="6d5cb-183">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-183">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-184">Windows PowerShell ISE 2.0에서는 다시 시작될 경우 스크립트를 자동으로 저장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-184">Windows PowerShell ISE 2.0 does not save the scripts automatically in the event of a restart.</span></span>

### <a name="most-recently-used-list"></a><span data-ttu-id="6d5cb-185">가장 최근에 사용한 목록</span><span class="sxs-lookup"><span data-stu-id="6d5cb-185">Most-recently used list</span></span>
<span data-ttu-id="6d5cb-186">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-186">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-187">이제 Windows PowerShell ISE에 가장 최근에 사용한 파일 목록이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-187">Windows PowerShell ISE now has a most-recently used list for files.</span></span> <span data-ttu-id="6d5cb-188">Windows PowerShell ISE에서 파일을 열면 **파일** 메뉴의 가장 최근에 사용한 목록에 해당 파일이 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-188">When you open a file in Windows PowerShell ISE, the file is added to the most-recently used list on the **File** menu.</span></span>

<span data-ttu-id="6d5cb-189">가장 최근에 사용한 목록의 기본 파일 수를 변경하려면 콘솔 창에서 다음 명령을 실행합니다. **$psise.Options.MruCount**.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-189">To change the default number of files in the most-recently used list, run the following command in the Console Pane: **$psise.Options.MruCount**.</span></span>

<span data-ttu-id="6d5cb-190">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-190">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-191">이제 가장 최근에 사용한 목록을 통해 최근에 사용한 파일을 쉽게 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-191">You can now use the most-recently used list to easily access your frequently-used files.</span></span>

<span data-ttu-id="6d5cb-192">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-192">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-193">Windows PowerShell ISE 2.0에는 가장 최근에 사용한 목록이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-193">Windows PowerShell ISE 2.0 does not have a most-recently used list.</span></span>

### <a name="console-pane"></a><span data-ttu-id="6d5cb-194">콘솔 창</span><span class="sxs-lookup"><span data-stu-id="6d5cb-194">Console Pane</span></span>
<span data-ttu-id="6d5cb-195">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-195">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-196">Windows PowerShell ISE의 첫 번째 릴리스에서 제공된 별도의 명령 및 출력 창이 단일 콘솔 창으로 결합되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-196">The separate Command and Output Panes that were available in the first release of Windows PowerShell ISE have been combined into a single Console Pane.</span></span> <span data-ttu-id="6d5cb-197">콘솔 창의 기능과 모양은 일반적인 Windows PowerShell 콘솔과 유사하지만 다음과 같은 기능이 향상되었습니다(대부분 이 항목에 설명되어 있음).</span><span class="sxs-lookup"><span data-stu-id="6d5cb-197">The Console Pane is similar in function and appearance to a typical Windows PowerShell console, but it includes the following enhancements (most are described in this topic).</span></span>

- <span data-ttu-id="6d5cb-198">XML 구문을 포함하여 입력 텍스트(출력 텍스트가 아님)의 구문 색 지정</span><span class="sxs-lookup"><span data-stu-id="6d5cb-198">Syntax coloring for input text (not output text), including XML syntax</span></span>

- <span data-ttu-id="6d5cb-199">IntelliSense</span><span class="sxs-lookup"><span data-stu-id="6d5cb-199">IntelliSense</span></span>

- <span data-ttu-id="6d5cb-200">중괄호 일치</span><span class="sxs-lookup"><span data-stu-id="6d5cb-200">Brace matching</span></span>

- <span data-ttu-id="6d5cb-201">오류 표시</span><span class="sxs-lookup"><span data-stu-id="6d5cb-201">Error indication</span></span>

- <span data-ttu-id="6d5cb-202">전체 유니코드 지원</span><span class="sxs-lookup"><span data-stu-id="6d5cb-202">Full Unicode support</span></span>

- <span data-ttu-id="6d5cb-203">**F1** 상황에 맞는 도움말</span><span class="sxs-lookup"><span data-stu-id="6d5cb-203">**F1** context-sensitive help</span></span>

- <span data-ttu-id="6d5cb-204">**Ctrl+F1** 상황에 맞는 Show-Command</span><span class="sxs-lookup"><span data-stu-id="6d5cb-204">**Ctrl+F1** context-sensitive Show-Command</span></span>

- <span data-ttu-id="6d5cb-205">복잡한 스크립트 및 오른쪽에서 왼쪽으로 쓰는 언어 지원</span><span class="sxs-lookup"><span data-stu-id="6d5cb-205">Complex script and right-to-left support</span></span>

- <span data-ttu-id="6d5cb-206">글꼴 지원</span><span class="sxs-lookup"><span data-stu-id="6d5cb-206">Font support</span></span>

- <span data-ttu-id="6d5cb-207">확대/축소</span><span class="sxs-lookup"><span data-stu-id="6d5cb-207">Zoom</span></span>

- <span data-ttu-id="6d5cb-208">줄 선택 및 블록 선택 모드</span><span class="sxs-lookup"><span data-stu-id="6d5cb-208">Line-select and block-select modes</span></span>

- <span data-ttu-id="6d5cb-209">**위쪽** 화살표를 눌러 콘솔에서 기록을 볼 때 명령줄에 입력된 콘텐츠 유지</span><span class="sxs-lookup"><span data-stu-id="6d5cb-209">Preservation of typed content at the command line when you press the **Up** arrow to view history in the console</span></span>

<span data-ttu-id="6d5cb-210">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-210">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-211">이러한 콘솔 창 변경 내용이 추가되어 콘솔 인터페이스와 보다 일치하는 스크립팅 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-211">The addition of these Console Pane changes provides a scripting experience that is more consistent with the console interface.</span></span>

<span data-ttu-id="6d5cb-212">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-212">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-213">Windows PowerShell ISE 2.0에는 별도의 명령 창과 출력 창이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-213">Windows PowerShell ISE 2.0 has separate Command and Output Panes.</span></span>

### <a name="command-line-switches"></a><span data-ttu-id="6d5cb-214">명령줄 스위치</span><span class="sxs-lookup"><span data-stu-id="6d5cb-214">Command-line switches</span></span>
<span data-ttu-id="6d5cb-215">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-215">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-216">**powershell_ise.exe**를 입력하여 명령줄에서 Windows PowerShell ISE를 시작하면 다음과 같은 새 명령줄 스위치를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-216">If you start Windows PowerShell ISE from the command line (by typing **powershell_ise.exe**), you can add the following new command-line switches.</span></span>

- <span data-ttu-id="6d5cb-217">*-NoProfile*: **$profile**을 실행하지 않고 Windows PowerShell ISE를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-217">*-NoProfile*: Starts Windows PowerShell ISE without running **$profile**</span></span>

- <span data-ttu-id="6d5cb-218">*-Help*: 도움말 창을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-218">*-Help*: Displays a Help window</span></span>

- <span data-ttu-id="6d5cb-219">*-mta*: 다중 스레드 아파트 모드로 Windows PowerShell ISE를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-219">*-mta*: Starts Windows PowerShell ISE in multithreaded apartment mode.</span></span> <span data-ttu-id="6d5cb-220">Windows PowerShell ISE에 대한 기본 작업 모드는 단일 스레드 아파트 모드, 즉 *-sta*입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-220">The default operation mode for Windows PowerShell ISE is single-threaded apartment mode, or *-sta*.</span></span>

<span data-ttu-id="6d5cb-221">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-221">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-222">이러한 명령줄 스위치가 추가되어 Windows PowerShell ISE가 실행되는 환경을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-222">The addition of these command-line switches allows you to control the environment in which the Windows PowerShell ISE runs.</span></span>

<span data-ttu-id="6d5cb-223">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-223">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-224">Windows PowerShell ISE 2.0에서는 이러한 명령줄 스위치를 인식할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-224">Windows PowerShell ISE 2.0 does not recognize these command-line switches.</span></span>

### <a name="new-editor-features"></a><span data-ttu-id="6d5cb-225">새 편집기 기능</span><span class="sxs-lookup"><span data-stu-id="6d5cb-225">New editor features</span></span>
<span data-ttu-id="6d5cb-226">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-226">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-227">다른 Windows PowerShell ISE에는 다음과 같은 편집 기능이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-227">Other Windows PowerShell ISE editing features include:</span></span>

- <span data-ttu-id="6d5cb-228">**XML 구문 색 지정**이제 Windows PowerShell ISE에서 Windows PowerShell 구문에 색을 지정하는 것과 동일한 방법으로 XML 구문에 색을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-228">**XML syntax coloring**Windows PowerShell ISE now colors XML syntax in the same way as it colors Windows PowerShell syntax.</span></span>

- <span data-ttu-id="6d5cb-229">**중괄호 일치** Windows PowerShell ISE에는 중괄호 일치 및 강조 표시가 포함되어 있으며, 다음과 같은 방법으로 사용할 수 있습니다. 예를 들어 여는 중괄호가 선택되어 있는 경우 **일치 항목으로 이동** 명령 또는 **Ctrl + ]** 를 사용하면 닫는 중괄호를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-229">**Brace matching** Windows PowerShell ISE includes brace matching and highlighting, and can be used in the following ways: (for example, using the **Go to Match** command or **Ctrl + ]** locates the closing brace, if you have an opening brace selected).</span></span>

- <span data-ttu-id="6d5cb-230">**개요 보기** 스크립트 창에서 개요 기능을 지원하므로 왼쪽 여백의 더하기 또는 빼기 기호를 클릭하여 코드의 섹션을 축소하거나 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-230">**Outline view** The Script Pane supports outlining, which allows collapsing or expanding sections of code by clicking plus or minus signs in the left margin.</span></span> <span data-ttu-id="6d5cb-231">중괄호 또는 **#region** 및 **#endregion** 태그를 사용하여 축소 가능한 섹션의 시작이나 끝을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-231">You can use braces or the **#region** and **#endregion** tags to mark the beginning or end of a collapsible section.</span></span> <span data-ttu-id="6d5cb-232">모든 영역을 확장하거나 축소하려면 **Ctrl + M**을 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-232">To expand or collapse all regions, press **Ctrl + M**.</span></span>

- <span data-ttu-id="6d5cb-233">**텍스트 끌어서 놓기**이제 Windows PowerShell ISE에서 텍스트 끌어서 놓기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-233">**Drag and drop text editing**Windows PowerShell ISE now supports drag and drop text editing.</span></span> <span data-ttu-id="6d5cb-234">텍스트 블록을 선택한 다음 텍스트를 편집기 또는 콘솔의 다른 위치로 끌어서 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-234">You can select any block of text and drag that text to another location in the editor or the console to move the text.</span></span> <span data-ttu-id="6d5cb-235">Ctrl 키를 누른 채 선택한 텍스트를 끄는 경우 마우스 단추를 놓으면 텍스트가 새 위치에 복사됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-235">If you hold down the Ctrl key while you drag the selected text, when you release the mouse button the text is copied to the new location.</span></span> <span data-ttu-id="6d5cb-236">이 버전의 Windows PowerShell ISE와 이전 버전의 Windows PowerShell ISE에서 파일을 Windows PowerShell ISE로 끌어다 놓으면 Windows PowerShell ISE에서 파일이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-236">In this version of Windows PowerShell ISE, as well as the previous version of Windows PowerShell ISE, when you drag and drop files onto Windows PowerShell ISE, Windows PowerShell ISE opens the file.</span></span>

- <span data-ttu-id="6d5cb-237">**구문 분석 오류 표시** 빨간색 밑줄을 사용하여 구문 분석 오류를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-237">**Parse error display** Parse errors are indicated with red underlines.</span></span> <span data-ttu-id="6d5cb-238">표시된 오류 위에 마우스를 놓으면 코드에서 검색된 문제가 도구 설명 텍스트에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-238">When you hover over an indicated error, tooltip text displays the problem that was found in the code.</span></span>

- <span data-ttu-id="6d5cb-239">**확대/축소** 확대/축소 슬라이더(Windows PowerShell ISE 창의 오른쪽 맨 아래에 있음)를 사용하거나 콘솔 창에 **$psise.options.Zoom** 명령을 입력하여 콘솔 콘텐츠의 확대/축소 비율을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-239">**Zoom** The zoom percentage of the console'™s content can be set by using the zoom slider (in the lower right corner of Windows PowerShell ISE window), or by entering the command **$psise.options.Zoom** in the Console Pane.</span></span>

- <span data-ttu-id="6d5cb-240">**서식 있는 텍스트 복사 및 붙여넣기** Windows PowerShell ISE에서 클립보드로 복사하면 원래 선택 항목의 글꼴, 크기 및 색상 정보가 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-240">**Rich text copy and paste** Copying to the clipboard in Windows PowerShell ISE preserves the font, size, and color information of the original selection.</span></span>

- <span data-ttu-id="6d5cb-241">**블록 선택** Alt 키를 누른 채 스크립트 창에서 마우스로 텍스트를 선택하거나 **Alt+Shift+Arrow**를 눌러 텍스트 블록을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-241">**Block selection** You can select a block of text by holding down the ALT key while selecting text in the Script Pane with your mouse, or by pressing **Alt+Shift+Arrow**.</span></span>

<span data-ttu-id="6d5cb-242">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-242">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-243">추가 편집 기능은 보다 일관되고 강력한 편집 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-243">The additional editing features provide a more consistent and powerful editing environment.</span></span>

<span data-ttu-id="6d5cb-244">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-244">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-245">Windows PowerShell ISE 2.0에는 이러한 향상된 편집 기능이 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-245">These editing enhancements were not present in Windows PowerShell ISE 2.0.</span></span>

### <a name="new-help-viewer-window"></a><span data-ttu-id="6d5cb-246">새 도움말 뷰어 창</span><span class="sxs-lookup"><span data-stu-id="6d5cb-246">New Help viewer window</span></span>
<span data-ttu-id="6d5cb-247">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-247">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-248">커서가 cmdlet에 있을 때 **F1** 키를 누르거나 cmdlet 일부를 강조 표시하면 강조 표시된 cmdlet에 대한 상황에 맞는 도움말이 새 도움말 뷰어에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-248">If you press **F1** when your cursor is in a cmdlet, or you have part of a cmdlet highlighted, the new Help viewer opens context-sensitive Help about the highlighted cmdlet.</span></span> <span data-ttu-id="6d5cb-249">Windows PowerShell 정보 도움말을 표시하려면 콘솔 창에 **operators**를 입력한 다음 **F1** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-249">To display Windows PowerShell About help, type  **operators** in the console pane, and then press **F1**.</span></span>

<span data-ttu-id="6d5cb-250">이 기능을 사용하려면 먼저 Microsoft 웹 사이트에서 최신 버전의 Windows PowerShell 도움말 항목을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-250">Before you use this feature, download the most current version of Windows PowerShell Help topics from the Microsoft website.</span></span> <span data-ttu-id="6d5cb-251">도움말 항목을 다운로드하는 가장 간단한 방법은 관리자 권한으로 Windows PowerShell ISE를 실행할 때 콘솔 창에서 **Update-Help** cmdlet을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-251">The simplest method for downloading the Help topics is to run the **Update-Help** cmdlet in the Console Pane when running Windows PowerShell ISE as administrator.</span></span>

<span data-ttu-id="6d5cb-252">**F1** 키가 도움말을 찾는 위치를 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-252">You can alter where the **F1** key looks for Help.</span></span> <span data-ttu-id="6d5cb-253">**도구**/**옵션** 메뉴의 **일반 설정** 탭에서 **기타 설정** 아래에 있는 **온라인 콘텐츠 대신 로컬 도움말 콘텐츠 사용** 확인란을 설정하거나 선택을 취소할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-253">In the **Tools**/**Options** menu, on the **General Settings** tab, under **Other Settings**, you can set or clear the checkbox **Use local help content instead of online content**.</span></span> <span data-ttu-id="6d5cb-254">이 확인란을 선택할 경우 클라이언트는 모듈 폴더에 다운로드된 도움말에서 cmdlet 도움말을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-254">If checked, then the client looks for the cmdlet Help in the downloaded Help found in the modules folder.</span></span>  <span data-ttu-id="6d5cb-255">이 확인란의 선택을 취소할 경우 클라이언트는 TechNet 라이브러리에서 cmdlet 도움말을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-255">If the checkbox is cleared, then the client looks on the TechNet library for the cmdlet help.</span></span>

<span data-ttu-id="6d5cb-256">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-256">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-257">현재 cmdlet 또는 스크립트를 종료하지 않는 상황에 맞는 도움말은 매끄러운 학습 환경을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-257">Context-sensitive Help without leaving your current cmdlet or script provides a seamless learning experience.</span></span>

<span data-ttu-id="6d5cb-258">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-258">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-259">이전 버전의 Windows PowerShell ISE에서 F1 키를 누르면 로컬 컴퓨터의 도움말 파일이 열렸습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-259">Pressing F1 in previous versions of Windows PowerShell ISE opened the help file on the local computer.</span></span> <span data-ttu-id="6d5cb-260">Windows PowerShell ISE 3.0 이상에서는 검색 및 구성할 수 있는 cmdlet 도움말이 포함된 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-260">In Windows PowerShell ISE 3.0 and later, a window opens that contains the help for the cmdlet that is searchable and configurable.</span></span> <span data-ttu-id="6d5cb-261">이 도움말 환경은 Windows PowerShell ISE 3.0의 새로운 기능이며, 업데이트 가능한 도움말은 Windows PowerShell 3.0의 새로운 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-261">This Help experience is new for Windows PowerShell ISE 3.0, and Updatable Help is new for Windows PowerShell 3.0.</span></span>

### <a name="show-command-cmdlet"></a><span data-ttu-id="6d5cb-262">Show-Command cmdlet</span><span class="sxs-lookup"><span data-stu-id="6d5cb-262">Show-Command cmdlet</span></span>
<span data-ttu-id="6d5cb-263">**PowerShell 3.0에 추가됨**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-263">**Added in PowerShell 3.0**</span></span>

<span data-ttu-id="6d5cb-264">**Show-Command** cmdlet을 사용하면 그래픽 양식에 입력하여 cmdlet 또는 함수를 작성하거나 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-264">The **Show-Command** cmdlet enables you to compose or run a cmdlet or function by filling in a graphical form.</span></span> <span data-ttu-id="6d5cb-265">이 양식을 사용하면 사용자가 그래픽 환경에서 Windows PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-265">The form lets users work with Windows PowerShell in a graphical environment.</span></span> <span data-ttu-id="6d5cb-266">또한 **Show-Command**를 사용하면 고급 스크립터가 Windows PowerShell 기반 GUI를 빠르게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-266">**Show-Command** also enables advanced scripters to create a quick Windows PowerShell-based GUI.</span></span>

<span data-ttu-id="6d5cb-267">**이와 같은 변경을 통해 더해지는 가치**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-267">**What value does this change add?**</span></span>

<span data-ttu-id="6d5cb-268">Windows PowerShell 스크립트에서 **Show-Command**를 사용하면 익숙한 그래픽 환경을 사용자에게 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-268">By using **Show-Command** in your Windows PowerShell scripts, you can provide your users with the graphical environment with which they are familiar.</span></span> <span data-ttu-id="6d5cb-269">**Show-Command**는 초급 사용자가 Windows PowerShell을 익히는 데 도움이 될 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-269">**Show-Command** can also help introductory users learn Windows PowerShell.</span></span>

<span data-ttu-id="6d5cb-270">**달라진 기능**</span><span class="sxs-lookup"><span data-stu-id="6d5cb-270">**What works differently?**</span></span>

<span data-ttu-id="6d5cb-271">Show-Command는 새로운 Windows PowerShell ISE 3.0 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-271">Show-Command is new Windows PowerShell ISE 3.0.</span></span>

## <a name="see-also"></a><span data-ttu-id="6d5cb-272">참고 항목</span><span class="sxs-lookup"><span data-stu-id="6d5cb-272">See also</span></span>
<span data-ttu-id="6d5cb-273">Windows PowerShell에서 Windows PowerShell ISE를 사용하는 방법에 대한 자세한 내용은 다음 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="6d5cb-273">For more information about using Windows PowerShell ISE in Windows PowerShell, see the following links.</span></span>

- [<span data-ttu-id="6d5cb-274">Windows PowerShell 통합 스크립팅 환경 탐색</span><span class="sxs-lookup"><span data-stu-id="6d5cb-274">Exploring the Windows PowerShell Integrated Scripting Environment</span></span>](../getting-started/fundamental/exploring-the-windows-powershell-ise.md)
- [<span data-ttu-id="6d5cb-275">TechNet Wiki의 ISE</span><span class="sxs-lookup"><span data-stu-id="6d5cb-275">ISE on the TechNet Wiki</span></span>](http://social.technet.microsoft.com/wiki/search/searchresults.aspx?q=ISE)
- [<span data-ttu-id="6d5cb-276">스크립트 센터</span><span class="sxs-lookup"><span data-stu-id="6d5cb-276">Script Center</span></span>](http://technet.microsoft.com/scriptcenter/default)