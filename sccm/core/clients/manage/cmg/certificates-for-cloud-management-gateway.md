---
title: CMG 인증서
description: 클라우드 관리 게이트웨이와 함께 사용할 다양한 디지털 인증서에 대해 알아봅니다.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 71eaa409-b955-45d6-8309-26bf3b3b0911
ms.openlocfilehash: e62b748596aba1404d6b097e5aa0bf74266f055b
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="certificates-for-the-cloud-management-gateway"></a>클라우드 관리 게이트웨이에 대한 인증서

*적용 대상: System Center Configuration Manager(현재 분기)*

CMG(클라우드 관리 게이트웨이)를 사용하여 인터넷에서 클라이언트를 관리하는 데 사용하는 시나리오에 따라 하나 이상의 디지털 인증서가 필요합니다. 다양한 시나리오에 대한 자세한 내용은 [클라우드 관리 게이트웨이에 대한 계획](/sccm/core/clients/manage/cmg/plan-cloud-management-gateway)을 참조하세요.


## <a name="cmg-server-authentication-certificate"></a>CMG 서버 인증 인증서

*이 인증서는 모든 시나리오에서 필요합니다.*

Configuration Manager 콘솔에서 CMG를 만들 때 이 인증서를 제공합니다.

CMG는 인터넷 기반 클라이언트에서 연결하는 HTTPS 서비스를 만듭니다. 서버에서 보안 채널을 구축하려면 서버 인증 인증서가 필요합니다. 이 목적을 위해 인증서를 공용 공급자로부터 구입하거나 PKI(공개 키 인프라)에서 발급합니다. 자세한 내용은 [클라이언트에서 신뢰할 수 있는 CMG 루트 인증서](#cmg-trusted-root-certificate-to-clients)를 참조하세요.

 > [!TIP]
 > 이 인증서에는 Azure에서 서비스를 식별하기 위해 전역적으로 고유한 이름을 필요합니다. 인증서를 요청하기 전에 원하는 Azure 도메인 이름이 고유한지 확인합니다. 예를 들어 *GraniteFalls.CloudApp.Net*과 같습니다. [Microsoft Azure Portal](https://portal.azure.com)에 로그온합니다. **리소스 만들기**를 클릭하고, **계산** 범주를 선택한 다음, **클라우드 서비스**를 클릭합니다. **DNS 이름** 필드에서 원하는 접두사를 입력합니다(예: *GraniteFalls*). 인터페이스에는 도메인 이름을 사용할 수 있는지, 아니면 다른 서비스에서 이미 사용 중인지 여부가 표시됩니다. 포털에서 서비스를 만들지 말고, 이 프로세스를 사용하여 이름 가용성을 확인하세요. 
  
 > [!NOTE]
 > 1802 버전부터 CMG 서버 인증 인증서는 와일드카드를 지원합니다. 일부 인증 기관은 호스트 이름에 와일드카드 문자를 사용하는 인증서를 발행합니다. 예를 들어 **\*.contoso.com**과 같습니다. 일부 조직에서는 PKI를 간소화하고 유지 관리 비용을 절약하기 위해 와일드카드 인증서를 사용합니다.
 <!--491233-->


### <a name="cmg-trusted-root-certificate-to-clients"></a>클라이언트에서 신뢰할 수 있는 CMG 루트 인증서

클라이언트는 CMG 서버 인증 인증서를 신뢰해야 합니다. 이 신뢰를 수행하는 데는 두 가지 방법이 있습니다.
- 공용 및 전역 신뢰할 수 있는 인증서 공급자의 인증서를 사용합니다. 예를 들어 VeriSign 또는 Thawte가 있지만, 이에 국한되지는 않습니다. Windows 클라이언트에는 이러한 공급자의 신뢰할 수 있는 루트 CA(인증 기관)가 포함됩니다. 이러한 공급자 중 하나에서 발급된 서버 인증 인증서를 사용하면 클라이언트에서 이 인증서를 자동으로 신뢰합니다. 
- PKI(공개 키 인프라)의 엔터프라이즈 CA에서 발급한 인증서를 사용합니다. 대부분의 엔터프라이즈 PKI 구현에서는 신뢰할 수 있는 루트 CA를 Windows 클라이언트에 추가합니다. 예를 들어 그룹 정책과 함께 Active Directory 인증서 서비스를 사용합니다. 클라이언트에서 자동으로 신뢰하지 않는 CA에서 CMG 서버 인증 인증서를 발급하는 경우 신뢰할 수 있는 루트 CA 인증서를 인터넷 기반 클라이언트에 추가해야 합니다.
    - Configuration Manager 인증서 프로필을 사용하여 클라이언트에 인증서를 프로비전할 수도 있습니다. 자세한 내용은 [인증서 프로필 소개](/sccm/protect/deploy-use/introduction-to-certificate-profiles)를 참조하세요.

### <a name="server-authentication-certificate-issued-by-public-provider"></a>공용 공급자가 발급한 서버 인증 인증서

이 방법을 사용하는 경우 클라이언트에서 인증서를 자동으로 신뢰하므로 사용자 지정 인증서를 직접 만들 필요가 없습니다. Configuration Manager는 cloudapp.net 도메인을 사용하여 Azure에 서비스를 만듭니다. 공용 인증서 공급자는 이 이름의 인증서를 발급할 수 없습니다. 다음 프로세스를 사용하여 DNS 별칭을 만듭니다.

1. 조직의 공용 DNS에 CNAME(정식 이름) 레코드를 만듭니다. 이 레코드는 CMG에 대한 별칭을 공용 인증서에서 사용하는 친숙한 이름으로 만듭니다.
예를 들어 Contoso는 Azure에서 **GraniteFalls.CloudApp.Net**이 되는 **GraniteFalls**라는 CMG 이름을 지정합니다. Contoso의 공용 DNS contoso.com 네임스페이스에서 DNS 관리자는 실제 호스트 이름인 **GraniteFalls.CloudApp.net**에 대해 **GraniteFalls.Contoso.com**이라는 새 CNAME 레코드를 만듭니다.
2. CNAME 별칭의 CN(일반 이름)을 사용하여 공용 공급자의 서버 인증 인증서를 요청합니다.
예를 들어 Contoso는 인증서 CN에 **GraniteFalls.Contoso.com**을 사용합니다.
3. 이 인증서를 사용하여 Configuration Manager 콘솔에서 CMG를 만듭니다. 클라우드 관리 게이트웨이 만들기 마법사의 **설정** 페이지에서 다음을 수행합니다. 
    - **인증서 파일**에서 이 클라우드 서비스에 대한 서버 인증서를 추가하면, 마법사에서 인증서 CN의 호스트 이름을 서비스 이름으로 추출합니다. 
    - 그런 다음, Azure에 서비스를 만들기 위해 해당 호스트 이름을 서비스 FQDN으로 **cloudapp.net** 또는 **usgovcloudapp.net**(Azure US Government 클라우드)에 추가합니다.
    - 예를 들어 Contoso에서 CMG를 만들면 Configuration Manager는 인증서 CN에서 **GraniteFalls** 호스트 이름을 추출합니다. Azure는 실제 서비스를 **GraniteFalls.CloudApp.net**으로 만듭니다.

### <a name="server-authentication-certificate-issued-from-enterprise-pki"></a>엔터프라이즈 PKI에서 발급한 서버 인증 인증서

클라우드 배포 지점과 마찬가지로 CMG에 대한 사용자 지정 SSL 인증서를 만듭니다. [클라우드 기반 배포 지점용 서비스 인증서 배포](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_clouddp2008_cm2012)에 대한 지침을 따르는 대신, 다음 작업은 다르게 수행하세요.

- 사용자 지정 웹 서버 인증서를 요청할 때 인증서의 일반 이름에 대해 FQDN을 제공합니다. Azure 공용 클라우드에서 CMG를 사용하려면 **cloudapp.net** 또는 **usgovcloudapp.net**(Azure US Government 클라우드)으로 끝나는 이름을 사용합니다.



## <a name="azure-management-certificate"></a>Azure 관리 인증서

*이 인증서는 클래식 서비스 배포에 필요하지만, Azure Resource Manager 배포에는 필요하지 않습니다.*

이 인증서는 Azure Portal 또는 Configuration Manager 콘솔에서 CMG를 만들 때 제공합니다.

Azure에서 CMG를 만들려면 먼저 Configuration Manager 서비스 연결 지점에서 Azure 구독을 인증해야 합니다. 클래식 서비스 배포를 사용하는 경우 이 인증에 Azure 관리 인증서를 사용합니다. Azure 관리자가 이 인증서를 구독에 업로드합니다. Configuration Manager 콘솔에서 CMG를 만들 때 이 인증서를 제공합니다.

관리 인증서를 업로드하는 방법에 대한 자세한 내용 및 지침은 Azure 설명서에서 다음 문서를 참조하세요.

- [클라우드 서비스 및 관리 인증서](/azure/cloud-services/cloud-services-certs-create#what-are-management-certificates)

- [Azure 서비스 관리 인증서 업로드](/azure/azure-api-management-certs)

> [!IMPORTANT]
> 관리 인증서와 연결된 구독 ID를 복사해야 합니다. 이는 Configuration Manager 콘솔에서 CMG를 만드는 데 사용합니다.



## <a name="client-authentication-certificate"></a>클라이언트 인증 인증서

*이 인증서는 Azure AD(Azure Active Directory)에 가입하지 않은 Windows 7, Windows 8.1 및 Windows 10 장치를 실행하는 인터넷 기반 클라이언트에 필요합니다. CMG 연결 지점에도 필요합니다. Azure AD에 가입한 Windows 10 클라이언트에는 필요하지 않습니다.*

클라이언트는 이 인증서를 사용하여 CMG를 인증합니다. 하이브리드 또는 클라우드 도메인에 가입한 Windows 10 장치는 Azure AD를 사용하여 인증하므로 이 인증서가 필요하지 않습니다.

Configuration Manager의 컨텍스트 외부에서 이 인증서를 제공합니다. 예를 들어 Active Directory 인증서 서비스 및 그룹 정책을 사용하여 클라이언트 인증 인증서를 발급합니다. 자세한 내용은 [Windows 컴퓨터용 클라이언트 인증서 배포](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_client2008_cm2012)를 참조하세요.


### <a name="client-trusted-root-certificate-to-cmg"></a>CMG에서 신뢰할 수 있는 클라이언트 루트 인증서

*이 인증서는 클라이언트 인증 인증서를 사용할 때 필요합니다. 모든 클라이언트에서 Azure AD를 인증에 사용하는 경우 이 인증서는 필요하지 않습니다.* 

Configuration Manager 콘솔에서 CMG를 만들 때 이 인증서를 제공합니다.

CMG는 클라이언트 인증 인증서를 신뢰해야 합니다. 이 신뢰를 수행하려면 신뢰할 수 있는 루트 인증서 체인을 제공합니다. 두 개의 신뢰할 수 있는 루트 CA 및 네 개의 중간(하위) CA를 지정할 수 있습니다. 


#### <a name="export-the-client-certificates-trusted-root"></a>클라이언트 인증서의 신뢰할 수 있는 루트 내보내기

컴퓨터에 클라이언트 인증 인증서를 발급한 후 해당 컴퓨터에서 이 프로세스를 사용하여 신뢰할 수 있는 루트를 내보냅니다.

1.  [시작] 메뉴를 엽니다. "run"을 입력하여 [실행] 창을 엽니다. **mmc**를 엽니다. 

2.  [파일] 메뉴에서 **스냅인 추가/제거**를 선택합니다.

3.  [스냅인 추가/제거] 대화 상자에서 **인증서**를 선택한 다음, **추가**를 클릭합니다. 
    a. [인증서 스냅인] 대화 상자에서 **컴퓨터 계정**을 선택한 다음, **다음**을 클릭합니다. 
    b. [컴퓨터 선택] 대화 상자에서 **로컬 컴퓨터**를 선택한 다음, **마침**을 클릭합니다. 
    c. [스냅인 추가/제거] 대화 상자에서 **확인**을 클릭합니다.

4.  **인증서**, **개인**을 차례로 펼치고 **인증서**를 선택합니다.

5.  [용도]가 **클라이언트 인증**인 인증서를 선택합니다. 
    a. [작업] 메뉴에서 **열기**를 선택합니다. 
    b. **인증 경로** 탭으로 전환합니다. c. 체인의 다음 인증서를 선택하고 **인증서 보기**를 클릭합니다.

6.  이 새 인증서 대화 상자에서 **세부 정보** 탭으로 전환합니다. **파일에 복사...** 를 클릭합니다.

7.  기본 인증서 형식인 **DER로 인코딩된 X.509 바이너리(.CER)** 를 사용하여 인증서 내보내기 마법사를 완료합니다. 내보낸 인증서의 이름과 위치를 적어 둡니다.

8. 원래 클라이언트 인증 인증서의 인증서 경로에 있는 모든 인증서를 내보냅니다. 내보낸 인증서 중 중간 CA 및 신뢰할 수 있는 루트 CA에 해당하는 인증서를 적어 둡니다.



## <a name="enable-management-point-for-https"></a>HTTPS에 대한 관리 지점 사용

*인증서 요구 사항*
- 1706 또는 1710 버전에서 클라이언트 인증 인증서를 사용하여 온-프레미스 ID가 있는 기존 클라이언트를 관리하는 경우 이 인증서를 권장하지만 반드시 필요한 것은 아닙니다.
- 1710 버전에서는 Azure AD에 가입한 Windows 10 클라이언트를 관리할 때 이 인증서가 관리 지점에 필요합니다. 
- 1802 버전부터 이 인증서는 모든 시나리오에서 필요합니다. CMG에 대해 사용할 수 있는 관리 지점만 HTTPS여야 합니다. 이 동작이 변경되면 Azure AD 토큰 기반 인증에 대한 지원이 개선됩니다. 

Configuration Manager의 컨텍스트 외부에서 이 인증서를 제공합니다. 예를 들어 Active Directory 인증서 서비스 및 그룹 정책을 사용하여 웹 서버 인증서를 발급합니다. 자세한 내용은 [PKI 인증 요구 사항](/sccm/core/plan-design/network/pki-certificate-requirements) 및 [IIS를 실행하는 사이트 시스템용 웹 서버 인증서 배포](/sccm/core/plan-design/network/example-deployment-of-pki-certificates#BKMK_webserver2008_cm2012)를 참조하세요.



## <a name="next-steps"></a>다음 단계

- [클라우드 관리 게이트웨이 설정](/sccm/core/clients/manage/cmg/setup-cloud-management-gateway)
- [클라우드 관리 게이트웨이에 대한 FAQ](/sccm/core/clients/manage/cmg/cloud-management-gateway-faq)
- [클라우드 관리 게이트웨이에 대한 보안 및 개인 정보](/sccm/core/clients/manage/cmg/security-and-privacy-for-cloud-management-gateway)
