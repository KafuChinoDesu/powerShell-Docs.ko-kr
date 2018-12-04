---
ms.date: 09/11/2018
contributor: JKeithB
keywords: gallery,powershell,psgallery
title: 수동 패키지 다운로드
ms.openlocfilehash: 57baa14089b803f58c42ccb54553ecace841e34b
ms.sourcegitcommit: e24525046dd37166b9d83eeecdc534726316f429
ms.translationtype: MTE95
ms.contentlocale: ko-KR
ms.lasthandoff: 12/01/2018
ms.locfileid: "52742825"
---
# <a name="manual-package-download"></a><span data-ttu-id="5122c-103">수동 패키지 다운로드</span><span class="sxs-lookup"><span data-stu-id="5122c-103">Manual Package Download</span></span>

<span data-ttu-id="5122c-104">PowerShell 갤러리는 PowerShellGet cmdlet을 사용하지 않고 웹 사이트에서 패키지를 직접 다운로드하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-104">The Powershell Gallery supports downloading a package from the website directly, without using the PowerShellGet cmdlets.</span></span> <span data-ttu-id="5122c-105">내부 저장소에 복사할 수 있습니다는 NuGet 패키지 (.nupkg) 파일과 모든 패키지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-105">You can download any package as a NuGet package (.nupkg) file, which you can then copy to an internal repository.</span></span>

> [!NOTE]
> <span data-ttu-id="5122c-106">수동 패키지 다운로드는 Install-Module cmdlet을 대체하기 위한 것이 **아닙니다**.</span><span class="sxs-lookup"><span data-stu-id="5122c-106">Manual package download is **not** intended as a replacement for the Install-Module cmdlet.</span></span>
> <span data-ttu-id="5122c-107">패키지를 다운로드해도 모듈이나 스크립트는 설치되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-107">Downloading the package does not install the module or script.</span></span> <span data-ttu-id="5122c-108">종속성은 다운로드한 NuGet 패키지에 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-108">Dependencies are not included in the NuGet package downloaded.</span></span> <span data-ttu-id="5122c-109">다음은 참조 목적으로만 제공되는 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-109">The following instructions are provided for reference purposes only.</span></span>

## <a name="using-manual-download-to-acquire-a-package"></a><span data-ttu-id="5122c-110">수동 다운로드를 사용하여 패키지 가져오기</span><span class="sxs-lookup"><span data-stu-id="5122c-110">Using manual download to acquire a package</span></span>

<span data-ttu-id="5122c-111">각 페이지에는 다음과 같은 [수동 다운로드] 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-111">Each page has a link for Manual Download, as shown here:</span></span>

![수동 다운로드](../../Images/packagedisplaypagewithpseditions.png)

<span data-ttu-id="5122c-113">수동으로 다운로드하려면 **원시 nupkg 파일 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-113">To download manually, click on **Download the raw nupkg file**.</span></span> <span data-ttu-id="5122c-114">이 파일은 이름이 `<name>.<version>.nupkg`인 브라우저의 다운로드 폴더에 복사된 패키지의 복사본입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-114">A copy of the package copied to the download folder for your browser with the name `<name>.<version>.nupkg`.</span></span>

<span data-ttu-id="5122c-115">NuGet 패키지는 패키지의 콘텐츠에 대한 정보가 포함된 추가 파일이 있는 ZIP 보관 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-115">A NuGet package is a ZIP archive with extra files containing information about the contents of the package.</span></span> <span data-ttu-id="5122c-116">Internet Explorer와 같은 일부 브라우저에서는 자동으로 `.nupkg` 파일 확장명을 `.zip`으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-116">Some browsers, like Internet Explorer, automatically replace the `.nupkg` file extension with `.zip`.</span></span> <span data-ttu-id="5122c-117">패키지를 확장하려면 필요한 경우 `.nupkg` 파일의 이름을 `.zip`으로 바꾼 다음, 로컬 폴더에 콘텐츠를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-117">To expand the package, rename the `.nupkg` file to `.zip`, if needed, then extract the contents to a local folder.</span></span>

<span data-ttu-id="5122c-118">NuGet 패키지 파일에는 원래 패키지된 코드의 일부가 아닌 다음 NuGet 관련 요소가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-118">A NuGet package file includes the following NuGet-specific elements that aren't part of the original packaged code:</span></span>

- <span data-ttu-id="5122c-119">`_rels` 폴더 - 종속성을 나열하는 `.rels` 파일이 있습니다</span><span class="sxs-lookup"><span data-stu-id="5122c-119">A folder named `_rels` - contains a `.rels` file that lists the dependencies</span></span>
- <span data-ttu-id="5122c-120">`package` 폴더 - NuGet 관련 데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-120">A folder named `package` - contains the NuGet-specific data</span></span>
- <span data-ttu-id="5122c-121">`[Content_Types].xml` 파일 - PowerShellGet과 같은 확장명이 NuGet에서 작동하는 방식을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-121">A file named `[Content_Types].xml` - describes how extensions like PowerShellGet work with NuGet</span></span>
- <span data-ttu-id="5122c-122">`<name>.nuspec` 파일 - 대량의 메타데이터가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-122">A file named `<name>.nuspec` - contains the bulk of the metadata</span></span>

## <a name="installing-powershell-modules-from-a-nuget-package"></a><span data-ttu-id="5122c-123">NuGet 패키지에서 PowerShell 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="5122c-123">Installing PowerShell Modules from a NuGet package</span></span>

