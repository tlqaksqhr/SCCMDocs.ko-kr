---
title: "마이그레이션 작업 계획 | System Center Configuration Manager"
description: "마이그레이션 작업을 사용하면 System Center Configuration Manager 환경으로 마이그레이션할 데이터를 구성할 수 있습니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: a70bfbd4-757a-4468-9312-1c3b373ef9fc
caps.latest.revision: 6
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
robots: noindex
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 21e00064a8ecad3dd1c24b7f02bd0a8a8c36924f


---
# <a name="planning-a-migration-job-strategy-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 마이그레이션 작업 전략 계획

*적용 대상: System Center Configuration Manager(현재 분기)*

마이그레이션 작업을 사용하면 System Center Configuration Manager 환경으로 마이그레이션할 특정 데이터를 구성할 수 있습니다. 마이그레이션 작업은 마이그레이션하려는 개체를 식별하며, 대상 계층의 최상위 사이트에서 실행됩니다. 원본 사이트별로 하나 이상의 마이그레이션 작업을 구성할 수 있습니다. 그러면 모든 개체를 한 번에 마이그레이션하거나 각 작업을 사용하여 데이터의 한정된 하위 집합을 마이그레이션할 수 있습니다.  

 Configuration Manager는 원본 계층의 사이트 하나 이상에서 데이터를 수집한 후에 마이그레이션 작업을 만들 수 있습니다. 데이터를 수집한 원본 사이트에서 원하는 순서에 따라 데이터를 마이그레이션할 수 있습니다. Configuration Manager 2007 원본 사이트에서는 개체가 만들어진 사이트에서만 데이터를 마이그레이션할 수 있습니다. System Center 2012 Configuration Manager 이상 버전을 실행하는 원본 사이트에서는 마이그레이션할 수 있는 모든 데이터를 원본 계층의 최상위 사이트에서 사용할 수 있습니다.  

 계층 간에 클라이언트를 마이그레이션하기 전에 해당 클라이언트에서 사용하는 개체를 마이그레이션해야 하며 이러한 개체를 대상 계층에서 사용할 수 있어야 합니다. 예를 들어 Configuration Manager 2007 SP2 원본 계층에서 마이그레이션하는 경우 클라이언트가 포함된 사용자 지정 컬렉션에 배포되는 콘텐츠에 대한 보급 알림이 있을 수 있습니다. 이 시나리오에서는 클라이언트를 마이그레이션하기 전에 컬렉션, 보급 알림 및 연결된 콘텐츠를 마이그레이션해야 합니다. 클라이언트를 마이그레이션하기 전에 콘텐츠, 컬렉션 및 보급 알림을 마이그레이션하지 않으면 이 데이터를 대상 계층의 클라이언트에 연결할 수 없기 때문입니다. 이전에 실행했던 보급 알림 및 콘텐츠와 관련된 데이터에 클라이언트를 연결하지 않으면 대상 계층에 설치하도록 클라이언트에 콘텐츠가 제공될 수 있으나 이는 불필요할 수 있습니다. 데이터를 마이그레이션한 후에 클라이언트를 마이그레이션하면 클라이언트가 이 콘텐츠 및 보급 알림에 연결되고, 보급 알림이 되풀이되지 않으면 마이그레이션된 보급 알림에 대해 이 콘텐츠가 다시 제공되지 않습니다.  

 일부 개체의 경우 원본 계층에서 대상 계층으로 데이터를 마이그레이션하는 작업 외에 더 많은 작업이 필요합니다. 예를 들어 클라이언트용 소프트웨어 업데이트를 대상 계층에 성공적으로 마이그레이션하려면 대상 계층에서 활성 소프트웨어 업데이트 지점을 배포하고, 제품의 카탈로그를 구성하고, 소프트웨어 업데이트 지점을 WSUS(Windows Server Update Services)와 동기화해야 합니다.  

 마이그레이션 작업을 계획하려면 다음 섹션을 참조하세요.  

