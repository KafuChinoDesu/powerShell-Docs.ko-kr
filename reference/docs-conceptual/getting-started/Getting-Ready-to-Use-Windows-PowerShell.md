---
ms.date: 2017-06-05
keywords: powershell,cmdlet
title: "Windows PowerShell 사용 준비"
ms.assetid: 6dc7052d-cc5a-4220-950f-98f963a2b587
ms.openlocfilehash: a87ec614a45f0b6c05c530110e52f87c646b3e8b
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/08/2017
---
# <a name="getting-ready-to-use-windows-powershell"></a>Windows PowerShell 사용 준비
Windows PowerShell을 설치하고 시작하는 경우 다음과 같은 설치 옵션을 고려합니다. 이러한 작업은 언제든지 수행할 수 있습니다.

- **도움말 파일을 설치합니다.** Windows PowerShell 3.0에 포함된 cmdlet은 도움말 파일이 함께 제공되지 않습니다. 그러나 [Update-Help](https://technet.microsoft.com/en-us/library/93e1d870-ace6-432b-8778-8920291d7545) cmdlet을 사용하여 최신 도움말 파일을 컴퓨터에 다운로드하고 설치할 수 있습니다. 파일을 설치한 후 [Get-Help](https://technet.microsoft.com/en-us/library/1f46eeb4-49d7-4bec-bb29-395d9b42f54a) cmdlet을 사용하여 명령줄에서 바로 표시할 수 있습니다. 자세한 내용은 [about_Updatable_Help](https://technet.microsoft.com/en-us/library/10bba75c-f4ac-4ca1-bbf3-8f34dd521ffe)를 참조하세요.

    도움말 파일을 설치하지 않아도 온라인에서 도움말 항목을 읽을 수 있습니다. 온라인 버전의 cmdlet 도움말 항목을 찾으려면 다음과 같이 입력합니다. `Get-Help <CmdletName> -Online`. TechNet 라이브러리에서 Windows PowerShell 도움말 항목을 찾으려면 [http://go.microsoft.com/fwlink/?LinkID=107116](http://go.microsoft.com/fwlink/?LinkID=107116)에서 시작합니다.

- **스크립트를 실행합니다.** Windows PowerShell의 보안을 유지하기 위해 Windows PowerShell의 기본 실행 정책은 **Restricted**입니다. 이 정책을 사용할 경우 cmdlet만 실행할 수 있고 스크립트는 실행할 수 없습니다. 스크립트를 실행하려면 [Set-ExecutionPolicy[PSITPro5_Security]](https://technet.microsoft.com/en-us/library/5690a0e1-495b-4e63-8280-65ead7bf01ab) cmdlet을 사용하여 실행 정책을 **AllSigned** 또는 **RemoteSigned**로 변경합니다. 컴퓨터에서 Administrators 그룹의 구성원만 이 cmdlet을 실행할 수 있습니다. 자세한 내용은 [about_Execution_Policies [v4]](https://technet.microsoft.com/en-us/library/347708dc-1515-4d74-978b-8334603472e6)를 참조하세요.

- **원격 기능을 사용하도록 설정합니다.** 다른 컴퓨터에서 원격 명령을 실행할 수 있도록 시스템이 이미 구성되었습니다. Windows Server 2012 R2 및 Windows Server 2012에서는 시스템이 원격 명령을 수신하도록 구성되어 있으므로 다른 컴퓨터가 로컬 컴퓨터에서 원격 명령을 실행할 수도 있습니다. 다른 버전의 Windows를 실행하는 컴퓨터가 원격 명령을 수신할 수 있게 하려면 원격으로 관리하려는 컴퓨터에서 [Enable-PSRemoting](https://technet.microsoft.com/en-us/library/19437c28-33b8-4ac1-9113-8439cc8beffb) cmdlet을 실행합니다. 컴퓨터에서 Administrators 그룹의 구성원만 이 cmdlet을 실행할 수 있습니다. 자세한 내용은 [about_Remote](https://technet.microsoft.com/en-us/library/9b4a5c87-9162-4adf-bdfe-fbc80b9b8970)를 참조하세요.

    참고: Windows PowerShell 2.0을 실행하는 컴퓨터에서 원격 기능을 사용하도록 설정한 경우 Windows Management Framework 3.0을 설치한 후에도 원격 기능을 사용할 수 있습니다. 그러나 Windows Management Framework 3.0을 설치한 후 Windows Server 2008(Windows Server 2008 R2 아님)에서 원격 기능을 사용하도록 다시 설정해야 합니다.

## <a name="see-also"></a>참고 항목
- [Windows PowerShell 설치](../setup/Installing-Windows-PowerShell.md)
- [Windows PowerShell 시작 [ps]](https://technet.microsoft.com/en-us/library/8ec8c2d7-8e7c-4722-a3d2-498fe5739a8e)

