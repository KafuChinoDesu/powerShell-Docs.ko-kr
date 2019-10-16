---
ms.date: 06/12/2017
keywords: dsc,powershell,configuration,setup
title: 리소스 디자이너 도구 사용
ms.openlocfilehash: 4f678f4586c75c830bf876b891fe4784aa3b4e95
ms.sourcegitcommit: 18985d07ef024378c8590dc7a983099ff9225672
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952860"
---
# <a name="using-the-resource-designer-tool"></a><span data-ttu-id="dda09-103">리소스 디자이너 도구 사용</span><span class="sxs-lookup"><span data-stu-id="dda09-103">Using the Resource Designer tool</span></span>

> <span data-ttu-id="dda09-104">적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="dda09-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="dda09-105">리소스 디자이너 도구는 Windows PowerShell DSC(필요한 상태 구성) 리소스를 만드는 작업을 더 쉽게 해주고 **xDscResourceDesigner** 모듈에 의해 노출된 cmdlet 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-105">The Resource Designer tool is a set of cmdlets exposed by the **xDscResourceDesigner** module that make creating Windows PowerShell Desired State Configuration (DSC) resources easier.</span></span> <span data-ttu-id="dda09-106">이 리소스의 cmdlet은 MOF 스키마, 스크립트 모듈 및 새 리소스에 대한 디렉터리 구조를 만드는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-106">The cmdlets in this resource help create the MOF schema, the script module, and the directory structure for your new resource.</span></span> <span data-ttu-id="dda09-107">DSC 리소스에 대한 자세한 내용은 [Build Custom Windows PowerShell Desired State Configuration Resources(사용자 지정 Windows PowerShell 필요한 상태 구성 리소스 빌드)](authoringResource.md)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="dda09-107">For more information about DSC resources, see [Build Custom Windows PowerShell Desired State Configuration Resources](authoringResource.md).</span></span>
<span data-ttu-id="dda09-108">이 항목에서는 Active Directory 사용자를 관리하는 DSC 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-108">In this topic, we will create a DSC resource that manages Active Directory users.</span></span>
<span data-ttu-id="dda09-109">[Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet을 사용하여 **xDscResourceDesigner** 모듈을 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="dda09-109">Use the [Install-Module](/powershell/module/PowershellGet/Install-Module) cmdlet to install the **xDscResourceDesigner** module.</span></span>

><span data-ttu-id="dda09-110">**참고**: Install-Module은 PowerShell 5.0에 포함된 **PowerShellGet** 모듈에 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-110">**Note**: **Install-Module** is included in the **PowerShellGet** module, which is included in PowerShell 5.0.</span></span> <span data-ttu-id="dda09-111">[PackageManagement PowerShell 모듈 미리 보기](https://www.microsoft.com/en-us/download/details.aspx?id=49186)에서 PowerShell 3.0 및 4.0용 **PowerShellGet** 모듈을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-111">You can download the **PowerShellGet** module for PowerShell 3.0 and 4.0 at [PackageManagement PowerShell Modules Preview](https://www.microsoft.com/en-us/download/details.aspx?id=49186).</span></span>

## <a name="creating-resource-properties"></a><span data-ttu-id="dda09-112">리소스 속성 만들기</span><span class="sxs-lookup"><span data-stu-id="dda09-112">Creating resource properties</span></span>
<span data-ttu-id="dda09-113">가장 먼저 해야 할 일은 리소스가 노출할 속성에 대해 결정하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-113">The first thing we need to do is decide on properties that the resource will expose.</span></span> <span data-ttu-id="dda09-114">이 예의 경우, 다음 속성으로 Active Directory 사용자를 정의하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-114">For this example, we will define an Active Directory user with the following properties.</span></span>

<span data-ttu-id="dda09-115">매개 변수 이름 설명</span><span class="sxs-lookup"><span data-stu-id="dda09-115">Parameter name  Description</span></span>
* <span data-ttu-id="dda09-116">**UserName**: 사용자를 고유하게 식별하는 주요 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-116">**UserName**: Key property that uniquely identifies a user.</span></span>
* <span data-ttu-id="dda09-117">**Ensure**: 사용자 계정이 있음인지 또는 없음인지 여부를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-117">**Ensure**: Specifies whether the user account should be Present or Absent.</span></span> <span data-ttu-id="dda09-118">이 매개 변수는 두 개의 가능한 값만 갖습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-118">This parameter will have only two possible values.</span></span>
* <span data-ttu-id="dda09-119">**DomainCredential**: 사용자에 대한 도메인 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-119">**DomainCredential**: The domain password for the user.</span></span>
* <span data-ttu-id="dda09-120">**Password**: 필요한 경우 구성으로 사용자 암호를 변경할 수 있도록 해주는 사용자에 대한 원하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-120">**Password**: The desired password for the user to allow a configuration to change the user password if necessary.</span></span>

<span data-ttu-id="dda09-121">속성을 만들기 위해 우리는 **New-xDscResourceProperty** cmdlet을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-121">To create the properties, we use the **New-xDscResourceProperty** cmdlet.</span></span> <span data-ttu-id="dda09-122">다음 PowerShell 명령을 사용하면 위에서 설명한 속성이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-122">The following PowerShell commands create the properties described above.</span></span>

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet "Present", "Absent"
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a><span data-ttu-id="dda09-123">리소스 만들기</span><span class="sxs-lookup"><span data-stu-id="dda09-123">Create the resource</span></span>

<span data-ttu-id="dda09-124">이제 리소스 속성이 만들어졌으므로 **New-xDscResource** cmdlet을 호출하여 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-124">Now that the resource properties have been created, we can call the **New-xDscResource** cmdlet to create the resource.</span></span> <span data-ttu-id="dda09-125">**New-xDscResource** cmdlet에서는 속성 목록을 매개 변수로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-125">The **New-xDscResource** cmdlet takes the list of properties as parameters.</span></span> <span data-ttu-id="dda09-126">또한 모듈을 만들어야 하는 경로, 새 리소스의 이름 및 리소스가 들어 있는 모듈의 이름도 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-126">It also takes the path where the module should be created, the name of the new resource, and the name of the module in which it is contained.</span></span> <span data-ttu-id="dda09-127">다음 PowerShell 명령은 리소스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-127">The following PowerShell command creates the resource.</span></span>

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path 'C:\Program Files\WindowsPowerShell\Modules' –ModuleName Demo_DSCModule
```

<span data-ttu-id="dda09-128">**New-xDscResource** cmdlet은 MOF 스키마, 뼈대 리소스 스크립트, 새 리소스에 대한 필수 디렉터리 구조와 새 리소스를 노출하는 모듈에 대한 매니페스트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-128">The **New-xDscResource** cmdlet creates the MOF schema, a skeleton resource script, the required directory structure for your new resource, and a manifest for the module that exposes the new resource.</span></span>

<span data-ttu-id="dda09-129">MOF 스키마 파일은 **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**에 있으며 그 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-129">The MOF schema file is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, and its contents are as follows.</span></span>

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
  [Key] string UserName;
  [Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
  [Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
  [Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

<span data-ttu-id="dda09-130">리소스 스크립트는 **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-130">The resource script is at **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**.</span></span> <span data-ttu-id="dda09-131">이 스크립트는 리소스를 구현하는 실제 논리를 포함하지 않습니다. 실제 논리는 직접 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-131">It does not include the actual logic to implement the resource, which you must add yourself.</span></span> <span data-ttu-id="dda09-132">뼈대 스크립트의 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-132">The contents of the skeleton script are as follows.</span></span>

```powershell
function Get-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Collections.Hashtable])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $returnValue = @{
  UserName = [System.String]
  Ensure = [System.String]
  DomainAdminCredential = [System.Management.Automation.PSCredential]
  Password = [System.Management.Automation.PSCredential]
  }

  $returnValue
  #>
}