-   [마이그레이션 작업 유형](#Types_of_Migration)  

-   [모든 마이그레이션 작업에 대한 일반적인 계획](#About_Migration_Jobs)  

-   [컬렉션 마이그레이션 작업 계획](#About_Collection_Migration)  

-   [개체 마이그레이션 작업 계획](#About_Object_Migration)  

-   [이전에 마이그레이션한 개체 마이그레이션 작업 계획](#About_Object_Migrations)  

##  <a name="a-nametypesofmigrationa-types-of-migration-jobs"></a><a name="Types_of_Migration"></a> 마이그레이션 작업 유형  
 Configuration Manager에서 지원하는 마이그레이션 작업 유형은 다음과 같습니다. 각 작업 유형은 해당 작업에 포함할 수 있는 개체를 정의할 수 있도록 되어 있습니다.  

 **컬렉션 마이그레이션**(Configuration Manager 2007 SP2에서 마이그레이션하는 경우에만 지원됨) - 선택하는 컬렉션과 관련된 개체를 마이그레이션합니다. 기본적으로 컬렉션 마이그레이션에는 컬렉션의 구성원과 연결된 모든 개체가 포함됩니다. 컬렉션 마이그레이션 작업을 사용할 때 특정 개체 인스턴스를 제외할 수 있습니다.  

 **개체 마이그레이션** - 선택하는 개별 개체를 마이그레이션합니다. 마이그레이션할 특정 데이터만 선택합니다.  

 **이전에 마이그레이션된 개체 마이그레이션** - 이전에 마이그레이션된 개체가 마지막으로 마이그레이션된 후 원본 계층에서 업데이트되면 해당 개체를 마이그레이션합니다.  

###  <a name="a-nameobjectsthatcanmigratea-objects-that-you-can-migrate"></a><a name="Objects_that_can_migrate"></a> 마이그레이션할 수 있는 개체  
 특정 유형의 마이그레이션 작업에서는 일부 개체만 마이그레이션할 수 있습니다. 다음에는 각 마이그레이션 작업 유형으로 마이그레이션할 수 있는 개체 유형이 나와 있습니다.  

> [!NOTE]  
>  컬렉션 마이그레이션 작업은 Configuration Manager 2007 SP2 원본 계층에서 개체를 마이그레이션할 때만 사용할 수 있습니다.  

 **각 개체를 마이그레이션하는 데 사용할 수 있는 작업 유형은 다음과 같습니다.**  

-   **보급 알림**(지원되는 Configuration Manager 2007 원본 사이트에서 마이그레이션 가능)  

    -   컬렉션 마이그레이션  

-   **Asset Intelligence 카탈로그**  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **Asset Intelligence 하드웨어 요구 사항**  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **Asset Intelligence 소프트웨어 목록**  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **경계**  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **구성 기준**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **자산 및 준수**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **유지 관리 기간**  

    -   컬렉션 마이그레이션  

-   **운영 체제 배포 부팅 이미지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **운영 체제 배포 드라이버 패키지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **운영 체제 배포 드라이버**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **운영 체제 배포 이미지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **운영 체제 배포 패키지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **소프트웨어 배포 패키지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **소프트웨어 계량 규칙**  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **소프트웨어 업데이트 배포 패키지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **소프트웨어 업데이트 배포 템플릿**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **소프트웨어 업데이트 배포**  

    -   컬렉션 마이그레이션  

-   **소프트웨어 업데이트 목록**  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **작업 순서.**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    -   이전에 마이그레이션된 개체 마이그레이션  

-   **가상 응용 프로그램 패키지**  

    -   컬렉션 마이그레이션  

    -   개체 마이그레이션  

    > [!IMPORTANT]  
    >  개체 마이그레이션을 사용하면 가상 응용 프로그램 패키지를 마이그레이션할 수 있지만 **이전에 마이그레이션된 개체 마이그레이션**이라는 마이그레이션 작업 유형을 사용하면 이 패키지를 마이그레이션할 수 없습니다. 대신 대상 사이트에서 마이그레이션된 가상 응용 프로그램 패키지를 삭제한 다음 새 마이그레이션 작업을 만들어 가상 응용 프로그램을 마이그레이션해야 합니다.  

##  <a name="a-nameaboutmigrationjobsa-general-planning-for-all-migration-jobs"></a><a name="About_Migration_Jobs"></a> 모든 마이그레이션 작업에 대한 일반적인 계획  
 마이그레이션 작업 만들기 마법사를 사용하면 대상 계층에 개체를 마이그레이션하는 마이그레이션 작업을 만들 수 있습니다. 만드는 마이그레이션 작업 유형에 따라 마이그레이션할 수 있는 개체가 결정됩니다. 여러 마이그레이션 작업을 만들고 사용하여 동일한 원본 사이트나 여러 원본 사이트에서 데이터를 마이그레이션할 수 있습니다. 한 가지 유형의 마이그레이션 작업을 사용할 경우 다른 유형의 마이그레이션 작업을 사용할 수 없는 것은 아닙니다.  

 마이그레이션 작업을 성공적으로 실행하면 상태가 **완료됨** 으로 표시되어 다시 실행할 수 없습니다. 그러나 새 마이그레이션 작업을 만들어 원래 작업으로 마이그레이션했던 개체를 마이그레이션할 수 있으며, 새 마이그레이션 작업에 다른 개체도 추가할 수 있습니다. 추가 마이그레이션 작업을 만들면 이전에 마이그레이션된 개체는 **마이그레이션됨**상태로 표시됩니다. 이러한 개체를 선택하여 다시 마이그레이션할 수는 있지만, 원본 계층에서 개체가 업데이트되지 않으면 이러한 개체를 다시 마이그레이션할 필요가 없습니다. 원본 계층에서 개체를 업데이트한 경우 **마이그레이션 후 수정된 개체**라는 마이그레이션 작업 유형을 사용하면 해당 개체를 식별할 수 있습니다.  

 마이그레이션 작업은 실행하기 전에 삭제할 수 있습니다. 그러나 마이그레이션 작업을 완료한 후에는 Configuration Manager 콘솔에 계속 표시되고 삭제할 수 없습니다. 완료되었거나 아직 실행하지 않은 각 마이그레이션 작업은 마이그레이션 프로세스를 완료하고 마이그레이션 데이터를 정리할 때까지 Configuration Manager 콘솔에 계속 표시됩니다.  

> [!NOTE]  
>  **마이그레이션 데이터 정리** 작업을 사용하여 마이그레이션을 완료한 후에는 현재 원본 계층과 같은 계층을 다시 구성하여 이전에 마이그레이션된 개체를 다시 표시할 수 있습니다.  

 마이그레이션 작업을 선택한 다음 **작업에 포함된 개체** 탭을 클릭하면 Configuration Manager 콘솔에서 마이그레이션 작업에 포함된 개체를 볼 수 있습니다.  

 모든 마이그레이션 작업을 계획하려면 다음 섹션의 정보를 참조하세요.  

### <a name="data-selection"></a>데이터 선택  
 컬렉션 마이그레이션 작업을 만들 때 컬렉션을 하나 이상 선택해야 합니다. 컬렉션을 선택하면 마이그레이션 작업 만들기 마법사에 컬렉션과 연결된 개체가 표시됩니다. 기본적으로는 선택한 컬렉션과 연결된 개체가 모두 마이그레이션되지만 해당 작업으로 마이그레이션하지 않을 개체를 선택 해제할 수 있습니다. 종속된 개체가 있는 개체를 선택 해제하면 해당하는 종속된 개체도 선택 해제됩니다. 선택 해제된 모든 개체는 제외 목록에 추가됩니다. 제외 목록의 개체는 향후 마이그레이션 작업의 자동 선택에서 제거됩니다. 앞으로 만들 마이그레이션 작업에서 마이그레이션하도록 자동 선택할 개체를 제외 목록에서 제거하려면 제외 목록을 수동으로 편집해야 합니다.  

### <a name="site-ownership-for-migrated-content"></a>마이그레이션된 콘텐츠에 대한 사이트 소유권  
 배포할 콘텐츠를 마이그레이션하는 경우 콘텐츠 개체를 대상 계층 내 사이트에 할당해야 합니다. 그러면 이 사이트는 대상 계층에서 해당 콘텐츠의 소유자가 됩니다. 대상 계층의 최상위 사이트는 콘텐츠의 메타데이터를 실제로 마이그레이션하는 사이트지만 네트워크를 통해 콘텐츠의 원래 원본 파일에 액세스하는 사이트는 할당된 사이트입니다.  

 마이그레이션 중에 사용되는 네트워크 대역폭을 최소화하려면 콘텐츠의 소유권을 사용 가능한 가장 가까운 사이트로 이전하는 것이 좋습니다. 콘텐츠에 대한 정보는 System Center Configuration Manager에서 전체적으로 공유되므로 모든 사이트에서 사용할 수 있습니다.  

 콘텐츠 관련 정보는 데이터베이스 복제를 통해 대상 계층의 모든 사이트에 공유되지만 기본 사이트에 할당한 후 다른 기본 사이트의 배포 지점에 배포한 콘텐츠는 파일 기반 복제를 통해 전송됩니다. 이 전송은 중앙 관리 사이트를 경유한 다음 각각의 다른 기본 사이트로 라우팅됩니다. 사이트를 콘텐츠 소유자로 할당하는 경우 마이그레이션 전이나 도중에 여러 기본 사이트에 배포할 패키지를 중앙에서 관리하면 대역폭이 낮은 네트워크를 통한 데이터 전송을 줄일 수 있습니다.  

### <a name="configure-role-based-administration-security-scopes-for-migrated-data"></a>마이그레이션된 데이터의 역할 기반 관리 보안 범위 구성  
 데이터를 대상 계층으로 마이그레이션할 때 마이그레이션되는 데이터를 소유한 개체에 역할 기반 관리 보안 범위를 하나 이상 할당해야 합니다. 그러면 마이그레이션 후에 이 데이터에 적절한 관리자만 액세스할 수 있습니다. 지정하는 보안 범위는 마이그레이션 작업에서 정의하며 해당 작업으로 마이그레이션하는 각 개체에 적용됩니다. 다른 개체 집합에 다른 보안 범위를 적용해야 하는 경우 마이그레이션 중에 해당 범위를 할당하려면 다른 마이그레이션 작업을 사용하여 다른 개체 집합을 마이그레이션해야 합니다.  

 마이그레이션 작업을 구성하기 전에 System Center Configuration Manager에서 역할 기반 관리 작동 방식을 검토하고, 필요한 경우 마이그레이션하는 데이터의 보안 범위를 하나 이상 구성하여 대상 계층에서 마이그레이션된 개체에 액세스할 수 있는 사용자를 제어합니다.  

 보안 범위 및 역할 기반 관리에 대한 자세한 내용은 [System Center Configuration Manager의 역할 기반 관리 기본 사항](../../core/understand/fundamentals-of-role-based-administration.md)을 참조하세요.  

### <a name="review-migration-actions"></a>마이그레이션 작업 검토  
 마이그레이션 작업을 구성하면 마이그레이션에 성공하기 위해 수행해야 할 작업 목록 및 선택한 데이터를 마이그레이션하는 동안 Configuration Manager에서 수행하는 작업 목록이 마이그레이션 작업 만들기 마법사에 표시됩니다. 이 정보를 주의 깊게 검토하여 예상 결과를 확인하세요.  

### <a name="scheduling-migration-jobs"></a>마이그레이션 작업 예약  
 기본적으로 마이그레이션 작업은 만들어진 직후에 실행됩니다. 그러나 마이그레이션 작업을 만들 때나 나중에 해당 작업의 속성을 편집하면 마이그레이션 작업을 실행할 시간을 지정할 수 있습니다. 마이그레이션 작업을 다음 시간에 실행하도록 예약할 수 있습니다.  

-   지금 작업 실행  

-   특정 시작 시간에 작업 실행  

-   작업 실행 안 함  

### <a name="specify-conflict-resolution-for-migrated-data"></a>마이그레이션된 데이터에 대한 충돌 해결 지정  
 이전에 대상 데이터베이스로 마이그레이션된 데이터를 건너뛰거나 덮어쓰도록 마이그레이션 작업을 구성하지 않으면 기본적으로 마이그레이션 작업은 대상 데이터베이스의 데이터를 덮어쓰지 않습니다.  

##  <a name="a-nameaboutcollectionmigration-a-planning-for-collection-migration-jobs"></a><a name="About_Collection_Migration "></a> 컬렉션 마이그레이션 작업 계획  
 컬렉션 마이그레이션 작업은 지원되는 버전의 Configuration Manager 2007을 실행하는 원본 계층에서 데이터를 마이그레이션하는 경우에만 사용할 수 있습니다. 컬렉션별로 마이그레이션할 때 마이그레이션할 컬렉션을 하나 이상 지정해야 합니다. 지정한 각 컬렉션별로 마이그레이션 작업 시 모든 마이그레이션 관련 개체가 자동으로 선택됩니다. 예를 들어 특정 사용자 컬렉션을 선택하는 경우 컬렉션 구성원이 식별된 후 해당 컬렉션과 연결된 배포를 마이그레이션할 수 있습니다. 선택적으로, 해당 구성원에 연결된 다른 배포 개체를 마이그레이션하도록 선택할 수 있습니다. 이러한 선택한 모든 항목이 마이그레이션할 개체 목록에 추가됩니다.  

 컬렉션을 마이그레이션할 때 System Center Configuration Manager는 유지 관리 기간 및 컬렉션 변수를 포함하는 컬렉션 설정도 마이그레이션하지만 AMT 클라이언트 프로비전에 대한 컬렉션 설정은 마이그레이션할 수 없습니다.  

 다음 섹션의 정보를 참조하면 컬렉션 기반 마이그레이션 작업에 적용할 수 있는 추가 구성을 파악할 수 있습니다.  

### <a name="excluding-objects-from-collection-migration-jobs"></a>컬렉션 마이그레이션 작업에서 개체 제외  
 컬렉션 마이그레이션 작업에서 특정 개체를 제외할 수 있습니다. 컬렉션 마이그레이션 작업에서 특정 개체를 제외하는 경우 해당 개체는 글로벌 제외 목록에 추가됩니다. 이 목록에는 현재 원본 계층에서 모든 원본 사이트에 대해 생성된 마이그레이션 작업에서 제외한 모든 개체가 포함되어 있습니다. 제외 목록의 개체는 나중에 마이그레이션 작업에 사용할 수 있지만, 새 컬렉션 기반 마이그레이션 작업을 만드는 경우 자동으로 포함되지는 않습니다.  

 이전에 제외한 개체를 제거하도록 제외 목록을 편집할 수 있습니다. 제외 목록에서 개체를 제거하면 새 마이그레이션 작업을 만들 때 관련 컬렉션이 지정되면 해당 개체가 자동으로 선택됩니다.  

### <a name="unsupported-collections"></a>지원되지 않는 컬렉션  
 Configuration Manager는 기본 사용자 컬렉션, 장치 컬렉션 및 Configuration Manager 2007 원본 계층의 사용자 지정 컬렉션 대부분을 마이그레이션할 수 있습니다. 하지만 동일한 컬렉션에 사용자와 장치를 포함하는 컬렉션은 Configuration Manager에서 마이그레이션할 수 없습니다.  

 마이그레이션할 수 없는 컬렉션은 다음과 같습니다.  

-   사용자 및 장치를 포함하는 컬렉션  

-   다른 리소스 유형의 컬렉션에 대한 참조를 포함하는 컬렉션. 예를 들어 하위 컬렉션 또는 사용자 기반 컬렉션에 대한 링크 중 하나가 있는 장치 기반 컬렉션이 있습니다. 이 예제에서는 최상위 컬렉션만 마이그레이션합니다.  

-   알 수 없는 컴퓨터를 포함하는 규칙이 있는 컬렉션. 컬렉션은 마이그레이션되지만, 알 수 없는 컴퓨터를 포함하는 규칙은 마이그레이션되지 않습니다.  

### <a name="empty-collections"></a>비어 있는 컬렉션  
 빈 컬렉션은 연결된 리소스가 없는 컬렉션입니다. Configuration Manager에서 빈 컬렉션을 마이그레이션하면 사용자나 장치를 포함하지 않는 폴더 구조로 컬렉션이 변환됩니다. 이 폴더는 Configuration Manager 콘솔 **자산 및 준수** 작업 영역의 **사용자 컬렉션** 또는 **장치 컬렉션** 노드 아래에 빈 컬렉션의 이름으로 작성됩니다.  

### <a name="linked-collections-and-subcollections"></a>연결된 컬렉션 및 하위 컬렉션  
 다른 컬렉션에 연결된 컬렉션 또는 하위 컬렉션이 있는 컬렉션을 마이그레이션하는 경우 Configuration Manager에서 연결된 컬렉션 및 하위 컬렉션뿐 아니라 **사용자 컬렉션** 또는 **장치 컬렉션** 노드 아래에 폴더가 만들어집니다.  

### <a name="collection-dependencies-and-include-objects"></a>컬렉션 종속성 및 개체 포함  
 마이그레이션 작업 만들기 마법사에서 마이그레이션할 컬렉션을 지정하면 종속된 컬렉션이 자동으로 작업에 포함되도록 선택됩니다. 이러한 동작을 통해 모든 필수 리소스를 마이그레이션 후에도 사용할 수 있게 됩니다.  

 예를 들면 다음과 같습니다. Windows 7을 실행하는 장치 컬렉션( **Win_7**)을 선택합니다. 이러한 컬렉션은 클라이언트 운영 체제를 모두 포함하는 **All_Clients**이라는 컬렉션으로 제한됩니다. **All_Clients** 컬렉션은 마이그레이션에 자동으로 선택됩니다.  

### <a name="collection-limiting"></a>컬렉션 제한  
 System Center Configuration Manager에서 컬렉션은 글로벌 데이터이며 계층 구조의 각 사이트에서 평가됩니다. 따라서 마이그레이션 후에 컬렉션의 범위를 제한할 방법을 계획해야 합니다. 마이그레이션하는 동안에는 사용할 대상 계층의 컬렉션을 식별하여 마이그레이션 중인 컬렉션 범위를 제한하여 예상치 않은 구성원이 마이그레이션된 컬렉션에 포함되지 않도록 할 수 있습니다.  

 예를 들어 Configuration Manager 2007에서 컬렉션은 컬렉션이 만들어진 사이트와 자식 사이트에서 평가됩니다. 보급 알림은 자식 사이트에만 배포될 수 있으며 이는 해당 보급 알림의 범위를 자식 사이트로 제한할 수 있습니다. 반면 System Center Configuration Manager에서는 각 사이트에서 컬렉션을 평가한 다음 각 사이트에 연결된 보급 알림을 평가합니다. 컬렉션 제한을 사용하면 예상치 않은 컬렉션 구성원이 추가되는 것을 방지하도록 다른 컬렉션에 기반하여 컬렉션 구성원을 구체적으로 지정할 수 있습니다.  

### <a name="site-code-replacement"></a>사이트 코드 대체  
 Configuration Manager 2007 사이트를 식별하는 기준을 포함하는 컬렉션을 마이그레이션하는 경우 대상 계층 구조에서 특정 사이트를 지정해야 합니다. 그래야 마이그레이션된 컬렉션이 대상 계층에서 계속 작동하고 범위가 증가하지 않게 됩니다.  

### <a name="specify-behavior-for-migrated-advertisements"></a>마이그레이션된 보급 알림에 대한 동작 지정  
 기본적으로, 컬렉션 기반 마이그레이션 작업은 대상 계층으로 마이그레이션되는 보급 알림을 사용하지 않도록 설정합니다. 여기에는 해당 보급 알림과 연결된 모든 프로그램도 포함됩니다. 보급 알림을 포함하는 컬렉션 기반 마이그레이션 작업을 만드는 경우 마이그레이션 작업 만들기 마법사의 **설정** 페이지에 **보급 알림이 원본 계층 구조에서 마이그레이션된 후에 Configuration Manager에서 배포용 프로그램 사용** 옵션이 나타납니다. 이 옵션을 선택하면 마이그레이션 이후 보급 알림과 연결된 프로그램이 사용하도록 설정됩니다. 가장 좋은 방법은 이 옵션을 선택하지 않는 것입니다. 대신, 프로그램을 수신할 클라이언트를 확인할 수 있는 경우 마이그레이션 이후 해당 프로그램을 사용하도록 설정하는 것입니다.  

> [!NOTE]  
>  **보급 알림이 원본 계층 구조에서 마이그레이션된 후에 Configuration Manager에서 배포용 프로그램 사용** 옵션은 컬렉션 기반 마이그레이션 작업을 생성한 경우 마이그레이션 작업에 보급 알림이 포함되어 있어야만 나타납니다.  

 마이그레이션 이후 프로그램을 사용하도록 설정하려면 프로그램 속성의 **고급** 탭에서 **배포된 컴퓨터에서 이 프로그램 사용 안 함** 옵션의 선택을 취소합니다.  

##  <a name="a-nameaboutobjectmigrationa-planning-for-object-migration-jobs"></a><a name="About_Object_Migration"></a> 개체 마이그레이션 작업 계획  
 컬렉션 마이그레이션과 달리, 마이그레이션하려는 각 개체와 개체 인스턴스를 선택해야 합니다. Configuration Manager 2007 계층 구조의 보급 알림, System Center 2012 Configuration Manager 또는 System Center Configuration Manager 계층 구조의 게시 등 개별 개체를 선택하여 특정 마이그레이션 작업의 마이그레이션할 개체 목록에 추가할 수 있습니다. 마이그레이션 목록에 추가하지 않은 개체는 개체 마이그레이션 작업을 통해 대상 사이트로 마이그레이션되지 않습니다.  

 개체 기반 마이그레이션 작업에는 모든 마이그레이션 작업에 적용되는 구성 이외에 계획해야 할 추가 구성이 없습니다.  

##  <a name="a-nameaboutobjectmigrationsa-planning-for-previously-migrated-object-migration-jobs"></a><a name="About_Object_Migrations"></a> 이전에 마이그레이션한 개체 마이그레이션 작업 계획  
 대상 계층으로 이미 마이그레이션한 개체가 원본 계층에서 업데이트된 경우 **마이그레이션 후 수정된 개체** 작업 유형을 사용하여 해당 개체를 다시 마이그레이션할 수 있습니다. 예를 들어 원본 계층에서 패키지의 이름을 변경하거나 원본 파일을 업데이트하는 경우 원본 계층에서 패키지 버전 번호가 증가합니다. 패키지 버전 번호가 증가한 후 패키지는 이러한 작업 유형에서 마이그레이션할 수 있도록 식별됩니다.  

 이러한 작업 유형은 개체 마이그레이션 유형과 유사하며, 마이그레이션할 개체를 선택하는 경우 이전 마이그레이션 작업에서 마이그레이션된 후 업데이트가 수행된 개체만 선택할 수 있다는 차이점만 있습니다.  

 이 작업 유형을 선택하는 경우 마이그레이션 작업 만들기 마법사의 **설정** 페이지에서 이전에 마이그레이션한 개체를 덮어쓰도록 충돌 해결 동작이 구성되며, 이 설정은 변경할 수 없습니다.  

> [!NOTE]  
>  이 마이그레이션 작업은 원본 계층에서 자동으로 업데이트된 개체와 관리자가 업데이트한 개체를 식별할 수 있습니다.  



<!--HONumber=Nov16_HO1-->

