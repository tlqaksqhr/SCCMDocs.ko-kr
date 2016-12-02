---
title: "데이터 전송 | System Center Configuration Manager"
description: "Configuration Manager에서 사이트 간 데이터를 이동하는 방법과 네트워크를 통해 해당 데이터의 전송을 관리할 수 있는 방법에 대해 알아봅니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: dc526e8d-fac3-4bb5-b206-03ad29b0ae11
caps.latest.revision: 12
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 1abd28aa4ce4f946f6328f8f7924b5f5a81e640c


---
# <a name="data-transfers-between-sites-in-system-center-configuration-manager"></a>System Center Configuration Manager의 사이트 간 데이터 전송

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager는 **파일 기반 복제** 및 **데이터베이스 복제**를 사용하여 사이트 간에 여러 유형의 정보를 전송합니다.  이 항목의 주제는 Configuration Manager에서 사이트 간에 데이터를 이동하는 방식과 네트워크를 통해 해당 데이터의 전송을 관리하는 방법을 이해하는 데 도움이 될 수 있습니다.  


##  <a name="a-namebkmkfileroutea-file-based-replication"></a><a name="bkmk_fileroute"></a> File-based replication  
 Configuration Manager는 파일 기반 복제를 사용하여 계층 내의 사이트 간에 파일 기반 데이터를 전송합니다. 이러한 데이터로는 자식 사이트의 배포 지점으로 배포하려는 응용 프로그램 및 패키지와 같은 콘텐츠, 처리될 수 있도록 부모 사이트로 전송되는 미처리 검색 데이터 레코드 등이 있습니다.  

 사이트 간의 파일 기반 통신에서는 **TCP/IP 포트 445** 를 통해 SMB( **서버 메시지 블록**) 프로토콜을 사용합니다. 네트워크를 통해 전송되는 데이터 양을 제어하는 대역폭 제한 및 펄스 모드, 네트워크로 데이터를 전송하는 시간을 제어하는 일정 등의 구성을 지정할 수 있습니다.  

###  <a name="a-namebkmkroutesa-file-replication-routes"></a><a name="bkmk_routes"></a> 파일 복제 경로  
 다음에는 파일 복제 경로를 구성하고 사용하는 데 유용한 정보가 정리되어 있습니다.  

 **파일 복제 경로** - 각 파일 복제 경로는 파일 기반 데이터가 전송될 수 있는 대상 사이트를 식별합니다. 각 사이트는 특정 대상 사이트로의 단일 파일 복제 경로를 지원합니다.  

 Configuration Manager에서 파일 복제 경로에 대해 다음 구성을 지원합니다.  

-   **파일 복제 계정**: 이 계정은 대상 사이트에 연결하고 해당 사이트의 **SMS_SITE** 공유에 데이터를 기록하는 데 사용됩니다. 이 공유에 기록되는 데이터는 수신 사이트에 의해 처리됩니다. 기본적으로, 계층에 사이트가 추가되면 Configuration Manager는 새 사이트의 사이트 서버에 대한 컴퓨터 계정을 해당 사이트의 **파일 복제 계정**으로 할당합니다. 그런 다음 이 계정은 대상 사이트의 **SMS_SiteToSiteConnection_&lt;사이트 코드\>** 그룹에 추가됩니다. 이 그룹은 **SMS_SITE** 공유에 대한 액세스 권한을 부여하는 컴퓨터의 로컬 그룹입니다. 이 계정을 Windows 사용자 계정으로 변경할 수 있습니다. 계정을 변경하는 경우 새 계정을 대상 사이트의 **SMS_SiteToSiteConnection_&lt;사이트 코드\>** 그룹에 추가해야 합니다.  

    > [!NOTE]  
    >  보조 사이트는 항상 보조 사이트 서버의 컴퓨터 계정을 **파일 복제 계정**으로 사용합니다.  

-   **일정**: 각 파일 복제 경로의 일정을 구성하여 데이터가 대상 사이트를 전송될 수 있는 시간과 데이터 유형을 제한할 수 있습니다.  

