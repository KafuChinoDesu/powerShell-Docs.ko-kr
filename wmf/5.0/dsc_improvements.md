---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: b2f50b9cbab792390dae8f37163873c5bf759089
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-in-desired-state-configuration-dsc"></a><span data-ttu-id="53520-102">DSC(원하는 상태 구성)의 향상된 기능</span><span class="sxs-lookup"><span data-stu-id="53520-102">Improvements in Desired State Configuration (DSC)</span></span>

## <a name="dsc-feedback-survey"></a><span data-ttu-id="53520-103">DSC 사용자 의견 설문 조사</span><span class="sxs-lookup"><span data-stu-id="53520-103">DSC Feedback Survey</span></span>

<span data-ttu-id="53520-104">새 PowerShell 원하는 상태 구성 기능 및 이 릴리스에서 도입된 기능을 사용하는 데 시간이 조금 걸린다면 간단한 [WMF 5.0 RTM survey(WMF 5.0 RTM 설문 조사)](https://www.surveymonkey.com/r/SGLQM5W)를 수행하여 지속적인 제품 품질 향상 노력에 도움을 주시기 바랍니다.</span><span class="sxs-lookup"><span data-stu-id="53520-104">Once you have had some time to use the new PowerShell Desired State Configuration features and functionality introduced in this release, please help us continue making the product better by taking a quick [WMF 5.0 RTM survey](https://www.surveymonkey.com/r/SGLQM5W).</span></span> <span data-ttu-id="53520-105">이 설문 조사를 통해 이러한 새 기능에 대한 사용자 의견을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53520-105">This survey will allow you to share your feedback about these new features and functionality.</span></span>

<span data-ttu-id="53520-106">설문 조사에 참여해 주셔서 감사합니다.</span><span class="sxs-lookup"><span data-stu-id="53520-106">Thank you for participating in our survey!</span></span> <span data-ttu-id="53520-107">사용자 의견은 제품의 품질 향상에 큰 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="53520-107">Your feedback is very important to us.</span></span>

<span data-ttu-id="53520-108">**PSDesiredStateConfiguration 모듈 버전이 1.1로 업데이트됨**</span><span class="sxs-lookup"><span data-stu-id="53520-108">**PSDesiredStateConfiguration module version updated to 1.1**</span></span>

<span data-ttu-id="53520-109">PsDesiredStateConfiguration의 모듈 버전이 1.1로 업데이트되었습니다.</span><span class="sxs-lookup"><span data-stu-id="53520-109">The module version of PsDesiredStateConfiguration has been updated to 1.1.</span></span> <span data-ttu-id="53520-110">WMF 5.0 Preview 2015년 2월 이전 버전에서 컴파일된 DSC 구성은 PowerShell/WMF 5.0에서 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="53520-110">DSC configurations compiled on WMF 5.0 Preview Feb 2015 or earlier will not work on PowerShell/WMF 5.0.</span></span>