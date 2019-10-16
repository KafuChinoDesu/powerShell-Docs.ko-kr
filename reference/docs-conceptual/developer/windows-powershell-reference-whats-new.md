---
title: Windows PowerShell 참조-새로운 기능
ms.date: 09/13/2016
ms.topic: article
ms.openlocfilehash: 364d081ddf2f87ceeaa47732266a35f4a126246f
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72366092"
---
# <a name="whats-new"></a><span data-ttu-id="678c2-102">새로운 기능</span><span class="sxs-lookup"><span data-stu-id="678c2-102">What's New</span></span>

<span data-ttu-id="678c2-103">Windows PowerShell 2.0에는 cmdlet, 공급자 및 호스트 응용 프로그램을 작성할 때 사용할 새 기능이 다음과 같이 제공 됩니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-103">Windows PowerShell 2.0 provides the following new features for use when writing cmdlets, providers, and host applications.</span></span>

## <a name="modules"></a><span data-ttu-id="678c2-104">모듈</span><span class="sxs-lookup"><span data-stu-id="678c2-104">Modules</span></span>

<span data-ttu-id="678c2-105">이제 모듈을 사용 하 여 Windows PowerShell 솔루션을 패키지 하 고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-105">You can now package and distribute Windows PowerShell solutions by using modules.</span></span> <span data-ttu-id="678c2-106">모듈을 사용 하 여 Windows PowerShell 코드를 독립적이 고 재사용 가능한 단위로 분할, 구성 및 추상화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-106">Modules allow you to partition, organize, and abstract your Windows PowerShell code into self-contained, reusable units.</span></span> <span data-ttu-id="678c2-107">모듈에 대 한 자세한 내용은 Windows PowerShell 모듈 작성을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-107">For more information about modules, see Writing a Windows PowerShell Module.</span></span>

## <a name="the-powershell-class"></a><span data-ttu-id="678c2-108">PowerShell 클래스</span><span class="sxs-lookup"><span data-stu-id="678c2-108">The PowerShell class</span></span>

<span data-ttu-id="678c2-109">PowerShell 클래스는 프로그래밍 방식으로 명령을 실행 하는 응용 프로그램을 만들기 위한 간단한 솔루션 (호스트 응용 프로그램 이라고 함)을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-109">The PowerShell class provides a simpler solution for creating applications, referred to as host applications, that programmatically run commands.</span></span> <span data-ttu-id="678c2-110">이 클래스를 사용 하 여 명령 파이프라인을 만들고, 명령을 실행 하는 데 사용 되는 runspace를 지정 하 고, 동기적 또는 비동기적으로 명령 호출을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-110">This class allows you to create a pipeline of commands, specify the runspace that is used to run the commands, and specify invoking the commands synchronously or asynchronously.</span></span>

## <a name="the-runspacepool-class"></a><span data-ttu-id="678c2-111">RunspacePool 클래스</span><span class="sxs-lookup"><span data-stu-id="678c2-111">The RunspacePool class</span></span>

<span data-ttu-id="678c2-112">Runspace 풀을 사용 하면 단일 호출을 사용 하 여 여러 runspace를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-112">Runspace pools allow you to create multiple runspaces by using a single call.</span></span> <span data-ttu-id="678c2-113">CreateRunspacePool 메서드는 동일한 호스트, 초기 세션 상태, 연결 정보 등 동일한 기능이 있는 runspace를 만드는 데 사용할 수 있는 여러 오버 로드를 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-113">The CreateRunspacePool method provides several overloads that can be used to create runspaces that have the same features, such as the same host, initial session state, and connection information.</span></span>

## <a name="the-initialsessionstate-class"></a><span data-ttu-id="678c2-114">InitialSessionState 클래스</span><span class="sxs-lookup"><span data-stu-id="678c2-114">The InitialSessionState class</span></span>

