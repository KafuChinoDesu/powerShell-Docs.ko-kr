---
title: Windows PowerShell 모듈 이해 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: d4e38235-9987-4347-afd2-0f7d1dc8f64a
caps.latest.revision: 19
ms.openlocfilehash: b42ba6b2bf42a74213eb78f2db22e16de7e90583
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72360642"
---
# <a name="understanding-a-windows-powershell-module"></a><span data-ttu-id="3f65f-102">Windows PowerShell 모듈 이해</span><span class="sxs-lookup"><span data-stu-id="3f65f-102">Understanding a Windows PowerShell Module</span></span>

<span data-ttu-id="3f65f-103">*모듈* 은 편리한 단위 (일반적으로 단일 디렉터리에 저장 됨)로 함께 그룹화 된 관련 Windows PowerShell 기능의 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-103">A *module* is a set of related Windows PowerShell functionalities, grouped together as a convenient unit (usually saved in a single directory).</span></span> <span data-ttu-id="3f65f-104">관련 스크립트 파일, 어셈블리 및 관련 리소스 집합을 모듈로 정의 하면 코드를 더 쉽게 참조, 로드, 유지 및 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-104">By defining a set of related script files, assemblies, and related resources as a module, you can reference, load, persist, and share your code much easier than you would otherwise.</span></span>

<span data-ttu-id="3f65f-105">모듈의 주요 목적은 Windows PowerShell 코드의 모듈화 (ie, 재사용 및 추상화)를 허용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-105">The main purpose of a module is to allow the modularization (ie, reuse and abstraction) of Windows PowerShell code.</span></span> <span data-ttu-id="3f65f-106">예를 들어 모듈을 만드는 가장 기본적인 방법은 Windows PowerShell 스크립트를 .psm1 파일로 저장 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-106">For example, the most basic way of creating a module is to simply save a Windows PowerShell script as a .psm1 file.</span></span> <span data-ttu-id="3f65f-107">이렇게 하면 스크립트에 포함 된 함수 및 변수를 제어할 수 있습니다 (즉, 공용 또는 개인으로 설정).</span><span class="sxs-lookup"><span data-stu-id="3f65f-107">Doing so allows you to control (ie, make public or private) the functions and variables contained in the script.</span></span> <span data-ttu-id="3f65f-108">스크립트를 .psm1 파일로 저장 하면 특정 변수의 범위를 제어할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-108">Saving the script as a .psm1 file also allows you to control the scope of certain variables.</span></span> <span data-ttu-id="3f65f-109">마지막으로, [모듈](/powershell/module/PowershellGet/Install-Module) 등의 cmdlet을 사용 하 여 스크립트를 구성 하 고, 설치 하 고, 더 큰 솔루션의 구성 요소로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-109">Finally, you can also use cmdlets such as [Install-Module](/powershell/module/PowershellGet/Install-Module) to organize, install, and use your script as building blocks for larger solutions.</span></span>

## <a name="module-components-and-types"></a><span data-ttu-id="3f65f-110">모듈 구성 요소 및 유형</span><span class="sxs-lookup"><span data-stu-id="3f65f-110">Module Components and Types</span></span>

<span data-ttu-id="3f65f-111">모듈은 네 가지 기본 구성 요소로 구성 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-111">A module is made up of four basic components:</span></span>

1. <span data-ttu-id="3f65f-112">일종의 코드 파일-일반적으로 PowerShell 스크립트나 관리 되는 cmdlet 어셈블리입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-112">Some sort of code file - usually either a PowerShell script or a managed cmdlet assembly.</span></span>

2. <span data-ttu-id="3f65f-113">추가 어셈블리, 도움말 파일 또는 스크립트와 같이 위의 코드 파일에 필요할 수 있는 다른 모든 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-113">Anything else that the above code file may need, such as additional assemblies, help files, or scripts.</span></span>

