---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "DSC 문제 해결"
ms.openlocfilehash: 4141e1f3304460dcaf310ce603fdc5d9550a5069
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/17/2018
---
# <a name="troubleshooting-dsc"></a><span data-ttu-id="0761b-103">DSC 문제 해결</span><span class="sxs-lookup"><span data-stu-id="0761b-103">Troubleshooting DSC</span></span>

><span data-ttu-id="0761b-104">적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0761b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="0761b-105">이 항목에서는 문제가 발생할 때 DSC 문제를 해결하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-105">This topic describes ways to troubleshoot DSC when problems arise.</span></span>

## <a name="winrm-dependency"></a><span data-ttu-id="0761b-106">WinRM 종속성</span><span class="sxs-lookup"><span data-stu-id="0761b-106">WinRM Dependency</span></span>

<span data-ttu-id="0761b-107">Windows PowerShell DSC(원하는 상태 구성)는 WinRM에 종속됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-107">Windows PowerShell Desired State Configuration (DSC) depends on WinRM.</span></span> <span data-ttu-id="0761b-108">WinRM은 Windows Server 2008 R2 및 Windows 7에서 기본적으로 사용하도록 설정되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-108">WinRM is not enabled by default on Windows Server 2008 R2 and Windows 7.</span></span> <span data-ttu-id="0761b-109">Windows PowerShell 관리자 권한 세션에서 ```Set-WSManQuickConfig```를 실행하여 WinRM을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-109">Run ```Set-WSManQuickConfig```, in a Windows PowerShell elevated session, to enable WinRM.</span></span>

## <a name="using-get-dscconfigurationstatus"></a><span data-ttu-id="0761b-110">Get-DscConfigurationStatus 사용</span><span class="sxs-lookup"><span data-stu-id="0761b-110">Using Get-DscConfigurationStatus</span></span>

<span data-ttu-id="0761b-111">[Get-DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx) cmdlet은 대상 노드에서 구성 상태에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-111">The [Get-DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx) cmdlet gets information about configuration status from a target node.</span></span> <span data-ttu-id="0761b-112">구성 실행의 성공 여부에 대한 상위 수준 정보를 포함하는 다양한 개체가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-112">A rich object is returned that includes high-level information about whether or not the configuration run was successful or not.</span></span> <span data-ttu-id="0761b-113">개체를 자세히 검토하면 다음과 같은 구성 실행에 대한 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-113">You can dig into the object to discover details about the configuration run such as:</span></span>

* <span data-ttu-id="0761b-114">실패한 모든 리소스</span><span class="sxs-lookup"><span data-stu-id="0761b-114">All of the resources that failed</span></span>
* <span data-ttu-id="0761b-115">다시 부팅을 요청한 모든 리소스</span><span class="sxs-lookup"><span data-stu-id="0761b-115">Any resource that requested a reboot</span></span>
* <span data-ttu-id="0761b-116">구성 실행 시 메타 구성 설정</span><span class="sxs-lookup"><span data-stu-id="0761b-116">Meta-Configuration settings at time of configuration run</span></span>
* <span data-ttu-id="0761b-117">기타</span><span class="sxs-lookup"><span data-stu-id="0761b-117">Etc.</span></span>

<span data-ttu-id="0761b-118">다음 매개 변수 집합은 마지막 구성 실행에 대한 상태 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-118">The following parameter set returns the status information for the last configuration run:</span></span>

```powershell
Get-DscConfigurationStatus  [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```
<span data-ttu-id="0761b-119">다음 매개 변수 집합은 모든 이전 구성 실행에 대한 상태 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-119">The following parameter set returns the status information for all previous configuration runs:</span></span>

```powershell
Get-DscConfigurationStatus  -All 
                            [-CimSession <CimSession[]>] 
                            [-ThrottleLimit <int>] 
                            [-AsJob] 
                            [<CommonParameters>]
```

## <a name="example"></a><span data-ttu-id="0761b-120">예제</span><span class="sxs-lookup"><span data-stu-id="0761b-120">Example</span></span>

```powershell
PS C:\> $Status = Get-DscConfigurationStatus 

PS C:\> $Status

Status      StartDate               Type            Mode    RebootRequested     NumberOfResources
------      ---------               ----            ----    ---------------     -----------------
Failure     11/24/2015  3:44:56     Consistency     Push    True                36

PS C:\> $Status.ResourcesNotInDesiredState

ConfigurationName       :   MyService
DependsOn               :   
ModuleName              :   PSDesiredStateConfiguration
ModuleVersion           :   1.1
PsDscRunAsCredential    :   
ResourceID              :   [File]ServiceDll
SourceInfo              :   c:\git\CustomerService\Configs\MyCustomService.ps1::5::34::File
DurationInSeconds       :   0.19
Error                   :   SourcePath must be accessible for current configuration. The related file/directory is:
                            \\Server93\Shared\contosoApp.dll. The related ResourceID is [File]ServiceDll
FinalState              :   
InDesiredState          :   False
InitialState            :   
InstanceName            :   ServiceDll
RebootRequested         :   False
ReosurceName            :   File
StartDate               :   11/24/2015  3:44:56
PSComputerName          :
```

## <a name="my-script-wont-run-using-dsc-logs-to-diagnose-script-errors"></a><span data-ttu-id="0761b-121">스크립트가 실행되지 않습니다: DSC 로그를 사용하여 스크립트 오류 진단</span><span class="sxs-lookup"><span data-stu-id="0761b-121">My script won’t run: Using DSC logs to diagnose script errors</span></span>

