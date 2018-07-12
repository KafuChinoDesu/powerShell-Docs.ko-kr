---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 0e8d0cb1e4afa7bc791d45bfb0b981654cb09ed5
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892572"
---
# <a name="unified-and-consistent-state-and-status-representation"></a><span data-ttu-id="39c39-102">통합되고 일관된 상태 및 상태 표현</span><span class="sxs-lookup"><span data-stu-id="39c39-102">Unified and Consistent State and Status Representation</span></span>

<span data-ttu-id="39c39-103">이번 릴리스에서는 자동화 빌드 LCM 상태 및 DSC 상태에 대한 일련의 기능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-103">A series of enhancements have been made in this release for automations built LCM state and DSC status.</span></span> <span data-ttu-id="39c39-104">여기에는 통합되고 일관된 상태 및 상태 표현, `Get-DscConfigurationStatus` cmdlet에서 반환하는 상태 개체의 관리 가능한 datetime 속성 및 `Get-DscLocalConfigurationManager` cmdlet에서 반환하는 향상된 LCM 상태 세부 정보 속성이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-104">These include unified and consistent state and status representations, manageable datetime property of status objects returned by `Get-DscConfigurationStatus` cmdlet and enhanced LCM state details property returned by `Get-DscLocalConfigurationManager` cmdlet.</span></span>

<span data-ttu-id="39c39-105">다음 규칙에 따라 LCM 상태 및 DSC 작업 상태의 표현을 다시 찾아 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-105">The representation of LCM state and DSC operation status are revisited and unified according to following rules:</span></span>