3. <span data-ttu-id="3f65f-114">위의 파일을 설명 하는 매니페스트 파일 뿐만 아니라 작성자 및 버전 관리 정보와 같은 메타 데이터를 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-114">A manifest file that describes the above files, as well as stores metadata such as author and versioning information.</span></span>

4. <span data-ttu-id="3f65f-115">위의 모든 콘텐츠를 포함 하는 디렉터리 이며 PowerShell에서 적절 하 게 찾을 수 있는 위치에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-115">A directory that contains all of the above content, and is located where PowerShell can reasonably find it.</span></span>

   <span data-ttu-id="3f65f-116">이러한 구성 요소는 실제로 실제로 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-116">Note that none of these components, by themselves, are actually necessary.</span></span> <span data-ttu-id="3f65f-117">예를 들어 모듈은 기술적으로 .psm1 파일에 저장 된 스크립트만 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-117">For example, a module can technically be only a script stored in a .psm1 file.</span></span> <span data-ttu-id="3f65f-118">구성 용도로 주로 사용 되는 매니페스트 파일은 아니지만 모듈을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-118">You can also have a module that is nothing but a manifest file, which is used mainly for organizational purposes.</span></span> <span data-ttu-id="3f65f-119">또한 모듈을 동적으로 만드는 스크립트를 작성할 수 있으며,이 경우에는 실제로 아무것도 저장할 디렉터리가 필요 하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-119">You can also write a script that dynamically creates a module, and as such doesn't actually need a directory to store anything in.</span></span> <span data-ttu-id="3f65f-120">다음 섹션에서는 모듈의 가능한 여러 부분을 함께 결합 하 고 일치 시켜 가져올 수 있는 모듈의 유형에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-120">The following sections describe the types of modules you can get by mixing and matching the different possible parts of a module together.</span></span>

### <a name="script-modules"></a><span data-ttu-id="3f65f-121">스크립트 모듈</span><span class="sxs-lookup"><span data-stu-id="3f65f-121">Script Modules</span></span>

<span data-ttu-id="3f65f-122">이름에서 알 수 있듯이 *스크립트 모듈* 은 유효한 Windows PowerShell 코드를 포함 하는 파일 (. .psm1)입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-122">As the name implies, a *script module* is a file (.psm1) that contains any valid Windows PowerShell code.</span></span> <span data-ttu-id="3f65f-123">스크립트 개발자와 관리자는이 유형의 모듈을 사용 하 여 해당 멤버에 함수, 변수 등이 포함 된 모듈을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-123">Script developers and administrators can use this type of module to create modules whose members include functions, variables, and more.</span></span> <span data-ttu-id="3f65f-124">그와 동시에 스크립트 모듈은 관리자가 가져오기, 내보내기 및 관리 기능을 사용할 수 있도록 하는 확장명이 다른 Windows PowerShell 스크립트입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-124">At heart, a script module is simply a Windows PowerShell script with a different extension, which allows administrators to use import, export, and management functions on it.</span></span>

<span data-ttu-id="3f65f-125">또한 매니페스트 파일을 사용 하 여 데이터 파일, 기타 종속 모듈 또는 런타임 스크립트와 같은 다른 리소스를 모듈에 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-125">In addition, you can use a manifest file to include other resources in your module, such as data files, other dependent modules, or runtime scripts.</span></span> <span data-ttu-id="3f65f-126">매니페스트 파일은 작성 및 버전 관리 정보와 같은 메타 데이터를 추적 하는 데에도 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-126">Manifest files are also useful for tracking metadata such as authoring and versioning information.</span></span>

