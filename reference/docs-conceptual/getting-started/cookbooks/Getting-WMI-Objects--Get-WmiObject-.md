---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "WMI 개체 가져오기(Get WmiObject)"
ms.assetid: f0ddfc7d-6b5e-4832-82de-2283597ea70d
ms.openlocfilehash: e7b10648e91d1c0dc1424944e55177dc7407fe36
ms.sourcegitcommit: 598b7835046577841aea2211d613bb8513271a8b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/08/2017
---
# <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="f3530-103">WMI 개체 가져오기(Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="f3530-103">Getting WMI Objects (Get-WmiObject)</span></span>

## <a name="getting-wmi-objects-get-wmiobject"></a><span data-ttu-id="f3530-104">WMI 개체 가져오기(Get-WmiObject)</span><span class="sxs-lookup"><span data-stu-id="f3530-104">Getting WMI Objects (Get-WmiObject)</span></span>
<span data-ttu-id="f3530-105">WMI(Windows Management Instrumentation)는 다양한 정보를 일관되게 표시하므로 Windows 시스템 관리를 위한 핵심 기술입니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-105">Windows Management Instrumentation (WMI) is a core technology for Windows system administration because it exposes a wide range of information in a uniform manner.</span></span> <span data-ttu-id="f3530-106">WMI가 표시하는 정보의 양이 제한되어 있기 때문에 WMI 개체에 액세스하기 위한 Windows PowerShell cmdlet인 **Get-WmiObject**는 실제 작업을 수행하는 데 있어서 가장 유용한 도구 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-106">Because of how much WMI makes possible, the Windows PowerShell cmdlet for accessing WMI objects, **Get-WmiObject**, is one of the most useful for doing real work.</span></span> <span data-ttu-id="f3530-107">이 장에서는 Get-WmiObject를 사용하여 WMI 개체에 액세스하는 방법과 WMI 개체를 사용하여 특정 작업을 수행하는 방법을 차례로 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-107">We are going to discuss how to use Get-WmiObject to access WMI objects and then how to use WMI objects to do specific things.</span></span>

### <a name="listing-wmi-classes"></a><span data-ttu-id="f3530-108">WMI 클래스 표시</span><span class="sxs-lookup"><span data-stu-id="f3530-108">Listing WMI Classes</span></span>
<span data-ttu-id="f3530-109">대부분의 WMI 사용자가 겪는 첫 번째 문제는 WMI를 사용하여 수행할 수 있는 작업을 검색하려고 할 때 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-109">The first problem most WMI users encounter is trying to find out what can be done with WMI.</span></span> <span data-ttu-id="f3530-110">WMI 클래스는 관리 가능한 리소스를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-110">WMI classes describe the resources that can be managed.</span></span> <span data-ttu-id="f3530-111">이러한 WMI 클래스는 수백 개가 있고 일부 클래스에는 수십 개의 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-111">There are hundreds of WMI classes, some of which contain dozens of properties.</span></span>

<span data-ttu-id="f3530-112">**Get-WmiObject**는 이 문제를 해결하기 위해 WMI를 검색 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-112">**Get-WmiObject** addresses this problem by making WMI discoverable.</span></span> <span data-ttu-id="f3530-113">다음과 같이 입력하면 로컬 컴퓨터에서 사용할 수 있는 WMI 클래스의 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-113">You can get a list of the WMI classes available on the local computer by typing:</span></span>

```
PS> Get-WmiObject -List

__SecurityRelatedClass                  __NTLMUser9X
__PARAMETERS                            __SystemSecurity
__NotifyStatus                          __ExtendedStatus
Win32_PrivilegesStatus                  Win32_TSNetworkAdapterSettingError
Win32_TSRemoteControlSettingError       Win32_TSEnvironmentSettingError
...
```

