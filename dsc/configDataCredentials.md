---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: 구성 데이터의 자격 증명 옵션
ms.openlocfilehash: 6ddf82c2b63309255ec3187d650677a6c3c2afb0
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="credentials-options-in-configuration-data"></a><span data-ttu-id="7baef-103">구성 데이터의 자격 증명 옵션</span><span class="sxs-lookup"><span data-stu-id="7baef-103">Credentials Options in Configuration Data</span></span>
><span data-ttu-id="7baef-104">적용 대상: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="7baef-104">Applies To: Windows PowerShell 5.0</span></span>

## <a name="plain-text-passwords-and-domain-users"></a><span data-ttu-id="7baef-105">일반 텍스트 암호 및 도메인 사용자</span><span class="sxs-lookup"><span data-stu-id="7baef-105">Plain Text Passwords and Domain Users</span></span>

<span data-ttu-id="7baef-106">암호화하지 않고 자격 증명을 포함하는 DSC를 구성하면 일반 텍스트 암호에 대한 오류 메시지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-106">DSC configurations containing a credential without encryption will generate an error message about plain text passwords.</span></span>
<span data-ttu-id="7baef-107">또한 DSC에서는 도메인 자격 증명을 사용하는 경우 경고를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-107">Also, DSC will generate a warning when using domain credentials.</span></span>
<span data-ttu-id="7baef-108">이러한 오류 및 경고 메시지가 발생하지 않도록 하려면, DSC 구성 데이터 키워드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-108">To suppress these error and warning messages use the DSC configuration data keywords:</span></span>
* <span data-ttu-id="7baef-109">**PsDscAllowPlainTextPassword**</span><span class="sxs-lookup"><span data-stu-id="7baef-109">**PsDscAllowPlainTextPassword**</span></span>
* <span data-ttu-id="7baef-110">**PsDscAllowDomainUser**</span><span class="sxs-lookup"><span data-stu-id="7baef-110">**PsDscAllowDomainUser**</span></span>

