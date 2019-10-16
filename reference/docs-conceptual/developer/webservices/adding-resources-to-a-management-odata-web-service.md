---
title: 관리 OData 웹 서비스에 리소스 추가 | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: e620bf6d-76be-47b0-a7a8-f43418f30c60
caps.latest.revision: 6
ms.openlocfilehash: b81a32b867795ae51c3f5308c2f82c31ed2747fa
ms.sourcegitcommit: 52a67bcd9d7bf3e8600ea4302d1fa8970ff9c998
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/15/2019
ms.locfileid: "72359822"
---
# <a name="adding-resources-to-a-management-odata-web-service"></a><span data-ttu-id="c1ff4-102">관리 OData 웹 서비스에 리소스 추가</span><span class="sxs-lookup"><span data-stu-id="c1ff4-102">Adding Resources to a Management OData Web Service</span></span>

<span data-ttu-id="c1ff4-103">이 예제에서는 관리 OData 스키마 디자이너를 사용 하 여 기존 관리 OData 웹 서비스에 리소스를 추가 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-103">This example demonstrates how to add a resource to an existing Management OData web service by using the Management OData Schema Designer.</span></span> <span data-ttu-id="c1ff4-104">[PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) 샘플은 프로세스 및 서버 리소스를 노출 하는 웹 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-104">The [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) sample creates a web service that exposes the Process and Server resources.</span></span> <span data-ttu-id="c1ff4-105">이 예제에서는 웹 서비스에 VM (가상 컴퓨터) 리소스를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-105">In this example, you will add a Virtual Machine (VM) resource to the web service.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1ff4-106">전제 조건</span><span class="sxs-lookup"><span data-stu-id="c1ff4-106">Prerequisites</span></span>

