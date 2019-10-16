---
title: Cmdlet 개발 지침 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- development guidelines [PowerShell Programmer's Guide]
- cmdlets [PowerShell Programmer's Guide], development guidelines
ms.assetid: c30cc3c0-e958-4a8f-b81f-1e38de772f13
caps.latest.revision: 14
ms.openlocfilehash: 89c7682e87fa6f389349fc44275be0d2ffc83957
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72369922"
---
# <a name="cmdlet-development-guidelines"></a><span data-ttu-id="199aa-102">Cmdlet 개발 지침</span><span class="sxs-lookup"><span data-stu-id="199aa-102">Cmdlet Development Guidelines</span></span>

<span data-ttu-id="199aa-103">이 단원의 항목에서는 올바른 형식의 cmdlet을 생성 하는 데 사용할 수 있는 개발 지침을 제공 합니다.</span><span class="sxs-lookup"><span data-stu-id="199aa-103">The topics in this section provide development guidelines that you can use to produce well-formed cmdlets.</span></span> <span data-ttu-id="199aa-104">Windows PowerShell 런타임이 제공 하는 일반적인 기능을 활용 하 고 이러한 지침에 따라 최소한의 노력으로 강력한 cmdlet을 개발 하 고 사용자에 게 일관 된 환경을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199aa-104">By leveraging the common functionality provided by the Windows PowerShell runtime and by following these guidelines, you can develop robust cmdlets with minimal effort and provide the user with a consistent experience.</span></span> <span data-ttu-id="199aa-105">또한 일반적인 기능에는 다시 테스트가 필요 하지 않으므로 테스트 부담을 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="199aa-105">Additionally, you will reduce the test burden because common functionality does not require retesting.</span></span>

## <a name="in-this-section"></a><span data-ttu-id="199aa-106">이 섹션의 내용</span><span class="sxs-lookup"><span data-stu-id="199aa-106">In This Section</span></span>

- [<span data-ttu-id="199aa-107">필수 개발 지침</span><span class="sxs-lookup"><span data-stu-id="199aa-107">Required Development Guidelines</span></span>](./required-development-guidelines.md)

- [<span data-ttu-id="199aa-108">권장 되는 개발 지침</span><span class="sxs-lookup"><span data-stu-id="199aa-108">Strongly Encouraged Development Guidelines</span></span>](./strongly-encouraged-development-guidelines.md)

- [<span data-ttu-id="199aa-109">자문 개발 지침</span><span class="sxs-lookup"><span data-stu-id="199aa-109">Advisory Development Guidelines</span></span>](./advisory-development-guidelines.md)

## <a name="see-also"></a><span data-ttu-id="199aa-110">참고 항목</span><span class="sxs-lookup"><span data-stu-id="199aa-110">See Also</span></span>

<span data-ttu-id="199aa-111">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)(Windows PowerShell Cmdlet 작성)</span><span class="sxs-lookup"><span data-stu-id="199aa-111">[Writing a Windows PowerShell Cmdlet](./writing-a-windows-powershell-cmdlet.md)</span></span>

[<span data-ttu-id="199aa-112">Windows PowerShell SDK</span><span class="sxs-lookup"><span data-stu-id="199aa-112">Windows PowerShell SDK</span></span>](../windows-powershell-reference.md)