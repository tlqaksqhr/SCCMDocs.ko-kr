---
title: Azure AD를 사용하여 클라이언트 설치
titleSuffix: Configuration Manager
description: 인증을 위해 Azure Active Directory를 사용하여 Windows 10 장치에서 Configuration Manager 클라이언트 설치 및 할당
ms.date: 03/28/2018
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.topic: conceptual
ms.assetid: a44006eb-8650-49f6-94e1-18fa0ca959ee
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: 91ebb0c35687b231a6f08b7bc92cccb83cf0e602
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="install-and-assign-configuration-manager-windows-10-clients-using-azure-ad-for-authentication"></a>인증을 위해 Azure AD를 사용하여 Configuration Manager Windows 10 클라이언트 설치 및 할당

Azure AD 인증을 사용하여 Windows 10 장치에서 Configuration Manager 클라이언트를 설치하려면 Azure AD(Azure Active Directory)와 Configuration Manager를 통합합니다. 클라이언트는 HTTPS 기반 관리 지점과 직접 통신하는 인트라넷에 있을 수 있습니다. 또한 클라이언트는 CMG을 통해 또는 인터넷 기반 관리 지점과 통신하는 인터넷 기반일 수 있습니다. 이 프로세스는 Azure AD를 사용하여 Configuration Manager 사이트에 클라이언트를 인증합니다. Azure AD를 사용하면 클라이언트 인증 인증서를 구성하고 사용할 필요가 없습니다.



## <a name="before-you-begin"></a>시작하기 전에

- Azure AD 테넌트는 필수 구성 요소  

- 장치 요구 사항  

    - Windows 10  

    - 순수 클라우드 도메인 연결이든 하이브리드 Azure AD 연결이든 Azure AD에 연결  