<span data-ttu-id="678c2-115">InitialSessionState 클래스를 사용 하 여 runspace를 열 때 사용 되는 세션 상태 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-115">The InitialSessionState class allows you to create a session state configuration that is used when a runspace is opened.</span></span> <span data-ttu-id="678c2-116">사용자 지정 구성, mshshort에서 제공 하는 명령을 포함 하는 기본 구성 및 세션의 기능에 따라 명령이 제한 되는 구성을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-116">You can create a custom configuration, a default configuration that includes the commands provided by mshshort, and a configuration whose commands are restricted based on the capabilities of the session.</span></span>

## <a name="remote-runspaces"></a><span data-ttu-id="678c2-117">원격 runspace</span><span class="sxs-lookup"><span data-stu-id="678c2-117">Remote runspaces</span></span>

<span data-ttu-id="678c2-118">이제 원격 컴퓨터에서 열 수 있는 runspace을 만들어 원격 컴퓨터에서 명령을 실행 하 고 결과를 로컬로 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-118">You can now create runspaces that can be opened on remote computers, allowing you to run commands on the remote machine and collect the results locally.</span></span> <span data-ttu-id="678c2-119">원격 runspace를 만들려면 runspace를 만들 때 원격 연결에 대 한 정보를 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-119">To create a remote runspace, you must specify information about the remote connection when creating the runspace.</span></span> <span data-ttu-id="678c2-120">예제는 CreateRunspace 및 CreateRunspacePool 메서드를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-120">See the CreateRunspace and CreateRunspacePool methods for examples.</span></span> <span data-ttu-id="678c2-121">연결 정보는 RunspaceConnectionInfo 클래스에 의해 정의 됩니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-121">The connection information is defined by the RunspaceConnectionInfo class.</span></span>

## <a name="private-runspace-elements"></a><span data-ttu-id="678c2-122">Private runspace 요소</span><span class="sxs-lookup"><span data-stu-id="678c2-122">Private runspace elements</span></span>

<span data-ttu-id="678c2-123">이제 해당 요소가 public 또는 private 인 runspace을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-123">You can now create runspaces whose elements are public or private.</span></span> <span data-ttu-id="678c2-124">그러면 해당 요소를 runspace에 사용할 수 있지만 사용자가 사용할 수 없는 runspace을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-124">This allows you to create runspaces whose elements are available to the runspace, but are not available to the user.</span></span> <span data-ttu-id="678c2-125">ConstrainedSessionStateEntry 클래스를 참조 하 여 전용으로 만들 수 있는 runspace 요소를 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-125">See the ConstrainedSessionStateEntry class to find out which elements of the runspace can be made private.</span></span>

## <a name="runspace-threading-modes-and-apartment-state"></a><span data-ttu-id="678c2-126">Runspace 스레딩 모드 및 아파트 상태</span><span class="sxs-lookup"><span data-stu-id="678c2-126">Runspace threading modes and apartment state</span></span>

<span data-ttu-id="678c2-127">이제 runspace에서 명령을 실행할 때 스레드를 만들고 사용 하는 방법을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-127">You can now specify how threads are created and used when running commands in a runspace.</span></span> <span data-ttu-id="678c2-128">Runspace 및 Runspace 및 RunspacePool 속성을 참조 하는 방법에 대해 자세한 내용을 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-128">See the System.Management.Automation.Runspaces.Runspace.ThreadOptions and System.Management.Automation.Runspaces.RunspacePool.ThreadOptions properties.</span></span>

<span data-ttu-id="678c2-129">이제 runspace에서 명령을 실행 하는 데 사용 되는 스레드의 아파트 상태를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-129">You can now get the apartment state of the threads that are used to run commands in a runspace.</span></span> <span data-ttu-id="678c2-130">System.threading.thread.apartmentstate 및 Runspace 속성을 참조 하세요. Runspace. System.threading.thread.apartmentstate 속성을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-130">See the System.Management.Automation.Runspaces.Runspace.ApartmentState and System.Management.Automation.Runspaces.RunspacePool.ApartmentState properties.</span></span>

