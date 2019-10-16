---
title: Cmdlet 특성 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- attributes [PowerShell SDK]
- attributes [PowerShell SDK], described
ms.assetid: d3f4f652-d929-4c27-9358-9baa390a094c
caps.latest.revision: 14
ms.openlocfilehash: 326cd408e86402974569fc76d5e473be5a56f0b6
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369962"
---
# <a name="cmdlet-attributes"></a><span data-ttu-id="51c02-102">Cmdlet 특성</span><span class="sxs-lookup"><span data-stu-id="51c02-102">Cmdlet Attributes</span></span>

<span data-ttu-id="51c02-103">Windows PowerShell은 사용자 코드 내에서 해당 기능을 구현 하지 않고 cmdlet에 일반적인 기능을 추가 하는 데 사용할 수 있는 여러 특성을 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-103">Windows PowerShell defines several attributes that you can use to add common functionality to your cmdlets without implementing that functionality within your own code.</span></span> <span data-ttu-id="51c02-104">여기에는 cmdlet 클래스로 Microsoft .NET Framework 클래스를 식별 하는 Cmdlet 특성, cmdlet에서 반환 되는 .NET Framework 형식을 지정 하는 OutputType 특성, 공용 속성을 cmdlet으로 식별 하는 매개 변수 특성이 포함 됩니다. 매개 변수 등</span><span class="sxs-lookup"><span data-stu-id="51c02-104">This includes the Cmdlet attribute that identifies a Microsoft .NET Framework class as a cmdlet class, the OutputType attribute that specifies the .NET Framework types returned by the cmdlet, the Parameter attribute that identifies public properties as cmdlet parameters, and more.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="51c02-105">이 섹션의 내용</span><span class="sxs-lookup"><span data-stu-id="51c02-105">In This Section</span></span>

<span data-ttu-id="51c02-106">[Cmdlet 코드의 특성](./attributes-in-cmdlet-code.md) Cmdlet 코드에서 특성을 사용 하는 경우의 이점을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-106">[Attributes in Cmdlet Code](./attributes-in-cmdlet-code.md) Describes the benefit of using attributes in cmdlet code.</span></span>

<span data-ttu-id="51c02-107">[특성 유형](./attribute-types.md) Cmdlet 클래스를 데코레이팅 할 수 있는 다양 한 특성에 대해 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-107">[Attribute Types](./attribute-types.md) Describes the different attributes that can decorate a cmdlet class.</span></span>

<span data-ttu-id="51c02-108">[별칭 특성 선언](./alias-attribute-declaration.md) Cmdlet 매개 변수 이름에 대 한 별칭을 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-108">[Alias Attribute Declaration](./alias-attribute-declaration.md) Describes how to define aliases for a cmdlet parameter name.</span></span>

<span data-ttu-id="51c02-109">[Cmdlet 특성 선언](./cmdlet-attribute-declaration.md) .NET Framework 클래스를 cmdlet으로 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-109">[Cmdlet Attribute Declaration](./cmdlet-attribute-declaration.md) Describes how to define a .NET Framework class as a cmdlet.</span></span>

<span data-ttu-id="51c02-110">[자격 증명 특성 선언](./credential-attribute-declaration.md) 문자열 입력을 [system.object](/dotnet/api/System.Management.Automation.PSCredential) 로 변환 하기 위한 지원을 추가 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-110">[Credential Attribute Declaration](./credential-attribute-declaration.md) Describes how to add support for converting string input into a [System.Management.Automation.PSCredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span>

<span data-ttu-id="51c02-111">[OutputType 특성 선언](./outputtype-attribute-declaration.md) Cmdlet에서 반환 되는 .NET Framework 유형을 지정 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-111">[OutputType attribute Declaration](./outputtype-attribute-declaration.md) Describes how to specify the .NET Framework types returned by the cmdlet.</span></span>

<span data-ttu-id="51c02-112">[매개 변수 특성 선언](./parameter-attribute-declaration.md) Cmdlet의 매개 변수를 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-112">[Parameter Attribute Declaration](./parameter-attribute-declaration.md) Describes how to define the parameters of a cmdlet.</span></span>

<span data-ttu-id="51c02-113">[Validatecount 특성 선언](./validatecount-attribute-declaration.md) 매개 변수에 허용 되는 인수 수를 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-113">[ValidateCount Attribute Declaration](./validatecount-attribute-declaration.md) Describes how to define how many arguments are allowed for a parameter.</span></span>

<span data-ttu-id="51c02-114">[ValidateLength 특성 선언](./validatelength-attribute-declaration.md) 매개 변수 인수의 길이 (문자 수)를 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-114">[ValidateLength Attribute Declaration](./validatelength-attribute-declaration.md) Describes how to define the length (in characters) of a parameter argument.</span></span>

<span data-ttu-id="51c02-115">[ValidatePattern 특성 선언](./validatepattern-attribute-declaration.md) 매개 변수 인수에 대 한 올바른 패턴을 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-115">[ValidatePattern Attribute Declaration](./validatepattern-attribute-declaration.md) Describes how to define the valid patterns for a parameter argument.</span></span>

<span data-ttu-id="51c02-116">[ValidateRange 특성 선언](./validaterange-attribute-declaration.md) 매개 변수 인수의 올바른 범위를 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-116">[ValidateRange Attribute Declaration](./validaterange-attribute-declaration.md) Describes how to define the valid range for a parameter argument.</span></span>

<span data-ttu-id="51c02-117">[ValidateSet 특성 선언](./validateset-attribute-declaration.md) 매개 변수 인수에 사용할 수 있는 값을 정의 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="51c02-117">[ValidateSet Attribute Declaration](./validateset-attribute-declaration.md) Describes how to define the possible values for a parameter argument.</span></span>

## <a name="reference"></a><span data-ttu-id="51c02-118">참조</span><span class="sxs-lookup"><span data-stu-id="51c02-118">Reference</span></span>

<span data-ttu-id="51c02-119">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)(Windows PowerShell Cmdlet 작성)</span><span class="sxs-lookup"><span data-stu-id="51c02-119">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>