<span data-ttu-id="0761b-122">모든 Windows 소프트웨어와 마찬가지로, DSC에서는 [이벤트 뷰어](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer)에서 볼 수 있는 [로그](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx)에 오류와 이벤트를 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-122">Like all Windows software, DSC records errors and events in [logs](https://msdn.microsoft.com/library/windows/desktop/aa363632.aspx) that can be viewed from the [Event Viewer](http://windows.microsoft.com/windows/what-information-event-logs-event-viewer).</span></span> <span data-ttu-id="0761b-123">이러한 로그를 검사하면 특정 작업이 실패한 이유와 나중에 오류를 방지하는 방법을 이해하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-123">Examining these logs can help you understand why a particular operation failed, and how to prevent failure in the future.</span></span> <span data-ttu-id="0761b-124">구성 스크립트 작성은 까다로울 수 있으므로, 작성자로서 오류 추적을 보다 쉽게 하려면, DSC 로그 리소스를 사용하여 분석 DSC 이벤트 로그에 있는 구성의 진행률을 추적합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-124">Writing configuration scripts can be tricky, so to make tracking errors easier as you author, use the DSC Log resource to track the progress of your configuration in the DSC Analytic event log.</span></span>

## <a name="where-are-dsc-event-logs"></a><span data-ttu-id="0761b-125">DSC 이벤트 로그는 어디에 있나요?</span><span class="sxs-lookup"><span data-stu-id="0761b-125">Where are DSC event logs?</span></span>

<span data-ttu-id="0761b-126">이벤트 뷰어에서 DSC 이벤트는 **응용 프로그램 및 서비스 로그/Microsoft/Windows/필요한 상태 구성**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-126">In Event Viewer, DSC events are in: **Applications and Services Logs/Microsoft/Windows/Desired State Configuration**</span></span>

<span data-ttu-id="0761b-127">해당 PowerShell cmdlet인 [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx)를 실행해도 이벤트 로그를 볼 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-127">The corresponding PowerShell cmdlet, [Get-WinEvent](https://technet.microsoft.com/library/hh849682.aspx), can also be run to view the event logs:</span></span>

```
PS C:\> Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                                                                                  
-----------                     -- ---------------- -------                                                                                                  
11/17/2014 10:27:23 PM        4102 Information      Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
```

