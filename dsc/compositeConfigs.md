---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: dsc,powershell,configuration,setup
title: "구성 중첩"
ms.openlocfilehash: 4de53b94056df46d74923dda56e02841cfac2cd1
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/12/2017
---
# <a name="nesting-dsc-configurations"></a><span data-ttu-id="dfc88-103">DSC 구성 중첩</span><span class="sxs-lookup"><span data-stu-id="dfc88-103">Nesting DSC configurations</span></span>

<span data-ttu-id="dfc88-104">중첩된 구성(복합 구성이라고도 함)은 다른 구성 내에서 마치 리소스인 것처럼 호출되는 구성입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc88-104">A nested configuration (also called composite configuration) is a configuration that is called within another configuration as if it were a resource.</span></span>
<span data-ttu-id="dfc88-105">두 구성이 모두 같은 파일에 정의되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc88-105">Both configurations must be defined in the same file.</span></span>

<span data-ttu-id="dfc88-106">간단한 예를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dfc88-106">Let's look at a simple example:</span></span>

```powershell
Configuration FileConfig 
{
    param (
        [Parameter(Mandatory = $true)]
        [String] $CopyFrom,

        [Parameter(Mandatory = $true)]
        [String] $CopyTo
    )

    Import-DscResource -ModuleName PSDesiredStateConfiguration

    File FileTest
       {
           SourcePath = $CopyFrom
           DestinationPath = $CopyTo
           Ensure = 'Present'
       }
    
}

Configuration NestedFileConfig
{
    Node localhost
    {
        FileConfig NestedConfig
        {
            CopyFrom = 'C:\Test\TestFile.txt'
            CopyTo = 'C:\Test2'
        }
    }
}
```

<span data-ttu-id="dfc88-107">이 예에서 `FileConfig`는 `File` 리소스 블록에서 **SourcePath** 및 **DestinationPath** 속성에 대한 값으로 사용되는 두 개의 필수 매개 변수 즉, **CopyFrom** 및 **CopyTo**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc88-107">In this example, `FileConfig` takes two mandatory parameters,  **CopyFrom** and **CopyTo**, which are used as the values for the **SourcePath** and **DestinationPath** properties in the `File` resource block.</span></span> <span data-ttu-id="dfc88-108">`NestedConfig` 구성은 마치 리소스인 것처럼 `FileConfig`를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="dfc88-108">The `NestedConfig` configuration calls `FileConfig` as if it were a resource.</span></span>
<span data-ttu-id="dfc88-109">`NestedConfig` 리소스 블록의 속성(**CopyFrom** 및 **CopyTo**)은 `FileConfig` 구성의 매개 변수입니다.</span><span class="sxs-lookup"><span data-stu-id="dfc88-109">The properties in the `NestedConfig` resource block (**CopyFrom** and **CopyTo**) are the parameters of the `FileConfig` configuration.</span></span>

## <a name="see-also"></a><span data-ttu-id="dfc88-110">참고 항목</span><span class="sxs-lookup"><span data-stu-id="dfc88-110">See Also</span></span>

- [<span data-ttu-id="dfc88-111">복합 리소스--DSC 구성을 리소스로 사용</span><span class="sxs-lookup"><span data-stu-id="dfc88-111">Composite resources--Using a DSC configuration as a resource</span></span>](authoringResourceComposite.md)

