---
title: "PowerShell 4.0에서 구성 ID를 사용하여 끌어오기 클라이언트 설정"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
ms.openlocfilehash: 730f2f26e2811996e79cf0073a4ef65cad390687
ms.sourcegitcommit: c732e3ee6d2e0e9cd8c40105d6fbfd4d207b730d
translationtype: HT
---
# <a name="setting-up-a-pull-client-using-configuration-id-in-powershell-40"></a>PowerShell 4.0에서 구성 ID를 사용하여 끌어오기 클라이언트 설정

>적용 대상: Windows PowerShell 4.0, Windows PowerShell 5.0

각 대상 노드는 끌어오기 모드를 사용하도록 지시 받고 끌어오기 서버에 연결하여 구성을 가져올 수 있는 URL을 받아야 합니다. 이를 수행하려면, 필요한 정보와 함께 LCM(로컬 구성 관리자)을 구성해야 합니다. LCM을 구성하려면 "메타 구성"으로 알려진 특수한 형식의 구성을 만듭니다. LCM 구성에 대한 자세한 내용은 [Windows PowerShell 4.0 필요한 상태 구성 로컬 구성 관리자](metaConfig4.md)를 참조하세요.

다음 스크립트는 "PullServer"라는 서버에서 구성을 끌어오도록 LCM을 구성합니다.

```powershell
Configuration SimpleMetaConfigurationForPull 
{ 
    LocalConfigurationManager 
    { 
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "WebDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30; 
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "http://PullServer:8080/PSDSCPullServer/PSDSCPullServer.svc"; AllowUnsecureConnection = “TRUE”}
    } 
} 
SimpleMetaConfigurationForPull -Output "."
```

스크립트에서 **DownloadManagerCustomData**는 끌어오기 서버의 URL을 전달하고, (이 예제의 경우) 보안되지 않은 연결을 허용합니다. 

이 스크립트가 실행되면, **SimpleMetaConfigurationForPull**이라는 새 출력 폴더가 생성되고, 그 안에 메타 구성 MOF 파일이 생깁니다.

구성을 적용하려면 **ComputerName**("localhost" 사용) 및 **Path**(대상 노드의 localhost.meta.mof 파일의 위치 경로)에 대한 매개 변수와 함께 **Set-DscLocalConfigurationManager**를 사용합니다. 예: 
```powershell
Set-DSCLocalConfigurationManager –ComputerName localhost –Path . –Verbose.
```

## <a name="configuration-id"></a>구성 ID
스크립트는 이전에 이 목적으로 만들어진 GUID에 LCM의 **ConfigurationID** 속성을 설정합니다(**New-Guid** cmdlet을 사용하여 GUID를 만들 수 있음). **ConfigurationID**는 LCM이 끌어오기 서버에서 적절한 구성의 찾는 데 사용하는 ID입니다. 끌어오기 서버의 구성 MOF 파일의 이름은 `ConfigurationID.mof`로 지정해야 합니다. 여기서 *ConfigurationID*는 대상 노드의 LCM의 **ConfigurationID** 속성의 값입니다.

## <a name="pulling-from-an-smb-server"></a>SMB 서버에서 끌어오기

끌어오기 서버가 웹 서비스가 아닌 SMB 파일 공유로 설정된 경우 **WebDownLoadManager** 대신 **DscFileDownloadManager**를 설정합니다.
**DscFileDownloadManager**는 **ServerUrl** 대신 **SourcePath** 속성을 사용합니다. 다음 스크립트는 "CONTOSO-SERVER"라는 서버에서 "SmbDscShare"라는 SMB 공유의 구성을 끌어오도록 LCM을 구성합니다.

```powershell
Configuration SimpleMetaConfigurationForPull 
{ 
    LocalConfigurationManager 
    { 
        ConfigurationID = "1C707B86-EF8E-4C29-B7C1-34DA2190AE24";
        RefreshMode = "PULL";
        DownloadManagerName = "DscFileDownloadManager";
        RebootNodeIfNeeded = $true;
        RefreshFrequencyMins = 30;
        ConfigurationModeFrequencyMins = 30; 
        ConfigurationMode = "ApplyAndAutoCorrect";
        DownloadManagerCustomData = @{ServerUrl = "\\CONTOSO-SERVER\SmbDscShare"}
    } 
} 
SimpleMetaConfigurationForPull -Output "."
```

## <a name="see-also"></a>참고 항목

- [DSC 웹 끌어오기 서버 설정](pullServer.md)
- [DSC SMB 끌어오기 서버 설정](pullServerSMB.md)

