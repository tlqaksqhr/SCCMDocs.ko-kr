---
title: 콘솔 내 업데이트
titleSuffix: Configuration Manager
description: Microsoft 클라우드에서 Configuration Manager에 업데이트 설치
ms.date: 04/10/2018
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: c14a3607-253b-41fb-8381-ae2d534a9022
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 9edf02333ec4ce272e69a896ed22e97fa6de0955
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="install-in-console-updates-for-system-center-configuration-manager"></a>System Center Configuration Manager의 콘솔 내 업데이트 설치

*적용 대상: System Center Configuration Manager(현재 분기)*

Configuration Manager는 Microsoft 클라우드 서비스와 동기화하여 업데이트를 가져옵니다. 그런 다음 Configuration Manager 콘솔 내에서 이러한 업데이트를 설치할 수 있습니다.

## <a name="get-available-updates"></a>사용 가능 업데이트 가져오기
인프라 및 버전에 적용되는 업데이트만 계층 구조로 다운로드하여 사용할 수 있습니다. 이 동기화는 계층 구조에 대한 서비스 연결 지점을 구성하는 방법에 따라 자동이나 수동이 될 수 있습니다.

-   **온라인 모드**에서, 서비스 연결 지점은 Microsoft 클라우드 서비스에 자동으로 연결하고 적용 가능한 업데이트를 다운로드합니다.  

     기본적으로 Configuration Manager는 24시간마다 새 업데이트를 확인합니다. Configuration Manager 콘솔의 **관리** > **업데이트 및 서비스** 노드에서 **업데이트 확인**을 선택하여 즉시 업데이트를 확인할 수도 있습니다. 

-   **오프라인 모드**에서는 서비스 연결 지점이 Microsoft 클라우드 서비스에 연결하지 않습니다. 사용 가능한 업데이트를 다운로드한 후 가져오려면 [서비스 연결 도구를 사용합니다](../../../core/servers/manage/use-the-service-connection-tool.md).  

> [!NOTE]  
>   대역 외 수정 내용을 콘솔로 가져올 수 있습니다. 이렇게 하려면 [업데이트 등록 도구](/sccm/core/servers/manage/use-the-update-registration-tool-to-import-hotfixes)를 사용합니다. 이러한 대역 외 수정 내용은 Microsoft 클라우드 서비스와 동기화할 때 가져오는 업데이트를 보완합니다.


업데이트를 동기화한 후 **관리** > **업데이트 및 서비스** 노드로 이동하여 Configuration Manager 콘솔에서 해당 업데이트를 볼 수 있습니다.  

-   설치하지 않은 업데이트는 **사용 가능**으로 표시됩니다.

-   설치한 업데이트는 **설치됨**으로 표시됩니다. 가장 최근에 설치된 업데이트만 표시됩니다. 리본에서 **기록** 단추를 선택하여 이전에 설치한 업데이트를 볼 수 있습니다.



서비스 연결 지점을 구성하기 전에 추가적인 사용을 이해하고 계획하세요. 다음 사용은 이 사이트 시스템 역할을 구성하는 방법에 영향을 줄 수 있습니다.  

-   서비스 연결 지점은 사이트에 대한 사용 정보를 업로드하는 데 사용됩니다. 이 정보는 Microsoft 클라우드 서비스에서 현재 인프라 버전에 사용할 수 있는 업데이트를 식별하는 데 도움이 됩니다. 자세한 내용은 [진단 및 사용 현황 데이터](../../../core/plan-design/diagnostics/diagnostics-and-usage-data.md)를 참조합니다.  

-   서비스 연결 지점은 Microsoft Intune 및 Configuration Manager 온-프레미스 모바일 장치 관리를 통해 장치를 관리하는 데 사용됩니다. 자세한 내용은 [System Center Configuration Manager 및 Microsoft Intune을 지원하는 하이브리드 MDM(모바일 장치 관리)](../../../mdm/understand/hybrid-mobile-device-management.md)을 참조하세요.  

업데이트를 다운로드할 때 수행되는 작업을 더 적절히 이해하려면 다음을 참조하세요.  

-   [순서도 – System Center Configuration Manager용 업데이트 다운로드](../../../core/servers/manage/download-updates-flowchart.md)

-   [순서도 - System Center Configuration Manager의 복제본 업데이트](../../../core/servers/manage/update-replication-flowchart.md)  



## <a name="assign-permissions-to-view-and-manage-updates-and-features"></a>업데이트 및 기능을 보고 관리할 수 있는 권한 할당
콘솔에서 업데이트를 보려면 사용자에게 **업데이트 패키지** 보안 클래스가 포함된 역할 기반 관리 보안 역할이 있어야 합니다. 이 클래스는 Configuration Manager 콘솔에서 업데이트를 보고 업데이트할 수 있는 액세스 권한을 부여합니다.    