1. <span data-ttu-id="39c39-106">처리되지 않은 리소스는 LCM 상태 및 DSC 상태에 영향을 주지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-106">Notprocessed resource does not impact LCM state and DSC status.</span></span>
2. <span data-ttu-id="39c39-107">LCM은 다시 부팅을 요청하는 리소스가 발견되면 추가 리소스 처리를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-107">LCM stop processing further resources once it encounters a resource that requests reboot.</span></span>
3. <span data-ttu-id="39c39-108">다시 부팅을 요청하는 리소스는 실제로 다시 부팅된 다음에야 원하는 상태가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-108">A resource that requests reboot is not in desired state until reboot actually happens.</span></span>
4. <span data-ttu-id="39c39-109">실패한 리소스가 발견되면 LCM은 추가 리소스가 실패 리소스에 종속되지 않는 한 계속 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-109">After encountering a resource that fails, LCM keeps processing further resources as long as they are not dependent on the failure one.</span></span>
5. <span data-ttu-id="39c39-110">`Get-DscConfigurationStatus` cmdlet에서 반환하는 전체 상태는 모든 리소스 상태의 상위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-110">The overall status returned by `Get-DscConfigurationStatus` cmdlet is the super set of all resources' status.</span></span>
6. <span data-ttu-id="39c39-111">PendingReboot 상태는 PendingConfiguration 상태의 상위 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-111">The PendingReboot state is a superset of PendingConfiguration state.</span></span>

   <span data-ttu-id="39c39-112">다음 표에서는 몇 가지 일반적인 시나리오의 결과 상태 및 상태 관련 속성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-112">The table below illustrates the resultant state and status related properties under a few typical scenarios.</span></span>

   | <span data-ttu-id="39c39-113">시나리오</span><span class="sxs-lookup"><span data-stu-id="39c39-113">Scenario</span></span>                    | <span data-ttu-id="39c39-114">LCMState</span><span class="sxs-lookup"><span data-stu-id="39c39-114">LCMState</span></span>       | <span data-ttu-id="39c39-115">상태</span><span class="sxs-lookup"><span data-stu-id="39c39-115">Status</span></span> | <span data-ttu-id="39c39-116">다시 부팅 요청</span><span class="sxs-lookup"><span data-stu-id="39c39-116">Reboot Requested</span></span>  | <span data-ttu-id="39c39-117">ResourcesInDesiredState</span><span class="sxs-lookup"><span data-stu-id="39c39-117">ResourcesInDesiredState</span></span>  | <span data-ttu-id="39c39-118">ResourcesNotInDesiredState</span><span class="sxs-lookup"><span data-stu-id="39c39-118">ResourcesNotInDesiredState</span></span> |
   |---------------------------------|----------------------|------------|---------------|------------------------------|--------------------------------|
   | <span data-ttu-id="39c39-119">S**^**</span><span class="sxs-lookup"><span data-stu-id="39c39-119">S**^**</span></span>                          | <span data-ttu-id="39c39-120">유휴 상태</span><span class="sxs-lookup"><span data-stu-id="39c39-120">Idle</span></span>                 | <span data-ttu-id="39c39-121">Success</span><span class="sxs-lookup"><span data-stu-id="39c39-121">Success</span></span>    | <span data-ttu-id="39c39-122">$false</span><span class="sxs-lookup"><span data-stu-id="39c39-122">$false</span></span>        | <span data-ttu-id="39c39-123">S</span><span class="sxs-lookup"><span data-stu-id="39c39-123">S</span></span>                            | <span data-ttu-id="39c39-124">$null</span><span class="sxs-lookup"><span data-stu-id="39c39-124">$null</span></span>                          |
   | <span data-ttu-id="39c39-125">F**^**</span><span class="sxs-lookup"><span data-stu-id="39c39-125">F**^**</span></span>                          | <span data-ttu-id="39c39-126">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="39c39-126">PendingConfiguration</span></span> | <span data-ttu-id="39c39-127">실패</span><span class="sxs-lookup"><span data-stu-id="39c39-127">Failure</span></span>    | <span data-ttu-id="39c39-128">$false</span><span class="sxs-lookup"><span data-stu-id="39c39-128">$false</span></span>        | <span data-ttu-id="39c39-129">$null</span><span class="sxs-lookup"><span data-stu-id="39c39-129">$null</span></span>                        | <span data-ttu-id="39c39-130">F</span><span class="sxs-lookup"><span data-stu-id="39c39-130">F</span></span>                              |
   | <span data-ttu-id="39c39-131">S,F</span><span class="sxs-lookup"><span data-stu-id="39c39-131">S,F</span></span>                             | <span data-ttu-id="39c39-132">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="39c39-132">PendingConfiguration</span></span> | <span data-ttu-id="39c39-133">실패</span><span class="sxs-lookup"><span data-stu-id="39c39-133">Failure</span></span>    | <span data-ttu-id="39c39-134">$false</span><span class="sxs-lookup"><span data-stu-id="39c39-134">$false</span></span>        | <span data-ttu-id="39c39-135">S</span><span class="sxs-lookup"><span data-stu-id="39c39-135">S</span></span>                            | <span data-ttu-id="39c39-136">F</span><span class="sxs-lookup"><span data-stu-id="39c39-136">F</span></span>                              |
   | <span data-ttu-id="39c39-137">F,S</span><span class="sxs-lookup"><span data-stu-id="39c39-137">F,S</span></span>                             | <span data-ttu-id="39c39-138">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="39c39-138">PendingConfiguration</span></span> | <span data-ttu-id="39c39-139">실패</span><span class="sxs-lookup"><span data-stu-id="39c39-139">Failure</span></span>    | <span data-ttu-id="39c39-140">$false</span><span class="sxs-lookup"><span data-stu-id="39c39-140">$false</span></span>        | <span data-ttu-id="39c39-141">S</span><span class="sxs-lookup"><span data-stu-id="39c39-141">S</span></span>                            | <span data-ttu-id="39c39-142">F</span><span class="sxs-lookup"><span data-stu-id="39c39-142">F</span></span>                              |
   | <span data-ttu-id="39c39-143">S<sub>1</sub>, F, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="39c39-143">S<sub>1</sub>, F, S<sub>2</sub></span></span> | <span data-ttu-id="39c39-144">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="39c39-144">PendingConfiguration</span></span> | <span data-ttu-id="39c39-145">실패</span><span class="sxs-lookup"><span data-stu-id="39c39-145">Failure</span></span>    | <span data-ttu-id="39c39-146">$false</span><span class="sxs-lookup"><span data-stu-id="39c39-146">$false</span></span>        | <span data-ttu-id="39c39-147">S<sub>1</sub>, S<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="39c39-147">S<sub>1</sub>, S<sub>2</sub></span></span> | <span data-ttu-id="39c39-148">F</span><span class="sxs-lookup"><span data-stu-id="39c39-148">F</span></span>                              |
   | <span data-ttu-id="39c39-149">F<sub>1</sub>, S, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="39c39-149">F<sub>1</sub>, S, F<sub>2</sub></span></span> | <span data-ttu-id="39c39-150">PendingConfiguration</span><span class="sxs-lookup"><span data-stu-id="39c39-150">PendingConfiguration</span></span> | <span data-ttu-id="39c39-151">실패</span><span class="sxs-lookup"><span data-stu-id="39c39-151">Failure</span></span>    | <span data-ttu-id="39c39-152">$false</span><span class="sxs-lookup"><span data-stu-id="39c39-152">$false</span></span>        | <span data-ttu-id="39c39-153">S</span><span class="sxs-lookup"><span data-stu-id="39c39-153">S</span></span>                            | <span data-ttu-id="39c39-154">F<sub>1</sub>, F<sub>2</sub></span><span class="sxs-lookup"><span data-stu-id="39c39-154">F<sub>1</sub>, F<sub>2</sub></span></span>   |
   | <span data-ttu-id="39c39-155">S, r</span><span class="sxs-lookup"><span data-stu-id="39c39-155">S, r</span></span>                            | <span data-ttu-id="39c39-156">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="39c39-156">PendingReboot</span></span>        | <span data-ttu-id="39c39-157">Success</span><span class="sxs-lookup"><span data-stu-id="39c39-157">Success</span></span>    | <span data-ttu-id="39c39-158">$true</span><span class="sxs-lookup"><span data-stu-id="39c39-158">$true</span></span>         | <span data-ttu-id="39c39-159">S</span><span class="sxs-lookup"><span data-stu-id="39c39-159">S</span></span>                            | <span data-ttu-id="39c39-160">r</span><span class="sxs-lookup"><span data-stu-id="39c39-160">r</span></span>                              |
   | <span data-ttu-id="39c39-161">F, r</span><span class="sxs-lookup"><span data-stu-id="39c39-161">F, r</span></span>                            | <span data-ttu-id="39c39-162">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="39c39-162">PendingReboot</span></span>        | <span data-ttu-id="39c39-163">실패</span><span class="sxs-lookup"><span data-stu-id="39c39-163">Failure</span></span>    | <span data-ttu-id="39c39-164">$true</span><span class="sxs-lookup"><span data-stu-id="39c39-164">$true</span></span>         | <span data-ttu-id="39c39-165">$null</span><span class="sxs-lookup"><span data-stu-id="39c39-165">$null</span></span>                        | <span data-ttu-id="39c39-166">F, r</span><span class="sxs-lookup"><span data-stu-id="39c39-166">F, r</span></span>                           |
   | <span data-ttu-id="39c39-167">r, S</span><span class="sxs-lookup"><span data-stu-id="39c39-167">r, S</span></span>                            | <span data-ttu-id="39c39-168">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="39c39-168">PendingReboot</span></span>        | <span data-ttu-id="39c39-169">Success</span><span class="sxs-lookup"><span data-stu-id="39c39-169">Success</span></span>    | <span data-ttu-id="39c39-170">$true</span><span class="sxs-lookup"><span data-stu-id="39c39-170">$true</span></span>         | <span data-ttu-id="39c39-171">$null</span><span class="sxs-lookup"><span data-stu-id="39c39-171">$null</span></span>                        | <span data-ttu-id="39c39-172">r</span><span class="sxs-lookup"><span data-stu-id="39c39-172">r</span></span>                              |
   | <span data-ttu-id="39c39-173">r, F</span><span class="sxs-lookup"><span data-stu-id="39c39-173">r, F</span></span>                            | <span data-ttu-id="39c39-174">PendingReboot</span><span class="sxs-lookup"><span data-stu-id="39c39-174">PendingReboot</span></span>        | <span data-ttu-id="39c39-175">Success</span><span class="sxs-lookup"><span data-stu-id="39c39-175">Success</span></span>    | <span data-ttu-id="39c39-176">$true</span><span class="sxs-lookup"><span data-stu-id="39c39-176">$true</span></span>         | <span data-ttu-id="39c39-177">$null</span><span class="sxs-lookup"><span data-stu-id="39c39-177">$null</span></span>                        | <span data-ttu-id="39c39-178">r</span><span class="sxs-lookup"><span data-stu-id="39c39-178">r</span></span>                              |

   <span data-ttu-id="39c39-179">^
   S<sub>i</sub>: 제대로 적용된 일련의 리소스 F<sub>i</sub>: 적용되지 않은 일련의 리소스 r: 다시 부팅이 필요한 리소스 \*</span><span class="sxs-lookup"><span data-stu-id="39c39-179">^
   S<sub>i</sub>: A series of resources that applied successfully F<sub>i</sub>: A series of resources that applied unsuccessfully r: A resource that requires reboot \*</span></span>

   ```powershell
   $LCMState = (Get-DscLocalConfigurationManager).LCMState
   $Status = (Get-DscConfigurationStatus).Status

   $RebootRequested = (Get-DscConfigurationStatus).RebootRequested

   $ResourcesInDesiredState = (Get-DscConfigurationStatus).ResourcesInDesiredState

   $ResourcesNotInDesiredState = (Get-DscConfigurationStatus).ResourcesNotInDesiredState
   ```

