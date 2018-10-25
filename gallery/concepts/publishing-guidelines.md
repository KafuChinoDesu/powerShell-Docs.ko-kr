---
ms.date: 06/12/2017
contributor: JKeithB
keywords: gallery,powershell,cmdlet,psgallery
description: 게시자용 지침
title: PowerShell 갤러리 게시 지침 및 모범 사례
ms.openlocfilehash: 2ddeae9fdb33a58f97bfeb66079541bb7c5791b1
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851172"
---
# <a name="powershellgallery-publishing-guidelines-and-best-practices"></a><span data-ttu-id="bf7bb-104">PowerShell 갤러리 게시 지침 및 모범 사례</span><span class="sxs-lookup"><span data-stu-id="bf7bb-104">PowerShellGallery Publishing Guidelines and Best Practices</span></span>

<span data-ttu-id="bf7bb-105">이 항목에서는 PowerShell 갤러리에 게시하는 항목이 광범위하게 채택되어 사용자들이 더욱 유용하게 활용할 수 있도록 하기 위해 Microsoft 팀에서 사용하는 권장 단계에 대해 설명합니다. 이 항목의 설명은 PowerShell 갤러리에서 매니페스트 데이터를 처리하는 방식과 다수의 PowerShell 갤러리 사용자들이 제공한 피드백을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-105">This topic describes recommended steps used by Microsoft teams to ensure the items published to the PowerShell Gallery will be widely adopted and provide high value to users, based on how the PowerShell Gallery handles manifest data and on feedback from large numbers of PowerShell Gallery users.</span></span>
<span data-ttu-id="bf7bb-106">다음 지침에 따라 게시된 항목은 보다 많은 사용자가 설치하고 신뢰하며 관심을 가질 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-106">Items that are published following these guidelines will be more likely to be installed, trusted, and attract more users.</span></span>