#### <a name="about-the-update-packages-class"></a>업데이트 패키지 클래스 정보   
기본적으로 **업데이트 패키지** 클래스(SMS_CM_Updatepackages)는 다음과 같이 나열된 권한이 있는 기본 제공 보안 역할의 일부입니다.
 -  **수정** 및 **읽기** 권한이 있는 **전체 관리자** :
    -   이 보안 역할 및 **모든** 보안 범위에 대한 액세스 권한이 있는 사용자는 업데이트를 보고 설치할 수 있습니다. 또한 사용자는 설치 중에 기능을 사용하도록 설정하고, 업데이트를 설치한 후에는 개별 기능을 사용하도록 설정할 수 있습니다.
    - 이 보안 역할 및 **기본** 보안 범위에 대한 액세스 권한이 있는 사용자는 업데이트를 보고 설치할 수 있습니다. 또한 사용자는 설치 중에 기능을 사용하도록 설정하고, 업데이트를 설치한 후에는 기능을 볼 수 있습니다. 하지만 업데이트를 설치한 후에는 이 사용자가 기능을 사용하도록 설정할 수 없습니다.

- **읽기** 권한이 있는 **읽기 전용 분석가** :
  -  이 보안 역할 및 **기본** 범위에 대한 액세스 권한을 가진 사용자는 업데이트를 볼 수 있지만 설치할 수는 없습니다. 또한 이 사용자는 업데이트가 설치된 후 기능을 볼 수 있지만 사용하도록 설정할 수는 없습니다.

#### <a name="permissions-required-for-updates-and-servicing"></a>업데이트 및 서비스에 필요한 권한   
  - **수정** 및 **읽기** 권한과 함께 **업데이트 패키지** 클래스를 포함하는 보안 역할이 할당된 계정을 사용합니다.
  - 계정에는 **기본** 범위를 할당해야 합니다.

#### <a name="permissions-to-only-view-updates"></a>업데이트 보기만 가능한 권한   
  - **읽기** 권한과 함께 **업데이트 패키지** 클래스를 포함하는 보안 역할이 할당된 계정을 사용합니다.
  - 계정에는 **기본** 범위를 할당해야 합니다.

#### <a name="permissions-required-to-enable-features-after-updates-are-installed"></a>업데이트가 설치된 후에 기능을 사용하도록 설정하는 데 필요한 권한   
  -  **수정** 및 **읽기** 권한과 함께 **업데이트 패키지** 클래스를 포함하는 보안 역할이 할당된 계정을 사용합니다.
  -  계정에는 **모든** 범위를 할당해야 합니다.



##  <a name="bkmk_beforeinstall"></a> 콘솔 내 업데이트를 설치하기 전에  
 Configuration Manager 콘솔 내에서 업데이트를 설치하기 전에 다음 단계를 검토합니다.  

###  <a name="bkmk_step1"></a> 1단계: 업데이트 검사 목록 검토  
업데이트를 시작하기 전에 수행할 작업에 해당하는 업데이트 검사 목록을 검토합니다.

- [업데이트 1706을 설치하기 위한 검사 목록](../../../core/servers/manage/checklist-for-installing-update-1706.md)  

- [업데이트 1710을 설치하기 위한 검사 목록](../../../core/servers/manage/checklist-for-installing-update-1710.md)  

- [업데이트 1802를 설치하기 위한 검사 목록](../../../core/servers/manage/checklist-for-installing-update-1802.md)


###  <a name="step-2-run-the-prerequisite-checker-before-installing-an-update"></a>2단계: 업데이트를 설치하기 전에 필수 조건 검사 실행  
업데이트를 설치하기 전에 해당 업데이트에 대한 필수 조건 검사를 실행하는 것이 좋습니다. 업데이트를 설치하기 전에 필수 구성 요소를 실행하면  

-   업데이트 파일이 업데이트를 설치하기 전에 다른 사이트에 복제됩니다.  

-   업데이트를 설치하도록 선택하면 필수 조건 검사가 자동으로 다시 실행됩니다.  

> [!NOTE]   
> 필수 조건 검사를 시작한 다음 상태를 보면 **설치** 단계가 활성인 것으로 표시되지만 업데이트는 실제로 설치되고 있지 않습니다. 필수 구성 요소 검사를 실행하기 위해 업데이트 프로세스가 콘텐츠 라이브러리에서 패키지를 추출하고 현재 필수 구성 요소 검사가 액세스할 수 있는 준비 폴더에 넣습니다. 업데이트를 설치할 때 이와 동일한 프로세스가 실행됩니다. 이러한 이유로 설치가 ‘진행 중’으로 표시됩니다. *업데이트 패키지 추출* 단계만 설치 범주에 표시됩니다.  

나중에 업데이트를 설치하면 필수 조건 검사 경고를 무시하도록 업데이트를 구성할 수 있습니다.  

#### <a name="to-run-the-prerequisite-checker-before-installing-an-update"></a>업데이트를 설치하기 전에 필수 조건 검사를 실행하려면  

1.  Configuration Manager 콘솔에서 **관리** > **업데이트 및 서비스**로 이동합니다.   