<span data-ttu-id="f3530-114">다음과 같이 ComputerName 매개 변수를 사용하여 컴퓨터 이름과 IP 주소를 지정하면 원격 컴퓨터에서도 이 정보를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-114">You can retrieve the same information from a remote computer by using the ComputerName parameter, specifying a computer name or IP address:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
__ProviderRegistration                  __ObjectProviderRegistration
...
```

<span data-ttu-id="f3530-115">원격 컴퓨터에서 반환되는 클래스 목록은 컴퓨터가 실행 중인 운영 체제와 설치된 응용 프로그램에서 추가한 WMI 확장에 따라 다를 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-115">The class listing returned by remote computers may vary due to the specific operating system the computer is running and the particular WMI extensions added by installed applications.</span></span>

> [!NOTE]
> <span data-ttu-id="f3530-116">Get-WmiObject를 사용하여 원격 컴퓨터에 연결할 때는 원격 컴퓨터에서 WMI를 실행 중이어야 하고, 기본 구성에서는 사용 중인 계정이 원격 컴퓨터의 로컬 관리자 그룹에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-116">When using Get-WmiObject to connect to a remote computer, the remote computer must be running WMI and, under the default configuration, the account you are using must be in the local administrators group on the remote computer.</span></span> <span data-ttu-id="f3530-117">원격 시스템에는 Windows PowerShell을 설치하지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-117">The remote system does not need to have Windows PowerShell installed.</span></span> <span data-ttu-id="f3530-118">이 경우 관리자는 Windows PowerShell을 실행 중이지 않지만 WMI를 사용할 수 있는 운영 체제를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-118">This allows you to administer operating systems that are not running Windows PowerShell, but do have WMI available.</span></span>

<span data-ttu-id="f3530-119">로컬 시스템에 연결할 때 ComputerName을 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-119">You can even include the ComputerName when connecting to the local system.</span></span> <span data-ttu-id="f3530-120">로컬 컴퓨터의 이름, IP 주소(또는 루프백 주소 127.0.0.1) 또는 WMI 스타일 '.'를 컴퓨터 이름으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-120">You can use the local computer's name, its IP address (or the loopback address 127.0.0.1), or the WMI-style '.' as the computer name.</span></span> <span data-ttu-id="f3530-121">IP 주소가 192.168.1.90이고 이름이 Admin01인 컴퓨터에서 Windows PowerShell을 실행 중인 경우 다음 명령을 실행하면 이 컴퓨터에서 사용할 수 있는 모든 WMI 클래스 목록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-121">If you are running Windows PowerShell on a computer named Admin01 with IP address 192.168.1.90, the following commands will all return the WMI class listing for that computer:</span></span>

```
Get-WmiObject -List
Get-WmiObject -List -ComputerName .
Get-WmiObject -List -ComputerName Admin01
Get-WmiObject -List -ComputerName 192.168.1.90
Get-WmiObject -List -ComputerName 127.0.0.1
Get-WmiObject -List -ComputerName localhost
```

<span data-ttu-id="f3530-122">Get-WmiObject는 기본적으로 root/cimv2 네임스페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-122">Get-WmiObject uses the root/cimv2 namespace by default.</span></span> <span data-ttu-id="f3530-123">다른 WMI 네임스페이스를 지정하려면 다음과 같이 **Namespace** 매개 변수를 사용하고 해당 네임스페이스 경로를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-123">If you want to specify another WMI namespace, use the **Namespace** parameter and specify the corresponding namespace path:</span></span>

```
PS> Get-WmiObject -List -ComputerName 192.168.1.29 -Namespace root

__SystemClass                           __NAMESPACE
__Provider                              __Win32Provider
...
```

### <a name="displaying-wmi-class-details"></a><span data-ttu-id="f3530-124">WMI 클래스 세부 정보 표시</span><span class="sxs-lookup"><span data-stu-id="f3530-124">Displaying WMI Class Details</span></span>
<span data-ttu-id="f3530-125">WMI 클래스의 이름을 알고 있으면 이 이름을 사용하여 정보를 즉시 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-125">If you already know the name of a WMI class, you can use it to get information immediately.</span></span> <span data-ttu-id="f3530-126">예를 들어 컴퓨터에 대한 정보를 검색하는 데 일반적으로 사용되는 WMI 클래스 중 하나는 **Win32_OperatingSystem**입니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-126">For example, one of the WMI classes commonly used for retrieving information about a computer is **Win32_OperatingSystem**.</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName .

SystemDirectory : C:\WINDOWS\system32
Organization    : Global Network Solutions
BuildNumber     : 2600
RegisteredUser  : Oliver W. Jones
SerialNumber    : 12345-678-9012345-67890
Version         : 5.1.2600
```

