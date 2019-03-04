---
title: 특성 선언을 자격 증명 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 96a5dcad-faed-44d8-8c80-321f10499710
caps.latest.revision: 6
ms.openlocfilehash: abdd6e915b768b8ac688b6fc8c3194723961765e
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56863399"
---
# <a name="credential-attribute-declaration"></a><span data-ttu-id="3ff5b-102">Credential 증명 특성 선언</span><span class="sxs-lookup"><span data-stu-id="3ff5b-102">Credential Attribute Declaration</span></span>

<span data-ttu-id="3ff5b-103">자격 증명 특성은 형식의 자격 증명 매개 변수를 사용 하 여 사용할 수 있는 선택적 특성 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 문자열 수 매개 변수에 인수로 전달 하는 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-103">The Credential attribute is an optional attribute that can be used with credential parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="3ff5b-104">이 특성 매개 변수 선언에 추가 되 면 Windows PowerShell 문자열 입력을 변환 된 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-104">When this attribute is added to a parameter declaration, Windows PowerShell converts the string input into a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span> <span data-ttu-id="3ff5b-105">예를 들어 합니다 [Get-credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet이이 특성을 사용 하 여 Windows powershell을 생성 합니다 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) cmdlet에서 반환 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-105">For example, the [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet uses this attribute to have Windows PowerShell generate the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object that is returned by the cmdlet.</span></span>
<span data-ttu-id="3ff5b-106">자격 증명 특성은 형식의 자격 증명 매개 변수를 사용 하 여 사용할 수 있는 선택적 특성 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 문자열 수 매개 변수에 인수로 전달 하는 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-106">The Credential attribute is an optional attribute that can be used with credential parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="3ff5b-107">이 특성 매개 변수 선언에 추가 되 면 Windows PowerShell 문자열 입력을 변환 된 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-107">When this attribute is added to a parameter declaration, Windows PowerShell converts the string input into a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object.</span></span> <span data-ttu-id="3ff5b-108">예를 들어 합니다 [Get-credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet이이 특성을 사용 하 여 Windows powershell을 생성 합니다 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) cmdlet에서 반환 되는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-108">For example, the [Get-Credential](/powershell/module/Microsoft.PowerShell.Security/Get-Credential) cmdlet uses this attribute to have Windows PowerShell generate the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object that is returned by the cmdlet.</span></span>

## <a name="syntax"></a><span data-ttu-id="3ff5b-109">구문</span><span class="sxs-lookup"><span data-stu-id="3ff5b-109">Syntax</span></span>

```csharp
[Credential]
```

## <a name="remarks"></a><span data-ttu-id="3ff5b-110">설명</span><span class="sxs-lookup"><span data-stu-id="3ff5b-110">Remarks</span></span>

- <span data-ttu-id="3ff5b-111">이 특성은 형식의 매개 변수에서 사용 되는 일반적으로 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 문자열 수 매개 변수에 인수로 전달 하는 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-111">Typically this attribute is used by parameters of type [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) so that a string can also be passed as an argument to the parameter.</span></span> <span data-ttu-id="3ff5b-112">경우는 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 개체는 매개 변수에 전달 되며, Windows PowerShell 아무 작업도 수행 하지.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-112">When a [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object is passed to the parameter, Windows PowerShell does nothing.</span></span>

- <span data-ttu-id="3ff5b-113">만들 때 합니다 [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) 개체를 Windows PowerShell 현재 호스트를 사용 하 여 사용자에 게 표시 되는 적절 한 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-113">When creating the [System.Management.Automation.Pscredential](/dotnet/api/System.Management.Automation.PSCredential) object, Windows PowerShell uses the current Host to display the appropriate prompts to the user.</span></span> <span data-ttu-id="3ff5b-114">예를 들어, 기본 호스트 프롬프트가 표시 됩니다는 사용자 이름 및 암호에 대 한이 특성을 사용 하는 경우.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-114">For example, the default Host displays a prompt for a user name and password when this attribute is used.</span></span> <span data-ttu-id="3ff5b-115">그러나 사용자 지정 호스트를 사용 하는 경우 다른 프롬프트를 정의 하는 다음 메시지를 표시 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-115">However, if a custom host is being used that defines a different prompt then that prompt would be displayed.</span></span>

- <span data-ttu-id="3ff5b-116">이 특성은 매개 변수 특성을 사용 하 여 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-116">This attribute is used with the Parameter attribute.</span></span> <span data-ttu-id="3ff5b-117">해당 특성에 대 한 자세한 내용은 참조 하세요. [매개 변수 특성 선언](./parameter-attribute-declaration.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-117">For more information about that attribute, see [Parameter Attribute Declaration](./parameter-attribute-declaration.md).</span></span>

- <span data-ttu-id="3ff5b-118">자격 증명 특성을 정의한 합니다 [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3ff5b-118">The credential attribute is defined by the [System.Management.Automation.Credentialattribute](/dotnet/api/System.Management.Automation.CredentialAttribute) class.</span></span>

## <a name="see-also"></a><span data-ttu-id="3ff5b-119">참고 항목</span><span class="sxs-lookup"><span data-stu-id="3ff5b-119">See Also</span></span>

[<span data-ttu-id="3ff5b-120">매개 변수 별칭</span><span class="sxs-lookup"><span data-stu-id="3ff5b-120">Parameter Aliases</span></span>](./parameter-aliases.md)

[<span data-ttu-id="3ff5b-121">매개 변수 특성 선언</span><span class="sxs-lookup"><span data-stu-id="3ff5b-121">Parameter Attribute Declaration</span></span>](./parameter-attribute-declaration.md)

<span data-ttu-id="3ff5b-122">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)(Windows PowerShell Cmdlet 작성)</span><span class="sxs-lookup"><span data-stu-id="3ff5b-122">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>