2.  필수 조건 검사를 실행하는 업데이트 패키지를 마우스 오른쪽 단추로 클릭합니다.  

3.  **필수 구성 요소 검사 실행**을 선택합니다.  

     필수 조건 검사를 실행하면 업데이트의 콘텐츠가 하위 사이트에 복제됩니다. 사이트 서버에서 distmgr.log를 보고 해당 콘텐츠가 성공적으로 복제되었는지 확인할 수 있습니다.  

4.  검사 결과를 보려면 Configuration Manager 콘솔에서 **모니터링** > **사이트 서비스 상태**로 이동하여 필수 조건 상태를 확인합니다. 또한 자세한 내용은 사이트 서버의 ConfigMgrPrereq.log에서 확인할 수 있습니다.  



##  <a name="bkmk_install"></a> 콘솔 내 업데이트 설치  
 Configuration Manager 콘솔 내에서 업데이트를 설치할 준비가 되면 계층 구조의 최상위 계층 사이트에서 시작합니다. 이 사이트는 중앙 관리 사이트나 독립 실행형 기본 사이트 중 하나입니다.  

 각 사이트에 대한 일상적인 업무 시간 외에 업데이트를 설치하여 비즈니스 작업에 미치는 영향을 최소화하는 것이 좋습니다. 업데이트 설치에는 사이트 구성 요소 및 사이트 시스템 역할을 다시 설치와 같은 작업이 포함될 수 있기 때문에 권장됩니다.  

-   중앙 관리 사이트에서 업데이트 설치를 완료한 후 자식 기본 사이트가 업데이트를 자동으로 시작합니다. 이것이 권장되는 기본 프로세스입니다. 그러나 [사이트 서버에 대한 서비스 기간](/sccm/core/servers/manage/service-windows)을 사용하여 기본 사이트에서 업데이트를 설치하는 시기를 제어할 수 있습니다.  

-   기본 상위 사이트 업데이트가 완료된 후 Configuration Manager 콘솔 내에서 보조 사이트를 수동으로 업데이트합니다. 보조 사이트 서버의 자동 업데이트는 지원되지 않습니다.  

-   사이트를 업데이트한 후 Configuration Manager 콘솔을 사용하면 콘솔을 업데이트하라는 메시지가 표시됩니다.  

-  사이트 서버는 업데이트 설치를 완료한 후 해당하는 사이트 시스템 역할을 자동으로 모두 업데이트합니다. 한 가지 주의할 사항은 배포 지점과 관련된 것입니다. 업데이트를 설치할 때, 모든 배포 지점이 동시에 다시 설치되어 업데이트를 위해 오프라인으로 전환되지는 않습니다. 대신, 사이트 서버에서 사이트의 콘텐츠 배포 설정을 사용하여 한 번에 하나씩 배포 지점 하위 집합에 업데이트를 배포합니다. 따라서 일부 배포 지점만 업데이트 설치를 위해 오프라인으로 전환됩니다. 업데이트가 시작되지 않았거나 업데이트가 완료된 배포 지점은 온라인 상태로 유지되고 클라이언트에 콘텐츠를 제공할 수 있습니다.


###  <a name="bkmk_overview"></a> 콘솔 내 업데이트 설치의 개요  
#### <a name="1-when-the-update-installation-starts"></a>1. 업데이트 설치가 시작되면  
업데이트가 적용되는 제품 영역의 목록을 표시하는 마법사가 나타납니다.  