<span data-ttu-id="0761b-128">위와 같이 DSC의 기본 로그 이름은 **Microsoft->Windows->DSC**(Windows 아래의 다른 로그 이름은 간결하게 하기 위해 표시하지 않음)입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-128">As shown above, DSC’s primary log name is **Microsoft->Windows->DSC** (other log names under Windows are not shown here for brevity).</span></span> <span data-ttu-id="0761b-129">기본 이름을 채널 이름에 추가하여 전체 로그 이름이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-129">The primary name is appended to the channel name to create the complete log name.</span></span> <span data-ttu-id="0761b-130">DSC 엔진은 [작업, 분석 및 디버그 로그](https://technet.microsoft.com/library/cc722404.aspx), 이렇게 주로 세 가지 유형의 로그에 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-130">The DSC engine writes mainly into three types of logs: [Operational, Analytic, and Debug logs](https://technet.microsoft.com/library/cc722404.aspx).</span></span> <span data-ttu-id="0761b-131">분석 및 디버그 로그는 기본적으로 해제 되어 있으므로, 이벤트 뷰어에서 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-131">Since the analytic and debug logs are turned off by default, you should enable them in Event Viewer.</span></span> <span data-ttu-id="0761b-132">이렇게 하려면 Windows PowerShell에서 Show-EventLog를 입력하여 이벤트 뷰어를 엽니다. 또는 **시작** 단추, **제어판**, **관리 도구**, **이벤트 뷰어**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-132">To do this, open Event Viewer by typing Show-EventLog in Windows PowerShell; or, click the **Start** button, click **Control Panel**, click **Administrative Tools**, and then click **Event Viewer**.</span></span> <span data-ttu-id="0761b-133">이벤트 뷰어의 **보기** 메뉴에서 **분석 및 디버그 로그 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-133">On the **View** menu in Event viewer, click **Show Analytic and Debug Logs**.</span></span> <span data-ttu-id="0761b-134">분석 채널에 대한 로그 이름은 **Microsoft-Windows-Dsc/Analytic**이고, 디버그 채널은 **Microsoft-Windows-Dsc/Debug**입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-134">The log name for the analytic channel is **Microsoft-Windows-Dsc/Analytic**, and the debug channel is **Microsoft-Windows-Dsc/Debug**.</span></span> <span data-ttu-id="0761b-135">다음 예에서 보듯이, [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) 유틸리티를 사용하여 로그를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-135">You could also use the [wevtutil](https://technet.microsoft.com/library/cc732848.aspx) utility to enable the logs, as shown in the following example.</span></span>

```powershell
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
```

## <a name="what-do-dsc-logs-contain"></a><span data-ttu-id="0761b-136">DSC 로그에 들어 있는 내용은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="0761b-136">What do DSC logs contain?</span></span>

<span data-ttu-id="0761b-137">DSC 로그는 메시지의 중요도에 따라 3개의 로그 채널로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-137">DSC logs are split over the three log channels based on the importance of the message.</span></span> <span data-ttu-id="0761b-138">DSC의 작업 로그는 모든 오류 메시지를 포함하며, 문제를 파악하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-138">The operational log in DSC contains all error messages, and can be used to identify a problem.</span></span> <span data-ttu-id="0761b-139">분석 로그는 더 많은 양의 이벤트를 포함하며, 오류가 발생한 위치를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-139">The analytic log has a higher volume of events, and can identify where error(s) occurred.</span></span> <span data-ttu-id="0761b-140">이 채널은 자세한 정보 메시지도 포함합니다(있는 경우).</span><span class="sxs-lookup"><span data-stu-id="0761b-140">This channel also contains verbose messages (if any).</span></span> <span data-ttu-id="0761b-141">디버그 로그는 오류가 발생하는 방식을 이해하는 데 도움이 될 수 있는 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-141">The debug log contains logs that can help you understand how the errors occurred.</span></span> <span data-ttu-id="0761b-142">DSC 이벤트 메시지는 모든 이벤트 메시지가 고유하게 DSC 작업을 나타내는 작업 ID로 시작되도록 구조화되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-142">DSC event messages are structured such that every event message begins with a job ID that uniquely represents a DSC operation.</span></span> <span data-ttu-id="0761b-143">아래 예제는 작업 DSC 로그에 로그되는 첫 번째 이벤트에서 메시지 가져오기를 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-143">The example below attempts to obtain the message from the first event logged into the operational DSC log.</span></span>

```powershell
PS C:\> $AllDscOpEvents = Get-WinEvent -LogName "Microsoft-Windows-Dsc/Operational"
PS C:\> $FirstOperationalEvent = $AllDscOpEvents[0]
PS C:\> $FirstOperationalEvent.Message
Job {02C38626-D95A-47F1-9DA2-C1D44A7128E7} : 
Consistency engine was run successfully. 
```

<span data-ttu-id="0761b-144">DSC 이벤트는 사용자가 하나의 DSC 작업에서 이벤트를 집계할 수 있도록 해주는 특정 구조로 로그됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-144">DSC events are logged in a particular structure that enables the user to aggregate events from one DSC job.</span></span> <span data-ttu-id="0761b-145">구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-145">The structure is as follows:</span></span>

<span data-ttu-id="0761b-146">**작업 ID: <Guid>**
**<Event Message>**</span><span class="sxs-lookup"><span data-stu-id="0761b-146">**Job ID : <Guid>**
**<Event Message>**</span></span>

## <a name="gathering-events-from-a-single-dsc-operation"></a><span data-ttu-id="0761b-147">단일 DSC 작업에서 이벤트 수집</span><span class="sxs-lookup"><span data-stu-id="0761b-147">Gathering events from a single DSC operation</span></span>

<span data-ttu-id="0761b-148">DSC 이벤트 로그에는 다양한 DSC 작업에서 생성된 이벤트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-148">DSC event logs contain events generated by various DSC operations.</span></span> <span data-ttu-id="0761b-149">그러나 우리는 일반적으로 하나의 특정 작업에 대한 세부 정보에 관심이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-149">However, you’ll usually be concerned with the detail about just one particular operation.</span></span> <span data-ttu-id="0761b-150">모든 DSC 로그는 각 DSC 작업에 대해 고유한 작업 ID 속성으로 그룹화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-150">All DSC logs can be grouped by the job ID property that is unique for every DSC operation.</span></span> <span data-ttu-id="0761b-151">작업 ID는 모든 DSC 이벤트에서 첫 번째 속성 값으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-151">The job ID is displayed as the first property value in all DSC events.</span></span> <span data-ttu-id="0761b-152">다음 단계에서는 그룹화된 배열 구조에서 모든 이벤트를 누적하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-152">The following steps explain how to accumulate all events in a grouped array structure.</span></span>

```powershell
<##########################################################################
 Step 1 : Enable analytic and debug DSC channels (Operational channel is enabled by default)
###########################################################################>
 
wevtutil.exe set-log “Microsoft-Windows-Dsc/Analytic” /q:true /e:true
wevtutil.exe set-log “Microsoft-Windows-Dsc/Debug” /q:True /e:true
 
<##########################################################################
 Step 2 : Perform the required DSC operation (Below is an example, you could run any DSC operation instead)
###########################################################################>
 
Get-DscLocalConfigurationManager
 
<##########################################################################
Step 3 : Collect all DSC Logs, from the Analytic, Debug and Operational channels
###########################################################################>
 
$DscEvents=[System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Operational") `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Analytic" -Oldest) `
         + [System.Array](Get-WinEvent "Microsoft-Windows-Dsc/Debug" -Oldest)
 
 
<##########################################################################
 Step 4 : Group all logs based on the job ID
###########################################################################>
$SeparateDscOperations = $DscEvents | Group {$_.Properties[0].value}  
```

<span data-ttu-id="0761b-153">여기, 변수 `$SeparateDscOperations`는 작업 ID로 그룹화된 로그를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-153">Here, the variable `$SeparateDscOperations` contains logs grouped by the job IDs.</span></span> <span data-ttu-id="0761b-154">이 변수의 각 배열 요소는 로그에 대한 추가 정보에 액세스할 수 있도록 다른 DSC 작업을 통해 로그되는 이벤트 그룹을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-154">Each array element of this variable represents a group of events logged by a different DSC operation, allowing access to more information about the logs.</span></span>

```
PS C:\> $SeparateDscOperations
 
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   48 {1A776B6A-5BAC-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
   40 {E557E999-5BA8-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
PS C:\> $SeparateDscOperations[0].Group
   ProviderName: Microsoft-Windows-DSC
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 3:47:29 PM          4115 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4198 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4114 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4102 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4098 Warning          Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4176 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...      
12/2/2013 3:47:29 PM          4182 Information      Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : ...       
```

<span data-ttu-id="0761b-155">[Where-Object](https://technet.microsoft.com/library/ee177028.aspx)를 사용하여 `$SeparateDscOperations` 변수에서 데이터를 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-155">You can extract the data in the variable `$SeparateDscOperations` using [Where-Object](https://technet.microsoft.com/library/ee177028.aspx).</span></span> <span data-ttu-id="0761b-156">다음은 DSC 문제 해결을 위해 데이터를 추출해야 하는 다섯 개의 시나리오입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-156">Following are five scenarios in which you might want to extract data for troubleshooting DSC:</span></span>

### <a name="1-operations-failures"></a><span data-ttu-id="0761b-157">1: 작업 오류</span><span class="sxs-lookup"><span data-stu-id="0761b-157">1: Operations failures</span></span>

<span data-ttu-id="0761b-158">모든 이벤트에는 [심각도](https://msdn.microsoft.com/library/dd996917(v=vs.85))가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-158">All events have [severity levels](https://msdn.microsoft.com/library/dd996917(v=vs.85)).</span></span> <span data-ttu-id="0761b-159">오류 이벤트를 식별하는 데 이 정보를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-159">This information can be used to identify the error events:</span></span>

```
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.LevelDisplayName -contains "Error"}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
   38 {5BCA8BE7-5BB6-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord, System.Diagnostics....
```

### <a name="2-details-of-operations-run-in-the-last-half-hour"></a><span data-ttu-id="0761b-160">2: 마지막 30분 안에 실행되는 작업의 세부 정보</span><span class="sxs-lookup"><span data-stu-id="0761b-160">2: Details of operations run in the last half hour</span></span>

<span data-ttu-id="0761b-161">모든 Windows 이벤트의 속성인 `TimeCreated`는 이벤트가 만들어진 시간을 기술합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-161">`TimeCreated`, a property of every Windows event, states the time the event was created.</span></span> <span data-ttu-id="0761b-162">이 속성을 특정 날짜/시간 개체와 비교하여 모든 이벤트를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-162">Comparing this property with a particular date/time object can be used to filter all events:</span></span>

```powershell
PS C:\> $DateLatest = (Get-Date).AddMinutes(-30)
PS C:\> $SeparateDscOperations | Where-Object {$_.Group.TimeCreated -gt $DateLatest}
Count Name                      Group                                                                     
----- ----                      -----                                                                     
    1 {6CEC5B09-5BB0-11E3-BF... {System.Diagnostics.Eventing.Reader.EventLogRecord}   
```

### <a name="3-messages-from-the-latest-operation"></a><span data-ttu-id="0761b-163">3: 최신 작업의 메시지</span><span class="sxs-lookup"><span data-stu-id="0761b-163">3: Messages from the latest operation</span></span>

<span data-ttu-id="0761b-164">최신 작업은 배열 그룹 `$SeparateDscOperations`의 첫 번째 인덱스에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-164">The latest operation is stored in the first index of the array group `$SeparateDscOperations`.</span></span> <span data-ttu-id="0761b-165">인덱스 0에 대한 그룹의 메시지를 쿼리하면 최신 작업에 대한 모든 메시지가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-165">Querying the group’s messages for index 0 returns all messages for the latest operation:</span></span>

```powershelll
PS C:\> $SeparateDscOperations[0].Group.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
Running consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Configuration is sent from computer NULL by user sid S-1-5-18.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Starting consistency engine.
Job {1A776B6A-5BAC-11E3-BF41-00155D553612} : 
Displaying messages from built-in DSC resources:
 WMI channel 1 
 ResourceID:  
 Message : [INCH-VM]:                            [] Consistency check completed. 
```

### <a name="4-error-messages-logged-for-recent-failed-operations"></a><span data-ttu-id="0761b-166">4: 최근 실패한 작업에 대해 로그된 오류 메시지</span><span class="sxs-lookup"><span data-stu-id="0761b-166">4: Error messages logged for recent failed operations</span></span>

<span data-ttu-id="0761b-167">`$SeparateDscOperations[0].Group`에는 최신 작업에 대한 이벤트 집합이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-167">`$SeparateDscOperations[0].Group` contains a set of events for the latest operation.</span></span> <span data-ttu-id="0761b-168">수준 표시 이름에 따라 이벤트를 필터링하려면 `Where-Object` cmdlet을 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="0761b-168">Run the `Where-Object` cmdlet to filter the events based on their level display name.</span></span> <span data-ttu-id="0761b-169">결과는 이벤트 메시지를 가져오기 위해 추가적으로 분석할 수 있는 `$myFailedEvent` 변수에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-169">Results are stored in the `$myFailedEvent` variable, which can be further dissected to get the event message:</span></span>

```powershell
PS C:\> $myFailedEvent = ($SeparateDscOperations[0].Group | Where-Object {$_.LevelDisplayName -eq "Error"})
 
PS C:\> $myFailedEvent.Message
Job {5BCA8BE7-5BB6-11E3-BF41-00155D553612} : 
DSC Engine Error : 
 Error Message Current configuration does not exist. Execute Start-DscConfiguration command with -Path pa
rameter to specify a configuration file and create a current configuration first. 
Error Code : 1 
```

### <a name="5-all-events-generated-for-a-particular-job-id"></a><span data-ttu-id="0761b-170">5: 특정 작업 ID에 대해 생성된 모든 이벤트</span><span class="sxs-lookup"><span data-stu-id="0761b-170">5: All events generated for a particular job ID.</span></span>

<span data-ttu-id="0761b-171">`$SeparateDscOperations`는 고유한 작업 ID로서 각각 이름이 있는 그룹의 배열입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-171">`$SeparateDscOperations` is an array of groups, each of which has the name as the unique job ID.</span></span> <span data-ttu-id="0761b-172">`Where-Object` cmdlet을 실행하면 특정 작업 ID를 가지고 있는 이벤트들의 그룹을 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-172">By running the `Where-Object` cmdlet, you can extract those groups of events that have a particular job ID:</span></span>

```powershell
PS C:\> ($SeparateDscOperations | Where-Object {$_.Name -eq $jobX} ).Group

   ProviderName: Microsoft-Windows-DSC
 
TimeCreated                     Id LevelDisplayName Message                                               
-----------                     -- ---------------- -------                                               
12/2/2013 4:33:24 PM          4102 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4168 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4146 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...      
12/2/2013 4:33:24 PM          4120 Information      Job {847A5619-5BB2-11E3-BF41-00155D553612} : ...  
```

## <a name="using-xdscdiagnostics-to-analyze-dsc-logs"></a><span data-ttu-id="0761b-173">xDscDiagnostics를 사용하여 DSC 로그 분석</span><span class="sxs-lookup"><span data-stu-id="0761b-173">Using xDscDiagnostics to analyze DSC logs</span></span>

<span data-ttu-id="0761b-174">**xDscDiagnostics**는 컴퓨터에서 DSC 실패를 분석하는 데 도움이 되는 여러 함수로 구성된 PowerShell 모듈입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-174">**xDscDiagnostics** is a PowerShell module that consists of several functions that can help analyze DSC failures on your machine.</span></span> <span data-ttu-id="0761b-175">이 함수들은 지난 DSC 작업의 모든 로컬 이벤트나 원격 컴퓨터의 DSC 이벤트(유효한 자격 증명 사용)를 식별하는 데 유용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-175">These functions can help you identify all local events from past DSC operations, or DSC events on remote computers (with valid credentials).</span></span> <span data-ttu-id="0761b-176">여기에서 DSC 작업이라는 용어는 시작부터 끝까지 하나의 고유한 DSC 실행을 정의하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-176">Here, the term DSC operation is used to define a single unique DSC execution from its start to its end.</span></span> <span data-ttu-id="0761b-177">예를 들어 `Test-DscConfiguration`은 별도의 DSC 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-177">For example, `Test-DscConfiguration` would be a separate DSC operation.</span></span> <span data-ttu-id="0761b-178">마찬가지로, DSC에 있는 모든 다른 cmdlet(예: `Get-DscConfiguration`, `Start-DscConfiguration` 등)은 각각 별도의 DSC 작업으로 식별될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-178">Similarly, every other cmdlet in DSC (such as `Get-DscConfiguration`, `Start-DscConfiguration`, etc.) could each be identified as separate DSC operations.</span></span> <span data-ttu-id="0761b-179">함수에 대한 설명은 [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics)에 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-179">The functions are explained at [xDscDiagnostics](https://github.com/PowerShell/xDscDiagnostics).</span></span> <span data-ttu-id="0761b-180">`Get-Help <cmdlet name>`을 실행하여 도움말을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-180">Help is available by running `Get-Help <cmdlet name>`.</span></span>

### <a name="getting-details-of-dsc-operations"></a><span data-ttu-id="0761b-181">DSC 작업의 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="0761b-181">Getting details of DSC operations</span></span> 

<span data-ttu-id="0761b-182">`Get-xDscOperation` 함수는 하나 또는 여러 컴퓨터에서 실행되는 DSC 작업의 결과를 찾을 수 있도록 해주며, 각 DSC 작업에서 생성된 이벤트의 컬렉션을 포함하는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-182">The `Get-xDscOperation` function lets you find the results of the DSC operations that run on one or multiple computers, and returns an object that contains the collection of events produced by each DSC operation.</span></span> <span data-ttu-id="0761b-183">예를 들어 다음의 출력에서는 세 가지 명령이 실행되었습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-183">For example, in the following output, three commands were run.</span></span> <span data-ttu-id="0761b-184">첫 번째 명령은 통과했고, 다른 두 개는 실패했습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-184">The first one passed, and the other two failed.</span></span> <span data-ttu-id="0761b-185">이 결과는 `Get-xDscOperation`의 출력에 요약되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-185">These results are summarized in the output of `Get-xDscOperation`.</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation

ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 9:37:52 AM  Failure  9701aadf-395e-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   2          6/23/2016 9:36:54 AM  Failure  7e8e2d6e-395c-11e6-9165-00155d390509  {@{Message=; TimeC...
SRV1   3          6/23/2016 9:36:54 AM  Success  af72c6aa-3960-11e6-9165-00155d390509  {@{Message=Operati...

```

<span data-ttu-id="0761b-186">또한 `Newest` 매개 변수를 사용하여 최신 작업에 대한 결과만 필요하다고 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-186">You can also specify that you want only results for the most recent operations by using the `Newest` parameter:</span></span>

```powershell
PS C:\DiagnosticsTest> Get-xDscOperation -Newest 5
ComputerName   SequenceId TimeCreated           Result   JobID                                 AllEvents            
------------   ---------- -----------           ------   -----                                 ---------            
SRV1   1          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   2          6/23/2016 4:36:54 PM  Success  5c06402b-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   3          6/23/2016 4:36:54 PM  Success                                        {@{Message=; TimeC...
SRV1   4          6/23/2016 4:36:54 PM  Success  5c06402a-399b-11e6-9165-00155d390509  {@{Message=Operati...
SRV1   5          6/23/2016 4:36:51 PM  Success                                        {@{Message=; TimeC...
```

### <a name="getting-details-of-dsc-events"></a><span data-ttu-id="0761b-187">DSC 이벤트의 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="0761b-187">Getting details of DSC events</span></span>

<span data-ttu-id="0761b-188">`Trace-xDscOperation` cmdlet은 이벤트의 컬렉션, 해당 이벤트 형식 및 특정 DSC 작업으로 생성된 메시지 출력을 포함하는 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-188">The `Trace-xDscOperation` cmdlet returns an object containing a collection of events, their event types, and the message output generated from a particular DSC operation.</span></span> <span data-ttu-id="0761b-189">일반적으로 `Get-xDscOperation`을 사용하는 작업 중에 오류가 발생하면, 오류를 초래한 이벤트를 찾기 위해 해당 작업을 추적하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-189">Typically, when you find a failure in any of the operations using `Get-xDscOperation`, you would trace that operation to find out which of the events caused a failure.</span></span>

<span data-ttu-id="0761b-190">`SequenceID` 매개 변수를 사용하여 특정 컴퓨터의 특정 작업에 대한 이벤트를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-190">Use the  `SequenceID` parameter to get the events for a specific operation for a specific computer.</span></span> <span data-ttu-id="0761b-191">예를 들어 `SequenceID`를 9로 지정하는 경우 `Trace-xDscOperaion`은 마지막 작업에서 9번째인 DSC 작업에 대한 추적을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-191">For example, if you specify a `SequenceID` of 9, `Trace-xDscOperaion` get the trace for the DSC operation that was 9th from the last operation:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -SequenceID 9

ComputerName   EventType    TimeCreated           Message                                                                                             
------------   ---------    -----------           -------                                                                                             
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.                
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM Running consistency engine.                                                                         
SRV1   OPERATIONAL  6/24/2016 10:51:52 AM The local configuration manager is updating the PSModulePath to WindowsPowerShell\Modules;C:\Prog...
SRV1   OPERATIONAL  6/24/2016 10:51:53 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer. 
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Consistency engine was run successfully.                                                            
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Job runs under the following LCM setting. ...                                                       
SRV1   OPERATIONAL  6/24/2016 10:51:54 AM Operation Consistency Check or Pull completed successfully. 
```

<span data-ttu-id="0761b-192">`Get-xDscOperation` cmldet에서 반환하는 특정 DSC 작업에 할당된 **GUID**를 전달하여 해당 DSC 작업에 대한 이벤트 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-192">Pass the **GUID** assigned to a specific DSC operation (as returned by the `Get-xDscOperation` cmldet) to get the event details for that DSC operation:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -JobID 9e0bfb6b-3a3a-11e6-9165-00155d390509

ComputerName   EventType    TimeCreated           Message                                                                                             
------------   ---------    -----------           -------                                                                                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 from computer NULL.                
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.                                                                         
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Starting consistency engine.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Current.mof.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.                                                                 
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature, [xDSCWebService]PSDSCPullServer. 
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with resource name [WindowsFeature]DSC...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[WindowsFeature]DSCServiceFeature] The operation 'Get...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCServiceFeature] True in 0.3130 sec...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCServiceFeature]                      
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with resource name [xDSCWebService]P...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Ensure           
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Port             
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check Physical Path ...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Check State            
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [[xDSCWebService]PSDSCPullServer] Get Full Path for We...
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCPullServer] True in 0.0160 seconds.
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCPullServer]                        
SRV1   VERBOSE      6/24/2016 11:36:56 AM [SRV1]:                            [] Consistency check completed.                          
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof                             
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.                                                            
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...                                                       
SRV1   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.                                         
SRV1   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCache.mof
```

<span data-ttu-id="0761b-193">`Trace-xDscOperation`에서는 분석, 디버그 및 작업 로그에서 이벤트를 집계하므로, 위에서 설명한 대로 이러한 로그를 사용하도록 설정하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-193">Note that, since `Trace-xDscOperation` aggregates events from the Analytic, Debug, and Operational logs, it will prompt you to enable these logs as described above.</span></span>

<span data-ttu-id="0761b-194">또는, `Trace-xDscOperation`의 출력을 변수에 저장하여 이벤트에 대한 정보를 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-194">Alternately, you can gather information on the events by saving the output of `Trace-xDscOperation` into a variable.</span></span> <span data-ttu-id="0761b-195">다음 명령을 사용하여 특정 DSC 작업에 대한 모든 이벤트를 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-195">You can use the following commands to display all the events for a particular DSC operation.</span></span>

```powershell
PS C:\DiagnosticsTest> $Trace = Trace-xDscOperation -SequenceID 4

PS C:\DiagnosticsTest> $Trace.Event
```

<span data-ttu-id="0761b-196">이렇게 하면 아래 출력과 같이 `Get-WinEvent` cmdlet과 동일한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-196">This will display the same results as the `Get-WinEvent` cmdlet, such as in the output below:</span></span>

```powershell
   ProviderName: Microsoft-Windows-DSC

TimeCreated                     Id LevelDisplayName Message                                                                                           
-----------                     -- ---------------- -------                                                                                           
6/23/2016 1:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 1:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 2:07:00 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 2:07:01 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 2:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 2:36:56 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 3:06:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 3:06:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 3:36:55 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 3:36:55 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 4:06:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 4:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 4:36:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 4:36:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 5:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 5:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 5:36:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 5:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 6:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 6:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 6:36:56 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 6:36:57 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 7:06:52 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 7:06:53 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 7:36:53 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.     
6/23/2016 7:36:54 AM          4343 Information      The DscTimer has successfully run LCM method PerformRequiredConfigurationChecks with flag 5.      
6/23/2016 8:06:54 AM          4312 Information      The DscTimer is running LCM method PerformRequiredConfigurationChecks with the flag set to 5.
```

<span data-ttu-id="0761b-197">먼저 `Get-xDscOperation`을 사용하여 컴퓨터에서의 마지막 몇 개 DSC 구성 실행을 나열하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-197">Ideally, you would first use `Get-xDscOperation` to list out the last few DSC configuration runs on your machines.</span></span> <span data-ttu-id="0761b-198">그런 다음에 `Trace-xDscOperation`으로 단일 작업(해당 SequenceID 또는 JobID 사용)을 검사하여 백그라운드에서 수행한 작업을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-198">Following this, you can examine any single operation (using its SequenceID or JobID) with `Trace-xDscOperation` to discover what it did behind the scenes.</span></span>

### <a name="getting-events-for-a-remote-computer"></a><span data-ttu-id="0761b-199">원격 컴퓨터에 대한 이벤트 가져오기</span><span class="sxs-lookup"><span data-stu-id="0761b-199">Getting events for a remote computer</span></span>

<span data-ttu-id="0761b-200">`Trace-xDscOperation` cmdlet의 `ComputerName` 매개 변수를 사용하여 원격 컴퓨터의 이벤트 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-200">Use the `ComputerName` parameter of the `Trace-xDscOperation` cmdlet to get the event details on a remote computer.</span></span> <span data-ttu-id="0761b-201">이렇게 하려면 먼저 원격 컴퓨터에서 원격 관리를 허용하도록 방화벽 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-201">Before you can do this, you have to create a firewall rule to allow remote administration on the remote computer:</span></span>

```powershell
New-NetFirewallRule -Name "Service RemoteAdmin" -DisplayName "Remote" -Action Allow
```
<span data-ttu-id="0761b-202">이제 호출에서 해당 컴퓨터를 `Trace-xDscOperation`으로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-202">Now you can specify that computer in your call to `Trace-xDscOperation`:</span></span>

```powershell
PS C:\DiagnosticsTest> Trace-xDscOperation -ComputerName SRV2 -Credential Get-Credential -SequenceID 5

ComputerName   EventType    TimeCreated           Message
------------   ---------    -----------           -------
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull started by user sid S-1-5-20 f...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Running consistency engine.
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Starting consistency...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Applying configuration from C:\Windows\System32\Configuration\Curr...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Parsing the configuration to apply.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM  Resource execution sequence :: [WindowsFeature]DSCServiceFeature,...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[WindowsFeature]DSCSer...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_RoleResource with re...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[WindowsFeature]DSCSer...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Resource ]  [[xDSCWebService]PSDSCP...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Executing operations for PS DSC resource MSFT_xDSCWebService with ...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ Start  Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Test     ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]: LCM:  [ End    Resource ]  [[xDSCWebService]PSDSCP...
SRV2   VERBOSE      6/24/2016 11:36:56 AM [SRV2]:                            [] Consistency check co...
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Consistency engine was run successfully.
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Job runs under the following LCM setting. ...
SRV2   OPERATIONAL  6/24/2016 11:36:56 AM Operation Consistency Check or Pull completed successfully.
SRV2   ANALYTIC     6/24/2016 11:36:56 AM Deleting file from C:\Windows\System32\Configuration\DSCEngineCach...
```

## <a name="my-resources-wont-update-how-to-reset-the-cache"></a><span data-ttu-id="0761b-203">리소스가 업데이트되지 않습니다: 캐시 재설정 방법</span><span class="sxs-lookup"><span data-stu-id="0761b-203">My resources won’t update: How to reset the cache</span></span>

<span data-ttu-id="0761b-204">DSC 엔진은 효율성 향상을 위해 PowerShell 모듈로서 구현하는 리소스를 캐시합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-204">The DSC engine caches resources implemented as a PowerShell module for efficiency purposes.</span></span> <span data-ttu-id="0761b-205">그러나 이렇게 하면 프로세스가 다시 시작되기 전까지 DSC가 캐시된 버전을 로드하게 되므로 리소스를 작성하고 동시에 테스트하는 경우 문제가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-205">However, this can cause problems when you are authoring a resource and testing it simultaneously because DSC will load the cached version until the process is restarted.</span></span> <span data-ttu-id="0761b-206">DSC가 최신 버전을 로드하도록 하는 유일한 방법은 DSC 엔진을 호스팅하는 프로세스를 명시적으로 종료하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-206">The only way to make DSC load the newer version is to explicitly kill the process hosting the DSC engine.</span></span>

<span data-ttu-id="0761b-207">마찬가지로, `Start-DscConfiguration`을 실행하는 경우, 사용자 지정 리소스를 추가하고 수정하면 컴퓨터를 다시 부팅하지 않으면, 또는 다시 부팅하기 전까지는 수정이 실행되지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-207">Similarly, when you run `Start-DscConfiguration`, after adding and modifying a custom resource, the modification may not execute unless, or until, the computer is rebooted.</span></span> <span data-ttu-id="0761b-208">이것은 DSC가 WMI 공급자 호스트 프로세스(WmiPrvSE)에서 실행되고, 일반적으로 한 번에 실행되는 WmiPrvSE 인스턴스가 많기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-208">This is because DSC runs in the WMI Provider Host Process (WmiPrvSE), and usually, there are many instances of WmiPrvSE running at once.</span></span> <span data-ttu-id="0761b-209">컴퓨터를 다시 부팅하면 호스트 프로세스가 다시 시작되고 캐시가 지워집니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-209">When you reboot, the host process is restarted and the cache is cleared.</span></span>

<span data-ttu-id="0761b-210">다시 부팅하지 않고도 구성을 성공적으로 재활용하고, 캐시를 지우려면, 호스트 프로세스를 중지했다가 다시 시작해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-210">To successfully recycle the configuration and clear the cache without rebooting, you must stop and then restart the host process.</span></span> <span data-ttu-id="0761b-211">이 작업은 인스턴스별로 수행할 수 있으며, 그에 따라 프로세스를 식별, 중지 및 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-211">This can be done on a per instance basis, whereby you identify the process, stop it, and restart it.</span></span> <span data-ttu-id="0761b-212">또는 아래 설명된 대로 `DebugMode`를 사용하여 PowerShell DSC 리소스를 다시 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-212">Or, you can use `DebugMode`, as demonstrated below, to reload the PowerShell DSC resource.</span></span>

<span data-ttu-id="0761b-213">인스턴스별로 DSC 엔진을 호스트하고 중지하는 프로세스를 식별하기 위해 DSC 엔진을 호스팅하는 WmiPrvSE의 프로세스 ID를 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-213">To identify which process is hosting the DSC engine and stop it on a per instance basis, you can list the process ID of the WmiPrvSE which is hosting the DSC engine.</span></span> <span data-ttu-id="0761b-214">그런 다음 공급자를 업데이트하려면, 아래 명령을 사용하여 WmiPrvSE 프로세스를 중지한 다음, **Start-DscConfiguration**을 다시 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-214">Then, to update the provider, stop the WmiPrvSE process using the commands below, and then run **Start-DscConfiguration** again.</span></span>

```powershell
###
### find the process that is hosting the DSC engine
###
$dscProcessID = Get-WmiObject msft_providers | 
Where-Object {$_.provider -like 'dsccore'} | 
Select-Object -ExpandProperty HostProcessIdentifier 

###
### Stop the process
###
Get-Process -Id $dscProcessID | Stop-Process
```

## <a name="using-debugmode"></a><span data-ttu-id="0761b-215">DebugMode 사용</span><span class="sxs-lookup"><span data-stu-id="0761b-215">Using DebugMode</span></span>

<span data-ttu-id="0761b-216">호스트 프로세스를 다시 시작할 때 항상 캐시가 지워지도록 하기 위해 `DebugMode`를 사용하도록 DSC LCM(로컬 구성 관리자)를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-216">You can configure the DSC Local Configuration Manager (LCM) to use `DebugMode` to always clear the cache when the host process is restarted.</span></span> <span data-ttu-id="0761b-217">**TRUE**로 설정하면, 엔진이 항상 PowerShell DSC 리소스를 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-217">When set to **TRUE**, it causes the engine to always reload the PowerShell DSC resource.</span></span> <span data-ttu-id="0761b-218">리소스를 작성을 완료하면, 다시 **FALSE**로 설정할 수 있으며, 엔진은 모듈을 캐싱하는 동작으로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-218">Once you are done writing your resource, you can set it back to **FALSE** and the engine will revert to its behavior of caching the modules.</span></span>

<span data-ttu-id="0761b-219">다음은 `DebugMode`가 캐시를 자동으로 새로 고칠 수 있는 방법을 보여 주는 데모입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-219">Following is a demonstration to show how `DebugMode` can automatically refresh the cache.</span></span> <span data-ttu-id="0761b-220">우선, 기본 구성을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-220">First, let’s look at the default configuration:</span></span>

```
PS C:\> Get-DscLocalConfigurationManager
 
 
AllowModuleOverwrite           : False
CertificateID                  : 
ConfigurationID                : 
ConfigurationMode              : ApplyAndMonitor
ConfigurationModeFrequencyMins : 30
Credential                     : 
DebugMode                      : False
DownloadManagerCustomData      : 
DownloadManagerName            : 
LocalConfigurationManagerState : Ready
RebootNodeIfNeeded             : False
RefreshFrequencyMins           : 15
RefreshMode                    : PUSH
PSComputerName                 :  
```

<span data-ttu-id="0761b-221">`DebugMode`가 **FALSE**로 설정된 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-221">You can see that `DebugMode` is set to **FALSE**.</span></span>

<span data-ttu-id="0761b-222">`DebugMode` 데모를 설정하려면 다음 PowerShell 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-222">To set up the `DebugMode` demonstration, use the following PowerShell resource:</span></span>

```powershell
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    "1" | Out-File -PSPath "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        $onlyProperty
    )
    return $false
} 
```

<span data-ttu-id="0761b-223">이제, `TestProviderDebugMode`라는 위의 리소스를 사용하여 구성을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-223">Now, author a configuration using the above resource called `TestProviderDebugMode`:</span></span>

```powershell
Configuration ConfigTestDebugMode
{
    Import-DscResource -Name TestProviderDebugMode
    Node localhost
    {
        TestProviderDebugMode test
        {
            onlyProperty = "blah"
        }
    }
}
ConfigTestDebugMode
```

<span data-ttu-id="0761b-224">파일 "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**"의 내용이 **1**인 것을 확인하게 될 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-224">You will see that the contents of file: “**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**” is **1**.</span></span>

<span data-ttu-id="0761b-225">이제, 다음 스크립트를 사용하여 공급자 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-225">Now, update the provider code using the following script:</span></span>

```powershell
$newResourceOutput = Get-Random -Minimum 5 -Maximum 30
$content = @"
function Get-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return @{onlyProperty = Get-Content -Path "$env:SystemDrive\OutputFromTestProviderDebugMode.txt"}
}
function Set-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    "$newResourceOutput" | Out-File -PSPath C:\OutputFromTestProviderDebugMode.txt
}
function Test-TargetResource
{
    param
    (
        [Parameter(Mandatory)]
        `$onlyProperty
    )
    return `$false
}
"@ | Out-File -FilePath "C:\Program Files\WindowsPowerShell\Modules\MyPowerShellModules\DSCResources\TestProviderDebugMode\TestProviderDebugMode.psm1
```

<span data-ttu-id="0761b-226">이 스크립트는 난수를 생성하고 그에 따라 공급자 코드를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-226">This script generates a random number and updates the provider code accordingly.</span></span> <span data-ttu-id="0761b-227">`DebugMode`가 false로 설정되면 파일 "**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**"의 내용은 결코 변경되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-227">With `DebugMode` set to false, the contents of the file “**$env:SystemDrive\OutputFromTestProviderDebugMode.txt**” are never changed.</span></span>

<span data-ttu-id="0761b-228">이제, 구성 스크립트에서 `DebugMode`를 **TRUE**로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-228">Now, set `DebugMode` to **TRUE** in your configuration script:</span></span>

```powershell
LocalConfigurationManager
{
    DebugMode = $true
} 
```

<span data-ttu-id="0761b-229">다시 위의 스크립트를 실행하면 파일의 내용이 매번 다른 것을 보게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0761b-229">When you run the above script again, you will see that the content of the file is different every time.</span></span> <span data-ttu-id="0761b-230">(`Get-DscConfiguration`를 실행하여 확인할 수 있습니다.)</span><span class="sxs-lookup"><span data-stu-id="0761b-230">(You can run `Get-DscConfiguration` to check it).</span></span> <span data-ttu-id="0761b-231">다음은 두 번의 추가 실행에 대한 결과입니다(결과는 스크립트를 실행하는 경우 다를 수 있음).</span><span class="sxs-lookup"><span data-stu-id="0761b-231">Below is the result of two additional runs (your results may be different when you run the script):</span></span>

```powershell
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
20                                      localhost                              
 
PS C:\> Get-DscConfiguration -CimSession (New-CimSession localhost)
 
onlyProperty                            PSComputerName                         
------------                            --------------                         
14                                      localhost
```

## <a name="see-also"></a><span data-ttu-id="0761b-232">참고 항목</span><span class="sxs-lookup"><span data-stu-id="0761b-232">See Also</span></span>

### <a name="reference"></a><span data-ttu-id="0761b-233">참조</span><span class="sxs-lookup"><span data-stu-id="0761b-233">Reference</span></span>
* [<span data-ttu-id="0761b-234">DSC 로그 리소스</span><span class="sxs-lookup"><span data-stu-id="0761b-234">DSC Log Resource</span></span>](logResource.md)

### <a name="concepts"></a><span data-ttu-id="0761b-235">개념</span><span class="sxs-lookup"><span data-stu-id="0761b-235">Concepts</span></span>
* [<span data-ttu-id="0761b-236">사용자 지정 Windows PowerShell 필요한 상태 구성 리소스 빌드</span><span class="sxs-lookup"><span data-stu-id="0761b-236">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

### <a name="other-resources"></a><span data-ttu-id="0761b-237">관련 자료</span><span class="sxs-lookup"><span data-stu-id="0761b-237">Other Resources</span></span>
* <span data-ttu-id="0761b-238">[Windows PowerShell Desired State Configuration Cmdlets(Windows PowerShell DSC(필요한 상태 구성) Cmdlet)](https://technet.microsoft.com/en-us/library/dn521624(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="0761b-238">[Windows PowerShell Desired State Configuration Cmdlets](https://technet.microsoft.com/en-us/library/dn521624(v=wps.630).aspx)</span></span>

