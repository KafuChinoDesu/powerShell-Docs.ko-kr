---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 80852bf750700d549de24e150ffd89ac55b7bf88
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
# <a name="network-switch-management-with-powershell"></a><span data-ttu-id="3f002-102">PowerShell을 사용하여 네트워크 스위치 관리</span><span class="sxs-lookup"><span data-stu-id="3f002-102">Network Switch Management with PowerShell</span></span>

<span data-ttu-id="3f002-103">**Get-NetworkSwitchEthernetPort** cmdlet은 인스턴스와 함께 다음과 같은 추가 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="3f002-103">The **Get-NetworkSwitchEthernetPort** cmdlet now returns the following additional information with instances:</span></span>

- <span data-ttu-id="3f002-104">IPAddress – 포트와 연결된 IP 주소</span><span class="sxs-lookup"><span data-stu-id="3f002-104">IPAddress – the IP address associated with the port</span></span>
- <span data-ttu-id="3f002-105">PortMode – 포트 모드: 액세스, 라우트 또는 트렁크</span><span class="sxs-lookup"><span data-stu-id="3f002-105">PortMode – the port mode: access, route, or trunk</span></span>
- <span data-ttu-id="3f002-106">AccessVLAN – 액세스 모드에서 이 포트와 연결된 VLAN의 ID</span><span class="sxs-lookup"><span data-stu-id="3f002-106">AccessVLAN – the ID of the VLAN associated with this port in access mode</span></span>
- <span data-ttu-id="3f002-107">TrunkedVLANList – 트렁크 모드에서 이 포트와 연결된 VLAN의 ID 목록</span><span class="sxs-lookup"><span data-stu-id="3f002-107">TrunkedVLANList – a list of IDs of VLANs associated with this port in trunk mode</span></span>

## <a name="fundamental-network-switch-management-with-windows-powershell"></a><span data-ttu-id="3f002-108">Windows PowerShell을 사용한 기본적인 네트워크 스위치 관리</span><span class="sxs-lookup"><span data-stu-id="3f002-108">Fundamental network switch management with Windows PowerShell</span></span>

