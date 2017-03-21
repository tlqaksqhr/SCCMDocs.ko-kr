---
title: "Exchange ActiveSync 메일 프로필 만들기 | Microsoft 문서"
description: "Microsoft Intune에서 작동하는 System Center Configuration Manager의 메일 프로필을 만들고 구성하는 방법을 알아봅니다."
ms.custom: na
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: get-started-article
ms.assetid: 120442be-179e-450c-a0c4-284046895da3
caps.latest.revision: 4
caps.handback.revision: 0
author: arob98
ms.author: angrobe
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 2c723fe7137a95df271c3612c88805efd8fb9a77
ms.openlocfilehash: 1cbe1d8f34b0a7482232488e907190a7a9cadf30
ms.lasthandoff: 03/06/2017


---

# <a name="exchange-activesync-email-profiles-in-system-center-configuration-manager"></a>System Center Configuration Manager의 Exchange ActiveSync 메일 프로필

*적용 대상: System Center Configuration Manager(현재 분기)*

메일 프로필이 Microsoft Intune을 사용하여 작동하면 Exchange ActiveSync를 사용하여 메일 프로필 및 제한 사항으로 장치를 프로비전할 수 있습니다. 이를 통해 사용자는 최소한의 설정으로 자신의 장치에서 회사 전자 메일에 액세스할 수 있습니다.  

 전자 메일 프로필을 사용하여 구성할 수 있는 장치 유형은 다음과 같습니다.  

-   Windows Phone 8을 실행하는 장치  

-   Windows Phone 8.1을 실행하는 장치  

-   Windows 10 Mobile을 실행하는 장치  

-   iOS 5, iOS 6, iOS 7 및 iOS 8을 실행하는 IPhone 장치  

-   iOS 5, iOS 6, iOS 7 및 iOS 8을 실행하는 IPad 장치  