-   **속도 제한**: 각 파일 복제 경로의 속도 제한을 구성하여 사이트가 대상 사이트로 데이터를 전송할 때 사용하는 네트워크 대역폭을 제어할 수 있습니다.  

    -   **펄스 모드** 를 사용하여 대상 사이트로 전송되는 데이터 블록의 크기를 지정합니다. 또한 각 데이터 블록 전송 간의 시간 지연을 지정할 수도 있습니다. 이 옵션은 매우 낮은 대역폭 네트워크 연결을 통해 데이터를 대상 사이트로 전송해야 하는 경우에 사용합니다. 예를 들어 특정 시간의 사용량이나 링크 속도에 상관없이 매 3초마다 1KB가 아닌, 매 5초마다 데이터 전송을 1KB로 제한할 수 있습니다.  

    -   지정한 시간 비율로만 사이트에서 대상 사이트로의 데이터 전송을 제한하려면 **지정한 시간별 최대 전송 속도로 제한** 을 사용합니다. 이 옵션을 사용하는 경우 Configuration Manager는 사용할 수 있는 네트워크 대역폭을 확인하지 않고 데이터를 보낼 수 있는 시간을 시간 조각으로 분할합니다. 그런 다음 데이터가 한 블록의 시간 내에 전송되고, 전송되지 않은 경우 여러 시간 블록들이 이어집니다. 예를 들어 최대 비율이 **50%**로 설정된 경우 Configuration Manager는 해당 시간 동안 데이터를 전송하고, 데이터가 전송되지 않은 경우 동일한 시간만큼 다시 전송됩니다. 실제 데이터 크기 또는 데이터 블록 크기는 관리되지 않습니다. 대신 데이터가 전송되는 시간의 길이만 관리됩니다.  

        > [!CAUTION]  
        >  기본적으로, 사이트는 **동시 발신 항목 수** 를 최대 3개까지 사용하여 데이터를 대상 사이트로 전송할 수 있습니다. 파일 복제 경로에 속도 제한을 사용하는 경우 해당 사이트에 대한 데이터 전송의 **동시 발신 항목 수** 는 1개로 제한됩니다. 이는 **사용 가능한 대역폭 제한 (%)** 을 **100%**로 설정한 경우에도 마찬가지입니다. 예를 들어 발신자의 기본 설정을 사용하는 경우 이는 기본 용량의 1/3이 되도록 대상 사이트에 대한 전송 속도를 낮춥니다.  

-   두 보조 사이트 간에 파일 복제 경로를 구성하여 두 사이트 간에 파일 기반 콘텐츠를 라우팅할 수 있습니다.  

파일 복제 경로를 관리하려면 **관리** 작업 영역에서 **계층 구성** 노드를 확장한 후 **파일 복제**를 선택합니다.  

**발신자** - 각 사이트에는 하나의 발신자가 있습니다. 발신자는 한 사이트에서 대상 사이트로의 네트워크 연결을 관리하며 여러 사이트에 대한 연결을 동시에 설정할 수 있습니다. 발신자는 사이트에 연결하기 위해 사이트에 대한 파일 복제 경로를 사용하여 네트워크 연결 설정에 사용할 계정을 확인합니다. 또한 발신자는 이 계정을 사용하여 데이터를 대상 사이트의 **SMS_SITE** 공유에 씁니다.  

 기본적으로 발신자는 보통 스레드라고 하는 여러 **동시 발신**을 사용하여 대상 사이트에 데이터를 씁니다. 각 동시 발신(또는 스레드)은 다양한 파일 기반 개체를 대상 사이트에 전송할 수 있습니다. 기본적으로 발신자는 개체를 보낼 때 개체가 모두 보내질 때까지 해당 개체에 대한 데이터 블록을 계속 씁니다. 개체에 대한 데이터를 모두 보내면 새 개체는 해당 스레드에서 보내기를 시작할 수 있습니다.  

 발신자에 대해 다음 설정을 구성할 수 있습니다.  

-   **최대 동시 발신 항목 수**: 기본적으로, 각 사이트는 **동시 발신**5개를 사용하고 하나의 대상 사이트에 데이터를 보낼 때 사용할 3개를 추가해 사용하도록 구성됩니다. 이 수를 늘리면 Configuration Manager에서 동시에 더 많은 파일을 전송할 수 있으므로 사이트 간 데이터 처리량도 증가합니다. 또한 이 수를 늘리면 사이트 간 네트워크 대역폭 요구량도 증가합니다.  