## <a name="transaction-cmdlets"></a><span data-ttu-id="678c2-131">트랜잭션 cmdlet</span><span class="sxs-lookup"><span data-stu-id="678c2-131">Transaction cmdlets</span></span>

<span data-ttu-id="678c2-132">이제 트랜잭션 내에서 사용할 수 있는 cmdlet을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-132">You can now create cmdlets that can be used within a transaction.</span></span> <span data-ttu-id="678c2-133">트랜잭션에서 cmdlet을 사용 하는 경우 해당 작업은 일시적 이며 Windows PowerShell에서 제공 하는 트랜잭션 cmdlet에 의해 허용 되거나 거부 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-133">When a cmdlet is used in a transaction, its actions are temporary, and they can be accepted or rejected by the transaction cmdlets provided by Windows PowerShell.</span></span>

<span data-ttu-id="678c2-134">트랜잭션에 대 한 자세한 내용은 트랜잭션을 지 원하는 방법을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-134">For more information about transactions, see How to Support Transactions.</span></span>

## <a name="transaction-provider"></a><span data-ttu-id="678c2-135">트랜잭션 공급자</span><span class="sxs-lookup"><span data-stu-id="678c2-135">Transaction provider</span></span>

<span data-ttu-id="678c2-136">이제 트랜잭션 내에서 사용할 수 있는 공급자를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-136">You can now create providers that can be used within a transaction.</span></span> <span data-ttu-id="678c2-137">Cmdlet과 마찬가지로 트랜잭션에서 공급자를 사용 하는 경우 해당 작업은 일시적 이며 Windows PowerShell에서 제공 하는 트랜잭션 cmdlet에 의해 허용 되거나 거부 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-137">Similar to cmdlets, when a provider is used in a transaction, its actions are temporary, and they can be accepted or rejected by the transaction cmdlets provided by Windows PowerShell.</span></span>

<span data-ttu-id="678c2-138">공급자 클래스 내에서 트랜잭션 지원을 지정 하는 방법에 대 한 자세한 내용은 CmdletProviderAttribute 속성을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-138">For more information about specifying support for transaction within a provider class, see the System.Management.Automation.Provider.CmdletProviderAttribute.ProviderCapabilities property.</span></span>

## <a name="job-cmdlets"></a><span data-ttu-id="678c2-139">작업 cmdlet</span><span class="sxs-lookup"><span data-stu-id="678c2-139">Job cmdlets</span></span>

<span data-ttu-id="678c2-140">이제 작업으로 작업을 수행할 수 있는 cmdlet을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-140">You can now write cmdlets that can perform their action as a job.</span></span> <span data-ttu-id="678c2-141">이러한 작업은 현재 세션과 상호 작용 하지 않고 백그라운드에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-141">These jobs are run in the background without interacting with the current session.</span></span> <span data-ttu-id="678c2-142">Windows PowerShell에서 작업을 지 원하는 방법에 대 한 자세한 내용은 백그라운드 작업을 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-142">For more information about how Windows PowerShell supports jobs, see Background Jobs.</span></span>

## <a name="cmdlet-output-types"></a><span data-ttu-id="678c2-143">Cmdlet 출력 형식</span><span class="sxs-lookup"><span data-stu-id="678c2-143">Cmdlet output types</span></span>

<span data-ttu-id="678c2-144">이제 cmdlet을 작성할 때 OutputType 특성을 선언 하 여 cmdlet에서 반환 되는 .NET Framework 형식을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-144">You can now specify the .NET Framework types that are returned by your cmdlets by declaring the OutputType attribute when writing your cmdlets.</span></span> <span data-ttu-id="678c2-145">이렇게 하면 cmdlet에서 반환 되는 개체 유형을 확인할 수 있습니다. cmdlet의 OutputType 속성을 살펴보면 cmdlet에서 반환 되는 개체 유형을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-145">This will allow others to determine what type of objects are returned by a cmdlet by looking at the OutputType property of the cmdlet.</span></span>

