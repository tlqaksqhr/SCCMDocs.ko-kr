---
title: 클라우드 관리 게이트웨이 설정
titleSuffix: Configuraton Manager
description: CMG(클라우드 관리 게이트웨이)를 설정하기 위해 이 단계별 프로세스를 사용합니다.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: e0ec7d66-1502-4b31-85bb-94996b1bc66f
ms.openlocfilehash: 04c1b262704ec6458bd9773c28c43a50d8fc0840
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="set-up-cloud-management-gateway-for-configuration-manager"></a>Configuration Manager용 클라우드 관리 게이트웨이 설정

*적용 대상: System Center Configuration Manager(현재 분기)*  

이 프로세스에는 CMG(클라우드 관리 게이트웨이)를 설정하는 데 필요한 단계가 포함됩니다. 

> [!Tip]
> 이 기능은 버전 1610에서 [시험판 기능](/sccm/core/servers/manage/pre-release-features)으로 처음 소개되었습니다. 버전 1802 버전부터 이 기능은 더 이상 시험판 기능이 아닙니다.



## <a name="before-you-begin"></a>시작하기 전에

[클라우드 관리 게이트웨이 계획](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway) 아티클을 읽고 시작합니다. 해당 아티클을 사용하여 CMG 디자인을 결정합니다. 

다음 검사 목록을 사용하여 CMG를 만드는 데 필요한 정보 및 필수 구성 요소가 있는지 확인합니다.  

- 사용할 Azure 환경입니다. 예: Azure 공용 클라우드 또는 Azure 미국 정부 클라우드  

- 디자인에 따라 CMG에 하나 이상의 인증서가 필요합니다. 자세한 내용은 [클라우드 관리 게이트웨이에 대한 인증서](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway)를 참조하세요.  

