---
title: 목록 보기 (GroupBy) | Microsoft Docs
ms.custom: ''
ms.date: 09/13/2016
ms.reviewer: ''
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a2e66c86-83a7-4148-8575-c28d6d429d4f
caps.latest.revision: 6
ms.openlocfilehash: ad7ea457fe0f67bfa41f6bf81f36d4b2e4a76cb3
ms.sourcegitcommit: b6871f21bd666f9cd71dd336bb3f844cf472b56c
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/03/2019
ms.locfileid: "56860149"
---
# <a name="list-view-groupby"></a><span data-ttu-id="ca394-102">목록 보기(GroupBy)</span><span class="sxs-lookup"><span data-stu-id="ca394-102">List View (GroupBy)</span></span>

<span data-ttu-id="ca394-103">이 예제에서는 목록의 행 그룹으로 구분 하는 목록 뷰를 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-103">This example shows how to implement a list view that separates the rows of the list into groups.</span></span> <span data-ttu-id="ca394-104">이 목록 보기의 속성을 표시 합니다 [System.Serviceprocess.Servicecontroller? Displayproperty =](/dotnet/api/System.ServiceProcess.ServiceController) 에서 반환 된 개체를 [Get-service](/powershell/module/microsoft.powershell.management/get-service) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca394-104">This list view displays the properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects returned by the [Get-Service](/powershell/module/microsoft.powershell.management/get-service) cmdlet.</span></span> <span data-ttu-id="ca394-105">목록 뷰 구성 요소에 대 한 자세한 내용은 참조 [목록 뷰를 만들면](./creating-a-list-view.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-105">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>
<span data-ttu-id="ca394-106">이 예제에서는 목록의 행 그룹으로 구분 하는 목록 뷰를 구현 하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-106">This example shows how to implement a list view that separates the rows of the list into groups.</span></span> <span data-ttu-id="ca394-107">이 목록 보기의 속성을 표시 합니다 [System.Serviceprocess.Servicecontroller? Displayproperty =](/dotnet/api/System.ServiceProcess.ServiceController) 에서 반환 된 개체를 [Get-service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ca394-107">This list view displays the properties of the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects returned by the [Get-Service](/powershell/module/Microsoft.PowerShell.Management/Get-Service) cmdlet.</span></span> <span data-ttu-id="ca394-108">목록 뷰 구성 요소에 대 한 자세한 내용은 참조 [목록 뷰를 만들면](./creating-a-list-view.md)합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-108">For more information about the components of a list view, see [Creating a List View](./creating-a-list-view.md).</span></span>

### <a name="to-load-this-formatting-file"></a><span data-ttu-id="ca394-109">이 서식 파일을 로드 하려면</span><span class="sxs-lookup"><span data-stu-id="ca394-109">To load this formatting file</span></span>

1. <span data-ttu-id="ca394-110">이 항목의 예제 섹션에서 XML을 텍스트 파일로 복사 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-110">Copy the XML from the Example section of this topic into a text file.</span></span>

2. <span data-ttu-id="ca394-111">텍스트 파일을 저장 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-111">Save the text file.</span></span> <span data-ttu-id="ca394-112">추가 해야 합니다 `format.ps1xml` 서식 파일로 식별 하는 파일 확장명입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-112">Be sure to add the `format.ps1xml` extension to the file to identify it as a formatting file.</span></span>

3. <span data-ttu-id="ca394-113">Windows PowerShell을 열고 현재 세션으로 서식 파일을 로드 하려면 다음 명령을 실행: `Update-formatdata -prependpath PathToFormattingFile`합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-113">Open Windows PowerShell, and run the following command to load the formatting file into the current session: `Update-formatdata -prependpath PathToFormattingFile`.</span></span>

   > [!WARNING]
   > <span data-ttu-id="ca394-114">이 서식 파일에는 Windows PowerShell 형식 지정 파일에서 이미 정의 되어 있는 개체의 표시를 정의 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-114">This formatting file defines the display of an object that is already defined by a Windows PowerShell formatting file.</span></span> <span data-ttu-id="ca394-115">사용 해야 합니다는 `prependPath` 모듈로 파일 매개 변수 cmdlet을 실행 하 고 형식을 로드할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-115">You must use the `prependPath` parameter when you run the cmdlet, and you cannot load this formatting file as a module.</span></span>

## <a name="demonstrates"></a><span data-ttu-id="ca394-116">시연</span><span class="sxs-lookup"><span data-stu-id="ca394-116">Demonstrates</span></span>

<span data-ttu-id="ca394-117">이 서식 파일에 다음 XML 요소를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-117">This formatting file demonstrates the following XML elements:</span></span>

- <span data-ttu-id="ca394-118">합니다 [이름을](./name-element-for-view-format.md) 뷰에 대 한 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-118">The [Name](./name-element-for-view-format.md) element for the view.</span></span>

- <span data-ttu-id="ca394-119">합니다 [ViewSelectedBy](./viewselectedby-element-format.md) 어떤 개체를 뷰에 표시를 정의 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-119">The [ViewSelectedBy](./viewselectedby-element-format.md) element that defines what objects are displayed by the view.</span></span>

- <span data-ttu-id="ca394-120">합니다 [GroupBy](./viewselectedby-element-format.md) 개체의 새 그룹을 표시 되는 방식을 정의 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-120">The [GroupBy](./viewselectedby-element-format.md) element that defines how a new group of objects is displayed.</span></span>

- <span data-ttu-id="ca394-121">합니다 [ListControl](./listcontrol-element-format.md) 어떤 속성은 보기에서 표시를 정의 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-121">The [ListControl](./listcontrol-element-format.md) element that defines what property is displayed by the view.</span></span>

- <span data-ttu-id="ca394-122">합니다 [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) 목록 뷰의 행에 표시 되는 항목을 정의 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-122">The [ListItem](./listitem-element-for-listitems-for-listcontrol-format.md) element that defines what is displayed in a row of the list view.</span></span>

- <span data-ttu-id="ca394-123">합니다 [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) 표시 되는 속성을 정의 하는 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-123">The [PropertyName](./propertyname-element-for-listitem-for-listcontrol-format.md) element that defines which property is displayed.</span></span>

## <a name="example"></a><span data-ttu-id="ca394-124">예제</span><span class="sxs-lookup"><span data-stu-id="ca394-124">Example</span></span>

<span data-ttu-id="ca394-125">새 시작 하는 목록 보기를 정의 하는 다음 XML 때마다 그룹의 값을 [System.Serviceprocess.Servicecontroller.Status](/dotnet/api/System.ServiceProcess.ServiceController.Status) 속성 변경 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-125">The following XML defines a list view that starts a new group whenever the value of the [System.Serviceprocess.Servicecontroller.Status](/dotnet/api/System.ServiceProcess.ServiceController.Status) property changes.</span></span> <span data-ttu-id="ca394-126">각 그룹 시작 되 면 속성의 새 값을 포함 하는 사용자 지정 레이블이 표시 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-126">When each group is started, a custom label is displayed that includes the new value of the property.</span></span>

```xml
<Configuration>
  <ViewDefinitions>
    <View>
      <Name>System.ServiceProcess.ServiceController</Name>
      <ViewSelectedBy>
        <TypeName>System.ServiceProcess.ServiceController</TypeName>
      </ViewSelectedBy>
      <GroupBy>
        <PropertyName>Status</PropertyName>
        <Label>New Service Status</Label>
      </GroupBy>
      <ListControl>
        <ListEntries>
          <ListEntry>
            <ListItems>
              <ListItem>
                <PropertyName>Name</PropertyName>
              </ListItem>
              <ListItem>
                <PropertyName>DisplayName</PropertyName>
              </ListItem>
              <ListItem>
                <PropertyName>ServiceType</PropertyName>
              </ListItem>
            </ListItems>
          </ListEntry>
        </ListEntries>
      </ListControl>
    </View>
  </ViewDefinitions>
</Configuration>
```

<span data-ttu-id="ca394-127">다음 예제에서는 Windows PowerShell의 표시 하는 방법을 보여 줍니다는 [System.Serviceprocess.Servicecontroller? Displayproperty =](/dotnet/api/System.ServiceProcess.ServiceController) 이 서식 파일 로드 된 후 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-127">The following example shows how Windows PowerShell displays the [System.Serviceprocess.Servicecontroller?Displayproperty=Fullname](/dotnet/api/System.ServiceProcess.ServiceController) objects after this format file is loaded.</span></span> <span data-ttu-id="ca394-128">그룹 레이블을 전후 추가한 빈 줄은 Windows PowerShell에서 자동으로 추가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca394-128">The blank lines added before and after the group label are automatically added by Windows PowerShell.</span></span>

```powershell
Get-Service f*
```

```output
   New Service Status: Stopped

Name        : Fax
DisplayName : Fax
ServiceType : Win32OwnProcess

   New Service Status: Running

Name        : FCSAM
DisplayName : Microsoft Antimalware Service
ServiceType : Win32OwnProcess

   New Service Status: Stopped

Name        : fdPHost
DisplayName : Function Discovery Provider Host
ServiceType : Win32ShareProcess

   New Service Status: Running

Name        : FDResPub
DisplayName : Function Discovery Resource Publication
ServiceType : Win32ShareProcess

Name        : FontCache
DisplayName : Windows Font Cache Service
ServiceType : Win32ShareProcess

   New Service Status: Stopped

Name        : FontCache3.0.0.0
DisplayName : Windows Presentation Foundation Font Cache 3.0.0.0
ServiceType : Win32OwnProcess

   New Service Status: Running

Name        : FSysAgent
DisplayName : Microsoft Forefront System Agent
ServiceType : Win32OwnProcess

Name        : FwcAgent
DisplayName : Firewall Client Agent
ServiceType : Win32OwnProcess
```

## <a name="see-also"></a><span data-ttu-id="ca394-129">참고 항목</span><span class="sxs-lookup"><span data-stu-id="ca394-129">See Also</span></span>

[<span data-ttu-id="ca394-130">서식 파일의 예</span><span class="sxs-lookup"><span data-stu-id="ca394-130">Examples of Formatting Files</span></span>](./examples-of-formatting-files.md)

[<span data-ttu-id="ca394-131">서식 파일을 PowerShell 작성</span><span class="sxs-lookup"><span data-stu-id="ca394-131">Writing a PowerShell Formatting File</span></span>](./writing-a-powershell-formatting-file.md)