- 사용자 요구 사항  

    - 로그온한 사용자는 Azure AD ID이어야 합니다.   

    - 사용자가 페더레이션되거나 동기화된 ID인 경우 Configuration Manager [Active Directory 사용자 겸색](/sccm/core/servers/deploy/configure/about-discovery-methods#bkmk_aboutUser) 및 [Azure AD 사용자 검색](/sccm/core/servers/deploy/configure/about-discovery-methods#azureaddisc)을 사용해야 합니다. 하이브리드 ID에 대한 자세한 내용은 [하이브리드 ID 채택 전략 정의](/azure/active-directory/active-directory-hybrid-identity-design-considerations-identity-adoption-strategy)를 참조합니다.<!--497750-->  

- 관리 지점 사이트 시스템 역할에 대한 [기존 필수 구성 요소](/sccm/core/plan-design/configs/site-and-site-system-prerequisites#bkmk_2012MPpreq) 외에 이 서버에 **ASP.NET 4.5**도 사용하도록 설정합니다. ASP.NET 4.5를 사용하도록 설정할 경우 자동으로 선택된 다른 모든 옵션을 포함합니다.  

- HTTPS 모드에 대한 모든 관리 지점을 구성합니다. 자세한 내용은 [PKI 인증 요구 사항](/sccm/core/plan-design/network/pki-certificate-requirements) 및 [IIS를 실행하는 사이트 시스템용 웹 서버 인증서 배포](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)를 참조하세요.  
    - 클라우드 관리 게이트웨이를 사용하는 경우 클라우드 관리 게이트웨이에 대해 사용하도록 설정한 관리 지점에 대해서만 HTTPS를 구성해야 합니다.
    - Azure AD 토큰 기반 인증을 사용하여 인트라넷에 클라이언트를 배포하는 경우 이러한 클라이언트가 연결할 수 있는 모든 관리 지점에서 HTTPS를 사용하도록 설정해야 합니다. 

- 인터넷 기반 클라이언트를 배포하려면 필요에 따라 [클라우드 관리 게이트웨이](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)(CMG)를 설정합니다. Azure AD로 인증하는 온-프레미스 클라이언트의 경우 CMG는 필요 없습니다.  


## <a name="configure-azure-services-for-cloud-management"></a>클라우드 관리를 위한 Azure 서비스 구성

첫 단계로 Configuration Manager 사이트를 Azure AD에 연결합니다. 이 프로세스의 세부 내용에 대해서는 [Azure 서비스 구성](/sccm/core/servers/deploy/configure/azure-services-wizard)을 참조합니다. **클라우드 관리** 서비스에 연결을 만듭니다.

[Azure AD 사용자 검색](/sccm/core/servers/deploy/configure/configure-discovery-methods#azureaadisc)을 **클라우드 관리**에 대한 온보딩의 일부로서 사용하도록 설정합니다. 

이 작업을 완료하면 Configuration Manager 사이트가 Azure AD에 연결됩니다. 



## <a name="configure-client-settings"></a>클라이언트 설정 구성

이러한 클라이언트 설정은 Azure AD를 사용하여 Windows 10 장치에 연결하도록 지원합니다. 또한 CMG 및 클라우드 배포 지점을 사용하려면 인터넷 기반 클라이언트를 사용하도록 설정할 수 있습니다.

1.  [클라이언트 설정 구성 방법](/sccm/core/clients/deploy/configure-client-settings)의 정보를 사용하여 **Cloud Services** 섹션에서 다음 클라이언트 설정을 구성합니다.  

    - **클라우드 배포 지점에 대한 액세스 허용**: 인터넷 기반 장치를 활용하는 이 설정을 사용하여 Configuration Manager 클라이언트를 설치하기 위해 필요한 콘텐츠를 가져옵니다. 콘텐츠가 클라우드 배포 지점에서 사용할 수 없는 경우 장치는 CMG에서 콘텐츠를 검색할 수 있습니다. 클라이언트 설치 부트스트랩은 CMG로 되돌아가기 전에 4시간 동안 클라우드 배포 지점을 다시 시도합니다.<!--495533-->  

    - **Azure Active Directory에 새 Windows 10 도메인에 연결된 장치를 자동으로 등록**: **예** 또는 **아니요**로 설정합니다. 기본 설정은 **예**입니다. 이 동작은 Windows 10 버전 1709에서 기본값이기도 합니다.

    - **클라이언트가 클라우드 관리 게이트웨이를 사용하도록 설정** – **예**(기본값) 또는 **아니요**로 설정합니다.  

2.  필요한 장치 컬렉션에 클라이언트 설정을 배포합니다. 이러한 설정을 사용자 컬렉션에 배포하지 않습니다.

장치가 Azure AD에 연결됐는지 확인하려면 명령 프롬프트에서 `dsregcmd.exe /status`을 실행합니다. 결과의 **AzureAdjoined** 필드는 장치가 Azure AD에 연결된 경우 **예**를 표시합니다.



## <a name="install-and-register-the-client-using-azure-ad-identity"></a>Azure AD ID를 사용하여 클라이언트 설치 및 등록

Azure AD ID를 사용하여 클라이언트를 수동으로 설치하려면 먼저 [클라이언트를 수동으로 설치하는 방법](/sccm/core/clients/deploy/deploy-clients-to-windows-computers#BKMK_Manual)에 관한 일반 프로세스를 검토합니다. 

 > [!Note]  
 > 장치는 Azure AD와 연결하려면 인터넷에 액세스해야 하지만 인터넷 기반일 필요는 없습니다. 

다음 예제에서는 `ccmsetup.exe /mp:<source management point> CCMHOSTNAME=<internet-based management point> SMSSiteCode=<site code> SMSMP=<initial management point> AADTENANTID=<Azure AD tenant identifier> AADCLIENTAPPID=<Azure AD client app identifier> AADRESOURCEURI=<Azure AD server app identifier>`와 같은 명령줄의 일반 구조를 보여줍니다.

자세한 내용은 [클라이언트 설치 속성](/sccm/core/clients/deploy/about-client-installation-properties)을 참조합니다.

/Mp 및 CCMHOSTNAME 속성은 시나리오에 따라 다음 중 하나를 지정합니다.
- 온-프레미스 관리 지점입니다. /mp 속성만 지정합니다. CCMHOSTNAME는 필요하지 않습니다.
- 클라우드 관리 게이트웨이
- 인터넷 기반 관리 지점, SMSMP 속성은 온-프레미스 또는 인터넷 기반 관리 지점 중 하나를 지정합니다.

이 예제는 클라우드 관리 게이트웨이를 사용합니다. 각 속성에 대한 예제 값을 대체합니다. `ccmsetup.exe /mp:https://CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 CCMHOSTNAME=CONTOSO.CLOUDAPP.NET/CCM_Proxy_MutualAuth/72186325152220500 SMSSiteCode=ABC SMSMP=https://mp1.contoso.com AADTENANTID=daf4a1c2-3a0c-401b-966f-0b855d3abd1a AADCLIENTAPPID=7506ee10-f7ec-415a-b415-cd3d58790d97 AADRESOURCEURI=https://contososerver`

Microsoft Intune을 통해 Azure AD ID를 사용하여 클라이언트 설치를 자동화하려면 [공동 관리를 위해 Windows 10 장치 준비](/sccm/core/clients/manage/co-management-prepare#command-line-to-install-configuration-manager-client) 프로세스를 참조합니다.



## <a name="next-steps"></a>다음 단계

완료되면 [클라이언트를 계속 모니터링 및 관리](/sccm/core/clients/manage/monitor-clients)할 수 있습니다.