-   **다시 시도 설정**: 기본적으로 각 사이트는 연결에 실패하면 1분의 간격을 두고 두 번에 걸쳐 연결을 다시 시도하도록 구성됩니다. 사이트에서 수행하는 연결 시도의 횟수와 각 시도 간 대기 간격을 수정할 수 있습니다.  

사이트의 발신자를 관리하려면 **관리** 작업 영역에서 **사이트 구성** 노드를 확장하고 **사이트** 노드를 선택한 다음 관리하려는 사이트의 **속성** 을 클릭합니다. 그리고 **발신자** 탭을 클릭하여 발신자 구성을 변경합니다.  

##  <a name="a-namebkmkdbrepa-database-replication"></a><a name="bkmk_dbrep"></a> Database replication  
Configuration Manager 데이터베이스 복제 기능에서는 SQL Server를 사용하여 데이터를 전송하고 사이트 데이터베이스에서 발생한 변경 내용을 계층 구조 내 다른 사이트의 데이터베이스에 저장된 정보와 병합합니다.  

-   이를 통해 모든 사이트가 동일한 정보를 공유할 수 있습니다.  

-   계층 구조에 사이트를 설치하면 데이터베이스 복제가 새 사이트와 지정된 부모 사이트 간에 자동으로 구성됩니다.  

-   사이트 설치가 완료되면 데이터베이스 복제는 자동으로 시작됩니다.  

계층 구조에 새 사이트를 추가하면 Configuration Manager에서 새 사이트에 일반 데이터베이스를 만듭니다. 그런 다음 부모 사이트에서는 자체 데이터베이스에 관련 데이터의 스냅숏을 만들고 이 스냅숏을 파일 기반 복제를 통해 새 사이트에 전송합니다. 새 사이트에서는 SQL Server BCP(대량 복사 프로그램)를 사용하여 Configuration Manager 데이터베이스의 자체 로컬 복사본에 정보를 로드합니다. 스냅숏이 로드되면 각 사이트는 다른 사이트와 함께 데이터베이스 복제를 수행합니다.  

Configuration Manager는 자체의 데이터베이스 복제 서비스를 사용하여 사이트 간에 데이터를 복제합니다. 데이터베이스 복제 서비스에서는 SQL Server 변경 내용 추적을 사용하여 로컬 사이트 데이터베이스에서 변경 내용을 모니터링한 다음 해당 변경 내용을 **SQL Server Service Broker**를 사용하여 다른 사이트에 복제합니다. 기본적으로 이 프로세스에는 **TCP/IP 포트 4022**가 사용됩니다.  

Configuration Manager에서는 데이터베이스 복제에 따라 복제되는 데이터를 여러 복제 그룹으로 그룹화합니다.  

-   각 복제 그룹에는 그룹 내 데이터의 변경 내용이 다른 사이트에 복제되는 빈도를 결정하는 개별적인 고정 복제 일정이 있습니다.  

     예를 들어 역할 기반 관리 구성에 대한 구성 변경 내용은 다른 사이트에 가능한 한 빨리 적용되도록 신속히 복제됩니다. 한편으로 새 보조 사이트 설치 요청과 같이 우선 순위가 낮은 구성 변경 내용은 덜 긴급한 것으로 간주되어 복제되므로 새 사이트 요청이 대상 기본 사이트에 도달하는 데는 몇 분 정도 걸립니다.  

-   데이터베이스 복제에 대한 다음 설정을 수정할 수 있습니다.  

    -   **데이터베이스 복제 링크** 를 사용하면 특정 트래픽이 네트워크를 트래버스하는 시점을 제어할 수 있습니다.  

    -   **분산 보기** 는 선택한 사이트 데이터에 대해 중앙 관리 사이트에서 만들어진 요청이 자식 기본 사이트의 데이터베이스에서 직접 해당 사이트 데이터에 액세스할 수 있도록 하는 복제 링크 구성입니다.  

    -   **일정** 을 사용하면 복제 링크 사용 시점을 구성하고 각 유형의 사이트 데이터 복제 시점을 지정할 수 있습니다.  

    -   복제 링크를 트래버스하는 네트워크 트래픽에 대한 데이터**요약** 은 기본적으로 15분마다 발생하며, 데이터베이스 복제 보고서에 사용됩니다.  

    -   **데이터베이스 복제 임계값** 은 링크가 저하됨 또는 실패 상태로 보고되는 시점을 정의합니다. 또한 저하됨 또는 실패 상태의 복제 링크에 대해 Configuration Manager에서 경고를 생성하는 시점을 구성할 수 있습니다.  