<span data-ttu-id="bf7bb-107">아래에는 유용한 PowerShell 갤러리 항목을 만들기 위한 지침, 가장 중요한 선택적 매니페스트 설정, 초기 검토자와 [Powershell 스크립트 분석기](https://aka.ms/psscriptanalyzer)의 피드백을 반영하여 코드를 개선하는 방법, 공유한 항목의 사용 방법을 알려 주는 모듈/문서/테스트/예제의 버전을 관리하는 방법이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-107">Included below are guidelines for what makes a good PowerShell Gallery item, what optional Manifest settings are most important, improving your code with feedback from initial reviewers and [Powershell Script Analyzer](https://aka.ms/psscriptanalyzer), versioning your module, documentation, tests & examples for how to use what you have shared.</span></span>
<span data-ttu-id="bf7bb-108">이 문서의 대다수 내용은 [고품질 DSC 리소스 모듈](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md) 게시를 위한 지침을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-108">Much of this documentation follows the guidelines for publishing [High Quality DSC Resource Modules](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md).</span></span>

<span data-ttu-id="bf7bb-109">PowerShell 갤러리에 있는 항목을 게시하는 방법은 [항목 만들기 및 게시](https://msdn.microsoft.com/powershell/gallery/psgallery/creating-and-publishing-an-item)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-109">For the mechanics of publishing an item to the PowerShell Gallery, see [Creating and Publishing an Item](https://msdn.microsoft.com/powershell/gallery/psgallery/creating-and-publishing-an-item).</span></span>

<span data-ttu-id="bf7bb-110">이러한 지침에 대한 여러분의 피드백을 기다리고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-110">Feedback on these guidelines is welcomed.</span></span> <span data-ttu-id="bf7bb-111">피드백이 있는 경우 [Github 문서 리포지토리](https://github.com/powershell/powershell-docs/)에 해당 사안의 게시물을 작성하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-111">If you do have feedback, please open issues in our [Github documentation repository](https://github.com/powershell/powershell-docs/).</span></span>

## <a name="best-practices-for-publishing-items"></a><span data-ttu-id="bf7bb-112">항목 게시에 대한 모범 사례</span><span class="sxs-lookup"><span data-stu-id="bf7bb-112">Best practices for publishing items</span></span>

<span data-ttu-id="bf7bb-113">아래에는 PowerShell 갤러리 항목 사용자들이 중요하다고 생각하는 모범 사례가 명목상의 우선 순위 순서대로 나열되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-113">The following best practices are what the users of PowerShell Gallery items say is important, and are listed in nominal priority order.</span></span>
<span data-ttu-id="bf7bb-114">이러한 지침을 따르는 항목은 다른 사용자들이 다운로드하여 채택할 가능성이 훨씬 높습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-114">Items that follow these guidelines are far more likely to be downloaded and adopted by others.</span></span>

- <span data-ttu-id="bf7bb-115">PSScriptAnalyzer 사용</span><span class="sxs-lookup"><span data-stu-id="bf7bb-115">Use PSScriptAnalyzer</span></span>
- <span data-ttu-id="bf7bb-116">설명서와 예제 포함</span><span class="sxs-lookup"><span data-stu-id="bf7bb-116">Include documentation and examples</span></span>
- <span data-ttu-id="bf7bb-117">피드백에 적절하게 응답</span><span class="sxs-lookup"><span data-stu-id="bf7bb-117">Be responsive to feedback</span></span>
- <span data-ttu-id="bf7bb-118">스크립트가 아닌 모듈 제공</span><span class="sxs-lookup"><span data-stu-id="bf7bb-118">Provide modules rather than scripts</span></span>
- <span data-ttu-id="bf7bb-119">프로젝트 사이트에 대한 링크 제공</span><span class="sxs-lookup"><span data-stu-id="bf7bb-119">Provide links to a project site</span></span>
- <span data-ttu-id="bf7bb-120">모듈에 테스트 포함</span><span class="sxs-lookup"><span data-stu-id="bf7bb-120">Include tests with your modules</span></span>
- <span data-ttu-id="bf7bb-121">사용 조건 포함 및/또는 링크 제공</span><span class="sxs-lookup"><span data-stu-id="bf7bb-121">Include and/or link to license terms</span></span>
- <span data-ttu-id="bf7bb-122">코드 서명</span><span class="sxs-lookup"><span data-stu-id="bf7bb-122">Sign your code</span></span>
- <span data-ttu-id="bf7bb-123">버전 관리용 [SemVer](http://semver.org/) 지침 준수</span><span class="sxs-lookup"><span data-stu-id="bf7bb-123">Follow [SemVer](http://semver.org/) guidelines for versioning</span></span>
- <span data-ttu-id="bf7bb-124">일반 PowerShell 갤러리 태그에 설명되어 있는 일반 태그 사용</span><span class="sxs-lookup"><span data-stu-id="bf7bb-124">Use common tags, as documented in Common PowerShell Gallery tags</span></span>
- <span data-ttu-id="bf7bb-125">로컬 리포지토리를 사용하여 게시 테스트</span><span class="sxs-lookup"><span data-stu-id="bf7bb-125">Test publishing using a local repository</span></span>
- <span data-ttu-id="bf7bb-126">PowerShellGet을 사용하여 게시</span><span class="sxs-lookup"><span data-stu-id="bf7bb-126">Use PowerShellGet to publish</span></span>

<span data-ttu-id="bf7bb-127">아래 섹션에서는 이러한 각 모범 사례에 대해 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-127">Each of these is covered briefly in the sections below.</span></span>

## <a name="use-psscriptanalyzer"></a><span data-ttu-id="bf7bb-128">PSScriptAnalyzer 사용</span><span class="sxs-lookup"><span data-stu-id="bf7bb-128">Use PSScriptAnalyzer</span></span>

<span data-ttu-id="bf7bb-129">[PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer)는 PowerShell 코드에서 작동하는 무료 정적 코드 분석 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-129">[PSScriptAnalyzer](https://www.powershellgallery.com/packages/PSScriptAnalyzer) is a free static code analysis tool that works on PowerShell code.</span></span>
<span data-ttu-id="bf7bb-130">PowerShell 코드에서 가장 흔히 발생하는 문제를 식별하며, 권장 문제 해결 방법을 제공하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-130">PSScriptAnalyzer will identify the most common issues seen in PowerShell code, and often a recommendation for how to fix the issue.</span></span>
<span data-ttu-id="bf7bb-131">손쉽게 사용할 수 있는 이 도구는 문제를 오류(해결해야 하는 심각한 문제), 경고(검토하여 해결해야 하는 문제) 및 정보(모범 사례를 확인하면 좋은 문제)로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-131">The tool is easy to use, and categorizes the issues as Errors (severe, must be addressed), Warning (need to be reviewed & should be addressed), and Information (worth checking out for best practices).</span></span>
<span data-ttu-id="bf7bb-132">PowerShell 갤러리에 게시하는 모든 항목은 PSScriptAnalyzer를 통해 검사되며 오류가 소유자에게 다시 보고됩니다. 그러면 소유자는 오류를 해결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-132">All items item published to the PowerShell Gallery will be scanned using PSScriptAnalyzer, and any errors will be reported back to the owner and must be addressed.</span></span>

<span data-ttu-id="bf7bb-133">`-Recurse` 및 `-Severity` 경고를 포함하여 `Invoke-ScriptAnalyzer`를 실행하는 것이 모범 사례입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-133">The best practice is to run `Invoke-ScriptAnalyzer` with `-Recurse` and `-Severity` Warning.</span></span>

<span data-ttu-id="bf7bb-134">실행 후에는 결과를 검토하여 다음 사항을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-134">Review the results, and ensure that:</span></span>

- <span data-ttu-id="bf7bb-135">설명서에서 모든 오류를 수정했거나 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-135">All Errors are corrected or addressed in your documentation</span></span>
- <span data-ttu-id="bf7bb-136">해당하는 경우 모든 경고를 검토하고 해결했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-136">All Warnings are reviewed, and addressed where applicable</span></span>

<span data-ttu-id="bf7bb-137">PowerShell 갤러리에서 항목을 가져오는 사용자는 PSScriptAnalyzer를 실행하여 모든 오류와 경고를 평가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-137">Users who acquire items from the PowerShell Gallery are strongly encouraged to run PSScriptAnalyzer and evaluate all Errors and Warnings.</span></span>
<span data-ttu-id="bf7bb-138">사용자가 PSScriptAnalyzer에서 보고하는 오류가 있음을 확인하면 항목 소유자에게 문의할 가능성이 매우 높습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-138">Users are very likely to contact item owners if they see that there is an error reported by PSScriptAnalyzer.</span></span>
<span data-ttu-id="bf7bb-139">항목에서 오류로 플래그가 지정된 코드를 유지해야 하는 이유가 있다면 같은 질문에 여러 번 대답하지 않아도 되도록 설명서에 해당 정보를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-139">If there is a compelling reason for your item to keep code that is flagged as an error, add that information to your documentation to avoid having to answer the same question many times.</span></span>

## <a name="include-documentation-and-examples"></a><span data-ttu-id="bf7bb-140">설명서와 예제 포함</span><span class="sxs-lookup"><span data-stu-id="bf7bb-140">Include documentation and examples</span></span>

<span data-ttu-id="bf7bb-141">사용자가 공유 코드를 효율적으로 활용할 수 있도록 하는 가장 좋은 수단이 설명서 및 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-141">Documentation and examples are the best way to ensure users can take advantage of any shared code.</span></span>

<span data-ttu-id="bf7bb-142">설명서는 PowerShell 갤러리에 게시하는 항목에 포함할 수 있는 가장 유용한 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-142">Documentation is the most helpful thing to include in items published to the PowerShell Gallery.</span></span>
<span data-ttu-id="bf7bb-143">사용자는 대개 설명서가 없는 항목을 건너뛰며, 대신 코드를 확인함으로써 해당 항목 및 사용 방법에 대해 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-143">Users will generally bypass items without documentation, as the alternative is to read the code to understand what the item is and how to use it.</span></span>
<span data-ttu-id="bf7bb-144">PowerShell 항목과 함께 설명서를 제공하는 방법을 설명하는 다음과 같은 여러 MSDN 문서를 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-144">There are several articles available in MSDN on how to provide documentation with PowerShell items, including:</span></span>

- <span data-ttu-id="bf7bb-145">도움말 제공 관련 지침은 [cmdlet 작성 방법 도움말](https://go.microsoft.com/fwlink/?LinkID=123415)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-145">Guidelines for providing help are in [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415)</span></span>
- <span data-ttu-id="bf7bb-146">모든 PowerShell 스크립트, 함수 또는 cmdlet에 가장 유용한 항목인 cmdlet 도움말을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-146">Creating cmdlet help, which is the best approach for any PowerShell script, function, or cmdlet.</span></span>
  <span data-ttu-id="bf7bb-147">cmdlet 도움말을 작성하는 방법에 대한 자세한 내용을 확인하려면 MSDN 라이브러리에서 [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415)(Cmdlet 도움말을 작성하는 방법)를 먼저 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-147">For information about how to create cmdlet help, start with [How to Write Cmdlet Help](https://go.microsoft.com/fwlink/?LinkID=123415) in the MSDN library.</span></span>
  <span data-ttu-id="bf7bb-148">스크립트 내에 도움말을 추가하려면 [주석 기반 도움말 정보](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_comment_based_help)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-148">To add help within a script, see [About Comment Based Help](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_comment_based_help).</span></span>
- <span data-ttu-id="bf7bb-149">대부분의 모듈에는 Markdown 파일과 같이 텍스트 형식의 설명서도 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-149">Many modules also include documentation in text format, such as MarkDown files.</span></span>
  <span data-ttu-id="bf7bb-150">이러한 설명서는 Markdown이 많이 사용되는 Github에 프로젝트 사이트가 있는 경우 특히 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-150">This can be particularly helpful when there is a project site in Github, where Markdown is a heavily used format.</span></span>
  <span data-ttu-id="bf7bb-151">따라서 [Github 지원 Markdown](https://help.github.com/categories/writing-on-github/)을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-151">The best practice is to use [Github-flavored Markdown](https://help.github.com/categories/writing-on-github/)</span></span>

<span data-ttu-id="bf7bb-152">예제는 사용자에게 항목의 올바른 사용 방식을 제시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-152">Examples show users how the item is intended to be used.</span></span>
<span data-ttu-id="bf7bb-153">대부분의 개발자는 설명서보다 먼저 예제를 확인하여 특정 작업 수행 방법을 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-153">Many developers will say that they look at examples before documentation to understand how to use something.</span></span>
<span data-ttu-id="bf7bb-154">가장 효율적인 예제 유형은 기본적인 사용 방식과 실제 사용 사례 시뮬레이션을 제공하며, 코드 주석도 적절하게 작성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-154">The best type of examples show basic use, plus a simulated realistic use case, and the code is well-commented.</span></span>
<span data-ttu-id="bf7bb-155">PowerShell 갤러리에 게시하는 모듈의 예제는 모듈 루트 아래의 Examples 폴더에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-155">Examples for modules published to the PowerShell Gallery should be in an Examples folder under the module root.</span></span>

<span data-ttu-id="bf7bb-156">적절한 예제 패턴은 [PSDscResource 모듈](https://www.powershellgallery.com/packages/PSDscResources)의 Examples\RegistryResource 폴더에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-156">A good pattern for examples can be found in the [PSDscResource module](https://www.powershellgallery.com/packages/PSDscResources) under the Examples\RegistryResource folder.</span></span>
<span data-ttu-id="bf7bb-157">이 폴더에는 4가지 샘플 사용 사례가 포함되어 있으며, 각 파일의 맨 위에는 해당 사용 사례에서 제시하는 사용 방식의 간략한 설명이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-157">There are four sample use cases with a brief description at the top of each file that documents what is being demonstrated.</span></span>

## <a name="respond-to-feedback"></a><span data-ttu-id="bf7bb-158">피드백에 응답</span><span class="sxs-lookup"><span data-stu-id="bf7bb-158">Respond to feedback</span></span>

<span data-ttu-id="bf7bb-159">피드백에 적절하게 응답하는 항목 소유자는 커뮤니티에서 높은 평가를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-159">Item owners who respond properly to feedback are highly valued by the community.</span></span>
<span data-ttu-id="bf7bb-160">특정 항목에 관심이 많아 항목 개선을 지원하고자 하여 건설적인 피드백을 제공하는 사용자에게는 적절하게 응답을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-160">Users who provide constructive feedback are important to respond to, as they are interested enough in the item to try to help improve it.</span></span>

<span data-ttu-id="bf7bb-161">PowerShell 갤러리에서는 두 가지 피드백 방법이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-161">There are two feedback methods available in the PowerShell Gallery:</span></span>

- <span data-ttu-id="bf7bb-162">소유자에게 문의: 사용자가 항목 소유자에게 전자 메일을 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-162">Contact Owner: This allows a user to send an email to the item owner(s).</span></span> <span data-ttu-id="bf7bb-163">항목 소유자는 PowerShell 갤러리 항목에 사용하는 전자 메일 주소를 모니터링하여 제기되는 문제에 응답을 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-163">As an item owner, is important to monitor the email address used with the PowerShell Gallery items, and respond to issues that are raised.</span></span> <span data-ttu-id="bf7bb-164">이 방법의 한 가지 단점은, 사용자와 소유자만이 교환하는 의견을 확인할 수 있으므로 소유자가 같은 질문에 여러 번 대답해야 할 수도 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-164">The one disadvantage to this method is that only the user and owner will ever see the communication, so the owner may have to answer the same question many times.</span></span>
- <span data-ttu-id="bf7bb-165">댓글: 항목 페이지의 맨 아래에는 댓글 필드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-165">Comments: At the bottom of the item page is a Comment field.</span></span>
  <span data-ttu-id="bf7bb-166">이 시스템의 장점은 다른 사용자들도 댓글과 응답을 볼 수 있으므로 질문 하나에 대답해야 하는 횟수를 줄일 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-166">The advantage to this system is that other users can see the comments and responses, which reduces the number of times any single question must be answered.</span></span>
  <span data-ttu-id="bf7bb-167">항목 소유자는 각 항목에 대한 댓글을 항목에 반영하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-167">As an item owner, it is strongly recommended that you Follow the comments made for each item.</span></span>
<span data-ttu-id="bf7bb-168">자세한 방법은 [소셜 미디어나 댓글을 통해 피드백 제공](../how-to/working-with-items/social-media-feedback.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-168">See [Providing Feedback via Social Media or Comments](../how-to/working-with-items/social-media-feedback.md) for details on how to do that.</span></span>

<span data-ttu-id="bf7bb-169">피드백에 건설적인 방식으로 응답하는 소유자는 커뮤니티에서 높은 평가를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-169">Owners who respond to feedback constructively are appreciated by the community.</span></span>
<span data-ttu-id="bf7bb-170">보고서를 활용하여 필요에 따라 추가 정보를 요청하거나, 해결 방법을 제공하거나, 업데이트를 통해 문제가 해결되는지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-170">Use the opportunity in the report to request more information if needed, provide a workaround, or identify if an update fixes a problem.</span></span>

<span data-ttu-id="bf7bb-171">이러한 통신 채널에서 부적절한 행위가 확인되는 경우 PowerShell 갤러리의 신고하기 기능을 사용하여 갤러리 관리자에게 문의하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-171">If there is inappropriate behavior observed from either of these communication channels, use the Report Abuse feature of the PowerShell Gallery to contact the Gallery Administrators.</span></span>

## <a name="modules-versus-scripts"></a><span data-ttu-id="bf7bb-172">모듈과 스크립트 비교</span><span class="sxs-lookup"><span data-stu-id="bf7bb-172">Modules Versus Scripts</span></span>

<span data-ttu-id="bf7bb-173">다른 사용자와 스크립트를 공유하면 해당 사용자에게 발생했을 수 있는 문제를 해결하는 방법의 예를 제공할 수 있으므로 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-173">Sharing a script with other users is great, and provides others with examples of how to solve problems they may have.</span></span>
<span data-ttu-id="bf7bb-174">그런데 PowerShell 갤러리의 스크립트는 별도의 설명서, 예제 및 테스트가 없는 단일 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-174">The issue is that scripts in the PowerShell Gallery are single files without separate documentation, examples, and tests.</span></span>

<span data-ttu-id="bf7bb-175">반면 PowerShell 모듈은 여러 폴더와 파일을 패키지에 포함할 수 있는 폴더 구조로 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-175">PowerShell Modules have a folder structure that allows multiple folders and files to be included with the package.</span></span>
<span data-ttu-id="bf7bb-176">이러한 모듈 구조를 활용하면 앞에서 모범 사례로 언급한 cmdlet 도움말, 설명서, 예제, 테스트 등의 기타 항목을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-176">The module structure enables including the other items we list as best practices: cmdlet help, documentation, examples, and tests.</span></span>
<span data-ttu-id="bf7bb-177">모듈의 가장 큰 단점은, 모듈 내의 스크립트를 노출하여 함수로 사용해야 한다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-177">The biggest disadvantage is that a script inside a module must be exposed and used as a function.</span></span>
<span data-ttu-id="bf7bb-178">모듈을 작성하는 방법에 대한 자세한 내용은 [Windows PowerShell 모듈 작성](http://go.microsoft.com/fwlink/?LinkId=144916)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-178">For information on how to create a module, see [Writing a Windows PowerShell Module](http://go.microsoft.com/fwlink/?LinkId=144916).</span></span>

<span data-ttu-id="bf7bb-179">스크립트가 사용자에게 보다 효율적인 환경을 제공하는 상황, 특히 DSC 구성을 사용하는 경우가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-179">There are situations where a script provides a better experience for the user, particularly with DSC configurations.</span></span>
<span data-ttu-id="bf7bb-180">DSC 구성의 모범 사례는 문서, 예제, 테스트가 들어 있는 모듈을 포함하여 구성을 스크립트로 게시하는 것입니다. </span><span class="sxs-lookup"><span data-stu-id="bf7bb-180">The best practice for DSC configurations is to publish the configuration as a script with an accompanying module that contains the docs, examples, and tests.</span></span>
<span data-ttu-id="bf7bb-181">이 스크립트에서는 RequiredModules = @(모듈 이름) 형식을 사용하여 포함된 모듈이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-181">The script lists the accompanying module using RequiredModules = @(Name of the Module).</span></span>
<span data-ttu-id="bf7bb-182">모든 스크립트에서 이 방식을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-182">This approach can be used with any script.</span></span>

<span data-ttu-id="bf7bb-183">사용자에 따라서는 다른 모범 사례를 따르는 독립 실행형 스크립트가 더욱 유용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-183">Standalone scripts that follow the other best practices provide real value to other users.</span></span>
<span data-ttu-id="bf7bb-184">PowerShell 갤러리에 스크립트를 게시할 때는 주석 기반 설명서와 프로젝트 사이트 링크를 제공하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-184">Providing comment-based documentation and a link to a Project Site are highly recommended when publishing a script to the PowerShell Gallery.</span></span>

## <a name="provide-a-link-to-a-project-site"></a><span data-ttu-id="bf7bb-185">프로젝트 사이트에 대한 링크 제공</span><span class="sxs-lookup"><span data-stu-id="bf7bb-185">Provide a link to a project site</span></span>

<span data-ttu-id="bf7bb-186">프로젝트 사이트에서는 게시자가 PowerShell 갤러리 항목의 사용자와 직접 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-186">A Project Site is where a publisher can interact directly with the users of their PowerShell Gallery items.</span></span>
<span data-ttu-id="bf7bb-187">사용자는 이러한 링크를 제공하는 항목을 선호합니다. 링크를 통해 항목에 대한 정보를 보다 쉽게 파악할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-187">Users prefer items that provide this, as it allows them to get information about the item more easily.</span></span>
<span data-ttu-id="bf7bb-188">PowerShell 갤러리의 대다수 항목은 GitHub에서 개발되지만 웹 서비스 전문 조직에서 제공하는 항목도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-188">Many items in the PowerShell Gallery are developed in GitHub, others are provided by organizations with a dedicated web presence.</span></span>
<span data-ttu-id="bf7bb-189">이러한 각 조직을 프로젝트 사이트로 간주할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-189">Each of these can be considered a project site.</span></span>

<span data-ttu-id="bf7bb-190">다음과 같이 매니페스트의 PSData 섹션에 ProjectURI를 포함하는 방식으로 링크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-190">Adding a link is done by including ProjectURI in the PSData section of the manifest as follows:</span></span>

        # A URL to the main website for this project.
        ProjectUri = 'https://github.com/powershell/powershell'

<span data-ttu-id="bf7bb-191">ProjectURI를 제공하면 PowerShell 갤러리의 항목 페이지 왼쪽에 프로젝트 사이트 링크가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-191">When a ProjectURI is provided, the PowerShell Gallery will include a link to the Project Site on the left side of the item page.</span></span>

## <a name="include-tests"></a><span data-ttu-id="bf7bb-192">테스트 포함</span><span class="sxs-lookup"><span data-stu-id="bf7bb-192">Include tests</span></span>

<span data-ttu-id="bf7bb-193">사용자는 오픈 소스 코드를 사용하는 테스트가 항목에 포함되어 있는지를 중요하게 고려합니다. 테스트가 있으면 항목의 유효성이 검사되었음을 확인할 수 있으며 코드 작동 방식에 대한 정보를 파악할 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-193">Including tests with open-source code is important to users, as it gives them assurance about what you validate, and provides information on how your code works.</span></span> <span data-ttu-id="bf7bb-194">또한 사용자가 환경에 맞게 코드를 수정하더라도 원래 기능이 손상되지 않도록 유지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-194">It also allows users to ensure they do not break your original functionality if they modify your code to fit their environment.</span></span>

<span data-ttu-id="bf7bb-195">PowerShell 전용으로 설계된 Pester 테스트 프레임워크를 활용할 수 있도록 테스트를 작성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-195">It is strongly recommended that tests be written to take advantage of the Pester test framework, which has been designed specifically for PowerShell.</span></span>
<span data-ttu-id="bf7bb-196">Pester는 [GitHub](https://github.com/Pester/Pester) 및 [PowerShell 갤러리](https://www.powershellgallery.com/packages/Pester/)에서 제공되며 Windows 10, Windows Server 2016, WMF 5.0, WMF 5.1에 기본적으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-196">Pester is available in [GitHub](https://github.com/Pester/Pester), the [PowerShell Gallery](https://www.powershellgallery.com/packages/Pester/), and ships in Windows 10, Windows Server 2016, WMF 5.0 and WMF 5.1.</span></span>

<span data-ttu-id="bf7bb-197">[GitHub의 Pester 프로젝트 사이트](https://github.com/Pester/Pester)에는 Pester 테스트 작성을 시작하는 단계에서 모범 사례에 이르기까지 전 과정을 설명하는 유용한 설명서가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-197">The [Pester project site in GitHub](https://github.com/Pester/Pester) includes good documentation on writing Pester tests, from getting started to best practices.</span></span>

<span data-ttu-id="bf7bb-198">테스트 범위의 대상은 [고품질 리소스 모듈 설명서](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md)에 나와 있습니다. 단위 테스트 코드의 70%를 대상으로 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-198">The targets for test coverage are called out in the [High Quality Resource Module documentation](https://github.com/PowerShell/DscResources/blob/master/HighQualityModuleGuidelines.md), with 70% unit test code coverage recommended.</span></span>

## <a name="include-andor-link-to-license-terms"></a><span data-ttu-id="bf7bb-199">사용 조건 포함 및/또는 링크 제공</span><span class="sxs-lookup"><span data-stu-id="bf7bb-199">Include and/or link to license terms</span></span>

<span data-ttu-id="bf7bb-200">PowerShell 갤러리에 게시하는 모든 항목은 사용 조건을 지정하거나 [사용 약관](https://www.powershellgallery.com/policies/Terms)의 "증 A"에 포함된 라이선스에 따라 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-200">All items published to the PowerShell Gallery must specify the license terms, or be bound by the license included in the [Terms of Use](https://www.powershellgallery.com/policies/Terms) under "Exhibit A".</span></span>
<span data-ttu-id="bf7bb-201">다른 라이선스를 지정하는 가장 효율적인 방식은 PSData에서 LicenseURI를 사용하여 라이선스 링크를 제공하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-201">The best approach to specifying a different license is to provide a link to the license using the LicenseURI in PSData.</span></span>
<span data-ttu-id="bf7bb-202">해당 예제는 권장 매니페스트 필드 항목에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-202">You can find an example in the Recommended Manifest Fields topic.</span></span>

```powershell
PrivateData = @{
    PSData = @{

        # Tags applied to this module. These help with module discovery in online galleries.
        Tags = @('.net','acl','active-directory')

        # A URL to the license for this module.
        LicenseUri = 'http://www.apache.org/licenses/LICENSE-2.0'
```

## <a name="sign-your-code"></a><span data-ttu-id="bf7bb-203">코드 서명</span><span class="sxs-lookup"><span data-stu-id="bf7bb-203">Sign your code</span></span>

<span data-ttu-id="bf7bb-204">코드에 서명하면 사용자가 항목 게시자를 최대한 신뢰할 수 있으며 사용자가 다운로드하는 코드의 복사본이 게시자가 제공한 것과 정확히 일치함을 보장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-204">Code signing provides users with the highest level of assurance for who published the item, and that the copy of the code they acquire is exactly what the publisher released.</span></span>
<span data-ttu-id="bf7bb-205">코드 서명에 대해 전반적으로 자세히 알아보려면 [코드 서명 소개](http://go.microsoft.com/fwlink/?LinkId=106296)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-205">To learn more about code signing generally, see [Introduction to Code Signing](http://go.microsoft.com/fwlink/?LinkId=106296).</span></span>
<span data-ttu-id="bf7bb-206">PowerShell에서는 두 가지 기본적인 방식을 통한 코드 서명 유효성 검사를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-206">PowerShell supports validation of code signing through two primary approaches:</span></span>

- <span data-ttu-id="bf7bb-207">스크립트 파일 서명</span><span class="sxs-lookup"><span data-stu-id="bf7bb-207">Signing script files</span></span>
- <span data-ttu-id="bf7bb-208">모듈 카탈로그 서명</span><span class="sxs-lookup"><span data-stu-id="bf7bb-208">Catalog signing a module</span></span>

<span data-ttu-id="bf7bb-209">PowerShell 파일에 서명하면 실행하는 코드가 신뢰할 수 있는 출처에서 제작되었으며 수정되지 않았음을 효율적으로 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-209">Signing PowerShell files is a well-established approach to ensuring that the code being executed was produced by a reliable source, and has not been modified.</span></span>
<span data-ttu-id="bf7bb-210">PowerShell 스크립트 파일에 서명하는 방법에 대한 자세한 내용은 [서명 정보](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_signing) 항목에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-210">Details on how to sign PowerShell script files is covered in the [About Signing](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_signing) topic.</span></span>
<span data-ttu-id="bf7bb-211">요약하자면, 스크립트를 로드할 때 PowerShell에서 유효성을 검사하는 모든 .PS1 파일에 서명을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-211">In overview, a signature can be added to any .PS1 file that PowerShell validates when the script is loaded.</span></span>
<span data-ttu-id="bf7bb-212">[실행 정책](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_execution_policies) cmdlet을 사용하면 서명된 스크립트를 사용하도록 PowerShell을 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-212">PowerShell can be constrained using the [Execution Policy](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_execution_policies) cmdlets to ensure use of signed scripts.</span></span>

<span data-ttu-id="bf7bb-213">카탈로그 서명 모듈은 PowerShell 버전 5.1에 추가된 기능입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-213">Catalog signing modules is a feature added to PowerShell in version 5.1.</span></span>
<span data-ttu-id="bf7bb-214">모듈에 서명하는 방법은 [카탈로그 cmdlet](https://msdn.microsoft.com/powershell/wmf/5.1/catalog-cmdlets) 항목에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-214">How to sign a module is covered in the [Catalog Cmdlets](https://msdn.microsoft.com/powershell/wmf/5.1/catalog-cmdlets) topic.</span></span>
<span data-ttu-id="bf7bb-215">요약하자면, 모듈의 모든 파일에 대한 해시 값이 포함된 카탈로그 파일을 만들어 해당 파일에 서명하는 방식으로 카탈로그 서명을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-215">In overview, catalog signing is done by creating a catalog file, which contains a hash value for every file in the module, and then signing that file.</span></span>
<span data-ttu-id="bf7bb-216">그러면 PowerShellGet publish-module, install-module, save-module 및 update-module cmdlet이 서명을 점검하여 유효한지를 확인한 다음 각 항목의 해시 값이 카탈로그에 포함된 값과 일치하는지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-216">The PowerShellGet publish-module, install-module, save-module, and update-module cmdlets will check the signature to ensure it is valid, then confirm that the hash value for each item matches what is in the catalog.</span></span>
<span data-ttu-id="bf7bb-217">이전 버전의 모듈이 시스템에 설치되어 있으면 install-module은 새 버전의 서명 기관이 이전에 설치한 모듈의 기관과 일치하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-217">If a previous version of the module is installed on the system, install-module will confirm that the signing authority for the new version matches what was previously installed.</span></span>
<span data-ttu-id="bf7bb-218">카탈로그 서명 방식은 스크립트 파일 서명 방식과 함께 사용할 수는 있지만 대신 사용할 수는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-218">Catalog signing works with, but does not replace signing script files.</span></span> <span data-ttu-id="bf7bb-219">PowerShell은 모듈 로드 시에 카탈로그 서명의 유효성을 검사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-219">PowerShell does not validate catalog signatures at module load time.</span></span>

## <a name="follow-semver-guidelines-for-versioning"></a><span data-ttu-id="bf7bb-220">버전 관리용 SemVer 지침 준수</span><span class="sxs-lookup"><span data-stu-id="bf7bb-220">Follow SemVer guidelines for versioning</span></span>

<span data-ttu-id="bf7bb-221">[SemVer](http://semver.org/)는 변경 내용을 쉽게 해석할 수 있도록 버전 구성 및 변경 방법을 설명하는 공개 규칙입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-221">[SemVer](http://semver.org/) is a public convention that describes how to structure and change a version to allow easy intepretation of changes.</span></span>
<span data-ttu-id="bf7bb-222">항목 버전을 매니페스트 데이터에 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-222">The version for your item must be included in the manifest data.</span></span>

- <span data-ttu-id="bf7bb-223">버전은 0.1.1 또는 4.11.192와 같이 마침표로 구분된 숫자 블록 3개로 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-223">The version should be structured as 3 numeric blocks separated by periods, as in 0.1.1 or 4.11.192</span></span>
- <span data-ttu-id="bf7bb-224">버전이 "0"으로 시작하는 항목은 아직 프로덕션 환경에서 사용할 준비가 되지 않은 것입니다. 버전에서 숫자 "0"만 사용되는 경우에만 첫 번째 숫자를 "0"으로 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-224">Versions starting with "0" indicate that the item is not yet production ready, and the first number should only begin with "0" if that is the only number used</span></span>
- <span data-ttu-id="bf7bb-225">첫 번째 숫자가 1.9.9999에서 2.0.0으로 바뀌는 등 변경되는 경우 버전 간에 중요한 변경 내용이 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-225">Changes in the first number (1.9.9999 to 2.0.0) indicate major and breaking changes between the versions</span></span>
- <span data-ttu-id="bf7bb-226">두 번째 숫자가 1.01에서 1.02로 바뀌는 등 변경되는 경우에는 모듈에 새 cmdlet이 추가되는 등의 기능 수준 변경이 적용된 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-226">Changes to the second number (1.01 to 1.02) indicate feature-level changes, such as adding new cmdlets to a module</span></span>
- <span data-ttu-id="bf7bb-227">세 번째 숫자가 변경되는 경우에는 새 매개 변수, 업데이트된 샘플, 새 테스트 등의 일반적인 변경 내용이 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-227">Changes to the third number indicate non-breaking changes, such as new parameters, updated samples, or new tests</span></span>
- <span data-ttu-id="bf7bb-228">PowerShell은 버전을 나열할 때 버전을 문자열로 정렬하므로 1.01.0이 1.001.0보다 더 큰 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-228">When listing versions, PowerShell will sort the versions as strings, so 1.01.0 will be treated as greater than 1.001.0</span></span>

<span data-ttu-id="bf7bb-229">PowerShell은 SemVer가 게시되기 전에 제작되었으므로 SemVer의 대다수 요소를 지원하기는 하지만 다음과 같이 지원되지 않는 요소도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-229">PowerShell was created before SemVer was published, so it provides support for most but not all elements of SemVer, specifically:</span></span>

- <span data-ttu-id="bf7bb-230">버전 번호의 시험판 문자열은 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-230">It does not support prerelease strings in version numbers.</span></span> <span data-ttu-id="bf7bb-231">시험판 문자열은 게시자가 버전 1.0.0을 제공한 후 새 주 버전의 미리 보기 릴리스를 제공하려는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-231">This is useful when a publisher wishes to deliver a preview release of a new major version after providing a version 1.0.0.</span></span> <span data-ttu-id="bf7bb-232">이 요소는 향후 PowerShell 갤러리 릴리스와 PowerShellGet cmdlet에서 지원될 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-232">This will be supported in a future release of the PowerShell Gallery and PowerShellGet cmdlets.</span></span>
- <span data-ttu-id="bf7bb-233">PowerShell 및 PowerShell 갤러리에서는 세그먼트가 1개, 2개, 4개인 버전 문자열을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-233">PowerShell and the PowerShell Gallery allow version strings with 1, 2, and 4 segments.</span></span> <span data-ttu-id="bf7bb-234">대부분의 초기 모듈은 이 지침을 따르지 않으며, Microsoft에서 릴리스된 제품에는 빌드 정보가 5.1.14393.1066에서와 같이 네 번째 숫자 블록으로 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-234">Many early modules did not follow the guidelines, and product releases from Microsoft include build information as a 4th block of numbers (for example 5.1.14393.1066).</span></span> <span data-ttu-id="bf7bb-235">버전 관리 측면에서는 이러한 차이가 무시됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-235">From a versioning standpoint, these differences are ignored.</span></span>

## <a name="test-using-a-local-repository"></a><span data-ttu-id="bf7bb-236">로컬 리포지토리를 사용하여 테스트</span><span class="sxs-lookup"><span data-stu-id="bf7bb-236">Test using a local repository</span></span>

<span data-ttu-id="bf7bb-237">PowerShell 갤러리는 게시 프로세스를 테스트하기 위한 대상으로 설계되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-237">The PowerShell Gallery is not designed to be a target for testing the publishing process.</span></span>
<span data-ttu-id="bf7bb-238">PowerShell 갤러리에 대한 게시의 종단 간 프로세스를 테스트하는 가장 좋은 방법은 자체 로컬 리포지토리를 설정해서 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-238">The best way to test out the end-to-end process of publishing to the PowerShell Gallery is to set up and use your own local repository.</span></span>
<span data-ttu-id="bf7bb-239">이 작업은 다음과 같은 몇 가지 방법으로 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-239">This can be done in a few ways, including:</span></span>

- <span data-ttu-id="bf7bb-240">GitHub의 [PS 전용 갤러리 프로젝트](https://github.com/PowerShell/PSPrivateGallery)를 사용하여 로컬 PowerShell 갤러리 인스턴스를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-240">Set up a local PowerShell Gallery instance, using the [PS Private Gallery project](https://github.com/PowerShell/PSPrivateGallery) in Github.</span></span> <span data-ttu-id="bf7bb-241">이 미리 보기 프로젝트는 제어하고 테스트에 사용할 수 있는 PowerShell 갤러리 인스턴스를 설정하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-241">This preview project will help you set up an instance of the PowerShell Gallery that you can control, and use for your tests.</span></span>
- <span data-ttu-id="bf7bb-242">[내부 Nuget 리포지토리](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/)를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-242">Set up an [internal Nuget repository](https://blogs.msdn.microsoft.com/powershell/2014/05/20/setting-up-an-internal-powershellget-repository/).</span></span> <span data-ttu-id="bf7bb-243">이렇게 하려면 설정하기 위해 수행할 작업이 더 많지만, 더 많은 요구 사항의 유효성을 검사할 수 있는 이점이 있으며, 특히 API 키 사용 유효성 검사가 가능하며 게시할 때 대상에 종속성이 있는지를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-243">This will require more work to set up, but will have the advantage of validating a few more of the requirements, notably validating use of an API key, and whether or not dependencies are present in the target when you publish.</span></span>
- <span data-ttu-id="bf7bb-244">파일 공유를 테스트 “리포지토리”로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-244">Set up a file share as the test “repository”.</span></span> <span data-ttu-id="bf7bb-245">이 설정은 쉽지만, 파일 공유이므로 위에서 설명한 유효성 검사가 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-245">This is easy to set up, but since it is a file share, the validations noted above will not take place.</span></span> <span data-ttu-id="bf7bb-246">이 경우의 한 가지 잠재적 이점은 파일 공유에서 (필수) API 키를 확인하지 않으므로 PowerShell 갤러리에 게시하는 데 사용하는 키와 같은 키를 사용할 수 있다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-246">One potential advantage in this case is that the file share does not check the (required) API key, so you can use the same key you would to publish to the PowerShell Gallery.</span></span>

<span data-ttu-id="bf7bb-247">이러한 솔루션 중 원하는 솔루션을 사용하고 Register-PSRepository를 사용하여 Publish-Module의 -Repository 속성에 사용하는 새 “리포지토리”를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-247">With any of these solutions, use Register-PSRepository to define a new "repository", which you use in the -Repository property for Publish-Module.</span></span>

<span data-ttu-id="bf7bb-248">게시 테스트에 대한 한 가지 추가 사항: PowerShell 갤러리에 게시하는 모든 항목은 게시하려는 항목에 종속된 항목이 없음을 확인할 운영 팀의 도움 없이는 삭제할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-248">One additional point about test publishing: any item you publish to the PowerShell Gallery cannot be deleted without help from the operations team, who will confirm that nothing is dependent upon the item you wish to publish.</span></span>
<span data-ttu-id="bf7bb-249">이러한 이유로 Microsoft에서는 PowerShell 갤러리를 테스트 대상으로 지원하지 않으며 이렇게 하는 게시자에게 연락합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-249">For that reason, we do not support the PowerShell Gallery as a testing target, and will contact any publisher who does so.</span></span>

## <a name="use-powershellget-to-publish"></a><span data-ttu-id="bf7bb-250">PowerShellGet을 사용하여 게시</span><span class="sxs-lookup"><span data-stu-id="bf7bb-250">Use PowerShellGet to publish</span></span>

<span data-ttu-id="bf7bb-251">게시자는 PowerShell 갤러리로 작업할 때 Publish-Module 및 Publish-Script cmdlet을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-251">It is strongly recommended that publishers use the Publish-Module and Publish-Script cmdlets when working with the PowerShell Gallery.</span></span> <span data-ttu-id="bf7bb-252">PowerShell 갤러리에 게시할 때 중요한 설치 세부 정보를 저장하지 않아도 되도록 PowerShellGet이 고안되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-252">PowerShellGet has been created to help you avoid remembering important details about installing from an publishing to the PowerShell Gallery.</span></span> <span data-ttu-id="bf7bb-253">경우에 따라 게시자는 PowerShellGet을 건너뛰고, Publish-Module 대신 NuGet 클라이언트 또는 PackageManagement cmdlet을 사용하도록 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-253">On occasion, publishers have chosen to skip PowerShellGet and use the NuGet client, or PackageManagement cmdlets, instead of Publish-Module.</span></span> <span data-ttu-id="bf7bb-254">여러 세부 사항이 쉽게 누락되면서 다양한 지원 요청을 초래합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-254">There are a number of details that are easily missed, which results in a variety of support requests.</span></span>

<span data-ttu-id="bf7bb-255">Publish-Module 또는 Publish-Script를 사용할 수 없는 이유가 있는 경우 저희에게 알려주세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-255">If there is a reason that you cannot use Publish-Module or Publish-Script, please let us know.</span></span> <span data-ttu-id="bf7bb-256">PowerShellGet GitHub 리포지토리에서 문제를 정리하고 NuGet 또는 PackageManagement 중에서 선택하는 데 도움이 되는 세부 정보를 제공하세요.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-256">File an issue in the PowerShellGet GitHub repo, and provide the details that cause you to choose NuGet or PackageManagement.</span></span> 

## <a name="recommended-workflow"></a><span data-ttu-id="bf7bb-257">권장 워크플로</span><span class="sxs-lookup"><span data-stu-id="bf7bb-257">Recommended workflow</span></span>

<span data-ttu-id="bf7bb-258">PowerShell 갤러리에 게시하는 항목을 가장 효율적으로 활용할 수 있는 방식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-258">The most successful approach we have found for items published to the PowerShell Gallery is this:</span></span>

- <span data-ttu-id="bf7bb-259">오픈 소스 프로젝트 사이트에서 초기 개발을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-259">Do initial development in a an open-source project site.</span></span> <span data-ttu-id="bf7bb-260">PowerShell 팀은 Github를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-260">The PowerShell Team uses Github.</span></span>
- <span data-ttu-id="bf7bb-261">검토자와 [Powershell 스크립트 분석기](https://aka.ms/psscriptanalyzer)의 피드백을 활용하여 안정적인 상태의 코드를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-261">Use feedback from reviewers and [Powershell Script Analyzer](https://aka.ms/psscriptanalyzer) to get the code to stable state</span></span>
- <span data-ttu-id="bf7bb-262">다른 사용자들이 작업한 코드의 사용 방식을 알 수 있도록 설명서를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-262">Include documentation, so others know how to use your work</span></span>
- <span data-ttu-id="bf7bb-263">로컬 리포지토리를 사용하여 게시 작업을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-263">Test out the publishing action using a local repository.</span></span>
- <span data-ttu-id="bf7bb-264">프로젝트 사이트 링크와 설명서를 포함하여 안정적인 릴리스 또는 알파 릴리스를 PowerShell 갤러리에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-264">Publish a stable or Alpha release to the PowerShell Gallery, making sure to include the documentation and link to your project site</span></span>
- <span data-ttu-id="bf7bb-265">피드백을 수집하고 프로젝트 사이트에서 코드를 반복 실행해 본 다음 안정적인 업데이트를 PowerShell 갤러리에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-265">Gather feedback and iterate on the code in your project site, then publish stable updates to the PowerShell Gallery</span></span>
- <span data-ttu-id="bf7bb-266">프로젝트와 모듈에 예제 및 Pester 테스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-266">Add examples and Pester tests in your project and your module</span></span>
- <span data-ttu-id="bf7bb-267">항목에 코드로 서명할지를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-267">Decide if you want to code sign your item</span></span>
- <span data-ttu-id="bf7bb-268">프로젝트가 프로덕션 환경에서 사용할 수 있는 상태가 되면 1.0.0 버전을 PowerShell 갤러리에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-268">When you feel the project is ready to use in a production environment, publish a 1.0.0 version to the PowerShell Gallery</span></span>
- <span data-ttu-id="bf7bb-269">계속 피드백을 수집하고 사용자 입력 내용을 바탕으로 코드를 반복 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bf7bb-269">Continue to gather feedback and iterate on your code based on user input</span></span>