> [!NOTE]
> <span data-ttu-id="5122c-124">이러한 지침은 `Install-Module`을 실행하는 것과 동일한 결과를 **제공하지 않으며**,</span><span class="sxs-lookup"><span data-stu-id="5122c-124">These instructions **DO NOT** give the same result as running `Install-Module`.</span></span> <span data-ttu-id="5122c-125">최소 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-125">These instructions fulfill the minimum requirements.</span></span> <span data-ttu-id="5122c-126">`Install-Module`을 대체하기 위한 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-126">They are not intended to be a replacement for `Install-Module`.</span></span> <span data-ttu-id="5122c-127">`Install-Module`에서 수행되는 일부 단계는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-127">Some steps performed by `Install-Module` are not included.</span></span>

<span data-ttu-id="5122c-128">가장 쉬운 방법은 폴더에서 NuGet 관련 요소를 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-128">The easiest approach is to remove the NuGet-specific elements from the folder.</span></span> <span data-ttu-id="5122c-129">그러면 패키지 작성자가 만든 PowerShell 코드가 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-129">This leaves the PowerShell code created by the package author.</span></span> <span data-ttu-id="5122c-130">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-130">The steps are:</span></span>

1. <span data-ttu-id="5122c-131">로컬 폴더에 NuGet 패키지의 콘텐츠를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-131">Extract the contents of the NuGet package to a local folder.</span></span>
2. <span data-ttu-id="5122c-132">폴더에서 NuGet 관련 요소를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-132">Delete the NuGet-specific elements from the folder.</span></span>
3. <span data-ttu-id="5122c-133">폴더 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-133">Rename the folder.</span></span> <span data-ttu-id="5122c-134">기본 폴더 이름은 일반적으로 `<name>.<version>`입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-134">The default folder name is usually `<name>.<version>`.</span></span> <span data-ttu-id="5122c-135">태그가 시험판 버전으로 지정된 모듈인 경우 버전에 "-prerelease"가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-135">The version can include "-prerelease" if the module is tagged as a prerelease version.</span></span> <span data-ttu-id="5122c-136">폴더 이름을 모듈 이름으로만 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-136">Rename the folder to just the module name.</span></span> <span data-ttu-id="5122c-137">예를 들어 "azurerm.storage.5.0.4-preview"는 "azurerm.storage"가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-137">For example, "azurerm.storage.5.0.4-preview" becomes "azurerm.storage".</span></span>
4. <span data-ttu-id="5122c-138">폴더의 폴더 중 하나를 복사 합니다 `$env:PSModulePath value`합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-138">Copy the folder to one of the folders in the `$env:PSModulePath value`.</span></span> <span data-ttu-id="5122c-139">`$env:PSModulePath` 세미콜론으로 구분 된 집합 모듈에 대 한 PowerShell 같아야 하는 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-139">`$env:PSModulePath` is a semicolon delimited set of paths in which PowerShell should look for modules.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5122c-140">수동 다운로드에는 모듈에 필요한 종속성이 모두 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-140">The manual download does not include any dependencies required by the module.</span></span> <span data-ttu-id="5122c-141">패키지에 종속성이 있는 경우 이 모듈이 제대로 작동하려면 시스템에 해당 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-141">If the package has dependencies, they must be installed on the system for this module to work correctly.</span></span> <span data-ttu-id="5122c-142">PowerShell 갤러리에는 패키지에 필요한 모든 종속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-142">The PowerShell Gallery shows all dependencies required by the package.</span></span>

## <a name="installing-powershell-scripts-from-a-nuget-package"></a><span data-ttu-id="5122c-143">NuGet 패키지에서 PowerShell 스크립트 설치</span><span class="sxs-lookup"><span data-stu-id="5122c-143">Installing PowerShell Scripts from a NuGet package</span></span>

> [!NOTE]
> <span data-ttu-id="5122c-144">이러한 지침은 `Install-Script`를 실행하는 것과 동일한 결과를 **제공하지 않으며**,</span><span class="sxs-lookup"><span data-stu-id="5122c-144">These instructions **DO NOT** give the same result as running `Install-Script`.</span></span> <span data-ttu-id="5122c-145">최소 요구 사항을 충족합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-145">These instructions fulfill the minimum requirements.</span></span> <span data-ttu-id="5122c-146">`Install-Script`를 대체하기 위한 것이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-146">They are not intended to be a replacement for `Install-Script`.</span></span>

<span data-ttu-id="5122c-147">가장 쉬운 방법은 NuGet 패키지를 추출한 다음, 스크립트를 직접 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-147">The easiest approach is to extract the NuGet package, then use the script directly.</span></span> <span data-ttu-id="5122c-148">단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-148">The steps are:</span></span>

1. <span data-ttu-id="5122c-149">NuGet 패키지의 콘텐츠를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-149">Extract the contents of the NuGet package.</span></span>
2. <span data-ttu-id="5122c-150">폴더의 `.PS1` 파일을 이 위치에서 직접 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-150">The `.PS1` file in the folder can be used directly from this location.</span></span>
3. <span data-ttu-id="5122c-151">폴더에 있는 NuGet 관련 요소를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-151">You may delete the NuGet-specific elements in the folder.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5122c-152">수동 다운로드에는 모듈에 필요한 종속성이 모두 포함되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-152">The manual download does not include any dependencies required by the module.</span></span> <span data-ttu-id="5122c-153">패키지에 종속성이 있는 경우 이 모듈이 제대로 작동하려면 시스템에 해당 패키지를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-153">If the package has dependencies, they must be installed on the system for this module to work correctly.</span></span> <span data-ttu-id="5122c-154">PowerShell 갤러리에는 패키지에 필요한 모든 종속성이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5122c-154">The PowerShell Gallery shows all dependencies required by the package.</span></span>