Configuration Manager에서 복제하는 데이터는 데이터베이스 복제별로 글로벌 데이터 또는 사이트 데이터로 분류됩니다. 데이터베이스 복제가 실행되면 글로벌 데이터 및 사이트 데이터에 대한 변경 내용은 데이터베이스 복제 링크를 통해 전송됩니다. 글로벌 데이터는 부모 사이트 또는 자식 사이트 모두에 복제할 수 있고 사이트 데이터는 부모 사이트에만 복제할 수 있습니다. 로컬 데이터라고 하는 세 번째 데이터 유형은 다른 사이트에 복제되지 않습니다. 로컬 데이터에는 다른 사이트에서 필요하지 않은 정보가 포함됩니다.  

-   **글로벌 데이터**: 글로벌 데이터는 계층 전체에서 모든 사이트에 복제되는 관리자 생성 개체를 나타냅니다. 한편 보조 사이트는 글로벌 데이터의 하위 집합으로 글로벌 프록시 데이터만 수신합니다. 글로벌 데이터의 예로는 소프트웨어 배포, 소프트웨어 업데이트, 컬렉션 정의, 역할 기반 관리 보안 범위 등이 있습니다. 관리자는 중앙 관리 사이트 및 기본 사이트에서 글로벌 데이터를 만들 수 있습니다.  

-   **사이트 데이터**: 사이트 데이터는 Configuration Manager 기본 사이트 및 기본 사이트에 보고하는 클라이언트에서 만드는 작업 정보를 나타냅니다. 사이트 데이터는 중앙 관리 사이트에 복제되지만 다른 기본 사이트에는 복제되지 않습니다. 사이트 데이터의 예로는 하드웨어 인벤토리 데이터, 상태 메시지, 경고, 쿼리 기반 컬렉션 결과 등이 있습니다. 사이트 데이터는 중앙 관리 사이트와 데이터가 처음 만들어진 기본 사이트에서만 볼 수 있습니다. 사이트 데이터는 해당 데이터가 만들어진 기본 사이트에서만 수정할 수 있습니다.  

     모든 사이트 데이터는 중앙 관리 사이트에 복제되므로 중앙 관리 사이트에서는 전체 계층에 대한 관리 및 보고를 수행할 수 있습니다.  

다음 섹션에서는 데이터베이스 복제를 관리하기 위한 구성 작업에 대해 자세히 설명합니다.  

###  <a name="a-namebkmkdblinksa-database-replication-links"></a><a name="bkmk_Dblinks"></a> 데이터베이스 복제 링크  
계층에 새 사이트를 설치하면 Configuration Manager에서 두 사이트 간의 데이터베이스 복제 링크를 자동으로 만듭니다. 이때 새 사이트를 부모 사이트에 연결하기 위한 단일 링크가 만들어집니다.  

각 데이터베이스 복제 링크에는 복제 링크를 통한 데이터 전송을 간편하게 제어할 수 있는 구성이 지원됩니다. 각 복제 링크에서는 개별 구성을 지원합니다. 데이터베이스 복제 링크에 대한 제어는 다음을 포함합니다.  

-   분산 보기를 사용하여 기본 사이트 및 중앙 관리 사이트 간에 선택한 사이트 데이터의 복제를 중지하고 중앙 관리 사이트가 기본 사이트의 데이터베이스에서 이 데이터를 직접 액세스하도록 설정합니다.  

-   선택한 사이트 데이터가 자식 기본 사이트에서 중앙 관리 사이트로 전송되는 시점을 예약합니다.  

-   데이터베이스 복제 링크가 저하 상태 또는 실패 상태가 되는 시점을 결정하는 설정을 정의합니다.  

-   실패한 복제 링크에 대한 경고를 생성하는 시점을 구성합니다.  

