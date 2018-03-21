---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: modulewithpseditionsupport
ms.openlocfilehash: 8a762ddf307f47ecec8d2a63098e75cde97c391f
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="modules-with-compatible-powershell-editions"></a>호환되는 PowerShell 버전이 있는 모듈
버전 5.1부터 PowerShell은 다양한 기능 집합 및 플랫폼 호환성을 나타내는 다양한 버전으로 사용 가능합니다.

- **Desktop Edition:** .NET Framework에서 구축되며 Server Core 및 Windows 데스크톱과 같은 전체 설치 공간 버전의 Windows에서 실행되는 PowerShell 버전을 대상으로 하는 스크립트 및 모듈과의 호환성을 제공합니다.
- **Core Edition:** .NET Core에서 구축되며 Nano Server 및 Windows IoT와 같은 축소된 설치 공간 버전의 Windows에서 실행되는 PowerShell 버전을 대상으로 하는 스크립트 및 모듈과의 호환성을 제공합니다.

## <a name="the-running-edition-of-powershell-is-shown-in-the-psedition-property-of-psversiontable"></a>실행 중인 PowerShell 버전은 $PSVersionTable의 PSEdition 속성에 표시됩니다.
```powershell
$PSVersionTable

Name                           Value
----                           -----
PSVersion                      5.1.14300.1000
PSEdition                      Desktop
PSCompatibleVersions           {1.0, 2.0, 3.0, 4.0...}
CLRVersion                     4.0.30319.42000
BuildVersion                   10.0.14300.1000
WSManStackVersion              3.0
PSRemotingProtocolVersion      2.3
SerializationVersion           1.1.0.1
```

## <a name="module-authors-can-declare-their-modules-to-be-compatible-with-one-or-more-powershell-editions-using-the-compatiblepseditions-module-manifest-key-this-key-is-only-supported-on-powershell-51-or-later"></a>모듈 작성자는 CompatiblePSEditions 모듈 매니페스트 키를 사용하여 하나 이상의 PowerShell 에디션과 호환된다고 해당 모듈을 선언할 수 있습니다. 이 키는 PowerShell 5.1 이상에서만 지원됩니다.
*참고* 모듈 매니페스트를 CompatiblePSEditions 키로 지정하면 낮은 버전의 PowerShell에서 가져올 수 없습니다.

```powershell
New-ModuleManifest -Path .\TestModuleWithEdition.psd1 -CompatiblePSEditions Desktop,Core -PowerShellVersion 5.1
$ModuleInfo = Test-ModuleManifest -Path .\TestModuleWithEdition.psd1
$ModuleInfo.CompatiblePSEditions
Desktop
Core

$ModuleInfo | Get-Member CompatiblePSEditions

   TypeName: System.Management.Automation.PSModuleInfo

Name                 MemberType Definition
----                 ---------- ----------
CompatiblePSEditions Property   System.Collections.Generic.IEnumerable[string] CompatiblePSEditions {get;}

```
사용 가능한 모듈 목록을 가져올 경우 PowerShell 에디션별로 목록을 필터링할 수 있습니다.
```powershell
Get-Module -ListAvailable -PSEdition Desktop

    Directory: C:\Program Files\WindowsPowerShell\Modules


ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   1.0        ModuleWithPSEditions

Get-Module -ListAvailable -PSEdition Core | % CompatiblePSEditions
Desktop
Core

```

## <a name="module-authors-can-publish-a-single-module-targeting-to-either-or-both-powershell-editions-desktop-and-core"></a>모듈 작성자는 PowerShell 에디션(Desktop 및 Core) 중 하나 또는 둘 다를 대상으로 하는 단일 모듈을 게시할 수 있습니다. 

단일 모듈은 Desktop 및 Core 에디션 둘 다에서 작동할 수 있습니다. 이 경우 모듈 작성자는 $PSEdition 변수를 사용하여 RootModule 또는 모듈 매니페스트에 필수 논리를 추가해야 합니다.
모듈에는 CoreCLR 및 FullCLR 둘 다를 대상으로 하는 컴파일된 두 가지 DLL 집합이 있을 수 있습니다.
적절한 dll을 로드하기 위한 논리를 사용하여 모듈을 패키징하는 몇 가지 옵션은 다음과 같습니다.

### <a name="option-1-packaging-a-module-for-targeting-multiple-versions-and-multiple-editions-of-powershell"></a>옵션 1: PowerShell의 여러 버전 및 여러 에디션을 대상으로 하도록 모듈 패키징

#### <a name="module-folder-contents"></a>모듈 폴더 콘텐츠
- Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll 
- Microsoft.Windows.PowerShell.ScriptAnalyzer.dll 
- PSScriptAnalyzer.psd1
- PSScriptAnalyzer.psm1
- ScriptAnalyzer.format.ps1xml
- ScriptAnalyzer.types.ps1xml
- coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll 
- coreclr\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll 
- en-US\about_PSScriptAnalyzer.help.txt
- en-US\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll-Help.xml
- PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.BuiltinRules.dll 
- PSv3\Microsoft.Windows.PowerShell.ScriptAnalyzer.dll 
- Settings\CmdletDesign.psd1
- Settings\DSC.psd1
- Settings\ScriptFunctions.psd1
- Settings\ScriptingStyle.psd1
- Settings\ScriptSecurity.psd1

#### <a name="contents-of-psscriptanalyzerpsd1-file"></a>PSScriptAnalyzer.psd1 파일의 내용

