---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: WMF 5.1의 향상된 PowerShell 엔진
ms.openlocfilehash: 738f72b910de7d44f48309013237d523d0dd40a4
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892895"
---
# <a name="powershell-engine-improvements"></a><span data-ttu-id="8f74a-103">향상된 PowerShell 엔진</span><span class="sxs-lookup"><span data-stu-id="8f74a-103">PowerShell Engine Improvements</span></span>

<span data-ttu-id="8f74a-104">WMF 5.1에서는 핵심 PowerShell 엔진에 대한 다음과 같은 개선 사항이 구현되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-104">The following improvements to the core PowerShell engine have been implemented in WMF 5.1:</span></span>

## <a name="performance"></a><span data-ttu-id="8f74a-105">성능</span><span class="sxs-lookup"><span data-stu-id="8f74a-105">Performance</span></span>

<span data-ttu-id="8f74a-106">몇 가지 중요한 영역에서 성능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-106">Performance has improved in some important areas:</span></span>

- <span data-ttu-id="8f74a-107">시작</span><span class="sxs-lookup"><span data-stu-id="8f74a-107">Startup</span></span>
- <span data-ttu-id="8f74a-108">`ForEach-Object` 및 `Where-Object`와 같은 cmdlet에 대한 파이프라이닝이 약 50% 더 빠릅니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-108">Pipelining to cmdlets like `ForEach-Object` and `Where-Object` is approximately 50% faster</span></span>

<span data-ttu-id="8f74a-109">몇 가지 예제 개선 사항(하드웨어에 따라 결과가 달라질 수 있음):</span><span class="sxs-lookup"><span data-stu-id="8f74a-109">Some example improvements (your results may vary depending on your hardware):</span></span>

| <span data-ttu-id="8f74a-110">시나리오</span><span class="sxs-lookup"><span data-stu-id="8f74a-110">Scenario</span></span> | <span data-ttu-id="8f74a-111">5.0 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="8f74a-111">5.0 Time (ms)</span></span> | <span data-ttu-id="8f74a-112">5.1 시간(밀리초)</span><span class="sxs-lookup"><span data-stu-id="8f74a-112">5.1 Time (ms)</span></span> |
| -------- | :---------------: | :---------------: |
| `powershell -command "echo 1"` | <span data-ttu-id="8f74a-113">900</span><span class="sxs-lookup"><span data-stu-id="8f74a-113">900</span></span> | <span data-ttu-id="8f74a-114">250</span><span class="sxs-lookup"><span data-stu-id="8f74a-114">250</span></span> |
| <span data-ttu-id="8f74a-115">처음 PowerShell 실행: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="8f74a-115">First ever PowerShell run: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="8f74a-116">30000</span><span class="sxs-lookup"><span data-stu-id="8f74a-116">30000</span></span> | <span data-ttu-id="8f74a-117">13000</span><span class="sxs-lookup"><span data-stu-id="8f74a-117">13000</span></span> |
| <span data-ttu-id="8f74a-118">빌드된 명령 분석 캐시: `powershell -command "Unknown-Command"`</span><span class="sxs-lookup"><span data-stu-id="8f74a-118">Command analysis cache built: `powershell -command "Unknown-Command"`</span></span> | <span data-ttu-id="8f74a-119">7000</span><span class="sxs-lookup"><span data-stu-id="8f74a-119">7000</span></span> | <span data-ttu-id="8f74a-120">520</span><span class="sxs-lookup"><span data-stu-id="8f74a-120">520</span></span> |
| <code>1..1000000 &#124; % { }</code> | <span data-ttu-id="8f74a-121">1400</span><span class="sxs-lookup"><span data-stu-id="8f74a-121">1400</span></span> | <span data-ttu-id="8f74a-122">750</span><span class="sxs-lookup"><span data-stu-id="8f74a-122">750</span></span> |

> [!Note]
> <span data-ttu-id="8f74a-123">시작과 관련된 한 가지 변경이 몇 가지 지원되지 않는 시나리오에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-123">One change related to startup might impact some unsupported scenarios.</span></span>
> <span data-ttu-id="8f74a-124">PowerShell은 더 이상 `$pshome\*.ps1xml` 파일을 읽지 않습니다. XML 파일 처리의 일부 파일 및 CPU 오버헤드를 방지하기 위해 이러한 파일이 C#으로 변환되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-124">PowerShell no longer reads the files `$pshome\*.ps1xml` -- these files have been converted to C# to avoid some file and CPU overhead of processing the XML files.</span></span>
> <span data-ttu-id="8f74a-125">이러한 파일은 V2를 나란히 지원하기 위해 여전이 있으므로 파일 콘텐츠를 변경하는 경우 V5에는 아무 영향이 없고 V2에만 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-125">The files still exist to support V2 side-by-side, so if you change the file contents, it will not have any effect to V5, only V2.</span></span>
> <span data-ttu-id="8f74a-126">이러한 파일의 콘텐츠를 변경하는 시나리오는 지원되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-126">Note that changing the contents of these files was never a supported scenario.</span></span>

<span data-ttu-id="8f74a-127">또 하나의 뚜렷한 변경 사항은 PowerShell이 시스템에 설치된 모듈에 대해 내보낸 명령 및 기타 정보를 캐시하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-127">Another visible change is how PowerShell caches the exported commands and other information for modules that are installed on a system.</span></span>
<span data-ttu-id="8f74a-128">이전에는 이 캐시가 `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis` 디렉터리에 저장되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-128">Previously, this cache was stored in the directory `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\CommandAnalysis`.</span></span>
<span data-ttu-id="8f74a-129">WMF 5.1에서 이 캐시는 단일 파일 `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`입니다.</span><span class="sxs-lookup"><span data-stu-id="8f74a-129">In WMF 5.1, the cache is a single file `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.</span></span>
<span data-ttu-id="8f74a-130">자세한 내용은 [모듈 분석 캐시](scenarios-features.md#module-analysis-cache)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8f74a-130">See [Module Analysis Cache](scenarios-features.md#module-analysis-cache) for more details.</span></span>