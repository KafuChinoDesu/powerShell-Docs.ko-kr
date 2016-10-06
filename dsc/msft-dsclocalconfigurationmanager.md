---
title: "MSFT_DSCLocalConfigurationManager 클래스"
ms.date: 2016-05-16
keywords: powershell,DSC
description: 
ms.topic: article
author: eslesar
manager: dongill
ms.prod: powershell
translationtype: Human Translation
ms.sourcegitcommit: 26db4a48af3aa3d6a9a2054fb85da8779626f284
ms.openlocfilehash: b9cb89bb120151df69e3cb26b50c3a0d15c23711

---

# MSFT_DSCLocalConfigurationManager 클래스

구성 파일의 상태를 제어하고 구성 에이전트를 사용해 구성을 적용하는 LCM(로컬 구성 관리자)입니다.

다음 구문은 MOF(Managed Object Format) 코드를 단순화한 것으로 상속된 속성이 모두 포함되어 있습니다.

## 구문
------

``` syntax
[ClassVersion("1.0.0"), dynamic, provider("dsccore"), AMENDMENT]
class MSFT_DSCLocalConfigurationManager
{
};
```

## 구성원
-------

**MSFT_DSCLocalConfigurationManager** 클래스에 다음 멤버가 있습니다.

-   [메서드][]

### 메서드

**MSFT_DSCLocalConfigurationManager** 클래스에 다음 메서드가 있습니다.

|방법 |설명 |
|:--- |:---|
| [ApplyConfiguration](msft-dsclocalconfigurationmanager-applyconfiguration.md)| 구성 에이전트를 사용해 보류 중인 구성을 적용합니다.| 
| [DisableDebugConfiguration](msft-dsclocalconfigurationmanager-disabledebugconfiguration.md)| DSC 리소스 디버깅을 사용하지 않도록 설정합니다.| 
| [EnableDebugConfiguration](msft-dsclocalconfigurationmanager-enabledebugconfiguration.md)| DSC 리소스 디버깅을 사용하도록 설정합니다.| 
| [GetConfiguration](msft-dsclocalconfigurationmanager-getconfiguration.md)| 구성 문서를 관리 노드로 보내고, 구성 에이전트의 **Get** 메서드를 사용해 구성을 적용합니다.| 
| [GetConfigurationResultOutput](msft-dsclocalconfigurationmanager-getconfigurationresultoutput.md)| 특정 작업과 관련된 구성 에이전트 출력을 가져옵니다.| 
| [GetConfigurationStatus](msft-dsclocalconfigurationmanager-getconfigurationstatus.md)| 구성 상태 기록을 가져옵니다.| 
| [GetMetaConfiguration](msft-dsclocalconfigurationmanager-getmetaconfiguration.md)| 구성 에이전트를 제어하는 데 사용되는 LCM 설정을 가져옵니다.| 
| [PerformRequiredConfigurationChecks](msft-dsclocalconfigurationmanager-performrequiredconfigurationchecks.md)| 일관성 확인을 시작합니다.| 
| [RemoveConfiguration](msft-dsclocalconfigurationmanager-removeconfiguration.md)| 구성 파일을 제거합니다.| 
| [ResourceGet](msft-dsclocalconfigurationmanager-resourceget.md)| DSC 리소스의 **Get** 메서드를 직접 호출합니다.| 
| [ResourceSet](msft-dsclocalconfigurationmanager-resourceset.md)| DSC 리소스의 **Set** 메서드를 직접 호출합니다.| 
| [ResourceTest](msft-dsclocalconfigurationmanager-resourcetest.md)| DSC 리소스의 **Test** 메서드를 직접 호출합니다.| 
| [롤백](msft-dsclocalconfigurationmanager-rollback.md)| 이전 구성으로 롤백합니다.| 
| [SendConfiguration](msft-dsclocalconfigurationmanager-sendconfiguration.md)| 구성 문서를 관리 노드로 보내고 보류 중인 변경으로 저장합니다.| 
| [SendConfigurationApply](msft-dsclocalconfigurationmanager-sendconfigurationapply.md)| 구성 문서를 관리 노드로 보내고, 구성 에이전트를 사용해 구성을 적용합니다.| 
| [SendConfigurationApplyAsync](msft-dsclocalconfigurationmanager-sendconfigurationapplyasync.md)| 구성 문서를 관리 노드로 보내고, 구성 에이전트를 사용해 구성을 적용합니다. GetConfigurationResultOutput을 사용해 결과 출력을 검색합니다.| 
| [SendMetaConfigurationApply](msft-dsclocalconfigurationmanager-sendmetaconfigurationapply.md)| 구성 에이전트를 제어하는 데 사용되는 LCM 설정을 구성합니다.| 
| [StopConfiguration](msft-dsclocalconfigurationmanager-stopconfiguration.md)| 진행 중인 구성을 중지합니다.| 
| [TestConfiguration](msft-dsclocalconfigurationmanager-testconfiguration.md)| 구성 문서를 관리 노드로 보내고, 문서에 대해 현재 구성을 확인합니다.| 



 

## 요구 사항
------------
>**MOF:** DscCore.mof

>**네임스페이스**: Root\Microsoft\Windows\DesiredStateConfiguration



 

 






<!--HONumber=Aug16_HO3-->