function Set-TargetResource
{
  [CmdletBinding()]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  #Include this line if the resource requires a system reboot.
  #$global:DSCMachineStatus = 1


}


function Test-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Boolean])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $result = [System.Boolean]

  $result
  #>
}


Export-ModuleMember -Function *-TargetResource
```

## <a name="updating-the-resource"></a><span data-ttu-id="dda09-133">리소스 업데이트</span><span class="sxs-lookup"><span data-stu-id="dda09-133">Updating the resource</span></span>

<span data-ttu-id="dda09-134">리소스의 매개 변수 목록을 추가하거나 수정해야 하는 경우 **Update-xDscResource** cmdlet을 호출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-134">If you need to add or modify the parameter list of the resource, you can call the **Update-xDscResource** cmdlet.</span></span> <span data-ttu-id="dda09-135">cmdlet은 새 매개 변수 목록으로 리소스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-135">The cmdlet updates the resource with a new parameter list.</span></span> <span data-ttu-id="dda09-136">이미 리소스 스크립트에서 논리를 추가한 경우 그대로 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-136">If you have already added logic in your resource script, it is left intact.</span></span>

<span data-ttu-id="dda09-137">예를 들어 리소스에서 사용자에 대한 마지막 로그인 시간을 포함하려고 한다고 가정할 경우,</span><span class="sxs-lookup"><span data-stu-id="dda09-137">For example, suppose you want to include the last log in time for the user in our resource.</span></span> <span data-ttu-id="dda09-138">리소스를 완전히 다시 작성하는 대신 **New-xDscResourceProperty**를 호출하여 새 속성을 만든 다음, **Update-xDscResource**를 호출하고 새 속성을 속성 목록에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-138">Rather than writing the resource again completely, you can call the **New-xDscResourceProperty** to create the new property, and then call **Update-xDscResource** and add your new property to the properties list.</span></span>

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description "For mapping users to their last log on time"
Update-xDscResource –Name 'Demo_ADUser' –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a><span data-ttu-id="dda09-139">리소스 스키마 테스트</span><span class="sxs-lookup"><span data-stu-id="dda09-139">Testing a resource schema</span></span>

<span data-ttu-id="dda09-140">리소스 디자이너 도구는 수동으로 작성한 MOF 스키마의 유효성을 테스트하는 데 사용할 수 있는 cmdlet을 하나 더 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-140">The Resource Designer tool exposes one more cmdlet that can be used to test the validity of a MOF schema that you have written manually.</span></span> <span data-ttu-id="dda09-141">**Test-xDscSchema** cmdlet을 호출하여 MOF 리소스 스키마의 경로를 매개 변수로 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-141">Call the **Test-xDscSchema** cmdlet, passing the path of a MOF resource schema as a parameter.</span></span> <span data-ttu-id="dda09-142">cmdlet이 스키마의 모든 오류를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="dda09-142">The cmdlet will output any errors in the schema.</span></span>

### <a name="see-also"></a><span data-ttu-id="dda09-143">참고 항목</span><span class="sxs-lookup"><span data-stu-id="dda09-143">See Also</span></span>

#### <a name="concepts"></a><span data-ttu-id="dda09-144">개념</span><span class="sxs-lookup"><span data-stu-id="dda09-144">Concepts</span></span>
[<span data-ttu-id="dda09-145">사용자 지정 Windows PowerShell 필요한 상태 구성 리소스 빌드</span><span class="sxs-lookup"><span data-stu-id="dda09-145">Build Custom Windows PowerShell Desired State Configuration Resources</span></span>](authoringResource.md)

#### <a name="other-resources"></a><span data-ttu-id="dda09-146">관련 자료</span><span class="sxs-lookup"><span data-stu-id="dda09-146">Other Resources</span></span>
[<span data-ttu-id="dda09-147">xDscResourceDesigner 모듈</span><span class="sxs-lookup"><span data-stu-id="dda09-147">xDscResourceDesigner Module</span></span>](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)