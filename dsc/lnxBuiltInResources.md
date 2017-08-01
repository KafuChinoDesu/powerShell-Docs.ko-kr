---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "Linux용 기본 제공 필요한 상태 구성 리소스"
ms.openlocfilehash: b85f32f7559d89bda566d35462cc613d73424c50
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
# <a name="built-in-desired-state-configuration-resources-for-linux"></a>Linux용 기본 제공 필요한 상태 구성 리소스

리소스는 PowerShell DSC(필요한 상태 구성) 스크립트를 작성하는 데 사용할 수 있는 구성 요소입니다. Linux용 DSC는 파일 및 폴더, 패키지, 환경 변수, 서비스 및 프로세스와 같은 리소스를 구성하기 위한 기본 제공 기능 집합과 함께 제공됩니다.

## <a name="built-in-resources"></a>기본 제공 리소스 

다음 표에서는 이러한 리소스와 이에 대해 자세히 설명하는 항목에 대한 링크 목록을 제공합니다.

* [nxArchive Resource](lnxArchiveResource.md)--특정 경로에 있는 보관 파일(.tar, .zip)의 압축을 푸는 메커니즘을 제공합니다.
* [nxEnvironment Resource](lnxEnvironmentResource.md)--대상 노드에 대한 환경 변수를 관리합니다. 
* [nxFile Resource](lnxFileResource.md)--Linux 파일 및 디렉터리를 관리합니다. 
* [nxFileLine Resource](lnxFileLineResource.md)--Linux 파일에 있는 개별 줄을 관리합니다. 
* [nxGroup Resource](lnxGroupResource.md)--로컬 Linux 그룹을 관리합니다. 
* [nxPackage Resource](lnxPackageResource.md)--Linux 노드에 있는 패키지를 관리합니다.
* [nxScript Resource](lnxScriptResource.md)--대상 노드에서 스크립트를 실행합니다.
* [nxService Resource](lnxServiceResource.md)--Linux 서비스를 관리합니다(데몬).
* [nxSshAuthorizedKeys Resource](lnxSshAuthorizedKeysResource.md)--Linux 사용자에 대한 공용 ssh 키를 관리합니다. 
* [nxUser Resource](lnxUserResource.md)--로컬 Linux 사용자를 관리합니다. 
  
