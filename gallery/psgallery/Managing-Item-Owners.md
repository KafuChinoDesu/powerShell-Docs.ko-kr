# 항목 소유자 관리

PowerShell 갤러리에 있는 항목의 소유권은 갤러리에 항목을 게시한 사람이 정의합니다.
초기 항목 게시 외에 이 메타데이터를 관리해야 하는 경우도 있으므로 항목 자체는 변경할 수 없지만 소유자 메타데이터는 변경할 수 있어야 합니다.

모든 항목 소유자는 피어입니다. 즉, 모든 항목 소유자가 항목의 새로운 버전을 게시할 수 있습니다. 또한 모든 항목 소유자가 다른 항목 소유자를 제거할 수 있습니다. 모든 소유자가 동일한 권한을 갖습니다.  

## 항목의 초기 소유자 설정 

PowerShell 갤러리에 새 항목을 게시할 때 항목을 게시한 사용자가 초기 소유자를 정의합니다. Publish-Module cmdlet에서 사용된 API 키의 소유자로 결정됩니다.

## 소유자 추가

PowerShell 갤러리에 항목을 게시한 후 추가 사용자를 항목의 소유자로 쉽게 초대할 수 있습니다.

1. 항목의 현재 소유자인 계정을 사용하여 PowerShell 갤러리에 [로그온](https://powershellgallery.com/users/account/LogOn)합니다.
2. '항목' 탭을 사용하거나, 검색하거나, 사용자 이름, [**내 항목 관리**](https://www.powershellgallery.com/account/Packages)를 차례로 클릭하여 항목 페이지로 이동합니다.
3. 항목의 소유자로 로그온한 경우 왼쪽에 클릭할 '소유자 관리' 링크가 있습니다.
4. 소유자로 추가할 사람의 사용자 이름을 입력하고 '추가'를 클릭합니다.
5. 항목의 소유자가 되도록 초대하는 메일이 새 공동 소유자에게 전송됩니다.
6. 해당 사용자가 링크를 클릭하면 소유자인 다른 사용자를 제거하는 기능을 포함하여 항목에 대한 모든 권한을 가진 전체 공동 소유자가 됩니다.

**참고**: 새 소유자가 소유권을 확인하기 전에는 항목의 소유자로 나열되지 *습니다*.
**소유자 관리** 페이지를 보고 있는 경우 현재 소유자에 "승인 보류 중" 항목이 표시됩니다.
다른 소유자를 제거할 수 있는 것과 마찬가지로 해당 초대를 제거할 수 있습니다.
이 초대 프로세스는 사용자가 다른 사용자를 항목의 소유자로 거짓 추가하는 것을 방지합니다.

"Authors" 메타데이터는 순수 자유형 텍스트이며 "Owners"만 제어됩니다.


## 소유자 제거
항목에 여러 소유자가 있고 한 소유자를 제거해야 하는 경우 프로세스는 간단합니다.

1. 항목의 현재 소유자인 계정을 사용하여 PowerShell 갤러리에 [로그온](https://powershellgallery.com/users/account/LogOn)합니다.
2. 항목 탭을 사용하거나, 검색하거나, 사용자 이름, [**내 항목 관리**](https://www.powershellgallery.com/account/Packages)를 차례로 클릭하여 항목 페이지로 이동합니다.
3. 항목의 소유자로 로그온한 경우 왼쪽에 클릭할 '소유자 관리' 링크가 있습니다.
4. 제거할 소유자 옆에 있는 '제거' 링크를 클릭합니다.



## 항목 소유권 이전
항목 소유권을 한 사용자에서 다른 사용자로 이전하라는 지원 요청을 받는 경우도 있지만, 이 작업은 대부분 직접 수행할 수 있습니다.
소유권을 한 사용자에서 다른 사용자로 이전하는 프로세스는 단순히 위의 두 가지 기능이 조합된 것입니다.

1. 현재 소유자가 새 사용자를 공동 소유자로 초대하고 새 사용자가 초대를 수락합니다.
2. 새 사용자가 소유자 목록에서 기존 사용자를 제거합니다.

이 요청은 두 가지 형태로 제공되었지만 프로세스는 동일합니다.

* 항목 소유권이 한 개발자에서 다른 개발자로 변경되는 경우
* 항목이 실수로 잘못된 계정을 사용하여 게시된 경우


## 분리된 항목
마지막 시나리오는 자주 발생하지는 않습니다.
항목이 분리되었으며 유일한 항목 소유자 계정을 사용하여 새 소유자를 추가할 수 없습니다.
이 시나리오의 몇 가지 예는 다음과 같습니다.

* 소유자 계정이 더 이상 존재하지 않는 메일 주소와 연결되어 있고 사용자가 암호를 잊어버린 경우
* 등록된 소유자가 항목을 생성하는 회사를 퇴사했으며 항목 소유권을 업데이트하도록 연락할 수 없는 경우
* 일부 항목에만 영향을 미친 버그로 인해 갤러리에서 항목의 소유자가 없는 경우

PowerShell 갤러리 관리자는 모든 항목에 대한 '소유자 관리' 링크에 액세스할 수 있습니다.
항목의 정당한 소유자가 소유권 권한을 얻기 위해 현재 소유자에게 문의할 수 없는 경우 갤러리의 '신고하기' 링크를 사용하여 PowerShell 갤러리 관리자에게 문의하세요.
그러면 프로세스에 따라 항목의 소유권을 확인합니다.
항목의 소유자로 확인되면 직접 항목에 대한 '소유자 관리' 링크를 사용하여 소유자로 초대하는 메일을 보냅니다.
이 작업은 사용자가 소유자로 확인된 후에만 수행되며 상황에 따라 프로세스가 달라집니다.
대체로 항목의 프로젝트 URL을 사용하여 프로젝트 소유자에게 문의하지만 Twitter, 메일 또는 다른 수단으로 프로젝트 소유자에게 문의할 수도 있습니다.

<!--HONumber=Aug16_HO3-->