## <a name="event-support"></a><span data-ttu-id="678c2-146">이벤트 지원</span><span class="sxs-lookup"><span data-stu-id="678c2-146">Event support</span></span>

<span data-ttu-id="678c2-147">이제 이벤트를 추가 하 고 사용 하는 cmdlet을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-147">You can now write cmdlets that add and consume events.</span></span> <span data-ttu-id="678c2-148">PSEvent 클래스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-148">See the PSEvent class.</span></span>

## <a name="proxy-commands"></a><span data-ttu-id="678c2-149">프록시 명령</span><span class="sxs-lookup"><span data-stu-id="678c2-149">Proxy commands</span></span>

<span data-ttu-id="678c2-150">이제 다른 명령을 실행 하는 데 사용할 수 있는 프록시 명령을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-150">You can now write proxy commands that can be used to run another command.</span></span> <span data-ttu-id="678c2-151">프록시 명령을 사용 하면 사용자가 사용할 수 있는 원본 cmdlet의 기능을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-151">A proxy command allows you to control what functionality of the source cmdlet is available to the user.</span></span> <span data-ttu-id="678c2-152">예를 들어 소스 명령에서 제공 하는 매개 변수를 제거 하는 프록시 명령을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-152">For example, you can create a proxy command that removes a parameter that is supplied by the source command.</span></span> <span data-ttu-id="678c2-153">ProxyCommand 클래스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-153">See the ProxyCommand class.</span></span>

## <a name="multiple-choice-prompts"></a><span data-ttu-id="678c2-154">여러 선택 프롬프트</span><span class="sxs-lookup"><span data-stu-id="678c2-154">Multiple choice prompts</span></span>

<span data-ttu-id="678c2-155">이제 사용자가 여러 선택 항목을 선택할 수 있는 프롬프트를 제공할 수 있는 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-155">You can now write applications that can provide prompts that allow the user to select multiple choices.</span></span> <span data-ttu-id="678c2-156">IHostUISupportsMultipleChoiceSelection 인터페이스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-156">See the IHostUISupportsMultipleChoiceSelection interface</span></span>

## <a name="interactive-sessions"></a><span data-ttu-id="678c2-157">대화형 세션</span><span class="sxs-lookup"><span data-stu-id="678c2-157">Interactive sessions</span></span>

<span data-ttu-id="678c2-158">이제 원격 컴퓨터에서 대화형 세션을 시작 하 고 중지할 수 있는 응용 프로그램을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-158">You can now write applications that can start and stop an interactive session on a remote computer.</span></span>
<span data-ttu-id="678c2-159">IHostSupportsInteractiveSession 인터페이스를 참조 하세요.</span><span class="sxs-lookup"><span data-stu-id="678c2-159">See the IHostSupportsInteractiveSession interface.</span></span>

## <a name="custom-cmdlet-help-for-providers"></a><span data-ttu-id="678c2-160">공급자에 대 한 사용자 지정 Cmdlet 도움말</span><span class="sxs-lookup"><span data-stu-id="678c2-160">Custom Cmdlet Help for Providers</span></span>

<span data-ttu-id="678c2-161">이제 공급자 cmdlet에 대 한 사용자 지정 도움말 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-161">You can now create customized Help topics for the provider cmdlets.</span></span> <span data-ttu-id="678c2-162">사용자 지정 cmdlet 도움말 항목에서는 공급자 경로에서 cmdlet이 작동 하는 방법 및 공급자가 cmdlet에 추가 하는 동적 매개 변수를 비롯 한 특수 기능을 문서화 하는 방법을 설명할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="678c2-162">Custom cmdlet help topics can explain how the cmdlet works in the provider path and document special features, including the dynamic parameters that the provider adds to the cmdlet.</span></span>