-   마법사의 **일반** 페이지에서, **필수 구성 요소 경고**를 구성할 수 있습니다.  
    -   필수 조건 오류는 항상 업데이트 설치를 중지합니다. 업데이트 설치를 성공적으로 다시 시도하려면 먼저 오류를 수정합니다. 자세한 내용은 [실패한 업데이트의 설치 다시 시도](#bkmk_retry)를 참조하세요.  

    -   필수 조건 경고도 업데이트 설치를 중지할 수 있습니다. 업데이트 설치를 다시 시도하려면 먼저 경고를 해결합니다. 자세한 내용은 [실패한 업데이트의 설치 다시 시도](#bkmk_retry)를 참조하세요.  
    -   **누락된 요구 사항과 관계 없이 모든 필수 조건 검사 경고를 무시하고 이 업데이트 설치**: 필수 조건 경고를 무시하는 업데이트 설치의 조건을 설정합니다. 이 옵션을 통해 업데이트 설치를 계속 진행할 수 있습니다. 이 옵션을 선택하지 않으면 경고가 발생할 때 업데이트 설치가 중지됩니다. 이전에 사이트에 대한 필수 조건을 실행하고 해결하지 않았다면 이 옵션을 사용하지 않는 것이 좋습니다.  

      **관리** 및 **모니터링** 작업 영역 둘 다에서 업데이트 및 서비스 노드에 **필수 조건 경고 무시**라는 리본 단추가 포함됩니다. 필수 조건 검사 경고로 인해 업데이트 패키지에서 설치를 완료하지 못하는 경우 이 단추를 사용할 수 있습니다. 예를 들어 필수 조건 경고를 무시하는 옵션을 사용하지 않고 업데이트를 설치한다고 가정해봅니다(업데이트 마법사에서). 업데이트 설치는 필수 조건 경고는 발생하지만 오류는 없이 중지됩니다. 나중에 리본 메뉴에서 **필수 조건 경고 무시**를 선택하여 해당 업데이트 설치가 자동으로 계속되고 필수 조건 경고가 무시되도록 할 수 있습니다. 이 옵션을 사용하면 몇 분 후에 업데이트 설치가 자동으로 진행됩니다.



-   Configuration Manager 클라이언트에 업데이트를 적용할 때 제한된 클라이언트 집합으로 클라이언트 업데이트를 테스트하는 옵션이 제공됩니다. 자세한 내용은 [사전 프로덕션 컬렉션에서 클라이언트 업그레이드를 테스트하는 방법](../../../core/clients/manage/upgrade/test-client-upgrades.md)을 참조하세요.  


#### <a name="2-during-the-update-installation"></a>2. 업데이트 설치 중  
업데이트 설치의 일부로 Configuration Manager는 다음을 수행합니다.  

-   사이트 시스템 역할 또는 Configuration Manager 콘솔과 같은 영향을 받는 모든 구성 요소를 다시 설치합니다.  

-   클라이언트 파일럿에 대한 선택 사항에 따라, 그리고 [자동 클라이언트 업그레이드](/sccm/core/clients/manage/upgrade/upgrade-clients-for-windows-computers#use-automatic-client-upgrade)를 위해 클라이언트 업데이트를 관리합니다.  

-   .NET이 사이트 시스템 역할 필수 조건의 일부로 설치되지 않은 경우 업데이트의 일부로 사이트 시스템 서버를 다시 시작하지 않습니다.  

> [!TIP]  
>  업데이트가 설치되면 Configuration Manager에서 CD.Latest 폴더도 업데이트합니다. 이 폴더는 사이트 복구 중에 사용됩니다.  


#### <a name="3-monitor-the-progress-of-updates-as-they-install"></a>3. 설치하는 업데이트의 진행률 모니터링  
다음을 사용하여 진행률을 모니터링합니다.  

-   Configuration Manager 콘솔에서 **관리** > **업데이트 및 서비스** 노드로 이동합니다. 이 노드에는 모든 업데이트 패키지의 설치 상태가 표시됩니다.


-   Configuration Manager 콘솔에서 **모니터링** > **개요** > **업데이트 및 서비스 상태** 노드로 이동합니다. 이 노드에는 현재 설치 중인 업데이트 패키지의 설치 상태만 표시됩니다.  

    업데이트 팩 설치가 모니터링의 편의를 위해 다음 단계를 통해 분할됩니다. 각 단계에 대한 추가 세부 정보에는 자세한 내용을 확인할 수 있는 로그 파일이 포함됩니다.  
    -   **다운로드**(이 단계는 서비스 연결 지점 사이트가 설치되어 있는 최상위 계층 사이트에만 적용됨)   

    -   **복제**   

    -   **필수 구성 요소 확인**   

    -   **설치**    

    -   **설치 후** - 자세한 내용은 [설치 후 작업](#post-installation-tasks)을 참조하세요.  

-   **&lt;ConfigMgr 설치 디렉터리>\Logs**에서 **CMUpdate.log** 파일을 볼 수 있습니다.  


#### <a name="4-when-the-update-installation-completes"></a>4. 업데이트 설치가 완료되면  
첫 번째 사이트 업데이트가 설치를 완료한 후  

-   자식 기본 사이트에서 업데이트를 자동으로 설치합니다. 추가 작업이 필요하지 않습니다.  

-   Configuration Manager 콘솔 내에서 보조 사이트를 수동으로 업데이트해야 합니다.
> [!TIP]
> 보조 사이트의 버전은 콘솔에 표시되지 않지만 Configuration Manager SDK를 사용하여 사이트 버전을 확인할 수 있습니다. [SMS_Site Server WMI 클래스](/sccm/develop/reference/core/servers/configure/sms_site-server-wmi-class)를 참조하세요.


-   계층의 모든 사이트가 새 버전으로 업데이트될 때까지 계층이 혼합 버전 모드로 작동합니다. 자세한 내용은 [다른 버전의 Configuration Manager 간 상호 운용성](../../../core/plan-design/hierarchy/interoperability-between-different-versions.md)을 참조하세요.  


#### <a name="5-update-configuration-manager-consoles"></a>5. Configuration Manager 콘솔 업데이트  
중앙 관리 사이트 또는 기본 사이트가 업데이트된 후 해당 사이트에 연결된 각 Configuration Manager 콘솔도 업데이트해야 합니다. 다음과 같은 경우에 콘솔을 업데이트하라는 메시지가 표시됩니다.  

-   콘솔을 열 때

-   열린 콘솔에서 새 노드로 이동할 때

즉시 업데이트를 설치하는 것이 좋습니다.  

콘솔 업데이트가 완료되면 콘솔 및 사이트 버전이 올바른지 확인할 수 있습니다. 콘솔의 왼쪽 위에 있는 **System Center Configuration Manager 정보**로 이동합니다.  

 > [!Note]  
 > 1802 버전부터는 콘솔 버전이 이제 사이트 버전과 약간 다릅니다. 이제 콘솔의 부 버전이 Configuration Manager 릴리스 버전에 해당합니다. 예를 들어, Configuration Manager 버전 1802에서 초기 사이트 버전은 5.0.8634.1000이고 초기 콘솔 버전은 5.**1802**.1082.1700입니다. 빌드(1082) 및 수정(1700) 번호는 향후 핫픽스에서 1802 릴리스로 변경될 수 있습니다.



###  <a name="bkmk_toptier"></a> 최상위 계층 사이트에서 업데이트 설치를 시작하려면  
계층 구조의 최상위 계층 사이트에 있는 Configuration Manager 콘솔에서 **관리** > **업데이트 및 서비스**로 이동한 다음 **사용 가능** 업데이트를 선택하고 **업데이트 팩 설치**를 클릭합니다.  


###  <a name="bkmk_secondary"></a> 보조 사이트에서 업데이트 설치를 시작하려면  
보조 사이트 상위 기본 사이트를 업데이트한 후 Configuration Manager 콘솔 내에서 보조 사이트를 업데이트할 수 있습니다. 그렇게 하려면 **보조 사이트 업그레이드 마법사**를 사용합니다.  

1.  Configuration Manager 콘솔에서 **관리** > **사이트 구성** > **사이트**로 이동한 다음 업데이트할 사이트를 선택하고 홈 탭의 **사이트** 그룹에서 **업그레이드**를 선택합니다.  

2.  **예** 를 클릭하여 보조 사이트의 업데이트를 시작합니다.  

보조 사이트에서 업데이트 설치를 모니터링하려면 보조 사이트 서버를 선택합니다. 그런 다음 **홈** 탭의 **사이트** 그룹에서 **설치 상태 표시**를 선택합니다. 각 보조 사이트의 버전을 볼 수 있도록 콘솔 디스플레이에 **버전** 열을 추가할 수 있습니다.  

보조 사이트를 업데이트한 후 콘솔에서 상태가 새로 고쳐지지 않거나 업데이트에 실패했다는 메시지가 표시되는 경우 **설치 다시 시도** 옵션을 사용합니다. 이 옵션은 업데이트가 성공적으로 설치되지 않은 보조 사이트에 대해 업데이트를 다시 설치하지 않지만 콘솔에서 상태를 강제로 업데이트합니다.


### <a name="post-installation-tasks"></a>설치 후 작업
사이트가 업데이트를 설치할 때 사이트 서버에서 업데이트 설치가 완료될 때까지 일부 작업을 시작할 수 없습니다. 다음은 사이트 및 계층 구조 작업에 중요한 설치 후 작업의 목록입니다. 이러한 작업은 중요하므로 적극적으로 모니터링됩니다. 직접 모니터링되지 않는 추가 작업에는 사이트 시스템 역할의 다시 설치가 포함됩니다. 중요한 설치 후 작업의 상태를 보려면 사이트에 대한 업데이트 설치를 모니터링하는 동안 **설치 후** 작업을 선택합니다.

모든 작업이 즉시 완료되는 것은 아닙니다. 일부 작업은 각 사이트에서 업데이트의 설치를 완료할 때까지 시작되지 않습니다. 이러한 작업이 완료될 때까지 필요한 새 기능이 지연될 수 있습니다. 새 기능을 켜도, 모든 사이트의 업데이트 설치가 완료될 때까지 시작되지 않으므로 얼마 동안 새 기능이 표시되지 않을 수 있습니다.

설치 후 작업에는 다음이 포함됩니다.

-   **SMS_EXECUTIVE 서비스 설치**
  -   사이트 서버에서 실행되는 중요한 서비스입니다.
  -   이 서비스의 다시 설치는 신속하게 완료됩니다.


-   **SMS_DATABASE_NOTIFICATION_MONITOR 구성 요소 설치**
  -   SMS_EXECUTIVE 서비스의 중요한 사이트 구성 요소 스레드입니다.
  -   이 서비스의 다시 설치는 신속하게 완료됩니다.


-   **SMS_HIERARCHY_MANAGER 구성 요소 설치**
  -   사이트 서버에서 실행되는 중요한 사이트 구성 요소입니다.
  -   사이트 시스템 서버에 사이트 시스템 역할을 다시 설치하는 역할을 합니다. 개별 사이트 시스템 역할 다시 설치에 대한 상태는 표시되지 않습니다.
  -   이 서비스의 다시 설치는 신속하게 완료됩니다.


-   **SMS_REPLICATION_CONFIGURATION_MONITOR 구성 요소 설치**
  -   사이트 서버에서 실행되는 중요한 사이트 구성 요소입니다.
  -   이 서비스의 다시 설치는 신속하게 완료됩니다.


-   **SMS_POLICY_PROVIDER 구성 요소 설치**
  -   기본 사이트서만 실행되는 중요한 사이트 구성 요소입니다.
  -   이 서비스의 다시 설치는 신속하게 완료됩니다.


-   **복제 초기화 모니터링**   
  -   이 작업만 중앙 관리 사이트 및 자식 기본 사이트에 표시됩니다.
  -   SMS_REPLICATION_CONFIGURATION_MONITOR에 종속됩니다.
  -   신속하게 완료해야 합니다.


-   **Configuration Manager 클라이언트 사전 프로덕션 패키지 업데이트**    
  -   이 작업은 클라이언트 사전 프로덕션(클라이언트 파일럿이라고도 함)이 사용되도록 설정되지 않는 경우에도 표시됩니다.
  -   계층 구조의 모든 사이트가 업데이트 설치를 완료할 때까지 시작되지 않습니다.


-   **사이트 서버에서 클라이언트 폴더 업데이트**
  -   이 작업은 사전 프로덕션에서 클라이언트를 사용하는 경우에는 표시되지 않습니다.  
  -   신속하게 완료해야 합니다.


-   **Configuration Manager 클라이언트 패키지 업데이트**
  -   이 작업은 사전 프로덕션에서 클라이언트를 사용하는 경우에는 표시되지 않습니다.  
  -   모든 사이트에서 업데이트를 설치한 후에만 완료됩니다.  


-   **기능 켜기**
  -   이 작업은 계층 구조의 최상위 계층 사이트에만 표시됩니다.
  -   계층 구조의 모든 사이트가 업데이트 설치를 완료할 때까지 시작되지 않습니다.
  -   개별 기능은 표시되지 않습니다.



##  <a name="bkmk_retry"></a> 실패한 업데이트의 설치 다시 시도  
업데이트를 설치하지 못하는 경우 콘솔 내 피드백을 검토하여 경고 및 오류가 해결되었는지 확인합니다. 또한 자세한 내용은 사이트 서버의 ConfigMgrPrereq.log에서 확인할 수 있습니다. 업데이트 설치를 다시 시도하기 전에 오류를 수정하고 경고를 해결해야 합니다.  

> [!TIP]  
> 업데이트를 다운로드하거나 복제하는 데 문제가 있는 경우 [업데이트 다시 설정 도구](/sccm/core/servers/manage/update-reset-tool)를 사용할 수 있습니다. 

업데이트 설치를 다시 시도할 준비가 되면 실패한 업데이트를 선택한 후 해당 옵션을 선택합니다. 업데이트 설치 다시 시도 동작은 다시 시도를 시작하는 노드와 사용하는 다시 시도 옵션에 따라 다릅니다.  

#### <a name="retry-installation-for-the-hierarchy"></a>계층에 대한 설치 다시 시도
해당 업데이트가 다음 상태 중 하나에 있으면 전체 계층에 대한 업데이트 설치를 다시 시도할 수 있습니다.  

  -   하나 이상의 경고와 함께 필수 조건 검사를 통과했으며, 필수 조건 검사 경고를 무시하는 옵션이 업데이트 마법사에서 설정되지 않았음 (**업데이트 및 서비스** 노드에서 **필수 조건 경고 무시** 의 업데이트 값이 **아니요**인 경우)   
  -   필수 조건 실패    
  -   설치 실패
  -   콘텐츠를 사이트로 복제 실패   

**관리** > **업데이트 및 서비스**로 이동하고, 다음 옵션 중 하나를 선택합니다.  

  -   **다시 시도** - 이 노드에서 **다시 시도**를 실행하면 업데이트 설치가 다시 시작되고 필수 조건 경고가 자동으로 무시됩니다. 또한 복제가 이전에 실패한 경우 업데이트의 콘텐츠도 다시 복제합니다.
  - **필수 조건 경고 무시** - 경고로 인해 업데이트 설치가 중지되면 **필수 조건 경고 무시**를 선택할 수 있습니다. 이 작업은 몇 분 후 업데이트의 설치를 계속 진행하며 필수 조건 경고를 무시하는 옵션을 사용합니다.   

#### <a name="retry-installation-for-the-site"></a>사이트에 대한 설치 다시 시도  
 해당 업데이트가 다음 상태 중 하나에 있으면 특정 사이트에서 업데이트 설치를 다시 시도할 수 있습니다.  

  -   하나 이상의 경고와 함께 필수 조건 검사를 통과했으며, 필수 조건 검사 경고를 무시하는 옵션이 업데이트 마법사에서 설정되지 않았음 (업데이트 및 서비스 노드에서 **필수 조건 경고 무시**의 업데이트 값이 **아니요**인 경우)  
  -   필수 조건 실패    
  -   설치 실패    

**모니터링** > **개요** > **사이트 서비스 상태**로 이동하고, 업데이트를 선택한 후 다음 옵션 중 하나를 클릭합니다.

  - **다시 시도** - 이 노드에서 **다시 시도**를 실행하면 해당 사이트에서만 업데이트 설치를 다시 시작합니다. **업데이트 및 서비스** 노드에서 **다시 시도**를 실행하는 경우와 달리 이 다시 시도 작업에서는 필수 조건 경고를 무시하지 않습니다.
  - **필수 조건 경고 무시** - 경고로 인해 업데이트 설치가 중지되면 **필수 조건 경고 무시**를 클릭할 수 있습니다. 이 작업은 몇 분 후 업데이트의 설치를 계속 진행하며 필수 조건 경고를 무시하는 옵션을 사용합니다.



##  <a name="bkmk_after"></a> 사이트에서 업데이트를 설치한 후  
다음 검사 목록을 사용하여 사이트를 업데이트한 후에 적용된 일반 작업 및 구성을 완료합니다.   

**사이트 간 복제가 활성화되었는지 확인:** Configuration Manager 콘솔에서 다음 위치로 이동하여 상태를 확인하고 복제가 활성화되었는지 확인합니다.  

-   **모니터링** > **개요** > **사이트 계층 구조**  

-   **모니터링** > **개요** > **데이터베이스 복제**  

자세한 내용은 [계층 구조 및 복제 인프라 모니터링](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 및 [Replication Link Analyzer 정보](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_RLA)를 참조하세요.  

 **사이트 서버 및 원격 사이트 시스템 서버가 다시 시작되었는지 확인(필요한 경우):** 사이트 인프라를 검토하고 해당하는 사이트 서버 및 사이트 시스템 서버가 성공적으로 다시 시작되었는지 확인합니다. 일반적으로, Configuration Manager에서 사이트 시스템 역할의 필수 조건으로 .NET을 설치하는 경우에만 사이트 서버가 다시 시작됩니다.  

 **독립 실행형 Configuration Manager 콘솔 업데이트:** 모든 원격 Configuration Manager 콘솔이 동일한 버전으로 업데이트되었는지 확인합니다. 다음과 같은 경우에 콘솔을 업데이트하라는 메시지가 표시됩니다.  

-   콘솔에서 새 노드로 이동하는 경우  

-   콘솔을 여는 경우

**기본 사이트의 관리 지점에 대한 데이터베이스 복제본 다시 구성** 기본 사이트의 관리 지점에 대한 데이터베이스 복제본을 사용할 경우 사이트를 업데이트하기 전에 데이터베이스 복제본을 제거해야 합니다. 기본 사이트를 업데이트한 후에는 관리 지점에 대한 데이터베이스 복제본을 다시 구성합니다. 자세한 내용은 [관리 지점에 대한 데이터베이스 복제본](../../../core/servers/deploy/configure/database-replicas-for-management-points.md)을 참조하세요.  

**업데이트 전에 비활성화한 모든 데이터베이스 유지 관리 작업 다시 구성:** 업데이트 설치 전에 사이트에서 데이터베이스 [유지 관리 작업](../../../core/servers/manage/maintenance-tasks.md)을 사용하지 않도록 설정한 경우 사이트에서 해당 작업을 다시 구성합니다. 업데이트 전에 사용하던 설정과 동일한 설정을 사용합니다.  

**클라이언트 업그레이드:** 자세한 내용은 [Windows 컴퓨터에 대한 클라이언트를 업그레이드하는 방법](../../../core/clients/manage/upgrade/upgrade-clients-for-windows-computers.md)을 참조하세요.  

**추가 구성:** 업데이트를 시작하기 전에 변경한 내용을 확인한 후 사이트 및 계층 구조로 이러한 구성을 복원합니다.  



##  <a name="bkmk_options"></a> 업데이트에서 선택적 기능 사용  
업데이트에 하나 이상의 선택적 기능이 포함될 때 계층에서 이러한 기능을 사용하도록 설정할 수 있습니다. 업데이트 설치 시 기능을 사용하도록 설정하거나 나중에 콘솔로 돌아가 선택적 기능을 사용하도록 설정할 수 있습니다.

사용 가능한 기능 및 해당 상태를 보려면 콘솔에서 **관리** > **업데이트 및 서비스** > **기능**으로 이동합니다.

옵션이 아닌 기능은 자동으로 설치됩니다. **기능** 노드에 나타나지 않습니다.  

> [!Important]  
> 다중 사이트 계층에서는 중앙 관리 사이트에서만 선택적 또는 시험판 기능을 활성화할 수 있습니다. 이 동작은 계층 전체에 충돌이 발생하지 않도록 합니다. <!--507197-->
 

새 기능 또는 시험판 기능을 사용하도록 설정하면 Configuration Manager HMAN(계층 구조 관리자)은 해당 기능을 사용할 수 있게 되기 전에 변경 내용을 처리해야 합니다. 변경 내용 처리는 대개 즉시 이루어지지만, HMAN 처리 주기에 따라 완료하는 데 최대 30분까지 걸릴 수 있습니다. 변경 내용이 처리된 후 콘솔을 다시 시작해야만 해당 기능과 관련된 새 노드를 볼 수 있습니다.

#### <a name="list-of-optional-features"></a>옵션 기능 목록
다음은 Configuration Manager 최신 버전의 옵션 기능입니다.<!--505213-->  
- [관리되는 PC에 대한 조건부 액세스](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm)  <!--1191496-->
- [Passport for Work](/sccm/protect/deploy-use/windows-hello-for-business-settings)(*비즈니스용 Windows Hello*라고도 함) <!--1245704-->
- [Windows 10용 VPN](/sccm/protect/deploy-use/vpn-profiles) <!--1283610-->
- [Windows Defender Exploit Guard 정책](/sccm/protect/deploy-use/create-deploy-exploit-guard-policy) <!--1355468-->
- [Microsoft OMS(Operations Management Suite) 커넥터](/sccm/core/clients/manage/sync-data-microsoft-operations-management-suite) <!--1258052-->
- [PFX 만들기](/sccm/protect/deploy-use/introduction-to-certificate-profiles) <!--1321368-->
- [클라이언트 피어 캐시](/sccm/core/plan-design/hierarchy/client-peer-cache) <!--1101436-->
- [데이터 웨어하우스 서비스 지점](/sccm/core/servers/manage/data-warehouse) <!--1277922-->
- [클라우드 관리 게이트웨이](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) <!--1101764-->
- [Surface 드라이버 업데이트](/sccm/sum/get-started/configure-classifications-and-products) <!--1098490-->
- [작업 순서 콘텐츠 사전 캐싱](/sccm/osd/deploy-use/create-a-task-sequence-to-upgrade-an-operating-system#configure-pre-cache-content) <!--1021244-->
- [작업 순서 실행 단계](/sccm/osd/deploy-use/manage-task-sequences-to-automate-tasks#add-child-task-sequences-to-a-task-sequence) <!--1261338-->
- [스크립트 만들기 및 실행](/sccm/apps/deploy-use/create-deploy-scripts) <!--1236459-->
- [조건부 액세스의 준수 정책에 대한 장치 상태 증명 평가](/sccm/mdm/deploy-use/manage-access-to-o365-services-for-pcs-managed-by-sccm) <!--1235616-->
- [장치당 사용자에 대한 응용 프로그램 요청 승인](/sccm/apps/deploy-use/deploy-applications#specify-deployment-settings) <!--1357015-->  


> [!Tip]  
> 사용하려면 동의가 필요한 기능에 대한 자세한 내용은 [시험판 기능](/sccm/core/servers/manage/pre-release-features)을 참조하세요.  
> 기술 미리 보기 분기에만 제공되는 기능에 대한 자세한 내용은 [기술 미리 보기](/sccm/core/get-started/technical-preview)를 참조하세요.



##  <a name="bkmk_prerelease"></a> 업데이트에서 시험판 기능 사용
시험판 기능은 프로덕션 환경의 초기 테스트를 위해 현재 분기에 포함됩니다. 이러한 기능은 프로덕션 환경에서 사용할 수 있지만 프로덕션 준비가 된 것으로 간주되지 않습니다. [시험판 기능](/sccm/core/servers/manage/pre-release-features) 및 사용자 환경에서 해당 기능을 사용하도록 설정하는 방법에 대해 자세히 알아봅니다.             



## <a name="frequently-asked-questions"></a>질문과 대답

###  <a name="bkmk_faq"></a> 콘솔에서 특정 업데이트가 표시되지 않는 이유는 무엇인가요?  
 Microsoft 클라우드 서비스와 성공적으로 동기화한 후 콘솔에서 어떤 업데이트도 찾을 수 없는 경우 이 동작은 다음의 이유 중 하나 때문일 수 있습니다.  

-   업데이트하려면 인프라에서 사용하지 않는 구성이 필요하거나 현재 제품 버전에서 업데이트를 받기 위한 필수 조건을 충족하지 않습니다.  

     누락된 업데이트에 대해 필요한 구성 및 필수 조건을 충족했다고 생각되면 서비스 연결 지점이 온라인 모드에 있는지 확인합니다. 그런 다음 **업데이트 및 서비스** 노드에서 **업데이트 확인** 옵션을 사용하여 확인을 강제로 적용합니다. 오프라인 모드에 있으면 서비스 연결 도구를 사용하여 클라우드 서비스와 수동으로 동기화해야 합니다.  

-   Configuration Manager 콘솔에서 업데이트를 볼 수 있는 올바른 역할 기반 관리 권한이 계정에 없습니다.

    콘솔에서 업데이트를 보고 기능을 사용하도록 설정하는 데 필요한 권한에 대한 자세한 내용은 이 항목에서 [업데이트를 관리할 수 있는 권한](../../../core/servers/manage/install-in-console-updates.md#assign-permissions-to-view-and-manage-updates-and-features)을 참조하세요.