> [!NOTE]
> <span data-ttu-id="7baef-111">일반적으로 암호화되지 않은 일반 텍스트 암호를 저장/전송하는 작업은 안전하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-111">Storing/transmitting plaintext passwords unencrypted is generally not secure.</span></span> <span data-ttu-id="7baef-112">이 항목의 뒷부분에 설명된 기술을 사용하여 자격 증명을 보호하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-112">Securing credentials by using the techniques covered later in this topic is recommended.</span></span>
> <span data-ttu-id="7baef-113">Azure Automation DSC 서비스를 사용하면 자격 증명을 중앙에서 관리하여 구성에서 컴파일하고 안전하게 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-113">The Azure Automation DSC service allows you to centrally manage credentials to be compiled in configurations and stored securely.</span></span>
> <span data-ttu-id="7baef-114">자세한 내용은 [DSC 구성 컴파일/자격 증명 자산](/azure/automation/automation-dsc-compile#credential-assets)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baef-114">For information, see: [Compiling DSC Configurations / Credential Assets](/azure/automation/automation-dsc-compile#credential-assets)</span></span>

<span data-ttu-id="7baef-115">다음은 일반 텍스트 자격 증명을 전달하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-115">The following is an example of passing plain text credentials:</span></span>

```powershell
#Prompt user for their credentials
#credentials will be unencrypted in the MOF
$promptedCreds = get-credential -Message "Please enter your credentials to generate a DSC MOF:"

# Store passwords in plaintext, in the document itself
# will also be stored in plaintext in the mof
$password = "ThisIsAPlaintextPassword" | ConvertTo-SecureString -asPlainText -Force
$username = "User1"
[PSCredential] $credential = New-Object System.Management.Automation.PSCredential($username,$password)

# DSC requires explicit confirmation before storing passwords insecurely
$ConfigurationData = @{
    AllNodes = @(
        @{
            # The "*" means "all nodes named in ConfigData" so we don't have to repeat ourselves
            NodeName="*"
            PSDscAllowPlainTextPassword = $true
        },
        #however, each node still needs to be explicitly defined for "*" to have meaning
        @{
            NodeName = "TestMachine1"
        },
        #we can also use a property to define node-specific passwords, although this is no more secure
        @{
            NodeName = "TestMachine2";
            UserName = "User2"
            LocalPassword = "ThisIsYetAnotherPlaintextPassword"
        }
        )
}
configuration unencryptedPasswordDemo
{
    Node "TestMachine1"
    {
        # We use the plaintext password to generate a new account
        User User1
        {
            UserName = $username
            Password = $credential
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }
        # We use the prompted password to add this account to the local admins group
        Group addToAdmin
        {
            # Ensure the user exists before we add the user to a group
            DependsOn = "[User]User1"
            Credential = $promptedCreds
            GroupName = "Administrators"
            Ensure = "Present"
            MembersToInclude = "User1"
        }
    }

    Node "TestMachine2"
    {
        # Now we'll use a node-specific password to this machine
        $password = $Node.LocalPass | ConvertTo-SecureString -asPlainText -Force
        $username = $node.UserName
        [PSCredential] $nodeCred = New-Object System.Management.Automation.PSCredential($username,$password)

        User User2
        {
            UserName = $username
            Password = $nodeCred
            Description = "local account"
            Ensure = "Present"
            Disabled = $false
            PasswordNeverExpires = $true
            PasswordChangeRequired = $false
        }

        Group addToAdmin
        {
            Credential = $domain
            GroupName = "Administrators"
            DependsOn = "[User]User2"
            Ensure = "Present"
            MembersToInclude = "User2"
        }
    }

}
# We declared the ConfigurationData in a local variable, but we need to pass it in to our configuration function
# We need to invoke the configuration function we created to generate a MOF
unencryptedPasswordDemo -ConfigurationData $ConfigurationData
# We need to pass the MOF to the machines we named.
#-wait: doesn't use jobs so we get blocked at the prompt until the configuration is done
#-verbose: so we can see what's going on and catch any errors
#-force: for testing purposes, I run start-dscconfiguration frequently + want to make sure i'm
#        not blocked by previous configurations that are still running
Start-DscConfiguration ./unencryptedPasswordDemo -verbose -wait -force
```

## <a name="handling-credentials-in-dsc"></a><span data-ttu-id="7baef-116">DSC에서의 자격 증명 처리</span><span class="sxs-lookup"><span data-stu-id="7baef-116">Handling Credentials in DSC</span></span>

<span data-ttu-id="7baef-117">기본적으로 DSC 구성 리소스는 `Local System`으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-117">DSC configuration resources run as `Local System` by default.</span></span>
<span data-ttu-id="7baef-118">그러나 일부 리소스는 `Package` 리소스가 특정 사용자 계정으로 소프트웨어를 설치해야 할 때와 같은 경우 자격 증명을 필요로 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-118">However, some resources need a credential, for example when the `Package` resource needs to install software under a specific user account.</span></span>

<span data-ttu-id="7baef-119">이전 리소스에서는 하드 코드된 `Credential` 속성 이름을 사용하여 이 문제를 처리했습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-119">Earlier resources used a hard-coded `Credential` property name to handle this.</span></span>
<span data-ttu-id="7baef-120">WMF 5.0에서는 모든 리소스에 대해 자동 `PsDscRunAsCredential` 속성을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-120">WMF 5.0 added an automatic `PsDscRunAsCredential` property for all resources.</span></span>
<span data-ttu-id="7baef-121">`PsDscRunAsCredential` 사용에 대한 자세한 내용은 [사용자 자격 증명을 사용하여 DSC 실행](runAsUser.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baef-121">For information about using `PsDscRunAsCredential`, see [Running DSC with user credentials](runAsUser.md).</span></span>
<span data-ttu-id="7baef-122">최신 리소스와 사용자 지정 리소스에서는 자격 증명에 대한 고유한 속성을 만드는 대신 이 자동 속성을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-122">Newer resources and custom resources can use this automatic property instead of creating their own property for credentials.</span></span>

> [!NOTE]
> <span data-ttu-id="7baef-123">일부 리소스의 디자인이 특정한 이유로 여러 자격 증명을 사용하게 되면 이러한 리소스는 고유한 자격 증명 속성을 갖게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-123">The design of some resources are to use multiple credentials for a specific reason, and they will have their own credential properties.</span></span>

<span data-ttu-id="7baef-124">리소스에 대해 사용 가능한 자격 증명 속성을 찾으려면 `Get-DscResource -Name ResourceName -Syntax`나 ISE의 Intellisense(`CTRL+SPACE`)를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="7baef-124">To find the available credential properties on a resource use either `Get-DscResource -Name ResourceName -Syntax` or the Intellisense in the ISE (`CTRL+SPACE`).</span></span>

```powershell
PS C:\> Get-DscResource -Name Group -Syntax
Group [String] #ResourceName
{
    GroupName = [string]
    [Credential = [PSCredential]]
    [DependsOn = [string[]]]
    [Description = [string]]
    [Ensure = [string]{ Absent | Present }]
    [Members = [string[]]]
    [MembersToExclude = [string[]]]
    [MembersToInclude = [string[]]]
    [PsDscRunAsCredential = [PSCredential]]
}
```

<span data-ttu-id="7baef-125">이 예제에서는 `PSDesiredStateConfiguration` 기본 제공 DSC 리소스 모듈의 [그룹](https://msdn.microsoft.com/powershell/dsc/groupresource) 리소스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-125">This example uses a [Group](https://msdn.microsoft.com/powershell/dsc/groupresource) resource from the `PSDesiredStateConfiguration` built-in DSC resource module.</span></span>
<span data-ttu-id="7baef-126">로컬 그룹을 만들고 구성원을 추가 또는 제거할 수 있으며,</span><span class="sxs-lookup"><span data-stu-id="7baef-126">It can create local groups and add or remove members.</span></span>
<span data-ttu-id="7baef-127">`Credential` 속성 및 자동 `PsDscRunAsCredential` 속성도 둘 다 받습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-127">It accepts both the `Credential` property and the automatic `PsDscRunAsCredential` property.</span></span>
<span data-ttu-id="7baef-128">그러나 리소스는 `Credential` 속성만 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-128">However, the resource only uses the `Credential` property.</span></span>

<span data-ttu-id="7baef-129">`PsDscRunAsCredential` 속성에 대한 자세한 내용은 [사용자 자격 증명을 사용하여 DSC 실행](runAsUser.md)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7baef-129">For more information about the `PsDscRunAsCredential` property, see [Running DSC with user credentials](runAsUser.md).</span></span>

## <a name="example-the-group-resource-credential-property"></a><span data-ttu-id="7baef-130">예: 그룹 리소스 자격 증명 속성</span><span class="sxs-lookup"><span data-stu-id="7baef-130">Example: The Group resource Credential property</span></span>

<span data-ttu-id="7baef-131">DSC는 `Local System`에서 실행되므로, DSC에는 이미 로컬 사용자 및 그룹을 변경할 권한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-131">DSC runs under `Local System`, so it already has permissions to change local users and groups.</span></span>
<span data-ttu-id="7baef-132">추가된 구성원이 로컬 계정이라면 자격 증명이 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-132">If the member added is a local account, then no credential is necessary.</span></span>
<span data-ttu-id="7baef-133">`Group` 리소스에서 로컬 그룹에 도메인 계정을 추가한다면, 자격 증명이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-133">If the `Group` resource adds a domain account to the local group, then a credential is necessary.</span></span>

<span data-ttu-id="7baef-134">Active Directory에 대한 익명 쿼리는 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-134">Anonymous queries to Active Directory are not allowed.</span></span>
<span data-ttu-id="7baef-135">`Group` 리소스의 `Credential` 속성은 Active Directory에 대해 쿼리하는 데 사용된 도메인 계정입니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-135">The `Credential` property of the `Group` resource is the domain account used to query Active Directory.</span></span>
<span data-ttu-id="7baef-136">대부분의 경우 사용자는 기본적으로 Active Directory에 있는 대부분의 개체에 대해 *읽기*가 가능하므로 이것은 일반 사용자 계정일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-136">For most purposes this could be a generic user account, because by default users can *read* most of the objects in Active Directory.</span></span>

## <a name="example-configuration"></a><span data-ttu-id="7baef-137">예제 구성</span><span class="sxs-lookup"><span data-stu-id="7baef-137">Example Configuration</span></span>

<span data-ttu-id="7baef-138">다음 코드 예제에서는 DSC를 사용하여 도메인 사용자로 로컬 그룹을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-138">The following example code uses DSC to populate a local group with a domain user:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred
```

<span data-ttu-id="7baef-139">이 코드는 오류 메시지와 경고 메시지를 모두 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-139">This code generates both an error and warning message:</span></span>

```
ConvertTo-MOFInstance : System.InvalidOperationException error processing
property 'Credential' OF TYPE 'Group': Converting and storing encrypted
passwords as plain text is not recommended. For more information on securing
credentials in MOF file, please refer to MSDN blog:
http://go.microsoft.com/fwlink/?LinkId=393729

At line:11 char:9
+   Group
At line:297 char:16
+     $aliasId = ConvertTo-MOFInstance $keywordName $canonicalizedValue
+                ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : InvalidOperation: (:) [Write-Error], InvalidOperationException
    + FullyQualifiedErrorId : FailToProcessProperty,ConvertTo-MOFInstance

WARNING: It is not recommended to use domain credential for node 'localhost'.
In order to suppress the warning, you can add a property named
'PSDscAllowDomainUser' with a value of $true to your DSC configuration data
for node 'localhost'.
```

<span data-ttu-id="7baef-140">이 예제에는 두 가지 문제가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-140">This example has two issues:</span></span>
1. <span data-ttu-id="7baef-141">오류에서는 일반 텍스트 암호는 권장되지 않는다고 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-141">An error explains that plain text passwords are not recommended</span></span>
2. <span data-ttu-id="7baef-142">경고에서는 도메인 자격 증명을 사용하지 말라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-142">A warning advises against using a domain credential</span></span>

## <a name="psdscallowplaintextpassword"></a><span data-ttu-id="7baef-143">PsDscAllowPlainTextPassword</span><span class="sxs-lookup"><span data-stu-id="7baef-143">PsDscAllowPlainTextPassword</span></span>

<span data-ttu-id="7baef-144">첫 번째 오류 메시지에는 설명이 있는 URL이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-144">The first error message has a URL with documentation.</span></span>
<span data-ttu-id="7baef-145">이 링크에서는 [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) 구조와 인증서를 사용하여 암호를 암호화하는 방법에 대해 설명입니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-145">This link explains how to encrypt passwords using a [ConfigurationData](https://msdn.microsoft.com/powershell/dsc/configdata) structure and a certificate.</span></span>
<span data-ttu-id="7baef-146">인증서 및 DSC에 대한 자세한 내용은 [이 게시물을 읽어 보세요](http://aka.ms/certs4dsc).</span><span class="sxs-lookup"><span data-stu-id="7baef-146">For more information on certificates and DSC [read this post](http://aka.ms/certs4dsc).</span></span>

<span data-ttu-id="7baef-147">일반 텍스트 암호를 적용하려면 다음과 같이 리소스의 구성 데이터 섹션에 `PsDscAllowPlainTextPassword` 키워드가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-147">To force a plain text password, the resource requires the `PsDscAllowPlainTextPassword` keyword in the configuration data section as follows:</span></span>

```powershell
Configuration DomainCredentialExample
{
    param
    (
        [PSCredential] $DomainCredential
    )
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    node localhost
    {
        Group DomainUserToLocalGroup
        {
            GroupName        = 'ApplicationAdmins'
            MembersToInclude = 'contoso\alice'
            Credential       = $DomainCredential
        }
    }
}

$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowPlainTextPassword = $true
        }
    )
}