<span data-ttu-id="3f002-109">WMF 5.0에서 도입된 네트워크 스위치 cmdlet을 사용하면 스위치, VLAN(가상 LAN) 및 기본 계층 2 네트워크 스위치 포트 구성을 Windows Server 2012 R2 로고 인증 네트워크 스위치에 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f002-109">The Network Switch cmdlets, introduced in WMF 5.0, enable you to apply switch, virtual LAN (VLAN), and basic Layer 2 network switch port configuration to Windows Server 2012 R2 logo-certified network switches.</span></span> <span data-ttu-id="3f002-110">Microsoft는 [DAL(데이터 센터 추상화 계층)](http://technet.microsoft.com/en-us/cloud/dal.aspx) 비전을 지원하고 이 공간에서 고객과 파트너에게 가치를 보여 주기 위해 최선을 다하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f002-110">Microsoft remains committed to supporting the [Datacenter Abstraction](http://technet.microsoft.com/en-us/cloud/dal.aspx) Layer (DAL) vision, and to show value for our customers and partners in this space.</span></span> <span data-ttu-id="3f002-111">이러한 cmdlet을 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3f002-111">Using these cmdlets you can perform:</span></span>

- <span data-ttu-id="3f002-112">다음과 같은 전역 스위치 구성:</span><span class="sxs-lookup"><span data-stu-id="3f002-112">Global switch configuration, such as:</span></span>
    - <span data-ttu-id="3f002-113">호스트 이름 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-113">Set host name</span></span>
    - <span data-ttu-id="3f002-114">스위치 배너 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-114">Set switch banner</span></span>
    - <span data-ttu-id="3f002-115">구성 유지</span><span class="sxs-lookup"><span data-stu-id="3f002-115">Persist configuration</span></span>
    - <span data-ttu-id="3f002-116">기능을 사용하거나 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-116">Enable or disable feature</span></span>

- <span data-ttu-id="3f002-117">VLAN 구성:</span><span class="sxs-lookup"><span data-stu-id="3f002-117">VLAN configuration:</span></span>
    - <span data-ttu-id="3f002-118">VLAN 만들기 또는 제거</span><span class="sxs-lookup"><span data-stu-id="3f002-118">Create or remove VLAN</span></span>
    - <span data-ttu-id="3f002-119">VLAN을 사용하거나 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-119">Enable or disable VLAN</span></span>
    - <span data-ttu-id="3f002-120">VLAN 열거</span><span class="sxs-lookup"><span data-stu-id="3f002-120">Enumerate VLAN</span></span>
    - <span data-ttu-id="3f002-121">VLAN의 식별 이름 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-121">Set friendly name to a VLAN</span></span>

- <span data-ttu-id="3f002-122">계층 2 포트 구성:</span><span class="sxs-lookup"><span data-stu-id="3f002-122">Layer 2 port configuration:</span></span>
    - <span data-ttu-id="3f002-123">포트 열거</span><span class="sxs-lookup"><span data-stu-id="3f002-123">Enumerate ports</span></span>
    - <span data-ttu-id="3f002-124">포트를 사용하거나 사용하지 않도록 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-124">Enable or disable ports</span></span>
    - <span data-ttu-id="3f002-125">포트 모드 및 속성 설정</span><span class="sxs-lookup"><span data-stu-id="3f002-125">Set port modes and properties</span></span>
    - <span data-ttu-id="3f002-126">포트의 트렁크 또는 액세스에 VLAN 추가 또는 연결</span><span class="sxs-lookup"><span data-stu-id="3f002-126">Add or associate VLAN to Trunk or Access on the port</span></span>

<span data-ttu-id="3f002-127">모든 NetworkSwitch cmdlet을 검색하여 탐색을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="3f002-127">Start exploring by looking for all of the NetworkSwitch cmdlets!</span></span>

```powershell
PS> Get-Command *-NetworkSwitch*

| CommandType | Name                                      | Source        |
|-------------|-------------------------------------------|---------------|
|             |                                           |               |
| Function    | Disable-NetworkSwitchEthernetPort         | NetworkSwitch |
| Function    | Disable-NetworkSwitchFeature              | NetworkSwitch |
| Function    | Disable-NetworkSwitchVlan                 | NetworkSwitch |
| Function    | Enable-NetworkSwitchEthernetPort          | NetworkSwitch |
| Function    | Enable-NetworkSwitchFeature               | NetworkSwitch |
| Function    | Enable-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Get-NetworkSwitchEthernetPort             | NetworkSwitch |
| Function    | Get-NetworkSwitchFeature                  | NetworkSwitch |
| Function    | Get-NetworkSwitchGlobalData               | NetworkSwitch |
| Function    | Get-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | New-NetworkSwitchVlan                     | NetworkSwitch |
| Function    | Remove-NetworkSwitchEthernetPortIPAddress | NetworkSwitch |
| Function    | Remove-NetworkSwitchVlan                  | NetworkSwitch |
| Function    | Restore-NetworkSwitchConfiguration        | NetworkSwitch |
| Function    | Save-NetworkSwitchConfiguration           | NetworkSwitch |
| Function    | Set-NetworkSwitchEthernetPortIPAddress    | NetworkSwitch |
| Function    | Set-NetworkSwitchPortMode                 | NetworkSwitch |
| Function    | Set-NetworkSwitchPortProperty             | NetworkSwitch |
| Function    | Set-NetworkSwitchVlanProperty             | NetworkSwitch |
```

<span data-ttu-id="3f002-128">자세한 내용은 Jeffrey Snover WMF 5.0 미리 보기 알림 블로그 게시물(<http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx>)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="3f002-128">More information is available in Jeffrey Snover’s WMF 5.0 Preview announcement blog post: <http://blogs.technet.com/b/windowsserver/archive/2014/04/03/windows-management-framework-v5-preview.aspx></span></span>