-   복제 링크를 사용하는 복제 트래픽과 관련된 데이터를 Configuration Manager에서 요약하는 빈도를 지정합니다. 이 데이터는 보고서에 사용됩니다.  

데이터베이스 복제 링크를 구성하기 위해 **데이터베이스 복제** 노드의 Configuration Manager 콘솔에서 해당 링크에 대한 속성을 편집합니다. 이 노드는 **모니터링** 작업 영역과 **관리** 작업 영역의 **계층 구성** 노드 아래에도 나타납니다. 복제 링크는 해당 복제 링크의 부모 사이트 또는 자식 사이트에서 편집할 수 있습니다.  

> [!TIP]  
>  데이터베이스 복제 링크는 두 작업 영역의 **데이터베이스 복제** 노드에서 편집할 수 있습니다. 그러나 **모니터링** 작업 영역의 **데이터베이스 복제** 노드를 사용하면 그 밖에 복제 링크에 대한 데이터베이스 복제 상태를 볼 수 있고 Replication Link Analyzer 도구를 사용하여 데이터베이스 복제 관련 문제를 검사할 수 있습니다.  

복제 링크를 구성하는 방법에 대한 자세한 내용은 [사이트 데이터베이스 복제 제어](#BKMK_DBRepControls)섹션을 참조하세요. 복제를 모니터링하는 방법에 대한 자세한 내용은 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 항목에서 [Monitor hierarchy and replication infrastructure in System Center Configuration Manager](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md) 섹션을 참조하세요.  

다음 섹션의 정보를 사용하면 데이터베이스 복제 링크에 대해 계획할 수 있습니다.  

###  <a name="a-namebkmkdistviewsa-distributed-views"></a><a name="bkmk_distviews"></a> 분산 보기  
분산 보기를 활용하면 선택한 사이트 데이터에 대해 중앙 관리 사이트에서 만들어진 요청은 자식 기본 사이트의 데이터베이스에서 직접 해당 사이트 데이터에 액세스할 수 있습니다. 이러한 직접 액세스로 인해 사이트 데이터를 기본 사이트에서 중앙 관리 사이트에 복제할 필요가 없습니다. 각 복제 링크는 상호 독립적이므로 선택한 복제 링크에서만 분산 보기를 사용하도록 설정할 수 있습니다. 분산 보기는 기본 사이트 및 보조 사이트 사이에서 지원되지 않습니다.  

분산 보기는 다음과 같은 이점을 제공합니다.  

-   중앙 관리 사이트 및 기본 사이트에서 데이터베이스 변경을 처리할 때 발생하는 CPU 부하가 줄어듭니다.  

-   네트워크를 통해 중앙 관리 사이트에 전송되는 데이터 양이 줄어듭니다.  

-   중앙 관리 사이트 데이터베이스를 호스팅하는 SQL Server의 성능이 향상됩니다.  

-   중앙 관리 사이트에서 데이터베이스에 필요한 디스크 공간이 줄어듭니다.  

기본 사이트가 네트워크에서 중앙 관리 사이트와 인접한 곳에 있으며 두 사이트가 상시적으로 작동하고 연결된 상태인 경우 분산 보기를 사용하는 것이 좋습니다. 이는 분산 보기를 사용하면 선택한 데이터를 각 사이트의 SQL Server 간 직접 연결을 통해 두 사이트 사이에서 복제하지 않아도 되기 때문입니다. 이러한 직접 연결은 중앙 관리 사이트에서 해당 데이터에 대한 요청이 만들어질 때마다 설정됩니다. 일반적으로 분산 보기에 사용하도록 설정할 데이터에 대한 요청은 리소스 탐색기에서 보고서나 쿼리, 보기 정보 등을 실행할 때, 그리고 사이트 데이터에 기반한 규칙을 포함하는 컬렉션에 대해 컬렉션 평가를 수행할 때 만들어집니다.  

기본적으로 분산 보기는 각 복제 링크에 대해 사용하지 않도록 설정됩니다. 복제 링크에 대해 분산 보기를 사용하도록 설정하면 이 링크를 통해 중앙 관리 사이트에 복제되지 않는 사이트 데이터를 선택하고 중앙 관리 사이트가 링크를 공유하는 자식 기본 사이트의 데이터베이스에서 이 데이터를 직접 액세스하도록 설정할 수 있습니다. 분산 보기에 대해 다음과 같은 유형의 사이트 데이터를 구성할 수 있습니다.  

-   클라이언트의 하드웨어 인벤토리 데이터  

-   소프트웨어 인벤토리 및 클라이언트의 계량 데이터  

-   클라이언트, 기본 사이트 및 모든 보조 사이트의 상태 메시지  

운영상, Configuration Manager 콘솔 또는 보고서에서 데이터를 확인하는 관리자는 분산 보기를 볼 수 없습니다. 분산 보기를 사용하도록 설정된 데이터에 대해 요청이 만들어지면 중앙 관리 사이트의 데이터베이스를 호스팅하는 SQL Server는 자식 기본 사이트의 SQL Server에 직접 액세스하여 정보를 검색합니다. 예를 들어 중앙 관리 사이트에서 Configuration Manager 콘솔을 사용하여 두 사이트의 하드웨어 인벤토리에 대한 정보를 요청하지만 한 사이트에만 분산 보기에 대해 설정된 하드웨어 인벤토리가 있다고 가정합니다. 분산 보기에 대해 구성되지 않은 사이트의 클라이언트에 대한 인벤토리 정보는 중앙 관리 사이트의 데이터베이스에서 검색됩니다. 분산 보기에 대해 구성된 사이트의 클라이언트에 대한 인벤토리 정보는 자식 기본 사이트의 데이터베이스에서 액세스됩니다. 이 정보는 Configuration Manager 콘솔 또는 보고서에 원본의 구별 없이 나타납니다.  

복제 링크에 분산 보기에 대해 설정된 데이터 유형이 있는 한 자식 기본 사이트에서는 이 데이터를 중앙 관리 사이트에 복제하지 않습니다. 데이터 유형에 대해 분산 보기를 해제하는 즉시 자식 기본 사이트에서는 정상적인 데이터 복제의 일부로 중앙 관리 사이트에 대해 해당 데이터의 복제를 다시 시작합니다. 그러나 이 데이터가 포함된 복제 그룹이 기본 사이트 및 중앙 관리 사이트 사이에서 다시 초기화된 후에야 중앙 관리 사이트에서 이 데이터를 사용할 수 있습니다. 마찬가지로, 분산 보기를 사용하도록 설정된 기본 사이트를 제거한 후에 중앙 관리 사이트의 분산 보기에 대해 설정된 데이터에 액세스하려면 먼저 중앙 관리 사이트에서 자체 데이터의 다시 초기화를 완료해야만 합니다.  

> [!IMPORTANT]  
>  계층 내 복제 링크에서 분산 보기를 사용할 경우 기본 사이트를 제거하기 전에 모든 복제 링크에 대한 분산 보기를 사용하지 않도록 설정해야 합니다. 자세한 내용은 [Uninstall a primary site that is configured with distributed views](../../../core/servers/deploy/install/uninstall-sites-and-hierarchies.md#BKMK_UninstallPrimaryDistViews)을 참조하십시오.  

**분산 보기의 필수 조건 및 제한 사항:**  

-   분산 보기는 중앙 관리 사이트 및 기본 사이트 간의 복제 링크에서만 지원됩니다.  

-  중앙 관리 사이트에서는 SQL Server의 Enterprise Edition을 사용해야 합니다. 기본 사이트에는 이 요구 사항이 없습니다.

-   중앙 관리 사이트에는 SMS 공급자의 인스턴스를 하나만 설치할 수 있으며 이 인스턴스는 사이트 데이터베이스 서버에 설치해야 합니다. 이 제한 사항은 중앙 관리 사이트의 SQL Server에서 자식 기본 사이트의 SQL Server에 액세스하는 데 필요한 Kerberos 인증을 지원하기 위해 필요합니다. 자식 기본 사이트의 SMS 공급자에 대한 제한 사항은 없습니다.  

-   중앙 관리 사이트에서는 SQL Server 보고 서비스 지점을 하나만 사이트 데이터베이스 서버에 설치할 수 있습니다. 이 제한 사항은 중앙 관리 사이트의 SQL Server에서 자식 기본 사이트의 SQL Server에 액세스하는 데 필요한 Kerberos 인증을 지원하기 위해 필요합니다.  

-   사이트 데이터베이스는 SQL Server 클러스터에 호스트할 수 없습니다.  

-   사이트 데이터베이스를 SQL Server AlwaysOn 가용성 그룹에서 호스트할 수 없습니다.  

-   중앙 관리 사이트에서 데이터베이스 서버의 컴퓨터 계정에는 기본 사이트의 사이트 데이터베이스에 대한 **Read** 권한이 필요합니다.  

> [!IMPORTANT]  
>  분산 보기 및 데이터 복제 시점 일정은 데이터베이스 복제 링크에 대해 상호 배타적인 구성입니다.  

###  <a name="a-namebkmkschedulesa-schedule-transfers-of-site-data-on-database-replication-links"></a><a name="BKMK_schedules"></a> 데이터베이스 복제 링크상의 사이트 데이터 전송 일정  
자식 기본 사이트의 사이트 데이터를 중앙 관리 사이트에 복제하는 데 사용되는 네트워크 대역폭을 제어하기 위해 복제 링크의 사용 시점을 예약하고 각 유형의 사이트 데이터가 복제되는 시점을 지정할 수 있습니다. 기본 사이트에서 상태 메시지, 인벤토리 및 계량 데이터를 복제하는 시점을 제어할 수 있습니다. 보조 사이트의 데이터베이스 복제 링크는 사이트 데이터에 대한 일정을 지원하지 않습니다. 글로벌 데이터의 전송은 예약할 수 없습니다.  

데이터베이스 복제 링크 일정을 구성할 경우 선택한 사이트 데이터를 기본 사이트에서 중앙 관리 사이트에 전송하는 작업을 제한할 수 있으며 서로 다른 유형의 사이트 데이터를 복제하도록 각기 다른 시간을 구성할 수 있습니다.  

> [!IMPORTANT]  
>  분산 보기 및 데이터 복제 시점 일정은 데이터베이스 복제 링크에 대해 상호 배타적인 구성입니다.  

###  <a name="a-namebkmksummarizedbreplicationa-summarization-of-database-replication-traffic"></a><a name="BKMK_SummarizeDBReplication"></a> 데이터베이스 복제 트래픽 요약  
각 사이트에서는 자신을 포함하는 데이터베이스 복제 링크에서 이동하는 네트워크 트래픽의 관련 데이터를 정기적으로 요약합니다. 이 요약된 데이터는 데이터베이스 복제용 보고서에 사용됩니다. 복제 링크의 두 사이트는 모두 복제 링크에서 이동하는 네트워크 트래픽을 요약합니다. 데이터의 요약은 사이트 데이터베이스를 호스팅하는 SQL Server에서 수행합니다. 데이터 요약이 끝나면 이 정보는 다른 사이트에 글로벌 데이터로 복제됩니다.  

기본적으로 요약은 15 분마다 발생합니다. 데이터베이스 복제 링크의 속성에서 **요약 간격** 을 편집하면 네트워크 트래픽에 대한 요약 빈도를 수정할 수 있습니다. 요약 빈도는 데이터베이스 복제 관련 보고서에 표시되는 정보에 영향을 줍니다. 이 간격은 5분에서 60분까지로 수정할 수 있습니다. 요약 빈도를 늘리면 복제 링크의 각 사이트에 있는 SQL Server에서 처리 부하도 늘어납니다.  

###  <a name="a-namebkmkdbrepthresholdsa-database-replication-thresholds"></a><a name="BKMK_DBRepThresholds"></a> 데이터베이스 복제 임계값  
데이터베이스 복제 임계값은 데이터베이스 복제 링크의 상태가 저하 또는 실패로 보고되는 시점을 정의합니다. 기본적으로 링크는 임의의 한 복제 그룹에서 복제를 12회 연속으로 시도했으나 실패한 경우 저하로 설정되고 복제 그룹에서 복제를 24회 연속으로 시도했으나 실패한 경우 실패로 설정됩니다.  

사용자 지정 값을 지정하여 Configuration Manager에서 복제 링크를 저하됨 또는 실패 상태로 보고하는 시점을 미세 조정할 수 있습니다. 데이터베이스 복제 링크의 각 상태를 Configuration Manager에서 보고하는 시점을 조정하면 데이터베이스 복제 링크를 통한 데이터베이스 복제의 상태를 정확히 모니터링하는 데 도움이 됩니다.  

다른 복제 그룹은 계속적으로 복제에 성공할 때 하나 이상의 몇몇 복제 그룹은 복제에 실패할 수도 있으므로 복제 링크에서 저하 상태를 처음 보고할 때 이 복제 링크의 복제 상태를 검토할 수 있는 계획을 세워야 합니다. 특정 복제 그룹에 반복되는 지연이 발생하지만 이 지연이 문제를 나타내지 않거나 사이트 간 네트워크 링크의 가용 대역폭이 낮은 경우 해당 링크의 저하 또는 실패 상태에 대한 재시도 값을 수정하는 것이 좋습니다. 링크가 저하 또는 실패로 설정되기 전의 재시도 횟수를 늘리면 알려진 문제에 대해 발생하는 거짓 경고를 방지할 수 있으므로 링크 상태를 좀더 정확하게 추적할 수 있습니다.  

또한 그룹의 복제가 발생하는 빈도를 파악하기 위해 각 복제 그룹에 대한 복제 동기화 간격을 고려해야 합니다. **모니터링** 작업 영역의 **데이터베이스 복제** 노드에 있는 복제 링크의 **복제 세부 정보** 탭에서 복제 그룹에 대한 **동기화 간격** 을 볼 수 있습니다.  

복제 상태를 확인하는 방법을 포함하여 데이터베이스 복제를 모니터링하는 방법에 대한 자세한 내용은 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 항목에서 [How to monitor database replication links and replication status](../../../core/servers/manage/monitor-hierarchy-and-replication-infrastructure.md#BKMK_MonitorRepLinksAndStatuss) 섹션을 참조하세요.  

데이터베이스 복제 임계값 구성에 대한 자세한 내용은 [사이트 데이터베이스 복제 제어](#BKMK_DBRepControls)섹션을 참조하세요.  

##  <a name="a-namebkmkdbrepcontrolsa-site-database-replication-controls"></a><a name="BKMK_DBRepControls"></a> 사이트 데이터베이스 복제 제어  
각 사이트 데이터베이스는 데이터베이스 복제에 사용되는 네트워크 대역폭을 제어하는 데 도움이 되는 구성을 지원합니다. 이러한 구성은 사용자가 설정을 구성하는 사이트 데이터베이스에만 적용되며 사이트에서 데이터베이스 복제를 통해 다른 사이트에 데이터를 복제할 때 항상 사용됩니다.  

각 사이트 데이터베이스에 대한 복제 제어는 다음을 포함합니다.  

-   Configuration Manager에서 SQL Server Service Broker에 대해 사용하는 포트를 변경합니다.  

-   복제 실패가 사이트에서 자체 사이트 데이터베이스 복사본을 다시 초기화하도록 트리거하기 전까지의 대기 시간을 구성합니다.  

-   데이터베이스 복제로 복제되는 데이터를 압축하도록 사이트 데이터베이스를 구성합니다. 데이터는 사이트 간 전송을 위해서만 압축되며 어느 사이트든 사이트 데이터베이스에 저장할 목적으로는 압축되지 않습니다.  

사이트 데이터베이스에 대한 복제 제어를 구성하기 위해 **데이터베이스 복제** 노드의 Configuration Manager 콘솔에서 사이트 데이터베이스의 속성을 편집합니다. 이 노드는 **관리** 작업 영역의 **계층 구성** 노드 아래에 나타나며 **모니터링 작업 영역**에도 나타납니다. 사이트 데이터베이스의 속성을 편집하려면 사이트 간 복제 링크를 선택한 다음 **부모 데이터베이스 속성** 또는 **자식 데이터베이스 속성**을 엽니다.  

> [!TIP]  
>  데이터베이스 복제 제어는 두 작업 영역의 **데이터베이스 복제** 노드에서 구성할 수 있습니다. 그러나 **모니터링** 작업 영역의 **데이터베이스 복제** 노드를 사용하면 그 밖에 복제 링크에 대한 데이터베이스 복제 상태를 볼 수 있고 Replication Link Analyzer 도구를 사용하여 복제 관련 문제를 검사할 수 있습니다.  



<!--HONumber=Nov16_HO1-->