## <a name="enhancement-in-get-dscconfigurationstatus-cmdlet"></a><span data-ttu-id="39c39-180">Get-DscConfigurationStatus cmdlet의 향상된 기능</span><span class="sxs-lookup"><span data-stu-id="39c39-180">Enhancement in Get-DscConfigurationStatus cmdlet</span></span>

<span data-ttu-id="39c39-181">이번 릴리스에서는 `Get-DscConfigurationStatus` cmdlet의 몇 가지 기능이 향상되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-181">A few enhancements have been made to `Get-DscConfigurationStatus` cmdlet in this release.</span></span> <span data-ttu-id="39c39-182">이전에는 cmdlet에서 반환하는 개체의 StartDate 속성이 String 형식이었습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-182">Previously, the StartDate property of objects returned by the cmdlet is of String type.</span></span> <span data-ttu-id="39c39-183">지금은 Datetime 형식이어서 Datetime 개체의 기본 속성에 따라 복잡한 선택 및 필터링을 더 쉽게 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-183">Now, it is of Datetime type, which enables complex selecting and filtering easier based on the intrinsic properties of a Datetime object.</span></span>

```powershell
(Get-DscConfigurationStatus).StartDate | Format-List *
DateTime : Friday, November 13, 2015 1:39:44 PM
Date : 11/13/2015 12:00:00 AM
Day : 13
DayOfWeek : Friday
DayOfYear : 317
Hour : 13
Kind : Local
Millisecond : 886
Minute : 39
Month : 11
Second : 44
Ticks : 635830187848860000
TimeOfDay : 13:39:44.8860000
Year : 2015
```

