---
title: "System Center Configuration Manager에 대한 장치 관리 솔루션 선택"
description: "System Center Configuration Manager에서 PC, 서버 및 장치 관리를 위해 제공하는 솔루션에 대해 알아봅니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-client
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 24633725-791a-4df7-8dce-2c24c1a19a03
caps.latest.revision: 14
caps.handback.revision: 0
author: Mtillman
ms.author: mtillman
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: b64135826dd49c594167999aebd322fa3ed61345


---
# <a name="choose-a-device-management-solution-for-system-center-configuration-manager"></a>System Center Configuration Manager에 대한 장치 관리 솔루션 선택

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager에서는 PC, 서버 및 장치를 관리하기 위한 다양한 솔루션을 제공합니다. 관리해야 하는 장치 플랫폼 및 필요한 관리 기능에 따라 적합한 솔루션을 선택할 수 있습니다.  


##  <a name="a-namebkmkoverviewa-overview-of-device-management-solutions"></a><a name="bkmk_overview"></a> 장치 관리 솔루션의 개요  
 다음 옵션은 Configuration Manager에서 컴퓨터 및 장치를 관리하는 데 사용할 수 있습니다.  

-   **Configuration Manager 클라이언트를 사용하여 장치 관리**  

     관리할 각 장치에 Configuration Manager 클라이언트 응용 프로그램을 설치해야 하는 이 옵션은 PC, 서버 및 사용자 환경의 기타 장치를 관리하기 위한 기능을 가장 많이 제공합니다. 이 옵션은 제품 출시 이후 Configuration Manager에서 장치 관리를 제공한 기존 방법입니다.  

     이 솔루션에 대한 자세한 내용은 [System Center Configuration Manager의 클라이언트 설치 방법](/sccm/core/client/deploy/plan/client-installation-methods)을 참조하세요.  

-   **온-프레미스 Configuration Manager 인프라를 사용하여 모바일 장치 관리**  

     이 옵션은 특정 장치 플랫폼의 운영 체제에 기본 제공되는 장치 관리 기능을 사용합니다. 클라이언트 기반 관리만큼 전체 기능을 갖추고 있지는 않지만 온\-프레미스 모바일 장치 관리는 온-프레미스 Configuration Manager 리소스를 사용하여 장치에 연결하고 관리하는 보다 가벼운 관리 방식을 제공합니다. 온\-프레미스 모바일 장치 관리는 현재 Windows 10 PC 및 Windows 10 Mobile 장치에 대해서만 지원됩니다.  

     이 솔루션에 대한 자세한 내용은 [System Center Configuration Manager의 온-프레미스 인프라로 모바일 장치 관리](../../mdm/understand/manage-mobile-devices-with-on-premises-infrastructure.md)를 참조하세요.  

-   **Microsoft Intune을 사용하여 모바일 장치 관리(하이브리드)**  

     이 옵션을 하이브리드 모바일 장치 관리라고 합니다.  Configuration Manager 온-프레미스 리소스를 사용하는 대신 Microsoft Intune을 사용하여 장치를 등록하고 관리합니다. Intune에서 장치를 관리하지만 Configuration Manager 콘솔에서 관리 작업을 제어할 수 있습니다. 이 옵션은 Windows 10 Mobile, Windows Phone, iOS, Android 등 모든 주요 모바일 장치 운영 체제를 지원합니다. 또한 조직의 Windows 8.1 및 Windows 10 컴퓨터를 관리하는 기능을 제공합니다.  

     이 솔루션에 대한 자세한 내용은 [System Center Configuration Manager 및 Microsoft Intune을 사용하는 하이브리드 MDM(모바일 장치 관리)](../../mdm/plan-design/hybrid-mobile-device-management.md)을 참조하세요.  

-   **Exchange를 사용하여 모바일 장치 관리**  

     Exchange Server 커넥터를 통해 여러 Exchange 서버를 Configuration Manager에 연결하는 이 옵션을 사용하면 Exchange ActiveSync에 연결할 수 있는 장치를 중앙에서 관리할 수 있습니다. Configuration Manager 콘솔에서 여러 Exchange 서버에 대한 설정 제어 및 원격 장치 초기화와 같은 Exchange 모바일 장치 관리 기능을 구성할 수 있습니다.  

     이 솔루션에 대한 자세한 내용은 [System Center Configuration Manager와 Exchange를 사용하여 모바일 장치 관리](../../mdm/deploy-use/manage-mobile-devices-with-exchange-activesync.md)를 참조하세요.  

 이러한 장치 관리 솔루션을 단독으로 사용하거나 서로 결합해서 사용할 수 있습니다. 예를 들어 클라이언트 기반 관리 방식을 사용하여 조직의 컴퓨터 및 서버를 관리하고 Intune 기반 관리를 사용하여 모바일 장치를 관리할 수 있습니다. 이러한 방식으로 결합하면 모든 장치 관리 요구를 처리하고 Configuration Manager 콘솔에서 모두 제어할 수 있습니다.  

##  <a name="a-namebkmkcomp1a-compare-device-management-solutions-based-on-supported-mobile-device-platforms"></a><a name="bkmk_comp1"></a> 지원되는 모바일 장치 플랫폼을 기준으로 장치 관리 솔루션 비교  

|플랫폼|Configuration Manager 클라이언트 사용|Configuration Manager 통합 Microsoft Intune(하이브리드)|온\-프레미스 모바일 장치 관리|Configuration Manager와 Exchange|  
|--------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|Android||예||예|  
|iOS||예||예|  
|Mac OS X|예|||예|  
|UNIX/Linux|예|||예|  
|Windows 10|예|예|예|예|  
|Windows 10 Mobile||예|예|예|  
|Windows(이전 버전)|예|예||예|  
|Windows CE|예(모바일 장치 레거시 클라이언트 사용)|||예|  
|Windows Embedded|예||||  
|Windows Phone||예||예|  
|Windows Server|예|||예|  

 지원되는 플랫폼의 전체 목록은 [Supported operating systems for clients and devices for System Center Configuration Manager](configs\supported-operating-systems-for-clients-and-devices.md)(System Center Configuration Manager용 클라이언트 및 장치에 대해 지원되는 운영 체제)를 참조하세요.

##  <a name="a-namebkmkcomp2a-compare-mobile-device-management-solutions-based-on-management-functionality"></a><a name="bkmk_comp2"></a> 관리 기능을 기준으로 모바일 장치 관리 솔루션 비교  

|관리 기능|Configuration Manager 클라이언트 사용|Configuration Manager 통합 Microsoft Intune(하이브리드)|온\-프레미스 모바일 장치 관리|Configuration Manager와 Exchange|  
|------------------------------|-------------------------------------------|-------------------------------------------------------------------|-------------------------------|-----------------------------------------|  
|상호 인증과 SSL을 통한 데이터 전송 암호화를 사용한 모바일 장치와 Configuration Manager 간의 PKI(공개 키 인프라)|예|예|예||  
|클라이언트 설치|예||||  
|인터넷을 통한 지원|예||||  
|검색|예|||예|  
|하드웨어 인벤토리|예|예|예|예|  
|소프트웨어 인벤토리|예|||예|  
|설정|예|예|예|예|  
|소프트웨어 배포|예|예|예||  
|대체 상태 지점을 사용한 모니터링|예||||  
|관리 지점에 대한 연결|예||예||  
|배포 지점에 대한 연결|예|예|예||  
|Configuration Manager의 블록|예|예|예||  
|Exchange Server(및 Configuration Manager)에서 격리 및 차단||||예|  
|원격 지우기|예|예|예|예|  



<!--HONumber=Nov16_HO1-->