<span data-ttu-id="f3530-127">이 명령에는 매개 변수가 모두 나와 있지만 불필요한 매개 변수를 표시하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-127">Although we are showing all of the parameters, the command can be expressed in a more succinct way.</span></span> <span data-ttu-id="f3530-128">로컬 시스템에 연결할 때는 **ComputerName** 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-128">The **ComputerName** parameter is not necessary when connecting to the local system.</span></span> <span data-ttu-id="f3530-129">여기에 이 매개 변수를 표시한 것은 가장 일반적인 경우를 보여 주고 이 매개 변수가 있다는 것을 알려 주기 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-129">We show it to demonstrate the most general case and remind you about the parameter.</span></span> <span data-ttu-id="f3530-130">**Namespace**는 기본적으로 root/cimv2로 설정되며 마찬가지로 생략될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-130">The **Namespace** defaults to root/cimv2, and can be omitted as well.</span></span> <span data-ttu-id="f3530-131">마지막으로 대부분의 cmdlet에서는 일반적인 매개 변수의 이름을 생략할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-131">Finally, most cmdlets allow you to omit the name of common parameters.</span></span> <span data-ttu-id="f3530-132">Get-WmiObject를 사용할 때 첫 번째 매개 변수의 이름을 지정하지 않으면 Windows PowerShell은 이 매개 변수를 **Class** 매개 변수로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-132">With Get-WmiObject, if no name is specified for the first parameter, Windows PowerShell treats it as the **Class** parameter.</span></span> <span data-ttu-id="f3530-133">즉, 다음과 같이 입력하여 위 명령을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-133">This means the last command could have been issued by typing:</span></span>

```
Get-WmiObject Win32_OperatingSystem
```

<span data-ttu-id="f3530-134">**Win32_OperatingSystem** 클래스에는 여기에 표시된 것보다 훨씬 더 많은 속성이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-134">The **Win32_OperatingSystem** class has many more properties than those displayed here.</span></span> <span data-ttu-id="f3530-135">Get-Member를 사용하면 이러한 속성을 모두 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-135">You can use Get-Member to see all the properties.</span></span> <span data-ttu-id="f3530-136">다음과 같이 WMI 클래스의 속성도 다른 개체 속성처럼 자동으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-136">The properties of a WMI class are automatically available like other object properties:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Get-Member -MemberType Property

   TypeName: System.Management.ManagementObject#root\cimv2\Win32_OperatingSyste
m

Name                                      MemberType Definition
----                                      ---------- ----------
__CLASS                                   Property   System.String __CLASS {...
...
BootDevice                                Property   System.String BootDevic...
BuildNumber                               Property   System.String BuildNumb...
...
```

#### <a name="displaying-non-default-properties-with-format-cmdlets"></a><span data-ttu-id="f3530-137">Format Cmdlet을 사용하여 기본 속성이 아닌 속성 표시</span><span class="sxs-lookup"><span data-stu-id="f3530-137">Displaying Non-Default Properties with Format Cmdlets</span></span>
<span data-ttu-id="f3530-138">기본적으로 표시되지 않는 **Win32_OperatingSystem** 클래스에 포함된 정보를 보려면 **Format** cmdlet을 사용하여 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-138">If you want information contained in the **Win32_OperatingSystem** class that is not displayed by default, you can display it by using the **Format** cmdlets.</span></span> <span data-ttu-id="f3530-139">예를 들어 사용 가능한 메모리 데이터를 보려면 다음과 같이 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-139">For example, if you want to display available memory data, type:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-Table -Property TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize TotalVisibleMem FreePhysicalMem FreeVirtualMemo FreeSpaceInPagi
                              ory              ry         ngFiles
--------------- --------------- --------------- --------------- ---------------
        2097024          785904          305808         2056724         1558232
```

> [!NOTE]
> <span data-ttu-id="f3530-140">**Format-Table**의 속성 이름에 와일드카드를 사용할 수 있으므로 마지막 파이프라인 요소를 **Format-Table -Property TotalV\&#42;,Free\&#42;**로 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-140">Wildcards work with property names in **Format-Table**, so the final pipeline element can be reduced to **Format-Table -Property TotalV\&#42;,Free\&#42;**</span></span>

<span data-ttu-id="f3530-141">다음과 같이 입력하여 메모리 데이터를 목록으로 표시하면 더 쉽게 읽을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f3530-141">The memory data might be more readable if you format it as a list by typing:</span></span>

```
PS> Get-WmiObject -Class Win32_OperatingSystem -Namespace root/cimv2 -ComputerName . | Format-List TotalVirtualMemorySize,TotalVisibleMemorySize,FreePhysicalMemory,FreeVirtualMemory,FreeSpaceInPagingFiles

TotalVirtualMemorySize : 2097024
TotalVisibleMemorySize : 785904
FreePhysicalMemory     : 301876
FreeVirtualMemory      : 2056724
FreeSpaceInPagingFiles : 1556644
```