<span data-ttu-id="3f65f-127">마지막으로, 동적으로 생성 되지 않은 다른 모듈과 마찬가지로 스크립트 모듈은 PowerShell에서 합리적으로 검색할 수 있는 폴더에 저장 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-127">Finally, a script module, like any other module that isn't dynamically created, needs to be saved in a folder that PowerShell can reasonably discover.</span></span> <span data-ttu-id="3f65f-128">일반적으로 PowerShell 모듈 경로에 있습니다. 그러나 필요한 경우 모듈이 설치 된 위치를 명시적으로 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-128">Usually, this is on the PowerShell module path; but if necessary you can explicitly describe where your module is installed.</span></span> <span data-ttu-id="3f65f-129">자세한 내용은 [PowerShell 스크립트 모듈을 작성 하는 방법](./how-to-write-a-powershell-script-module.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3f65f-129">For more information, see [How to Write a PowerShell Script Module](./how-to-write-a-powershell-script-module.md).</span></span>

### <a name="binary-modules"></a><span data-ttu-id="3f65f-130">이진 모듈</span><span class="sxs-lookup"><span data-stu-id="3f65f-130">Binary Modules</span></span>

<span data-ttu-id="3f65f-131">*이진 모듈* 은와 C#같은 컴파일된 코드를 포함 하는 .NET Framework 어셈블리 (.dll)입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-131">A *binary module* is a .NET Framework assembly (.dll) that contains compiled code, such as C#.</span></span> <span data-ttu-id="3f65f-132">Cmdlet 개발자는이 유형의 모듈을 사용 하 여 cmdlet, 공급자 등을 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-132">Cmdlet developers can use this type of module to share cmdlets, providers, and more.</span></span> <span data-ttu-id="3f65f-133">(기존 스냅인을 이진 모듈로 사용할 수도 있습니다.) 스크립트 모듈과 비교할 때 이진 모듈을 사용 하면 Windows PowerShell 스크립트에서 코드를 사용 하는 것이 쉽지 않은 더 빠른 cmdlet (예: 다중 스레딩)을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-133">(Existing snap-ins can also be used as binary modules.) Compared to a script module, a binary module allows you to create cmdlets that are faster or use features (such as multithreading) that are not as easy to code in Windows PowerShell scripts.</span></span>

<span data-ttu-id="3f65f-134">스크립트 모듈과 마찬가지로 매니페스트 파일을 포함 하 여 모듈에서 사용 하는 추가 리소스를 설명 하 고 모듈에 대 한 메타 데이터를 추적할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-134">As with script modules, you can include a manifest file to describe additional resources that your module uses, and to track metadata about your module.</span></span> <span data-ttu-id="3f65f-135">마찬가지로, PowerShell 모듈 경로를 따라 어딘가에 있는 폴더에 이진 모듈을 설치 해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-135">Similarly, you probably should install your binary module in a folder somewhere along the PowerShell module path.</span></span> <span data-ttu-id="3f65f-136">자세한 내용은 [PowerShell 이진 모듈을 작성](./how-to-write-a-powershell-binary-module.md)하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3f65f-136">For more information, see How to [How to Write a PowerShell Binary Module](./how-to-write-a-powershell-binary-module.md).</span></span>

### <a name="manifest-modules"></a><span data-ttu-id="3f65f-137">매니페스트 모듈</span><span class="sxs-lookup"><span data-stu-id="3f65f-137">Manifest Modules</span></span>

<span data-ttu-id="3f65f-138">*매니페스트 모듈* 은 매니페스트 파일을 사용 하 여 모든 구성 요소를 설명 하지만 어떠한 종류의 핵심 어셈블리나 스크립트도 포함 하지 않는 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-138">A *manifest module* is a module that uses a manifest file to describe all of its components, but doesn't have any sort of core assembly or script.</span></span> <span data-ttu-id="3f65f-139">(공식적으로 매니페스트 모듈은 매니페스트의 `ModuleToProcess` 또는 `RootModule` 요소를 비워 둡니다.) 그러나 종속 어셈블리를 로드 하거나 특정 전처리 스크립트를 자동으로 실행 하는 기능과 같은 모듈의 다른 기능을 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-139">(Formally, a manifest module leaves the `ModuleToProcess` or `RootModule` element of the manifest empty.) However, you can still use the other features of a module, such as the ability to load up dependent assemblies or automatically run certain pre-processing scripts.</span></span> <span data-ttu-id="3f65f-140">매니페스트 모듈을 사용 하 여 다른 모듈에서 사용할 리소스 (예: 중첩 모듈, 어셈블리, 형식 또는 형식)를 패키지할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-140">You can also use a manifest module as a convenient way to package up resources that other modules will use, such as nested modules, assemblies, types, or formats.</span></span> <span data-ttu-id="3f65f-141">자세한 내용은 [PowerShell 모듈 매니페스트를 작성 하는 방법](./how-to-write-a-powershell-module-manifest.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3f65f-141">For more information, see [How to Write a PowerShell Module Manifest](./how-to-write-a-powershell-module-manifest.md).</span></span>

### <a name="dynamic-modules"></a><span data-ttu-id="3f65f-142">동적 모듈</span><span class="sxs-lookup"><span data-stu-id="3f65f-142">Dynamic Modules</span></span>

<span data-ttu-id="3f65f-143">*동적 모듈* 은 파일에서 로드 되거나 파일에 저장 되지 않은 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-143">A *dynamic module* is a module that is not loaded from, or saved to, a file.</span></span> <span data-ttu-id="3f65f-144">대신, [새 모듈](/powershell/module/Microsoft.PowerShell.Core/New-Module) cmdlet을 사용 하 여 스크립트에 의해 동적으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-144">Instead, they are created dynamically by a script, using the [New-Module](/powershell/module/Microsoft.PowerShell.Core/New-Module) cmdlet.</span></span> <span data-ttu-id="3f65f-145">이 유형의 모듈을 사용 하면 스크립트를 사용 하 여 영구 저장소에 로드 하거나 저장할 필요가 없는 모듈을 주문형으로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-145">This type of module enables a script to create a module on demand that does not need to be loaded or saved to persistent storage.</span></span> <span data-ttu-id="3f65f-146">동적 모듈은 기본적으로 수명이 짧을 것 이므로 `Get-Module` cmdlet으로 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-146">By its nature, a dynamic module is intended to be short-lived, and therefore cannot be accessed by the `Get-Module` cmdlet.</span></span> <span data-ttu-id="3f65f-147">마찬가지로 일반적으로 모듈 매니페스트가 필요 하지 않으며 관련 어셈블리를 저장 하는 데 영구적인 폴더가 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-147">Similarly, they usually do not need module manifests, nor do they likely need permanent folders to store their related assemblies.</span></span>

## <a name="module-manifests"></a><span data-ttu-id="3f65f-148">모듈 매니페스트</span><span class="sxs-lookup"><span data-stu-id="3f65f-148">Module Manifests</span></span>

<span data-ttu-id="3f65f-149">*모듈 매니페스트* 는 해시 테이블을 포함 하는 psd1 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-149">A *module manifest* is a .psd1 file that contains a hash table.</span></span> <span data-ttu-id="3f65f-150">해시 테이블의 키와 값은 다음 작업을 수행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-150">The keys and values in the hash table do the following things:</span></span>

- <span data-ttu-id="3f65f-151">모듈의 내용 및 특성을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-151">Describe the contents and attributes of the module.</span></span>

- <span data-ttu-id="3f65f-152">필수 구성 요소를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-152">Define the prerequisites.</span></span>

- <span data-ttu-id="3f65f-153">구성 요소를 처리 하는 방법을 결정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-153">Determine how the components are processed.</span></span>

  <span data-ttu-id="3f65f-154">매니페스트는 모듈에 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-154">Manifests are not required for a module.</span></span> <span data-ttu-id="3f65f-155">모듈은 스크립트 파일 (ps1), 스크립트 모듈 파일 (. .psm1), 매니페스트 파일 (. psd1), 형식 지정 및 형식 파일 (. types.ps1xml), cmdlet 및 공급자 어셈블리 (.dll), 리소스 파일, 도움말 파일, 지역화 파일 또는 기타 형식의 파일 또는 리소스를 참조할 수 있습니다. 는 모듈의 일부로 번들로 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-155">Modules can reference script files (.ps1), script module files (.psm1), manifest files (.psd1), formatting and type files (.ps1xml), cmdlet and provider assemblies (.dll), resource files, Help files, localization files, or any other type of file or resource that is bundled as part of the module.</span></span> <span data-ttu-id="3f65f-156">국제화 된 스크립트의 경우 module 폴더에도 메시지 카탈로그 파일 집합이 포함 되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-156">For an internationalized script, the module folder also contains a set of message catalog files.</span></span> <span data-ttu-id="3f65f-157">모듈 폴더에 매니페스트 파일을 추가 하는 경우 매니페스트를 참조 하 여 여러 파일을 단일 단위로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-157">If you add a manifest file to the module folder, you can reference the multiple files as a single unit by referencing the manifest.</span></span>

  <span data-ttu-id="3f65f-158">매니페스트 자체는 다음과 같은 범주의 정보를 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-158">The manifest itself describes the following categories of information:</span></span>

- <span data-ttu-id="3f65f-159">모듈 버전 번호, 저자 및 설명과 같은 모듈에 대 한 메타 데이터입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-159">Metadata about the module, such as the module version number, the author, and the description.</span></span>

- <span data-ttu-id="3f65f-160">Windows PowerShell 버전, CLR (공용 언어 런타임) 버전 및 필수 모듈과 같은 모듈을 가져오는 데 필요한 필수 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-160">Prerequisites needed to import the module, such as the Windows PowerShell version, the common language runtime (CLR) version, and the required modules.</span></span>

- <span data-ttu-id="3f65f-161">처리할 스크립트, 형식 및 형식과 같은 처리 지시문</span><span class="sxs-lookup"><span data-stu-id="3f65f-161">Processing directives, such as the scripts, formats, and types to process.</span></span>

- <span data-ttu-id="3f65f-162">내보낼 모듈의 멤버에 대 한 제한 (예: 내보낼 별칭, 함수, 변수 및 cmdlet).</span><span class="sxs-lookup"><span data-stu-id="3f65f-162">Restrictions on the members of the module to export, such as the aliases, functions, variables, and cmdlets to export.</span></span>

  <span data-ttu-id="3f65f-163">자세한 내용은 [PowerShell 모듈 매니페스트를 작성 하는 방법](./how-to-write-a-powershell-module-manifest.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3f65f-163">For more information, see [How to Write a PowerShell Module Manifest](./how-to-write-a-powershell-module-manifest.md).</span></span>

## <a name="storing-and-installing-a-module"></a><span data-ttu-id="3f65f-164">모듈 저장 및 설치</span><span class="sxs-lookup"><span data-stu-id="3f65f-164">Storing and Installing a Module</span></span>

<span data-ttu-id="3f65f-165">스크립트, 이진 또는 매니페스트 모듈을 만든 후에는 다른 사용자가 액세스할 수 있는 위치에 작업을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-165">Once you have created a script, binary, or manifest module, you can save your work in a location that others may access it.</span></span> <span data-ttu-id="3f65f-166">예를 들어 Windows PowerShell이 설치 된 시스템 폴더에 모듈을 저장 하거나 사용자 폴더에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-166">For example, your module can be stored in the system folder where Windows PowerShell is installed, or it can be stored in a user folder.</span></span>

<span data-ttu-id="3f65f-167">일반적으로 `$ENV:PSModulePath` 변수에 저장 된 경로 중 하나를 사용 하 여 모듈을 설치 해야 하는 위치를 결정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-167">Generally speaking, you can determine where you should install your module by using one of the paths stored in the `$ENV:PSModulePath` variable.</span></span> <span data-ttu-id="3f65f-168">이러한 경로 중 하나를 사용 하면 사용자가 코드에서 모듈을 호출할 때 PowerShell에서 자동으로 모듈을 찾아 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-168">Using one of these paths means that PowerShell can automatically find and load your module when a user makes a call to it in their code.</span></span> <span data-ttu-id="3f65f-169">다른 위치에 모듈을 저장 하는 경우 @no__t를 호출할 때 모듈의 위치를 매개 변수로 전달 하 여 PowerShell에서 명시적으로 알릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-169">If you store your module somewhere else, you can explicitly let PowerShell know by passing in the location of your module as a parameter when you call `Install-Module`.</span></span>

<span data-ttu-id="3f65f-170">폴더 경로는 모듈 (ModuleBase)의 *기반* 으로 참조 되며 스크립트, 이진 또는 매니페스트 모듈 파일의 이름은 모듈 폴더 이름과 동일 해야 합니다. 단, 다음과 같은 경우는 예외입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-170">Regardless, the path of the folder is referred to as the *base* of the module (ModuleBase), and the name of the script, binary, or manifest module file should be the same as the module folder name, with the following exceptions:</span></span>

- <span data-ttu-id="3f65f-171">@No__t-0 cmdlet에 의해 생성 된 동적 모듈은 cmdlet의 `Name` 매개 변수를 사용 하 여 이름을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-171">Dynamic modules that are created by the `New-Module` cmdlet can be named using the `Name` parameter of the cmdlet.</span></span>

- <span data-ttu-id="3f65f-172">다음 구문에 따라 어셈블리 개체에서 가져온 모듈의 이름은 **@no__t** . `"dynamic_code_module_" + assembly.GetName()`입니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-172">Modules imported from assembly objects by the **`Import-Module` -Assembly** command are named according to the following syntax: `"dynamic_code_module_" + assembly.GetName()`.</span></span>

  <span data-ttu-id="3f65f-173">자세한 내용은 [PowerShell 모듈 설치](./installing-a-powershell-module.md) 및 [PSModulePath 설치 경로 수정](./modifying-the-psmodulepath-installation-path.md)을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="3f65f-173">For more information, see [Installing a PowerShell Module](./installing-a-powershell-module.md) and [Modifying the PSModulePath Installation Path](./modifying-the-psmodulepath-installation-path.md).</span></span>

## <a name="module-cmdlets-and-variables"></a><span data-ttu-id="3f65f-174">모듈 Cmdlet 및 변수</span><span class="sxs-lookup"><span data-stu-id="3f65f-174">Module Cmdlets and Variables</span></span>

<span data-ttu-id="3f65f-175">모듈을 만들고 관리 하기 위해 Windows PowerShell에서 제공 하는 cmdlet 및 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-175">The following cmdlets and variables are provided by Windows PowerShell for the creation and management of modules.</span></span>

<span data-ttu-id="3f65f-176">[새 모듈](/powershell/module/Microsoft.PowerShell.Core/New-Module) cmdlet이 cmdlet은 메모리에만 있는 새 동적 모듈을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-176">[New-Module](/powershell/module/Microsoft.PowerShell.Core/New-Module) cmdlet This cmdlet creates a new dynamic module that exists only in memory.</span></span> <span data-ttu-id="3f65f-177">모듈은 스크립트 블록에서 만들어지며, 해당 함수 및 변수와 같은 내보낸 멤버는 세션에서 즉시 사용할 수 있으며 세션이 닫힐 때까지 계속 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-177">The module is created from a script block, and its exported members, such as its functions and variables, are immediately available in the session and remain available until the session is closed.</span></span>

<span data-ttu-id="3f65f-178">[New-modulemanifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) cmdlet이 cmdlet은 새 모듈 매니페스트 (. psd1) 파일을 만들고 해당 값을 채운 다음 매니페스트 파일을 지정 된 경로에 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-178">[New-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/New-ModuleManifest) cmdlet This cmdlet creates a new module manifest (.psd1) file, populates its values, and saves the manifest file to the specified path.</span></span> <span data-ttu-id="3f65f-179">이 cmdlet을 사용 하 여 수동으로 채울 수 있는 모듈 매니페스트 템플릿을 만들 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-179">This cmdlet can also be used to create a module manifest template that can be filled in manually.</span></span>

<span data-ttu-id="3f65f-180">[Import-module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet이 cmdlet은 하나 이상의 모듈을 현재 세션에 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-180">[Import-Module](/powershell/module/Microsoft.PowerShell.Core/Import-Module) cmdlet This cmdlet adds one or more modules to the current session.</span></span>

<span data-ttu-id="3f65f-181">[Import-module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet이 cmdlet은 현재 세션으로 가져올 수 있거나 현재 세션으로 가져올 수 있는 모듈에 대 한 정보를 검색 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-181">[Get-Module](/powershell/module/Microsoft.PowerShell.Core/Get-Module) cmdlet This cmdlet retrieves information about the modules that have been or that can be imported into the current session.</span></span>

<span data-ttu-id="3f65f-182">[Export-modulemember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) cmdlet이 cmdlet은 스크립트 모듈 (.psm1) 파일 또는 `New-Module` cmdlet을 사용 하 여 만든 동적 모듈에서 내보낸 모듈 멤버 (예: cmdlet, 함수, 변수 및 별칭)를 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-182">[Export-ModuleMember](/powershell/module/Microsoft.PowerShell.Core/Export-ModuleMember) cmdlet This cmdlet specifies the module members (such as cmdlets, functions, variables, and aliases) that are exported from a script module (.psm1) file or from a dynamic module created by using the `New-Module` cmdlet.</span></span>

<span data-ttu-id="3f65f-183">이 cmdlet은 [모듈을 제거](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) 합니다 .이 cmdlet은 현재 세션에서 모듈을 제거 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-183">[Remove-Module](/powershell/module/Microsoft.PowerShell.Core/Remove-Module) cmdlet This cmdlet removes modules from the current session.</span></span>

<span data-ttu-id="3f65f-184">[New-modulemanifest](/powershell/module/Microsoft.PowerShell.Core/Test-ModuleManifest) cmdlet이 cmdlet은 모듈 매니페스트 파일 (. psd1)에 나열 된 파일이 지정 된 경로에 실제로 존재 하는지 확인 하 여 모듈 매니페스트가 모듈의 구성 요소를 정확 하 게 설명 하는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-184">[Test-ModuleManifest](/powershell/module/Microsoft.PowerShell.Core/Test-ModuleManifest) cmdlet This cmdlet verifies that a module manifest accurately describes the components of a module by verifying that the files that are listed in the module manifest file (.psd1) actually exist in the specified paths.</span></span>

<span data-ttu-id="3f65f-185">이 변수에는 스크립트 모듈이 실행 되는 디렉터리가 포함 되어 $PSScriptRoot.</span><span class="sxs-lookup"><span data-stu-id="3f65f-185">$PSScriptRoot This variable contains the directory from which the script module is being executed.</span></span> <span data-ttu-id="3f65f-186">이를 통해 스크립트는 모듈 경로를 사용 하 여 다른 리소스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-186">It enables scripts to use the module path to access other resources.</span></span>

<span data-ttu-id="3f65f-187">$env:P SModulePath이 환경 변수는 Windows PowerShell 모듈을 저장 하는 디렉터리 목록을 포함 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-187">$env:PSModulePath This environment variable contains a list of the directories in which Windows PowerShell modules are stored.</span></span> <span data-ttu-id="3f65f-188">Windows PowerShell은 모듈을 자동으로 가져올 때이 변수의 값을 사용 하 고 모듈에 대 한 도움말 항목을 업데이트 합니다.</span><span class="sxs-lookup"><span data-stu-id="3f65f-188">Windows PowerShell uses the value of this variable when importing modules automatically and updating Help topics for modules.</span></span>

## <a name="see-also"></a><span data-ttu-id="3f65f-189">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3f65f-189">See Also</span></span>

[<span data-ttu-id="3f65f-190">Windows PowerShell 모듈 작성</span><span class="sxs-lookup"><span data-stu-id="3f65f-190">Writing a Windows PowerShell Module</span></span>](./writing-a-windows-powershell-module.md)