> [!IMPORTANT]  
>  iOS, Android Samsung KNOX Standard, Windows Phone 및 Windows 8.1 또는 Windows 10 장치에 프로필을 배포하려면 이러한 장치를 Intune에 등록해야 합니다. 장치를 등록하는 방법에 대한 자세한 내용은 [Microsoft Intune을 사용하여 모바일 장치 관리](https://technet.microsoft.com/en-us/library/dn646962.aspx)를 참조하세요.  

 장치에서 전자 메일 계정을 구성하는 것 외에 연락처, 일정 및 작업에 대한 동기화 설정을 구성할 수도 있습니다.  

 메일 프로필을 만들 때 System Center Configuration Manager 인증서 프로필을 사용하여 프로비전한 ID, 암호화 및 서명용 인증서를 비롯하여 다양한 보안 설정을 포함할 수 있습니다. 인증서 프로필에 대한 자세한 내용은 [System Center Configuration Manager의 인증서 프로필](introduction-to-certificate-profiles.md)을 참조하세요.    


## <a name="create-a-new-exchange-activesync-email-profile"></a>새 Exchange ActiveSync 메일 프로필 만들기  

Exchange ActiveSync 메일 프로필 만들기 마법사 시작  

1.  System Center Configuration Manager 콘솔에서 **자산 및 준수**를 클릭합니다.  

2.  **자산 및 호환성** 작업 영역에서 **호환성 설정**및 **회사 리소스 액세스**를 각각 확장하고 **전자 메일 프로필**을 클릭합니다.  

3.  **홈** 탭의 **만들기** 그룹에서 **Exchange ActiveSync 프로필 만들기**를 클릭합니다.

4.  마법사의 지시를 따릅니다.   

### <a name="to-configure-exchange-activesync-settings-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 전자 메일 프로필에 대한 Exchange ActiveSync 설정을 구성하려면  

1.  Exchange ActiveSync 전자 메일 프로필 만들기 마법사의 **Exchange ActiveSync** 페이지에서 다음 정보를 지정합니다.  

    -   **Exchange ActiveSync 호스트:** Exchange ActiveSync 서비스를 호스트하는 회사 Exchange Server의 호스트 이름을 지정합니다.  

    -   **계정 이름:** 장치에서 사용자에게 표시할 메일 계정의 표시 이름을 지정합니다.  

    -   **계정 사용자 이름:** 클라이언트 장치에서 메일 계정 사용자 이름을 구성하는 방법을 선택합니다. 드롭다운 목록에서 다음 옵션 중 하나를 선택할 수 있습니다.  

        -   **사용자 계정 이름** 전체 사용자 계정 이름을 사용하여 Exchange에 로그온합니다.  

        -   **sAMAccountName** 사용  

        -   **기본 SMTP 주소** 사용자의 기본 SMTP 주소를 사용하여 Exchange에 로그온합니다.  

    -   **메일 주소:** 각 클라이언트 장치에서 사용자의 메일 주소가 생성되는 방식을 선택합니다. 드롭다운 목록에서 다음 옵션 중 하나를 선택할 수 있습니다.  

        -   **기본 SMTP 주소** 사용자의 기본 SMTP 주소를 사용하여 Exchange에 로그온합니다.  

        -   **사용자 계정 이름** 전체 사용자 계정 이름을 전자 메일 주소로 사용합니다.  

    -   **계정 도메인:** 다음 옵션 중 하나를 선택합니다.  

        -   **Active Directory에서 가져오기**  

        -   **사용자 지정**  

         이 필드는 **계정 사용자 이름** 드롭다운 목록에서 **sAMAccountName** 을 선택한 경우에만 적용됩니다.  

    -   **인증 방법:** 다음 인증 방법 중에서 Exchange ActiveSync에 대한 연결을 인증하는 데 사용할 방법 하나를 선택합니다.  

        -   **인증서** ID 인증서를 사용하여 Exchange ActiveSync 연결을 인증합니다.  

        -   **사용자 이름 및 암호** 장치 사용자는 Exchange ActiveSync에 연결할 암호를 제공해야 합니다(사용자 이름은 전자 메일 프로필의 일부로 구성됨).  

    -   **ID 인증서:** **선택** 을 클릭하고 ID에 사용할 인증서를 선택합니다.  

        > [!NOTE]  
        >  ID 인증서를 선택하려면 먼저 해당 인증서를 SCEP(단순 인증서 등록 프로토콜) 인증서 프로필로 구성해야 합니다. 인증서 프로필에 대한 자세한 내용은 [System Center Configuration Manager의 인증서 프로필](introduction-to-certificate-profiles.md)을 참조하세요.  

         이 옵션은 **인증 방법** 에서 **인증서**를 선택한 경우에만 사용할 수 있습니다.  

    -   **S/MIME 사용** S/MIME 암호화를 사용하여 보내는 전자 메일을 전송합니다. 이 옵션은 iOS 장치에만 적용됩니다.  

    -   **암호화 인증서:** **선택** 을 클릭하고 암호화에 사용할 인증서를 선택합니다. 이 옵션은 iOS 장치에만 적용됩니다.  

        > [!NOTE]  
        >  암호화 인증서를 선택하려면 먼저 해당 인증서를 SCEP(단순 인증서 등록 프로토콜) 인증서 프로필로 구성해야 합니다. 인증서 프로필에 대한 자세한 내용은 [System Center Configuration Manager의 인증서 프로필](introduction-to-certificate-profiles.md)을 참조하세요.  

         이 옵션은 **S/MIME 사용**을 선택한 경우에만 사용할 수 있습니다.  

    -   **서명 인증서:** **선택** 을 클릭하고 서명에 사용할 인증서를 선택합니다. 이 옵션은 iOS 장치에만 적용됩니다.  

        > [!NOTE]  
        >  서명 인증서를 선택하려면 먼저 해당 인증서를 SCEP(단순 인증서 등록 프로토콜) 인증서 프로필로 구성해야 합니다. 인증서 프로필에 대한 자세한 내용은 [System Center Configuration Manager의 인증서 프로필](introduction-to-certificate-profiles.md)을 참조하세요.  

         이 옵션은 **S/MIME 사용**을 선택한 경우에만 사용할 수 있습니다.  

###   <a name="configure-synchronization-settings-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 전자 메일 프로필에 대한 동기화 설정을 구성합니다.  

1.  Exchange ActiveSync 전자 메일 프로필 만들기 마법사의 **동기화 설정 구성** 페이지에서 다음 정보를 지정합니다.  

    -   **일정:** 장치가 Exchange 서버의 데이터를 동기화할 일정을 선택합니다. 이 옵션은 Windows Phone 장치에만 적용됩니다. 다음 중에서 선택합니다.  

        -   **구성되어 있지 않음** 동기화 일정이 적용되지 않습니다. 이 경우 사용자는 고유한 동기화 일정을 구성할 수 있습니다.  

        -   **메시지가 도착할 때** 전자 메일 및 일정 항목과 같은 데이터가 도착 시 자동으로 동기화됩니다.  

        -   **15분** 전자 메일 및 일정 항목과 같은 데이터가 15분마다 자동으로 동기화됩니다.  

        -   **30분** 전자 메일 및 일정 항목과 같은 데이터가 30분마다 자동으로 동기화됩니다.  

        -   **60분** 전자 메일 및 일정 항목과 같은 데이터가 60분마다 자동으로 동기화됩니다.  

        -   **수동** 장치 사용자가 동기화를 수동으로 시작해야 합니다.  

    -   **메일을 동기화할 기간(일):** 드롭다운 목록에서 동기화할 메일의 일 수를 선택합니다. 다음 값 중 하나를 선택합니다.  

        -   **구성되어 있지 않음** 설정이 적용되지 않습니다. 이 경우 사용자는 장치에 다운로드할 전자 메일 수를 구성할 수 있습니다.  

        -   **무제한** 사용 가능한 모든 전자 메일을 동기화합니다.  

        -   **1일**  

        -   **3일**  

        -   **1주**  

        -   **2주**  

        -   **1개월**  

    -   **메시지를 다른 전자 메일 주소로 이동하도록 허용** 사용자가 자신의 장치에 구성한 여러 계정 간에 전자 메일 메시지를 이동할 수 있도록 허용하려면 이 옵션을 선택합니다. 이 옵션은 iOS 장치에만 적용됩니다.  

    -   **타사 응용 프로그램에서 전자 메일을 보내도록 허용** 사용자가 기본이 아닌 특정 타사 전자 메일 응용 프로그램에서 전자 메일을 보낼 수 있도록 허용하려면 이 옵션을 선택합니다. 이 옵션은 iOS 장치에만 적용됩니다.  

    -   **최근에 사용한 전자 메일 주소 동기화** 장치에서 최근에 사용된 전자 메일 주소 목록을 동기화하려면 이 옵션을 선택합니다. 이 옵션은 iOS 장치에만 적용됩니다.  

    -   **SSL 사용** 전자 메일을 보내거나 받고 Exchange 서버와 통신할 때 SSL(Secure Sockets Layer)을 사용하려면 이 옵션을 선택합니다.  

    -   **동기화할 콘텐츠 형식:** 장치에 동기화할 콘텐츠 형식을 선택합니다. 이 옵션은 Windows Phone 장치에만 적용됩니다. 다음 중에서 선택합니다.  

        -   **전자 메일**  

        -   **연락처**  

        -   **일정**  

        -   **태스크**  

###  <a name="specify-supported-platforms-for-the-exchange-activesync-email-profile"></a>Exchange ActiveSync 전자 메일 프로필에 대한 지원되는 플랫폼을 지정합니다.  

1.  Exchange ActiveSync 전자 메일 프로필 만들기 마법사의 **지원되는 플랫폼** 페이지에서 전자 메일 프로필을 설치할 운영 체제를 선택하거나, 사용 가능한 모든 운영 체제에 전자 메일 프로필을 설치하려면 **모두 선택** 을 클릭합니다.  

2.  마법사를 완료합니다.

Exchange ActiveSync 메일 프로필을 배포하는 방법에 대한 자세한 내용은 [System Center Configuration Manager의 프로필 배포](../../protect/deploy-use/deploy-wifi-vpn-email-cert-profiles.md)를 참조하세요.  