```powershell
@{
 
# Author of this module
Author = 'Microsoft Corporation'

# Script module or binary module file associated with this manifest.
RootModule = 'PSScriptAnalyzer.psm1'

# Version number of this module.
ModuleVersion = '1.6.1'

# ---
}
```

#### <a name="contents-of-psscriptanalyzerpsm1-file"></a>PSScriptAnalyzer.psm1 파일의 내용
아래 논리는 현재 에디션 또는 버전에 따라 필요한 어셈블리를 로드합니다.

```powershell
#
# Script module for module 'PSScriptAnalyzer'
#
Set-StrictMode -Version Latest

# Set up some helper variables to make it easier to work with the module
$PSModule = $ExecutionContext.SessionState.Module
$PSModuleRoot = $PSModule.ModuleBase

# Import the appropriate nested binary module based on the current PowerShell version
$binaryModuleRoot = $PSModuleRoot


if (($PSVersionTable.Keys -contains "PSEdition") -and ($PSVersionTable.PSEdition -ne 'Desktop')) {
    $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'coreclr'
}
else
{
    if ($PSVersionTable.PSVersion -lt [Version]'5.0') {
        $binaryModuleRoot = Join-Path -Path $PSModuleRoot -ChildPath 'PSv3'
    }    
}

$binaryModulePath = Join-Path -Path $binaryModuleRoot -ChildPath 'Microsoft.Windows.PowerShell.ScriptAnalyzer.dll'
$binaryModule = Import-Module -Name $binaryModulePath -PassThru

# When the module is unloaded, remove the nested binary module that was loaded with it
$PSModule.OnRemove = {
    Remove-Module -ModuleInfo $binaryModule
} 

```

### <a name="option-2-use-psedition-variable-in-the-psd1-file-to-load-the-proper-dlls-and-nestedrequired-modules"></a>옵션 2: PSD1 파일의 $PSEdition 변수를 사용하여 적절한 DLL 및 중첩/필수 모듈 로드

PS 5.1 이상에서 $PSEdition 전역 변수는 모듈 매니페스트 파일에서 허용됩니다.
모듈 작성자는 이 변수를 사용하여 모듈 매니페스트 파일에 조건부 값을 지정할 수 있습니다. $PSEdition 변수는 제한된 언어 모드 또는 데이터 섹션에서 참조될 수 있습니다. 

*참고* 모듈 매니페스트를 CompatiblePSEditions 키로 지정하거나 $PSEdition 변수를 사용하면 낮은 버전의 PowerShell에서 가져올 수 없습니다.


#### <a name="sample-module-manifest-file-with-compatiblepseditions-key"></a>CompatiblePSEditions 키가 있는 샘플 모듈 매니페스트 파일

```powershell
@{ 
# - - -
 
# Script module or binary module file associated with this manifest.
RootModule = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrRM.dll'
}
else # Desktop
{
'clr\MyFullClrRM.dll'
}
 
# Supported PSEditions
CompatiblePSEditions = 'Desktop', 'Core'
 
# Modules to import as nested modules of the module specified in RootModule/ModuleToProcess
NestedModules = if($PSEdition -eq 'Core')
{
'coreclr\MyCoreClrNM1.dll',
'coreclr\MyCoreClrNM2.dll'
}
else # Desktop
{
'clr\MyFullClrNM1.dll',
'clr\MyFullClrNM2.dll'
}
 
# -- - -
}
```

#### <a name="module-contents"></a>모듈 콘텐츠

```powershell

PS C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions> dir -Recurse
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
d-----         7/5/2016   1:37 PM                clr                                                                                 
d-----         7/5/2016   1:36 PM                coreclr                                                                             
-a----         7/5/2016   1:34 PM           4906 ModuleWithEditions.psd1                                                             
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\clr
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
-a----         7/5/2016   1:35 PM              0 MyFullClrNM1.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyFullClrNM2.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyFullClrRM.dl                                                                      
 
    Directory: C:\Users\manikb\Documents\WindowsPowerShell\Modules\ModuleWithEditions\coreclr
 
Mode                LastWriteTime         Length Name                                                                                
----                -------------         ------ ----                                                                                
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM1.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyCoreClrNM2.dll                                                                    
-a----         7/5/2016   1:35 PM              0 MyCoreClrRM.dl                                                                      
```

## <a name="powershell-gallery-users-can-find-the-list-of-modules-supported-on-a-specific-powershell-edition-using-tags-pseditiondesktop-and-pseditioncore"></a>PowerShell 갤러리 사용자는 PSEdition_Desktop 및 PSEdition_Core 태그를 사용하여 특정 PowerShell 버전에서 지원되는 모듈 목록을 찾을 수 있습니다.
PSEdition_Desktop 및 PSEdition_Core 태그가 없는 모듈은 PowerShell Desktop 버전에서 제대로 작동하는 것으로 간주됩니다.

```powershell

# Find modules supported on PowerShell Desktop edition
Find-Module -Tag PSEditon_Desktop

# Find modules supported on PowerShell Core editions
Find-Module -Tag PSEditon_Core

```


## <a name="more-details"></a>자세한 내용
### <a name="scripts-with-pseditionsscriptscriptwithpseditionsupportmd"></a>[PSEditions가 있는 스크립트](../script/scriptwithpseditionsupport.md)
### <a name="pseditions-support-on-powershellgallerypsgallerypsgallerypseditionsmd"></a>[PowerShellGallery의 PSEditions 지원](../../psgallery/psgallery_pseditions.md)
### <a name="update-module-manifest-psgetupdate-modulemanifestmd"></a>[모듈 매니페스트 업데이트](./psget_update-modulemanifest.md)

