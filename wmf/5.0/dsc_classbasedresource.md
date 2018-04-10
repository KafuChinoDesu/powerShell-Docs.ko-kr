---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 4def20aa95f66ab23c9eee575150bc3db02541d8
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/09/2018
---
# <a name="class-based-dsc-resources"></a>클래스 기반 DSC 리소스

## <a name="defining-dsc-resources-with-classes"></a>클래스를 사용하여 DSC 리소스 정의

피드백에 따라 클래스 기반 DSC 리소스 작성을 보다 간단하고 이해하기 쉽게 만들었습니다.
클래스 기반 DSC 리소스와 cmdlet DSC 리소스 공급자의 주요 차이점은 다음과 같습니다.

* 스키마에 대한 MOF 파일이 필요하지 않습니다.
* 모듈 폴더에서 **DSCResource** 하위 폴더가 필요하지 않습니다.
* PowerShell 모듈 파일에 여러 가지 DSC 리소스 클래스가 포함될 수 있습니다.

자세한 내용은 [PowerShell 클래스를 사용하여 사용자 지정 DSC 리소스 작성](https://msdn.microsoft.com/powershell/dsc/authoringresource)을 참조하세요.