$cred = Get-Credential -UserName contoso\genericuser -Message "Password please"
DomainCredentialExample -DomainCredential $cred -ConfigurationData $cd
```

> [!NOTE]
> <span data-ttu-id="7baef-148">`NodeName` 은 별표와 같을 수 없으며 특정 노드 이름은 필수입니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-148">`NodeName` cannot equal asterisk, a specific node name is mandatory.</span></span>

<span data-ttu-id="7baef-149">**Microsoft에서는 일반 텍스트 암호가 상당한 보안 위험이 있으므로 사용하지 말 것을 권고합니다.**</span><span class="sxs-lookup"><span data-stu-id="7baef-149">**Microsoft advises to avoid plain text passwords due to the significant security risk.**</span></span>

<span data-ttu-id="7baef-150">데이터가 항상 암호화되어 저장되기 때문에(전송 중, 서비스에서 대기 중 및 노드에서 대기 중) 유일한 예외는 Azure Automation DSC 서비스를 사용할 때입니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-150">An exception would be when using the Azure Automation DSC service, only because the data is always stored encrypted (in transit, at rest in the service, and at rest on the node).</span></span>

## <a name="domain-credentials"></a><span data-ttu-id="7baef-151">도메인 자격 증명</span><span class="sxs-lookup"><span data-stu-id="7baef-151">Domain Credentials</span></span>

<span data-ttu-id="7baef-152">예제 구성 스크립트를 다시 실행(암호화를 사용하든 사용하지 않든)해도 여전히 자격 증명에 대한 도메인 계정을 사용하지 않는 것이 좋다는 경고가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-152">Running the example configuration script again (with or without encryption), still generates the warning that using a domain account for a credential is not recommended.</span></span>
<span data-ttu-id="7baef-153">로컬 계정을 사용하면 다른 서버에 사용할 수 있는 도메인 자격 증명이 노출될 가능성을 없어집니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-153">Using a local account eliminates potential exposure of domain credentials that could be used on other servers.</span></span>

<span data-ttu-id="7baef-154">**DSC 리소스에서 자격 증명을 사용할 경우 가능하면 도메인 계정보다는 로컬 계정을 사용하도록 합니다.**</span><span class="sxs-lookup"><span data-stu-id="7baef-154">**When using credentials with DSC resources, prefer a local account over a domain account when possible.**</span></span>

<span data-ttu-id="7baef-155">자격 증명의 `Username` 속성에 '\' 또는 '\@'가 없다면 DSC에서는 이것을 도메인 계정으로 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-155">If there is a '\' or '@' in the `Username` property of the credential, then DSC will treat it as a domain account.</span></span>
<span data-ttu-id="7baef-156">사용자 이름의 도메인 부분에 "localhost", "127.0.0.1" 및 "::1"에 대한 예외가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-156">There is an exception for "localhost", "127.0.0.1", and "::1" in the domain portion of the user name.</span></span>

## <a name="psdscallowdomainuser"></a><span data-ttu-id="7baef-157">PSDscAllowDomainUser</span><span class="sxs-lookup"><span data-stu-id="7baef-157">PSDscAllowDomainUser</span></span>

<span data-ttu-id="7baef-158">위의 DSC `Group` 리소스 예제에서 Active Directory 도메인에 대해 쿼리하려면 도메인 계정이 *있어야 합니다*.</span><span class="sxs-lookup"><span data-stu-id="7baef-158">In the DSC `Group` resource example above, querying an Active Directory domain *requires* a domain account.</span></span>
<span data-ttu-id="7baef-159">이 경우 다음과 같이 `PSDscAllowDomainUser` 속성을 `ConfigurationData` 블록에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-159">In this case add the `PSDscAllowDomainUser` property to the `ConfigurationData` block as follows:</span></span>

```powershell
$cd = @{
    AllNodes = @(
        @{
            NodeName = 'localhost'
            PSDscAllowDomainUser = $true
            # PSDscAllowPlainTextPassword = $true
            CertificateFile = "C:\PublicKeys\server1.cer"
        }
    )
}
```

<span data-ttu-id="7baef-160">이제 구성 스크립트가 오류 또는 경고 없이 MOF 파일을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="7baef-160">Now the configuration script will generate the MOF file with no errors or warnings.</span></span>