<span data-ttu-id="c1ff4-107">이 항목에서는 [Windows PowerShell 웹 서비스 만들기](./creating-a-management-odata-web-service.md)에 설명 된 대로 [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) 샘플을 다운로드 하 여 설치 하 고 [관리 OData 스키마 디자이너](https://marketplace.visualstudio.com/items?itemName=jlisc0.ManagementODataSchemaDesigner)를 다운로드 하 여 설치 했다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-107">This topic assumes that you have downloaded and installed the [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) sample as described in [Creating a Windows PowerShell Web Service](./creating-a-management-odata-web-service.md), and that you have downloaded and installed the [Management OData Schema Designer](https://marketplace.visualstudio.com/items?itemName=jlisc0.ManagementODataSchemaDesigner).</span></span> <span data-ttu-id="c1ff4-108">또한이 항목에서는 관리 Odata 끝점을 설정 하는 컴퓨터에 Hyper-v Windows PowerShell 모듈이 설치 되어 있다고 가정 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-108">This topic also assumes that you have the Hyper-V Windows PowerShell module installed on the computer where you set up the Management Odata endpoint.</span></span>

## <a name="adding-vm-as-a-resource-to-the-web-service"></a><span data-ttu-id="c1ff4-109">웹 서비스에 리소스로 VM 추가</span><span class="sxs-lookup"><span data-stu-id="c1ff4-109">Adding VM as a Resource to the Web Service</span></span>

<span data-ttu-id="c1ff4-110">첫 번째 단계는 기존 관리 OData 끝점에서 스키마 디자이너로 스키마를 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-110">The first step is to import the schema from the existing Management OData endpoint into the schema designer.</span></span> <span data-ttu-id="c1ff4-111">다음 절차에서는이 작업을 수행 하는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-111">The following procedure describes how to do that.</span></span>

#### <a name="importing-an-existing-schema-into-the-schema-designer"></a><span data-ttu-id="c1ff4-112">스키마 디자이너로 기존 스키마 가져오기</span><span class="sxs-lookup"><span data-stu-id="c1ff4-112">Importing an existing schema into the schema designer</span></span>

1. <span data-ttu-id="c1ff4-113">관리 OData 스키마 디자이너를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-113">Open the Management OData Schema Designer.</span></span>

2. <span data-ttu-id="c1ff4-114">**파일** 메뉴에서 **파일** 을 선택 합니다. **새로 만들기** **파일**.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-114">From the **File** menu, select **File** ; **New** ; **File**.</span></span> <span data-ttu-id="c1ff4-115">**새 파일** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-115">The **New File** dialog appears.</span></span>

3. <span data-ttu-id="c1ff4-116">**관리 OData 모델**을 클릭 한 다음 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-116">Click **Management OData Model**, and then click **Open**.</span></span>

4. <span data-ttu-id="c1ff4-117">주 창을 마우스 오른쪽 단추로 클릭 하 고 **스키마 파일** 을 클릭 합니다. **가져오기**.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-117">Right-click in the main window, and click **Schema file** ; **Import**.</span></span> <span data-ttu-id="c1ff4-118">**열기** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-118">The **Open** dialog appears.</span></span>

5. <span data-ttu-id="c1ff4-119">[PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) 샘플에 대 한 관리 OData 웹 서비스를 설정한 폴더로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-119">Navigate to the folder where you set up the Management OData web service for the [PswsRoleBasedPlugins](https://code.msdn.microsoft.com:443/windowsdesktop/PswsRoleBasedPlugins-9c79b75a) sample.</span></span> <span data-ttu-id="c1ff4-120">해당 샘플과 함께 제공 된 Windows PowerShell 스크립트를 사용 하 여 스크립트를 수정 하지 않고 끝점을 설정 하면 해당 폴더는 **C:\inetpub\wwwroot\Modata**됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-120">If you used the Windows PowerShell script provided with that sample to set up the endpoint without modifying the script, that folder is **C:\inetpub\wwwroot\Modata**.</span></span> <span data-ttu-id="c1ff4-121">Schema .mof를 선택 하 고 **열기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-121">Select Schema.mof, and click **Open**.</span></span>

   <span data-ttu-id="c1ff4-122">이 시점에서 텍스트 편집기에서 스키마 .mof 및 스키마 .xml 파일을 열고 프로세스 및 서비스 리소스에 대 한 매핑을 포함 하 고 있는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-122">At this point, open the Schema.mof and Schema.xml files in a text editor, and notice that they contain mappings for the Process and Service resources.</span></span> <span data-ttu-id="c1ff4-123">Schema .mof 파일은 DTMF ( [Distributed Management Task Force](https://www.dmtf.org/) ) Mof (Managed Object) 표준을 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-123">The Schema.mof file uses [Distributed Management  Task Force](https://www.dmtf.org/) (DTMF) Managed Object (MOF) standard.</span></span> <span data-ttu-id="c1ff4-124">Schema .xml 파일은 [리소스 매핑 스키마](./resource-mapping-schema.md)에 설명 된 xml 스키마를 사용 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-124">The schema.xml file uses an XML schema that is described in [Resource Mapping Schema](./resource-mapping-schema.md).</span></span>

   <span data-ttu-id="c1ff4-125">다음 절차에서는의 Hyper-v cmdlet을 스키마 모델로 가져오는 방법을 설명 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-125">The following procedure describes how to import Hyper-V cmdlets in to the schema model.</span></span>

#### <a name="importing-cmdlets-into-the-schema"></a><span data-ttu-id="c1ff4-126">Cmdlet을 스키마로 가져오기</span><span class="sxs-lookup"><span data-stu-id="c1ff4-126">Importing cmdlets into the schema</span></span>

1. <span data-ttu-id="c1ff4-127">스키마 디자이너 창의 빈 영역을 마우스 오른쪽 단추로 클릭 하 고 **Cmdlet 가져오기**를 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-127">Right-click on a blank area of the schema designer window, and click **Import Cmdlets**.</span></span> <span data-ttu-id="c1ff4-128">**Cmdlet 가져오기 마법사** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-128">The **Cmdlet Import Wizard** dialog appears.</span></span>

2. <span data-ttu-id="c1ff4-129">**로컬 컴퓨터** 가 선택 되어 있는지 확인 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-129">Make sure **Local Computer** is selected, and click **Next**.</span></span>

3. <span data-ttu-id="c1ff4-130">설치 된 Windows PowerShell 모듈이 선택 되어 있는지 확인 하 고 드롭다운 목록에서 Hyper-v를 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-130">Make sure that Installed Windows PowerShell Modules is selected, and select Hyper-V from the drop-down list.</span></span> <span data-ttu-id="c1ff4-131">**다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-131">click **Next**.</span></span> <span data-ttu-id="c1ff4-132">클릭 하 여 **다음**.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-132">Click **Next**.</span></span>

4. <span data-ttu-id="c1ff4-133">**Cmdlet 명사** 목록에서 **VM**을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-133">In the **Cmdlet Noun** list, select **VM**.</span></span> <span data-ttu-id="c1ff4-134">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-134">Click **Next**</span></span>

5. <span data-ttu-id="c1ff4-135">이 예에서는 cmdlet을 사용 하 여 Get 및 Delete 명령만 바인딩합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-135">For this example, we will bind only the Get and Delete commands with cmdlets.</span></span> <span data-ttu-id="c1ff4-136">**만들기** 및 **업데이트** 확인란의 선택을 취소 하 고 **가져오기** 및 **삭제** 확인란을 선택 했는지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-136">Clear the **CREATE** and **UPDATE** checkboxes, and make sure the **GET** and **DELETE** checkboxes are checked.</span></span> <span data-ttu-id="c1ff4-137">**GET**에 `Get-VM` cmdlet을 선택 했는지 확인 하 고 @no__t Cmdlet을 **삭제**하도록 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-137">Make sure that the `Get-VM` cmdlet is selected for **GET**, and the `Remove-VM` cmdlet is selected for **DELETE**.</span></span>

6. <span data-ttu-id="c1ff4-138">VM cmdlet에 대 한 메타 데이터는 출력 유형을 지정 하지 않으므로 cmdlet을 실행 하 여 출력 유형을 지정 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-138">Because the metadata for the VM cmdlets does not specify an output type, you will need to run the cmdlet to specify the output type.</span></span> <span data-ttu-id="c1ff4-139">**출력 유형 제공** 을 선택 하 고 **cmdlet 실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-139">Select **Provide output type** and click **Run cmdlet**.</span></span> <span data-ttu-id="c1ff4-140">**Cmdlet 실행** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-140">The **Run Cmdlet** dialog appears.</span></span> <span data-ttu-id="c1ff4-141">**실행**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-141">Click **Run**.</span></span> <span data-ttu-id="c1ff4-142">**CLR 유형** 상자는 `VirtualMachine` 유형으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-142">The **CLR Type** box is populated with the `VirtualMachine` type.</span></span> <span data-ttu-id="c1ff4-143">**확인**을 클릭 한 후 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-143">Click **OK**, then click **Next**.</span></span>

7. <span data-ttu-id="c1ff4-144">기본적으로 VirtualMachine 개체의 모든 속성이 선택 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-144">By default, all of the properties of the VirtualMachine object are selected.</span></span> <span data-ttu-id="c1ff4-145">웹 서비스에서이 리소스를 요청할 때 반환 되는 데이터의 일부로 원하지 않는 속성은 모두 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-145">You can clear any properties that you do not want as part of the data returned when you request this resource from the web service.</span></span> <span data-ttu-id="c1ff4-146">클릭 하 여 **다음**.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-146">Click **Next**.</span></span>

8. <span data-ttu-id="c1ff4-147">키로 사용할 속성을 하나 이상 선택 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-147">You must select at least one property to be used as a key.</span></span> <span data-ttu-id="c1ff4-148">목록에서 **이름** 을 선택 하 고 **다음**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-148">Select **Name** in the list, and click **Next**.</span></span>

9. <span data-ttu-id="c1ff4-149">다음 창에서는 관리 OData 리소스의 속성을 기본 cmdlet의 속성에 매핑할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-149">The next window allows you to map properties of the Management OData resource to properties of the underlying cmdlets.</span></span> <span data-ttu-id="c1ff4-150">마법사는 기본적으로 동일한 이름의 속성을 매핑합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-150">The wizard maps properties with identical names by default.</span></span> <span data-ttu-id="c1ff4-151">예를 들어 리소스의 `ComputerName` 속성은 cmdlet의 `ComputerName` 속성에 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-151">For example, the `ComputerName` property of the resource is mapped to the `ComputerName` property of the cmdlets.</span></span>  <span data-ttu-id="c1ff4-152">이렇게 하면 웹 서비스에 대 한 요청에서 `ComputerName` 속성을 지정 하 고 지정 하는 값을 `Get-VM` cmdlet으로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-152">This allows you to specify the `ComputerName` property in a request to the web service, and have the value you specify be passed to the `Get-VM` cmdlet.</span></span> <span data-ttu-id="c1ff4-153">`Id` 및 `Name`도 기본적으로 매핑됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-153">`Id` and `Name` are also mapped by default.</span></span>

   10. <span data-ttu-id="c1ff4-154">**다음**을 클릭 한 다음 **마침**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-154">Click **Next**, then click **Finish**.</span></span>

       <span data-ttu-id="c1ff4-155">이제 VM 리소스가 스키마 디자이너 창에 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-155">The VM resource now appears in the schema designer window.</span></span> <span data-ttu-id="c1ff4-156">리소스와 연결 된 속성 및 작업을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-156">You can examine the properties and operations associated with the resource.</span></span> <span data-ttu-id="c1ff4-157">다음에는 업데이트 된 스키마 파일을 웹 서비스의 가상 디렉터리로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-157">Next, you will export the updated schema files into the virtual directory for the web service.</span></span>

#### <a name="exporting-schema-files-from-the-schema-designer"></a><span data-ttu-id="c1ff4-158">스키마 디자이너에서 스키마 파일 내보내기</span><span class="sxs-lookup"><span data-stu-id="c1ff4-158">Exporting schema files from the schema designer</span></span>

1. <span data-ttu-id="c1ff4-159">스키마 디자이너 창의 빈 영역을 마우스 오른쪽 단추로 클릭 하 고 **스키마 파일** 을 클릭 합니다. **내보내기**.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-159">Right-click on a blank area of the schema designer window, and click **Schema file** ; **Export**.</span></span> <span data-ttu-id="c1ff4-160">다른 **이름으로 저장** 대화 상자가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-160">The **Save As** dialog appears.</span></span>

2. <span data-ttu-id="c1ff4-161">MOF 파일을 가져온 디렉터리와 동일한 디렉터리로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-161">Navigate to the same directory from where you imported the MOF file.</span></span> <span data-ttu-id="c1ff4-162">파일의 이름을 원래 MOF 파일 (기본적으로 Schema .mof)와 동일 하 게 이름을로 하 고 **저장**을 클릭 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-162">Name the file the same as the original MOF file (Schema.mof by default), and click **Save**.</span></span> <span data-ttu-id="c1ff4-163">기존 파일을 덮어쓸 것인지 확인 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-163">Confirm that you want to overwrite the existing file.</span></span>

   <span data-ttu-id="c1ff4-164">**다른 이름으로 저장** 대화 상자에는 명시적으로 명시 되어 있지 않지만 스키마와 스키마 .xml 파일이 모두 바뀝니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-164">Although it is not explicitly stated in the **Save As** dialog, this replaces both the Schema.mof and Schema.xml files.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1ff4-165">다음 단계</span><span class="sxs-lookup"><span data-stu-id="c1ff4-165">Next Steps</span></span>

<span data-ttu-id="c1ff4-166">관리 OData 웹 서비스에서 새 VM 리소스에 액세스 하기 전에 [역할 기반 권한 부여 구성](./configuring-role-based-authorization.md)에 설명 된 대로 Hyper-v Windows PowerShell 모듈에 대 한 액세스를 허용 하도록 RbacConfiguration 파일을 업데이트 해야 합니다. 웹 서비스를 다시 시작 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c1ff4-166">Before you access the new VM resource from the Management OData web service, you must update the RbacConfiguration.xml file to allow access to the Hyper-V Windows PowerShell module as described in [Configuring Role-based Authorization](./configuring-role-based-authorization.md), and you will also need to restart the web service.</span></span>