<span data-ttu-id="39c39-184">다음은 오늘과 같은 요일에 수행된 모든 DSC 작업 레코드를 반환하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-184">Following is an example that returns all DSC operation records happened on the same day of week as today.</span></span>

```powershell
(Get-DscConfigurationStatus –All) | Where-Object { $_.startdate.dayofweek -eq (Get-Date).DayOfWeek }
```

<span data-ttu-id="39c39-185">노드의 구성을 변경하지 않는 작업(예: 읽기 전용 작업)의 레코드는 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-185">Records of operations that do not make changes to node’s configuration (i.e. read only operations) are eliminated.</span></span> <span data-ttu-id="39c39-186">따라서, `Test-DscConfiguration`, `Get-DscConfiguration` 작업이 `Get-DscConfigurationStatus` cmdlet에서 반환된 개체에서 더 이상 저하되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-186">Therefore, `Test-DscConfiguration`, `Get-DscConfiguration` operations are no longer adulterated in returned objects from `Get-DscConfigurationStatus` cmdlet.</span></span>
<span data-ttu-id="39c39-187">메타 구성 설정 작업의 레코드는 `Get-DscConfigurationStatus` cmdlet의 반환 값에 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-187">Records of meta configuration setting operation is added to the return of `Get-DscConfigurationStatus` cmdlet.</span></span>

<span data-ttu-id="39c39-188">다음은 `Get-DscConfigurationStatus` –All cmdlet에서 반환된 결과의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-188">Following is an example of result returned from `Get-DscConfigurationStatus` –All cmdlet.</span></span>

```output
All configuration operations:

Status StartDate Type RebootRequested
------ --------- ---- ---------------
Success 11/13/2015 11:38:16 AM Consistency False
Success 11/13/2015 11:23:16 AM Reboot False
Success 11/13/2015 11:21:43 AM Reboot True
Success 11/13/2015 11:20:44 AM Initial True
Success 11/13/2015 11:20:44 AM LocalConfigurationManager False
```

## <a name="enhancement-in-get-dsclocalconfigurationmanager-cmdlet"></a><span data-ttu-id="39c39-189">Get-DscLocalConfigurationManager cmdlet에서 향상된 기능</span><span class="sxs-lookup"><span data-stu-id="39c39-189">Enhancement in Get-DscLocalConfigurationManager cmdlet</span></span>

<span data-ttu-id="39c39-190">LCMStateDetail의 새 필드가 `Get-DscLocalConfigurationManager` cmdlet에서 반환된 개체에 추가되었습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-190">A new field of LCMStateDetail is added to the object returned from `Get-DscLocalConfigurationManager` cmdlet.</span></span> <span data-ttu-id="39c39-191">이 필드는 LCMState가 “사용 중”일 때 채워지며.</span><span class="sxs-lookup"><span data-stu-id="39c39-191">This field is populated when LCMState is "Busy".</span></span> <span data-ttu-id="39c39-192">다음 cmdlet으로 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-192">It can be retrieved by following cmdlet:</span></span>

```powershell
(Get-DscLocalConfigurationManager).LCMStateDetail
```

<span data-ttu-id="39c39-193">다음은 원격 노드에서 두 번 다시 부팅해야 하는 구성에 대한 연속 모니터링의 예제 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="39c39-193">Following is an example output of a continuous monitoring on a configuration that requires two reboots on a remote node.</span></span>

```output
Start a configuration that requires two reboots

Monitor LCM State:
LCM State: Busy, LCM is applying a new configuration.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: PendingReboot,
Machine is rebooting...
LCM State: Busy, LCM is continuing applying configuration after last reboot.
LCM State: Idle,
LCM State: Busy, LCM is performing a consistency check.
LCM State: Idle,
```