---
title: "서비스 연결 지점 | System Center Configuration Manager"
description: "이 Configuration Manager 사이트 시스템 역할에 대해 알아보고 사용 범위를 이해하고 계획합니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bc2282d5-0571-465b-9528-a555855eaacd
caps.latest.revision: 18
caps.handback.revision: 0
author: Brenduns
ms.author: brenduns
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: e30c3d4bbf42e008a3f570c843b2f63251bce158


---
# <a name="about-the-service-connection-point-in-system-center-configuration-manager"></a>System Center Configuration Manager의 서비스 연결 지점 정보

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 서비스 연결 지점은 계층 구조에 대한 여러 중요한 기능을 제공하는 사이트 시스템 역할입니다. 서비스 연결 지점을 구성하기 전에 이 사이트 시스템 역할을 구성하는 방법에 영향을 줄 수 있는 사용 범위를 이해하고 계획합니다.  

-   **Microsoft Intune을 사용하여 모바일 장치 관리** - 이 역할은 이전 버전의 Configuration Manager에서 사용된 Windows Intune 커넥터를 대체하며 Intune 구독 세부 정보로 구성할 수 있습니다. [System Center Configuration Manager 및 Microsoft Intune을 지원하는 하이브리드 MDM(모바일 장치 관리)](../../../../mdm/plan-design/hybrid-mobile-device-management.md)을 참조하세요.  

-   **온-프레미스 MDM을 사용하여 모바일 장치 관리** - 이 역할은 인터넷에 연결하지 않는 관리되는 온-프레미스 장치를 지원합니다. [System Center Configuration Manager의 온-프레미스 인프라로 모바일 장치 관리](../../../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)를 참조하세요.  

-   **Configuration Manager 인프라에서 사용 현황 데이터 업로드** - 업로드하는 세부 정보 수준이나 정보량을 제어할 수 있습니다. 업로드된 데이터를 활용하여 다음 작업을 수행할 수 있습니다.  

    -   사전에 문제 식별 및 해결  

    -   제품 및 서비스 개선  

    -   사용하는 버전의 Configuration Manager에 적용되는 Configuration Manager 업데이트 식별  

     [사용 현황 데이터 수준 및 설정](../../../../core/servers/deploy/install/setup-reference.md#bkmk_usage)을 참조하세요.  

-   **Configuration Manager 인프라에 적용되는 업데이트 다운로드** - 업로드하는 사용 현황 데이터를 기준으로 인프라와 관련된 업데이트만 사용할 수 있습니다.  

 **각 계층 구조는 이 역할의 단일 인스턴스를 지원합니다.**  

-   사이트 시스템 역할은 계층 구조의 최상위 계층 사이트(중앙 관리 사이트 또는 독립 실행형 기본 사이트)에만 설치할 수 있습니다.  

-   독립 실행형 기본 사이트를 더 큰 계층 구조로 확장하는 경우 기본 사이트에서 이 역할을 제거한 다음 중앙 관리 사이트에서 설치해야 합니다.  

##  <a name="a-namebkmkmodesa-modes-of-operation"></a><a name="bkmk_modes"></a> 작동 모드  
 서비스 연결 지점은 다음 두 가지 작동 모드를 지원합니다.  

-   **온라인 모드**에서는 서비스 연결 지점이 24시간마다 업데이트를 자동으로 확인한 다음 현재 인프라 및 제품 버전에 사용 가능한 새 업데이트를 자동으로 다운로드하여 Configuration Manager 콘솔에서 사용할 수 있게 합니다.  

-   **오프라인 모드**에서는 서비스 연결 지점이 Microsoft 클라우드 서비스에 연결하지 않으며, 수동으로 [System Center Configuration Manager의 서비스 연결 도구를 사용](../../../../core/servers/manage/use-the-service-connection-tool.md)하여 사용 가능한 업데이트를 가져와야 합니다.  

서비스 연결 지점을 설치한 후 온라인 또는 오프라인 간에 모드를 변경할 때 이 변경 내용을 적용하려면 먼저 Configuration Manager SMS_Executive 서비스의 SMS_DMP_DOWNLOADER 스레드를 다시 시작해야 합니다.  이를 수행하려면 Configuration Manager Service Manager를 사용하여 SMS_Execctuive 서비스의 SMS_DMP_DOWNLOADER 스레드만 다시 시작합니다.  Configuration Manager에 대한 SMS_Executive 서비스를 다시 시작(대부분의 사이트 구성 요소를 다시 시작)하거나, 사이트 백업과 같은 예약 작업(SMS_Executive를 중지했다가 나중에 자동으로 다시 시작함)을 기다릴 수 있습니다.  

Configuration Manager 서비스 관리자를 사용하려면 콘솔에서 **모니터링** > **시스템 상태** > **구성 요소 상태**로 이동하고, **시작**을 클릭한 후 **Configuration Manager Service Manager**를 선택합니다.  Service manager에서 다음을 수행합니다.  

-   탐색 창에서 사이트와 **구성 요소**를 차례로 확장한 후 다시 시작하려는 구성 요소를 선택합니다.  

-   세부 정보 창에서, 구성 요소를 마우스 오른쪽 단추로 클릭하고 **쿼리**를 선택합니다.  

-   구성 요소의 상태를 확인한 후 구성 요소를 마우스 오른쪽 단추로 다시 클릭하고 **중지**를 선택합니다.  

-   구성 요소를 다시 **쿼리**하여 중지되었음을 확인한 후 구성 요소를 마우스 오른쪽 단추로 한 번 더 클릭하고 **시작**을 선택합니다.  

> [!IMPORTANT]  
>  서비스 연결 지점에 Microsoft Intune 구독을 추가하면 사이트 시스템 역할이 자동으로 온라인 상태로 설정됩니다. Intune 구독으로 구성된 경우 서비스 연결 지점에서 오프라인 모드를 지원하지 않습니다.  

**사이트 서버에서 원격 컴퓨터에 역할을 설치하는 경우:**  

-   사이트 시스템 설치 계정을 사용하여 역할을 호스트하는 사이트 시스템 서버를 구성해야 합니다.  

-   사이트 시스템 설치 계정은 사이트 서버의 배포 관리자가 서비스 연결 지점에서 업데이트를 전송하는 데 사용됩니다.  

##  <a name="a-namebkmkurlsa-internet-access-requirements"></a><a name="bkmk_urls"></a> 인터넷 액세스 요구 사항  
작업을 사용하려면 서비스 연결 지점 및 해당 컴퓨터와 인터넷 간의 모든 방화벽을 호스트하는 컴퓨터에서 **포트 TCP 443**을 통해 다음 인터넷 위치로 통신을 전달해야 합니다. 서비스 연결 지점에서도 웹 프록시(인증을 사용하거나 사용하지 않고)를 통해 이러한 위치에 액세스할 수 있습니다.  

**업데이트 및 서비스**  

-   *.akamaiedge.net  

-   *.manage.microsoft.com

-   go.microsoft.com

-   blob.core.windows.net  

-   download.microsoft.com  

-   sccmconnected-a01.cloudapp.net  

**Microsoft Intune**  

-   *.manage.microsoft.com  
-   https://bspmts.mp.microsoft.com/V
-   https://login.microsoftonline.com/{TenantID}


**Windows 10 서비스**  

-   download.microsoft.com  

-   https://go.microsoft.com/fwlink/?LinkID=619849  



<!--HONumber=Nov16_HO1-->

