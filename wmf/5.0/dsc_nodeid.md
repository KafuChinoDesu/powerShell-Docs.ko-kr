---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 5b9eea1c90bfd5a8cee3897d832bf7775a750308
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
<a id="separation-of-node-and-configuration-ids" class="xliff"></a>
# 노드 및 구성 ID의 분리

<a id="overview" class="xliff"></a>
## 개요

끌어오기 모드에서 DSC를 사용할 때 보다 유연하고 원활한 환경을 제공하기 위해 이번 릴리스에서 많은 기능을 추가했습니다. 이러한 기능은 각 노드에 대해 개별적으로 상태를 추적하고 정보를 보고하면서 여러 노드 간에 구성을 쉽게 설정하고 배포할 수 있는 유연성을 제공하기 위한 것입니다. 이러한 기능은 다음과 같습니다.

* 컴퓨터에 대한 구성을 식별하는 구성 이름. 이 이름은 여러 대상 노드에서 공유할 수 있습니다. 
* 단일 노드를 고유하게 식별하는 에이전트 ID
* 대상 노드가 끌어오기 서버에 처음으로 연결할 때만 수행되는 등록 단계

**참고:** 이러한 기능은 추가된 것이며 기존의 끌어오기 기능 및 개념을 대체하지 않습니다. 이번 릴리스에서 제공되는 새로운 끌어오기 서버에서는 이러한 새로운 기능이나 이전 기능을 사용할 수 있습니다.

자세한 내용은 [구성 이름을 사용하여 끌어오기 클라이언트 설정](https://msdn.microsoft.com/powershell/dsc/pullclientconfignames)를 참조하세요.