- 1802 버전부터는 **Azure Resource Manager 배포** 또는 **클래식 서비스 배포**를 사용할지 선택합니다. 자세한 내용은 [Azure Resource Manager](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway#azure-resource-manager)를 참조하세요. CMG의 Azure Resource Manager 배포에 다음 요구 사항이 필요합니다.  

    - **클라우드 관리**를 위해 [Azure AD](/sccm/core/servers/deploy/configure/azure-services-wizard)와 통합 Azure AD 사용자 검색은 필요하지 않습니다.  

    - 구독 관리자는 로그온해야 합니다.  

- CMG의 클래식 서비스 배포에 다음 요구 사항이 필요합니다.  

    - Azure 구독 ID  

    - Azure 관리 인증서  

- 서비스에서 전역적으로 고유한 이름입니다. 이 이름은 [CMG 서버 인증 인증서](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#cmg-server-authentication-certificate)에서 비롯됩니다.  

- 이 CMG 배포에 대한 Azure 지역입니다.  

- 규모 및 중복성에 대해 필요한 VM 인스턴스 수입니다.  



## <a name="set-up-a-cmg"></a>CMG 설정

최상위 사이트에서 이 프로시저를 수행합니다. 해당 사이트는 독립 실행형 기본 사이트나 중앙 관리 사이트 중 하나입니다.

1. Configuration Manager 콘솔에서 **관리** 작업 영역으로 이동하고, **Cloud Services**를 확장하고, **클라우드 관리 게이트웨이**를 선택합니다.  

2. 리본에서 **클라우드 관리 게이트웨이 만들기**를 클릭합니다.  

3. 1802 버전부터는 마법사의 일반 페이지에서 먼저 CMG 배포 메서드, **Azure Resource Manager 배포** 또는 **클래식 서비스 배포**를 선택합니다.  

    1. **Azure Resource Manager 배포**에서 **로그인**을 클릭하여 Azure 구독 관리자 계정으로 인증합니다. 마법사가 Azure AD 통합 필수 구성 요소 중에 저장된 정보로 나머지 필드를 자동으로 채웁니다. 여러 구독을 소유하고 있는 경우 사용할 구독의 **구독 ID**를 선택합니다.  

    2. **클래식 서비스 배포**, *Configuration Manager 버전 1706 및 1710*:에서 Azure **구독 ID**를 입력합니다. 그런 다음, **찾아보기**를 클릭하고, Azure 관리 인증서에 대한 PFX 파일을 선택합니다. 

4. 이 CMG에 대한 **Azure 환경**을 지정합니다. 드롭다운 목록에 있는 옵션은 배포 메서드에 따라 달라질 수 있습니다.  

5. **다음**을 클릭합니다. 사이트가 Azure에 대한 연결을 테스트할 때까지 기다립니다.  

4. 마법사의 설정 페이지에서 먼저 **찾아보기**를 클릭하고, CMG 서버 인증 인증서에 대한 .PFX 파일을 선택합니다. 이 인증서의 이름은 필수 **서비스 FQDN** 및 **서비스 이름** 필드를 채웁니다.  

   > [!NOTE]  
   > 1802 버전부터 CMG 서버 인증 인증서는 와일드카드를 지원합니다. 와일드카드 인증서를 사용하는 경우 **서비스 FQDN** 필드의 별표(\*)를 CMG에 원하는 호스트 이름으로 바꿉니다.  
   <!--491233-->  

5. **지역** 드롭다운 목록을 클릭하고 이 CMG에 대한 Azure 지역을 선택합니다.  

6. 1802 버전부터는 Azure Resource Manager 배포를 사용하고 **리소스 그룹** 옵션을 선택합니다. 
   1. **기존 항목 사용**을 선택하는 경우 드롭다운 목록에서 기존 리소스 그룹을 선택합니다.
   2. **새로 만들기**를 선택하면 새 리소스 그룹 이름을 입력합니다.

6. **VM 인스턴스** 필드에서 이 서비스에 대한 VM 수를 입력합니다. 기본값은 1이지만 CMG당 최대 16대의 VM으로 확장할 수 있습니다.  

7. **인증서**를 클릭하여 신뢰할 수 있는 클라이언트 루트 인증서를 추가합니다. 최대 두 개의 신뢰할 수 있는 루트 CA 및 네 개의 중간(하위) CA를 추가합니다.  

8. 마법사는 기본적으로 **클라이언트 인증서 해지를 확인**하는 옵션을 사용합니다. 이 확인이 작동하도록 CRL(인증서 해지 목록)이 공개적으로 게시되어야 합니다. CRL을 게시하지 않는 경우 이 옵션의 선택을 취소합니다.  

9. **다음**을 클릭합니다.  

10. 14일 임계값을 포함한 CMG 트래픽을 모니터링하려면 임계값 경고를 설정하는 확인란을 선택합니다. 그런 다음 임계값을 지정하고 각 경고 수준을 높일 백분율을 지정합니다. 작업을 완료한 후 **다음**을 선택합니다.  

11. 설정을 검토하고 **다음**을 선택합니다. Configuration Manager가 서비스 설정을 시작합니다. 마법사를 닫은 후 Azure에서 서비스를 완전히 프로비전하는 데 5-15분 정도 걸립니다. 새 CMG에 대한 **상태** 열을 통해 서비스가 준비되었는지 확인합니다.  

 > [!Note]  
 > 배포 문제를 해결하려면 **CloudMgr.log** 및 **CMGSetup.log**를 사용합니다. 자세한 내용은 [로그 파일](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)을 참조하세요.



## <a name="configure-primary-site-for-client-certificate-authentication"></a>클라이언트 인증서 인증에 대한 기본 사이트 구성

클라이언트가 CMG를 사용하여 인증하도록 [클라이언트 인증 인증서](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate)를 사용하는 경우 각 기본 사이트를 구성하는 이 프로시저를 수행합니다.  

1. Configuration Manager 콘솔에서 **관리** 작업 영역으로 이동하여 **사이트 구성**을 확장한 다음, **사이트**을 선택합니다.  

2. 인터넷 기반 클라이언트를 할당할 기본 사이트를 선택하고 **속성**을 선택합니다.  

3. 기본 사이트 속성 시트의 **클라이언트 컴퓨터 통신** 탭으로 전환하고, **사용 가능한 경우 PKI 클라이언트 인증서(클라이언트 인증 기능) 사용**을 선택합니다.  

4. CRL을 게시하지 않는 경우 **클라이언트는 사이트 시스템에 대한 CRL(인증서 해지 목록)을 확인합니다.** 라는 옵션의 선택을 취소합니다.  



## <a name="add-the-cmg-connection-point"></a>CMG 연결점 추가

CMG 연결점은 CMG와 통신하기 위한 사이트 시스템 역할입니다. CMG 연결점을 추가하려면 일반 지침에 따라 [사이트 시스템 역할을 설치](/sccm/core/servers/deploy/configure/install-site-system-roles)합니다. 사이트 시스템 역할 추가 마법사의 시스템 역할 선택 페이지에서 **클라우드 관리 게이트웨이 연결점**을 선택합니다. 그런 다음, 이 서버가 연결될 **클라우드 관리 게이트웨이 이름**을 선택합니다. 마법사는 선택한 CMG에 대한 지역을 표시합니다. 

> [!Important]
> 일부 시나리오에서 CMG 연결점에는 [클라이언트 인증 인증서](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#client-authentication-certificate)가 있어야 합니다. 

 > [!Note]  
 > CMG 서비스 상태 문제를 해결하려면 **CMGService.log** 및 **SMS_Cloud_ProxyConnector.log**를 사용합니다. 자세한 내용은 [로그 파일](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)을 참조하세요.



## <a name="configure-client-facing-roles-for-cmg-traffic"></a>CMG 트래픽에 대한 클라이언트 쪽 역할 구성

CMG 트래픽을 허용하도록 관리 지점 및 소프트웨어 업데이트 지점을 구성합니다. 인터넷 기반 클라이언트를 제공하는 모든 관리 지점 및 소프트웨어 업데이트 지점에 대한 기본 사이트에서 이 프로시저를 수행합니다.  

1. Configuration Manager 콘솔에서는 **관리** 작업 영역으로 이동하고, **사이트 구성**을 확장하고, **서버 및 사이트 시스템 역할**을 마우스 오른쪽 단추로 클릭하고, 목록에서 **관리 지점**을 선택합니다.  

2. CMG 트래픽에 대해 구성하려는 사이트 시스템 서버를 선택합니다. 세부 정보 창에서 **관리 지점** 역할을 선택한 다음, 리본 메뉴에서 **속성**을 클릭합니다.  

3. 관리 지점 속성 시트의 클라이언트 연결에서 **Configuration Manager 클라우드 관리 게이트웨이 트래픽 허용** 옆의 확인란을 선택합니다. 
    - CMG 디자인 및 Configuration Manager 버전에 따라 **HTTPS** 옵션을 사용하도록 설정해야 할 수 있습니다. 자세한 내용은 [HTTPS에 대한 관리 지점 설정](/sccm/core/clients/manage/cmg/certificates-for-cloud-management-gateway#enable-management-point-for-https)을 참조하세요.  

4. **확인**을 클릭합니다.   

필요에 따라 추가 관리 지점 및 소프트웨어 업데이트 지점에 대해 이러한 단계를 반복합니다. 



## <a name="configure-clients-for-cmg"></a>CMG에 대한 클라이언트 구성

CMG 및 사이트 시스템 역할을 실행하면 클라이언트는 다음 위치 요청에 대한 CMG 서비스의 위치를 자동으로 가져옵니다. [인증을 위해 Azure AD를 사용하여 Windows 10 클라이언트를 설치하고 할당](/sccm/core/clients/deploy/deploy-clients-cmg-azure)하지 않으면 클라이언트는 CMG 서비스의 위치를 수신하기 위해 인트라넷에 비치되어야 합니다. 위치 요청에 대한 폴링 주기는 매 24시간입니다. 정상적으로 예약된 위치 요청을 기다리고 싶지 않으면 컴퓨터에서 SMS 에이전트 호스트 서비스(ccmexec.exe)를 다시 시작하여 요청을 강제로 실시할 수 있습니다.  

> [!Note]
> 기본적으로 모든 클라이언트가 CMG 정책을 수신합니다. 클라이언트 설정 [클라이언트에서 클라우드 관리 게이트웨이를 사용하도록 설정](/sccm/core/clients/deploy/about-client-settings#enable-clients-to-use-a-cloud-management-gateway)을 사용하여 이 동작을 컨트롤합니다.

Configuration Manager 클라이언트는 인트라넷 또는 인터넷에 배치할지를 자동으로 결정합니다. 클라이언트가 도메인 컨트롤러 또는 온-프레미스 관리 지점에 연결할 수 있는 경우 해당 연결 형식을 **현재 인트라넷**으로 설정합니다. 그렇지 않으면, **현재 인터넷**로 전환하고 CMG 서비스의 위치를 사용하여 사이트와 통신합니다.

>[!NOTE]
> 인트라넷 또는 인터넷에 있는지와 관계없이 클라이언트가 항상 CMG를 사용하도록 강제할 수 있습니다. 이 구성은 테스트 목적 또는 CMG를 적용하려는 원격 사무실의 클라이언트에 유용합니다. 클라이언트에 다음과 같은 레지스트리 키를 설정합니다.
>
> `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\CCM\Security, ClientAlwaysOnInternet = 1`
>
> [CCMALWAYSINF](/sccm/core/clients/deploy/about-client-installation-properties#ccmalwaysinf) 속성을 사용하여 클라이언트 설치 중에 이 설정을 지정할 수도 있습니다.

클라이언트에 CMG를 지정하는 정책이 있는지를 확인하려면 클라이언트 컴퓨터에서 관리자 권한으로 Windows PowerShell 명령 프롬프트를 열고 `Get-WmiObject -Namespace Root\Ccm\LocationServices -Class SMS_ActiveMPCandidate | Where-Object {$_.Type -eq "Internet"}` 명령을 실행합니다.

이 명령은 클라이언트가 알고 있는 인터넷 기반 관리 지점을 모두 표시합니다. CMG가 기술적으로 인터넷 기반 관리 지점이 아닌 반면 클라이언트에는 그렇게 나타납니다.

 > [!Note]  
 > CMG 클라이언트 트래픽 문제를 해결하려면 **CMGHttpHandler.log**, **CMGService.log** 및 **SMS_Cloud_ProxyConnector.log**를 사용합니다. 자세한 내용은 [로그 파일](/sccm/core/plan-design/hierarchy/log-files#cloud-management-gateway)을 참조하세요.



## <a name="modify-a-cmg"></a>CMG 수정

CMG를 만든 후에 일부 설정을 수정할 수 있습니다. Configuration Manager 콘솔에서 CMG를 선택하고 **속성**을 클릭합니다. 다음 설정을 구성할 수 있습니다.  

- **일반**  

    - **Azure 관리 인증서**: CMG에 대한 Azure 관리 인증서를 변경합니다. 이 옵션은 인증서가 만료되기 전에 업데이트할 때 유용합니다.  

- **설정**  

    - **인증서 파일**: CMG에 대한 서버 인증 인증서를 변경합니다. 이 옵션은 인증서가 만료되기 전에 업데이트할 때 유용합니다.  

    - **VM 인스턴스**: Azure에서 서비스가 사용하는 가상 머신의 수를 변경합니다. 이 설정을 사용하면 사용률 또는 비용에 따라 서비스를 동적으로 확장하거나 축소할 수 있습니다.  

    - **인증서**: 신뢰할 수 있는 루트 또는 중간 CA 인증서를 추가하거나 제거합니다. 새 CA를 추가하거나 만료된 인증서의 사용을 중지하는 경우 이 옵션이 유용합니다.  

    - **클라이언트 인증서 해지 확인**: CMG를 만들 때 원래 이 설정을 사용하지 않은 경우 나중에 CRL을 게시하고 나서 사용할 수 있습니다.  

- **경고**: CMG를 만든 후에 언제든지 경고를 구성할 수 있습니다. 

다음 구성 등의 보다 중요한 변경 내용은 서비스를 다시 배포해야 합니다.
- 클래식 배포 메서드에서 Azure Resource Manager
- 구독
- 서비스 이름
- 개인에서 공개 PKI
- 지역

업데이트된 정책을 수신하기 위해 인터넷 기반 클라이언트에서 적어도 하나의 CMG를 활성으로 유지합니다. 인터넷 기반 클라이언트는 제거된 CMG와 통신할 수 없습니다. 클라이언트가 인트라넷으로 다시 로밍될 때까지 새로운 항목을 사용할 수 없습니다. 첫 번째 CMG 인스턴스를 삭제하기 위해 두 번째 CMG 인스턴스를 만들 때 다른 CMG 연결점을 만듭니다.

클라이언트는 기본적으로 24시간마다 정책을 새로 고치므로 이전 CMG를 삭제하기 전에 새 CMG를 만들고 나서 적어도 하루를 기다립니다. 클라이언트가 꺼지거나 인터넷이 연결되지 않은 경우 더 많이 대기해야 합니다. 

1802 버전부터는 클래식 배포 메서드에서 기존 CMG가 설치되어 있다면 새 CMG를 배포하여 Azure Resource Manager 배포 메서드를 사용해야 합니다.<!--509753--> 두 가지 옵션 중에서 선택할 수 있습니다.
- 동일한 서비스 이름을 다시 사용하려면:
    1. 인터넷 기반 클라이언트에 항상 하나 이상의 활성 CMG가 있어야 한다는 지침을 고려하여 먼저 클래식 CMG를 삭제합니다.
    2. Resource Manager 배포를 사용하여 새 CMG를 만듭니다. 동일한 서버 인증 인증서를 다시 사용합니다.
    3. 새 CMG 인스턴스를 사용하도록 CMG 연결점을 다시 구성합니다.
- 새로운 서비스 이름을 사용하려면:
    1. Resource Manager 배포를 사용하여 새 CMG를 만듭니다. 새로운 서버 인증 인증서를 사용합니다.
    2. 새 CMG 연결점을 만들고 새 CMG와 연결합니다.
    3. 새 CMG에 대한 정책을 수신하도록 인터넷 기반 클라이언트에 대해 적어도 하루를 기다립니다.
    4. 클래식 CMG를 삭제합니다.

Configuration Manager 콘솔에서만 CMG를 수정합니다. Azure에서 직접 서비스 또는 기본 VM을 수정하도록 지원하지 않습니다. 변경 내용은 통지 없이 손실될 수 있습니다. PaaS와 마찬가지로 서비스는 언제든지 VM을 다시 빌드할 수 있습니다. 이러한 다시 빌드는 백 엔드 하드웨어 유지 관리하거나 업데이트 VM OS를 적용하기 위해 발생할 수 있습니다.

CMG를 삭제해야 하는 경우 Configuration Manager 콘솔에서도 수행할 수 있습니다. Azure의 모든 구성 요소를 수동으로 제거하면 시스템에 불일치가 발생할 수 있습니다. 이 상태는 분리된 정보를 남기고, 예기치 않은 동작이 발생할 수 있습니다. 



## <a name="next-steps"></a>다음 단계

- [클라이언트에서 클라우드 관리 게이트웨이 모니터링](/sccm/core/clients/manage/cmg/monitor-clients-cloud-management-gateway)
- [클라우드 관리 게이트웨이에 대한 FAQ](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
