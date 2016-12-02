---
title: "보관 | 새로운 기능 하이브리드 MDM | Microsoft Intune | System Center Configuration Manager"
description: "System Center Configuration Manager 및 Intune을 포함하는 하이브리드 배포에 사용할 수 있는 과거 모바일 장치 관리 기능의 보관 파일입니다."
ms.custom: na
ms.date: 10/25/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-hybrid
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 4c27b161-9eb7-4cdd-b469-d8eb27e71aea
author: Mtillman
ms.author: mtillman
manager: angrobe
ROBOTS: NOINDEX, NOFOLLOW
translationtype: Human Translation
ms.sourcegitcommit: bfc4baefbdddc5125c38272f2087d214151c91d5
ms.openlocfilehash: 4c0910ae365e1fda7b9747b79e13782a6056c0da

---
# <a name="past-hybrid-features-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 및 Microsoft Intune을 사용하는 이전 하이브리드 기능

*적용 대상: System Center Configuration Manager(현재 분기)*

이 문서에서는 System Center Configuration Manager 및 Intune을 포함하는 하이브리드 배포에 사용할 수 있는 과거 MDM(모바일 장치 관리) 기능에 대한 세부 정보를 제공합니다.  

##  <a name="compatibility-with-configuration-manager-versions"></a>Configuration Manager 버전과 호환성  

 이 문서의 각 섹션에서는 세 가지 범주로 하이브리드 기능이 나열되어 있습니다. 각 범주의 기능과 다양한 Configuration Manager 버전 간의 호환성을 확인하려면 다음 지침을 따르세요.  

|기능 범주|
|-|  
|**Microsoft Intune의 새로운 기능** - 일반적으로 이 범주 아래에 나열된 모든 기능은 Intune 서비스만 필요하고 Configuration Manager의 추가 기능이 필요하지 않으므로 System Center 2012 R2 Configuration Manager 릴리스를 비롯한 모든 Configuration Manager 릴리스에서 사용할 수 있어야 합니다.<br /><br /> **Configuration Manager Technical Preview의 새로운 기능** - 이 범주 아래에 나열된 모든 기능은 지정된 기술 미리 보기 릴리스에서만 사용할 수 있습니다. 이러한 기능을 시험해보려면 기능 설명에 지정된 기술 미리 보기 버전을 설치해야 합니다. 자세한 내용은 [System Center Configuration Manager Technical Preview](../../core/get-started/technical-preview.md)를 참조하세요.<br /><br /> **Configuration Manager(현재 분기)의 새로운 기능** - 이 범주 아래에 나열된 모든 기능은 지정된 버전의 Configuration Manager(현재 분기)(예: 버전 1511 또는 1602)에서만 사용할 수 있습니다. 하이브리드 배포에 이전 버전의 Configuration Manager를 사용하는 경우 기능 설명에 지정된 Configuration Manager(현재 분기) 버전으로 업그레이드해야 합니다. 자세한 내용은 [System Center Configuration Manager 업그레이드](../../core/servers/deploy/install/upgrade-to-configuration-manager.md)를 참조하세요.|  

## <a name="new-hybrid-features-in-june-2016"></a>2016년 6월의 새로운 하이브리드 기능

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능
2016년 6월에 도입된 다음 Intune 기능은 하이브리드 배포에서 사용할 수 있습니다.

- **Intune 서비스 상태** Intune에 대한 서비스 상태 정보가 다른 Microsoft 서비스와 함께 중앙 위치로 이동되었습니다. 이제 Office 365 관리 포털의 서비스 상태 아래에서 이 정보를 확인할 수 있습니다. 자세한 내용은 이 [블로그 게시물](https://blogs.technet.microsoft.com/enterprisemobility/2016/04/28/intune-service-health-is-now-available-in-the-office-365-portal/)을 참조하세요.

- **향상된 Windows 10 Enterprise 데이터 정책 구성 환경**

  이제 Intune에 Windows 10 Information Protection 정책을 구성하기 위한 향상된 환경이 있습니다. 향상된 기능에는 앱 규칙을 만들고, 네트워크 경계 정의 및 기타 Windows Information Protection 설정을 지정하는 더 나은 방법이 포함됩니다. 자세한 내용은 [Microsoft Intune을 사용하여 WIP(Windows Information Protection) 정책 만들기](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-intune)를 참조하세요.

- **Intune에 대한 Cisco ISE 네트워크 액세스 제어 정책**

  Cisco ISE(Identity Service Engine) 2.1을 사용하고 Microsoft Intune도 사용하는 고객은 ISE에서 네트워크 액세스 제어 정책을 설정할 수 있습니다. 이 정책을 사용하는 경우 WiFi 또는 VPN을 통해 네트워크에 연결해야 하는 장치는 다음 조건을 충족해야 액세스가 허용됩니다.

  - Intune에서 관리해야 함
  - 배포된 Intune 준수 정책을 준수해야 함

  비규격 장치의 최종 사용자는 액세스하기 위해 등록하고 준수 문제를 해결하라는 메시지가 표시됩니다.

- **브라우저에 대한 조건부 액세스**

  관리되는 규격 iOS 및 Android 장치의 지원되는 웹 브라우저에서만 액세스할 수 있도록 Exchange Online 및 SharePoint Online에 대한 조건부 액세스 정책을 설정할 수 있습니다. iOS 및 Android 장치를 사용하여 OWA(Outlook Web Access) 및 SharePoint 사이트에 로그인하려는 최종 사용자에게는 Intune에 장치를 등록하고 비준수 문제를 해결해야 로그인을 완료할 수 있다는 메시지가 표시됩니다. 자세한 내용은

  * [Intune을 사용하여 Exchange Online 및 새 Exchange Online Dedicated에 대한 메일 액세스 제한](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-exchange-online-with-microsoft-intune)
  * [Microsoft Intune을 사용하여 SharePoint Online에 대한 액세스 제한](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-sharepoint-online-with-microsoft-intune)

- **Dynamics CRM Online에서 조건부 액세스 지원**

  관리되는 규격 iOS 및 Android 장치에서만 액세스할 수 있도록 Dynamics CRM Online에 대한 조건부 액세스 정책을 설정할 수 있습니다. iOS 및 Android의 Dynamics CRM 모바일 앱에 로그인하려는 최종 사용자에게는 Intune에 등록하고 비준수 문제를 해결해야 로그인을 완료할 수 있다는 메시지가 표시됩니다. 자세한 내용은 [Microsoft Intune을 사용하여 Dynamics CRM Online에 대한 액세스 제한](https://docs.microsoft.com/intune/deploy-use/restrict-access-to-dynamics-crm-online-with-microsoft-intune)을 참조하세요.

- **Android 회사 포털 앱에 대한 업데이트**

  이제 Intune에 Android 회사 포털 사용자에게 영향을 주는 다음과 같은 새 정책이 있습니다.   

  정책  |사용자에 미치는 영향  
  ---------|---------
  장치가 알 수 없는 소스의 앱 설치를 방지해야 함(Android 4.0 이상)     |  Android 4.0 이상 장치를 사용하는 최종 사용자에게는 "알 수 없는 소스의 설치를 사용하지 않도록 설정해야 합니다."라는 메시지가 표시됩니다. 사용자는 해당 장치에서 **설정 > 보안**으로 이동한 다음 **알 수 없는 소스**를 꺼야 합니다. 사용자는 준수 메시지에 있는 링크를 통해 메시지에 대한 자세한 정보와 설정을 꺼야 하는 이유를 확인할 수 있습니다.
  장치가 알 수 없는 소스의 앱 설치를 방지해야 함(Android 4.0 이상)  |    Android 4.0 이상 장치를 사용하는 최종 사용자에게는 "장치의 보안 위협 검색"이라는 메시지가 표시됩니다. 사용자가 해당 장치에서 **설정 > Google > 보안**으로 이동한 다음 **장치의 보안 위협 검색**을 켜야 합니다. 사용자는 준수 메시지에 있는 링크를 통해 메시지에 대한 자세한 정보와 설정을 켜야 하는 이유를 확인할 수 있습니다.     
  USB 디버깅을 사용하지 않도록 설정되어야 함(Android 4.2 이상)  | Android 4.2 이상 장치를 사용하는 최종 사용자에게는 "USB 디버깅을 사용하지 않도록 설정해야 합니다."라는 메시지가 표시됩니다. 사용자는 해당 장치에서 **설정 > 개발자 옵션**으로 이동한 다음 **USB 디버깅**을 꺼야 합니다. 사용자는 준수 메시지에 있는 링크를 통해 메시지에 대한 자세한 정보와 설정을 꺼야 하는 이유를 확인할 수 있습니다.
  최소 Android 보안 패치 수준(Android 6.0 이상)  | Android 6.0 이상 장치를 사용하는 최종 사용자에게는 "이 장치는 최소 Android 보안 패치 수준을 충족하지 않습니다."라는 메시지가 표시됩니다. 사용자가 필요한 보안 패치를 설치해야 합니다. 사용자는 준수 메시지에 있는 링크를 통해 필요한 보안 패치를 설치하는 방법에 대한 자세한 정보를 얻고 현재 설치된 보안 패치를 확인할 수 있습니다.

- **iOS 회사 포털 앱에 대한 업데이트**

  * 이제 최종 사용자가 LOB(기간 업무) 앱을 설치할 때 향상된 앱 설치 환경이 표시됩니다. 앱 설치에 오랜 시간이 걸리는 경우 사용자가 장치를 수동으로 동기화하여 동기화 프로세스를 강제로 다시 시작할 수 있습니다. 최종 사용자 지침을 검토하려면 iOS 장치 수동 동기화를 참조하세요.
  * iOS용 Microsoft Intune 회사 포털 앱은 iOS 버전 8.0 이상을 지원하도록 업데이트되었습니다. 이 업데이트를 사용하면 장치가 iOS 버전 8.0 이상을 실행하는 경우 최종 사용자가 회사 포털 앱을 설치하고 Intune에 새 장치를 등록할 수 있습니다. 지원되지 않는 iOS 버전을 실행 중이고 이미 등록된 장치가 있는 사용자는 자신의 장치에 있는 회사 포털 앱을 계속 사용할 수 있습니다.


### <a name="new-in-1606-technical-preview"></a>1606 기술 미리 보기의 새로운 기능
2016년 6월에 도입된 다음 새로운 기능은 Intune과 Configuration Manager Technical Preview 1606을 포함하는 하이브리드 배포에서 사용할 수 있습니다.

- **컬렉션으로 장치 자동 분류**

  Intune에서 Configuration Manager를 사용하는 경우 장치 컬렉션에 장치를 자동으로 배치하는 데 사용할 수 있는 장치 범주를 만들 수 있습니다. 그런 다음 사용자는 Intune에 장치를 등록할 때 장치 범주를 선택해야 합니다. 또한 Configuration Manager 콘솔에서 장치의 범주를 변경할 수 있습니다. 자세한 내용은 [System Center Configuration Manager용 Technical Preview 1606의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1606.md)에서 [컬렉션으로 장치 자동 분류](/sccm/core/get-started/capabilities-in-technical-preview-1606.md#dmp_category)를 참조하세요.

  > [!IMPORTANT]
  > 이 기능은 Microsoft Intune의 2016년 6월 릴리스에 작동합니다. 이러한 절차를 시도하기 전에 이 릴리스로 업데이트했는지 확인합니다.

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager(현재 분기)의 새로운 기능
Configuration Manager(현재 분기) 2016년 6월에 도입된 새로운 하이브리드 기능은 없습니다.

##  <a name="new-hybrid-features-in-may-2016"></a>2016년 5월의 새로운 하이브리드 기능  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능  
 2016년 5월에 도입된 다음 Intune 기능은 하이브리드 배포에서 사용할 수 있습니다.

- **MAM SDK: PIN 길이 구성 지원**

  이제 장치 PIN과 유사한 PIN 길이를 MAM 앱에 지정할 수 있습니다. 이 경우 최종 사용자가 설정된 새로운 제한 사항을 준수해야 합니다. PIN 화면이 더 긴 입력을 수용하기 위해 약간 수정되었습니다. 자세한 내용은 [Android에 대한 MAM 정책 설정](https://docs.microsoft.com/intune/deploy-use/android-mam-policy-settings) 및 [iOS에 대한 MAM 정책 설정](https://docs.microsoft.com/intune/deploy-use/ios-mam-policy-settings)을 참조하세요.  

- **iOS 및 Android의 비즈니스용 Skype**

  이제 [등록 정책을 사용하지 않는 MAM](https://docs.microsoft.com/intune/deploy-use/get-ready-to-configure-mobile-app-management-policies-with-microsoft-intune)을 통해 비즈니스용 Skype의 대상을 지정할 수 있습니다. 사용자가 로그인하면 MAM 정책이 적용됩니다.  

- **MAM 정책을 사용한 관리를 위해 제공되는 새 앱**

  이제 Android용 Microsoft Word, Excel 및 PowerPoint 앱을 Intune에 등록되지 않은 장치의 MAM 정책과 연결할 수 있습니다. 지원되는 앱의 전체 목록을 보려면 [Microsoft Intune 응용 프로그램 파트너](https://www.microsoft.com/en-us/server-cloud/products/microsoft-intune/partners.aspx) 페이지의 Microsoft Intune 모바일 응용 프로그램 갤러리로 이동합니다.  

- **Android 회사 포털 앱: 최종 사용자 알림 메시지**

  최종 사용자가 장치를 등록하거나 회사 포털에서 제거하면 Android 회사 포털 앱의 알림 메시지가 나타납니다.  

- **회사 포털 웹 사이트: 장치 식별 배너에서 최종 사용자에게 자세한 정보를 제공함**

  이제 최종 사용자가 회사 포털 웹 사이트를 사용할 때 선택한 장치를 보다 쉽게 식별할 수 있습니다. 잘못된 장치를 선택한 경우 홈페이지 배너의 **여기를 탭하세요.** 링크를 탭하여 올바른 장치를 선택할 수 있습니다.  


### <a name="new-in-1605-technical-preview"></a>1605 기술 미리 보기의 새로운 기능  
 2016년 5월에 도입된 다음 새로운 기능은 Intune과 Configuration Manager Technical Preview 1605를 포함하는 하이브리드 배포에서 사용할 수 있습니다. 이러한 기능은 Configuration Manager 콘솔을 사용하여 구성 및 관리해야 합니다.  

- **Windows 10 장치를 위한 앱 트리거 VPN**

  Intune에서 Configuration Manager를 사용하여 관리되는 Windows 10 장치의 경우, Configuration Manager 관리 콘솔을 통해 구성한 VPN 연결을 자동으로 여는 앱 목록을 추가할 수 있습니다. 자세한 내용은 [System Center Configuration Manager용 Technical Preview 1605의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1605)에서 [Windows 10 장치를 위한 앱 트리거 VPN](/sccm/core/get-started/capabilities-in-technical-preview-1605)을 참조하세요.  

- **원격 장치 작업을 위한 새로운 환경**

  Configuration Manager 콘솔에서 원격 장치 작업을 수행하기 위한 환경이 개선되었습니다.

  이제 **자산 및 준수** 작업 영역에서 액세스되는 **원격 장치 작업** 메뉴에서 **사용 중지/초기화**, **암호 다시 설정**, **원격 잠금** 및 **활성화 잠금 무시** 등의 일반 작업을 찾을 수 있습니다.

  자세한 내용은 [System Center Configuration Manager용 Technical Preview 1605의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1605)에서 [원격 장치 작업을 위한 새로운 환경](/sccm/core/get-started/capabilities-in-technical-preview-1605#new-experience-for-remote-device-actions)을 참조하세요.  

- **비즈니스용 Windows 스토어 앱**

  [비즈니스용 Windows 스토어](https://www.microsoft.com/en-us/business-store)에서 조직을 위한 앱을 찾아서 개별적으로 또는 대량으로 구매할 수 있습니다. 스토어를 Configuration Manager에 연결하여 Configuration Manager 콘솔에서 대량 구매 앱을 관리할 수 있습니다. 자세한 내용은 [System Center Configuration Manager용 Technical Preview 1605의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1605)에서 [비즈니스용 Windows 스토어 앱](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#windows-store-for-business-apps)을 참조하세요.  

- **대량 구매 앱의 일반적인 향상 기능**

  비즈니스용 Windows 스토어와 iOS App Store의 대량 구매 앱이 동일한 보기, **스토어 앱에 대한 라이선스 정보**로 통합되었습니다. 또한 iOS용 대량 구매 앱을 만드는 방식으로 향상되었습니다. 자세한 내용은 [System Center Configuration Manager용 Technical Preview 1605의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1605)에서 [대량 구매 앱에 대한 일반적인 향상 기능](/sccm/core/get-started/capabilities-in-technical-preview-1605.md#general-improvements-for-volume-purchased-apps)을 참조하세요.  

- **IMEI 또는 iOS 일련 번호로 회사 소유 장치 미리 선언**

  이제 IMEI(International station Mobile Equipment Identity) 번호를 가져와서 회사 소유 장치를 식별할 수 있습니다. 장치 IMEI 번호를 포함한 쉼표로 구분된 값(.csv) 파일을 업로드하거나 장치 정보를 수동으로 입력할 수 있습니다.  또한 iOS 장치의 일련 번호를 가져올 수 있습니다.  자세한 내용은 [System Center Configuration Manager용 Technical Preview 1605의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1605)에서 [IMEI 또는 iOS 일련 번호로 회사 소유 장치 미리 선언](../../core/get-started/capabilities-in-technical-preview-1605.md#pre-declare-corporate-owned-devices-with-with-imei-or-ios-serial-number)을 참조하세요.  

- **WIP(Windows Information Protection)**

  보호된 앱, WIP 보호 수준 및 네트워크에서 엔터프라이즈 데이터를 찾는 방법을 선택하는 항목을 포함하여 WIP(Windows Information Protection) 정책을 배포할 수 있는 구성 항목을 만들 수 있습니다. WIP에 대한 자세한 내용은 다음 항목을 참조하세요.  

  -   [WIP(Windows Information Protection)를 사용하여 엔터프라이즈 데이터 보호](https://technet.microsoft.com/itpro/windows/keep-secure/protect-enterprise-data-using-wip)  

  -   [System Center Configuration Manager를 사용하여 WIP(Windows Information Protection) 정책 만들기 및 배포](https://technet.microsoft.com/itpro/windows/keep-secure/create-wip-policy-using-sccm)  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager(현재 분기)의 새로운 기능  
 Configuration Manager(현재 분기) 2016년 5월에 도입된 새로운 하이브리드 기능은 없습니다.  

##  <a name="new-hybrid-features-in-april-2016"></a>2016년 4월의 새로운 하이브리드 기능  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능  
 2016년 4월에 도입된 다음 Intune 기능은 하이브리드 배포에서 사용할 수 있습니다.  

- **MAM 사용자 준수**

  이제 AAD(Azure Active Directory) 테넌트의 사용자에 대한 응용 프로그램 관리 정책의 상태를 볼 수 있습니다.  자세한 내용은 Intune 라이브러리에서 [Microsoft Intune으로 모바일 앱 관리 정책 모니터링](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)을 참조하세요.  

- **Outlook 연락처 동기화를 방지하는 MAM 컨트롤(Android)**

  응용 프로그램이 Android 장치의 기본 주소록에 연락처를 동기화할 수 없도록 하는 새로운 설정을 사용할 수 있습니다. 이 새로운 설정은 처음에 Android 장치의 Outlook 응용 프로그램에서 지원됩니다. 자세한 내용은 Intune 라이브러리에서 [Microsoft Intune으로 모바일 앱 관리 정책 만들기 및 배포](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)를 참조하세요.  

- **회사 포털 웹 사이트의 향상된 기능**

  Windows 10 Mobile 및 Windows Phone 8.1 사용자가 LOB(기간 업무) 앱을 설치하는 경우 이제 설치 상태에 대한 자세한 정보를 제공하는 다음과 같은 새 상태가 표시됩니다.  

  -   **장치가 동기화될 때까지 기다리는 중** – 사용자가 "설치"를 탭했으며 이제 장치에서 Intune 인프라와 동기화하려고 합니다. 먼저 동기화해야 설치를 완료할 수 있습니다. "장치가 동기화될 때까지 기다리는 중" 메시지는 동기화 프로세스가 시간이 오래 걸리거나 정지될 경우 수동으로 Intune과 장치를 동기화하는 방법에 대한 지침을 보기 위해 사용자가 탭할 수 있는 링크이기도 합니다.  

  -   **다운로드 중** - 사용자의 다운로드 요청이 처리되고 있으며 장치에서 앱을 다운로드하여 설치 중입니다.  

- **Android 회사 포털 앱에 대한 향상된 기능**

  Intune에 장치를 등록하지 않았으며 올바른 인증서가 설치되어 있지 않은 사용자는 Android 회사 포털 앱에 로그인할 수 없으며 "필요한 인증서가 장치에 없으므로 로그인할 수 없습니다."라는 메시지가 표시됩니다. 메시지에는 사용자가 인증서 설치 지침을 보기 위해 탭할 수 있는 "이 문제를 해결하는 방법" 링크가 포함되어 있습니다. 최종 사용자가 문제를 해결하기 위해 수행할 단계를 보려면 Intune 라이브러리에서 [장치에 필요한 인증서가 없는 경우](/intune/enduser/using-your-android-device-with-intune)를 참조하세요.  

- **iOS 회사 포털 앱에 대한 향상된 기능**

  앱 목록, 장치 목록 및 IT 연락처 정보를 포함하는 홈 화면의 콘텐츠를 새로 고치기 위한 끌어오기-새로 고침 작업에 대한 지원이 추가되었습니다. 끌어오기-새로 고침 작업은 현재 장치에 대한 타일을 선택하고 **동기화** 단추를 탭하여 수행할 수 있는 준수 또는 정책 정보를 확인하지 않습니다.  

- **Windows 10 Mobile 및 Windows Phone 8.1 회사 포털 앱에 대한 향상된 기능**

  이제 최종 사용자가 LOB(기간 업무) 앱을 설치할 때 향상된 앱 설치 환경이 표시됩니다. 앱 설치에 오랜 시간이 걸리는 경우 사용자가 장치를 수동으로 동기화하여 동기화 프로세스를 강제로 다시 시작할 수 있습니다. 최종 사용자 지침을 검토하려면 Intune 라이브러리에서 [장치를 수동으로 동기화하여 앱 설치 속도 향상](/intune/enduser/using-your-windows-device-with-intune)을 참조하세요.  

###  <a name="new-in-1604-technical-preview"></a>1604 기술 미리 보기의 새로운 기능
 2016년 4월에 도입된 다음 새로운 기능은 Intune과 Configuration Manager Technical Preview 1604를 포함하는 하이브리드 배포에서 사용할 수 있습니다. 이러한 기능은 Configuration Manager 콘솔을 사용하여 구성 및 관리해야 합니다.  

- **Configuration Manager 콘솔에서 Windows 10 장치에 대한 비즈니스용 Windows 스토어 앱 찾기, 관리 및 배포**


  Configuration Manager Technical Preview 1604에서는 관리하는 Windows 10 장치에 대한 앱을 찾고 관리 및 배포할 수 있도록 도와주는 비즈니스용 Windows 스토어에 대한 지원을 사용할 수 있습니다. 자세한 내용은 [System Center Configuration Manager용 Technical Preview 1604의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1604)에서 [비즈니스용 Windows 스토어에서 대량 구매 앱 관리](/sccm/core/get-started/capabilities-in-technical-preview-1604#manage-volume-purchased-apps-from-the-windows-store-for-business)를 참조하세요.  

- **Android 장치에 대한 SmartLock 설정**

  새 설정이 Android 및 삼성 KNOX 구성 항목에 추가되었습니다. 이를 통해 호환되는 Android 장치에서 SmartLock 기능을 제어할 수 있습니다.  이 설정을 사용하면 최종 사용자가 SmartLock을 구성하지 않도록 방지할 수 있습니다. [System Center Configuration Manager용 Technical Preview 1604의 기능](/sccm/core/get-started/capabilities-in-technical-preview-1604.md)에서 [Android 장치에 대한 SmartLock 설정](/sccm/get-started/capabilities-in-technical-preview-1604#smartlock-setting-for-android-devices)을 참조하세요.  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager(현재 분기)의 새로운 기능  
 Configuration Manager(현재 분기) 2016년 4월에 도입된 새로운 하이브리드 기능은 없습니다.  

##  <a name="new-hybrid-features-in-march-2016"></a>2016년 3월의 새로운 하이브리드 기능  

### <a name="new-in-microsoft-intune"></a>Microsoft Intune의 새로운 기능  
 2016년 3월에 도입된 다음 Intune 기능은 하이브리드 배포에서 사용할 수 있습니다.  

- **Outlook 연락처 동기화를 방지하는 MAM 컨트롤(iOS)**

  응용 프로그램이 iOS 장치의 기본 주소록에 연락처를 동기화할 수 없도록 하는 새로운 설정을 사용할 수 있습니다. 이 새로운 설정은 iOS 장치의 Outlook 응용 프로그램에서 지원됩니다. 이 설정 및 기타 설정에 대한 자세한 내용은 Intune 라이브러리에서 [MAM 정책 만들기 및 배포](/intune/deploy-use/monitor-mobile-app-management-policies-with-microsoft-intune)를 참조하세요.  

- **비즈니스용 Skype Online에서 조건부 액세스 지원**

  관리되는 규격 iOS 및 Android 장치에서만 액세스할 수 있도록 비즈니스용 Skype Online에 대한 조건부 액세스 정책을 설정할 수 있습니다.  자세한 내용은 Intune 라이브러리에서 [비즈니스용 Skype Online에 대한 액세스 관리](/intune/deploy-use/restrict-access-to-skype-for-business-online-with-microsoft-intune)를 참조하세요.  

- **iOS 9.3에 대한 지원**

  3월 21일 월요일에 Apple은 iOS 9.3의 가용성을 발표했습니다. 현재 iOS 장치 관리에 사용할 수 있는 기존의 모든 Intune 기능은 사용자가 장치를 iOS 9.3으로 업그레이드할 때도 계속 원활하게 작동합니다.  

- **회사 포털 웹 사이트에서 직접 사용할 수 있는 Windows 앱 패키지**

  이제 Windows 8, Windows 8.1 및 Windows RT PC 사용자가 회사 포털 웹 사이트에서 직접 Windows 앱 패키지(.appx 확장명 사용)을 설치할 수 있습니다. 이전에는 관리자가 배포하거나, 사용자가 앱을 설치할 장치에 회사 포털 앱을 설치해야 했습니다.  

- **사용자가 회사 포털 웹 사이트에서 원격으로 장치를 잠글 수 있음**

  사용자가 장치를 분실하거나 도난당한 경우 포털에서 원격으로 장치를 잠글 수 있도록 하는 새로운 원격 잠금 옵션이 회사 포털 웹 사이트에 추가되었습니다.  

- **타사 MDM 솔루션에 등록된 장치에 대해 iOS "다음에서 열기" 관리 활용**

  타사 MDM(모바일 장치 관리) 공급업체를 사용하여 iOS "다음에서 열기" 관리를 활용할 수 있습니다. 구성 프로필 설정에서 제한을 설정하고 MDM 소프트웨어를 사용하여 앱을 배포할 수 있습니다. 사용자가 관리되는 앱을 설치하면 제한 사항이 적용됩니다. 자세한 내용은 Intune 라이브러리에서 [Microsoft Intune 모바일 앱 관리 정책 및 iOS 다음에서 열기](/intune/deploy-use/introduction-to-device-compliance-policies-in-microsoft-intune)를 참조하세요.  

- **MAM을 지원하는 Microsoft 앱**

  Intune 모바일 응용 프로그램 관리 정책과 함께 사용할 수 있는 Microsoft 앱 목록이 최신 앱을 포함하도록 업데이트되었습니다(Intune에 등록된 장치에만 해당).  

- **엔터프라이즈의 Intune 관리 iOS 장치에 Microsoft Intune용 Adobe Reader 배포**

  이제 Intune 모바일 응용 프로그램 관리 정책에 등록된 장치에서 iOS용 Adobe Reader 앱을 관리할 수 있습니다.  

- Android에 대해 Rights Management 공유 앱이 지원됨

  IT에서 Intune을 사용하여 장치를 관리하는지 여부에 관계없이 최종 사용자가 이미지, AV 및 PDF 파일을 보다 안전하게 볼 수 있도록 IT 관리자가 모바일 응용 프로그램 관리 정책을 배포할 수 있습니다.  

- **Android 및 iOS 회사 포털 앱에 대한 향상된 기능**

  -   사용자가 MAM(모바일 응용 프로그램 관리)에서 관리되는 앱을 실행하는 경우 앱이 회사에서 관리된다고 알리는 메시지가 표시됩니다. 이제 사용자가 "자세한 정보" 링크를 탭하여 "관리되는 앱"의 의미에 대한 자세한 정보를 여기서 확인할 수 있습니다. 앱을 실행할 때 메시지는 더 이상 표시되지 않도록 "다시 표시 안 함"을 탭할 수도 있습니다.  

  -   사용자에게 등록 과정을 안내하고 사용자가 등록해야 이유 및 IT 관리자가 등록된 장치에서 볼 수 있는 사항과 볼 수 없는 사항에 대한 자세한 정보를 제공하는 새 화면이 추가되었습니다.  

  -   이제 등록 오류 메시지가 회사 포털 앱에 표시됩니다.  

### <a name="new-in-configuration-manager-technical-preview"></a>Configuration Manager Technical Preview의 새로운 기능  
 Configuration Manager Technical Preview의 2016년 3월에 도입된 새로운 하이브리드 기능은 없습니다.  

### <a name="new-in-configuration-manager-current-branch"></a>Configuration Manager(현재 분기)의 새로운 기능  
 2016년 3월에 도입된 다음 새로운 기능은 Intune과 Configuration Manager(현재 분기) 버전 1602를 포함하는 하이브리드 배포에서 사용할 수 있습니다. 이러한 기능은 Configuration Manager 콘솔을 사용하여 구성 및 관리해야 합니다.  

- **iOS 앱 구성 정책**

  Configuration Manager(현재 분기) 버전 1602에서는 앱 구성 정책을 사용하여 사용자가 iOS 앱을 실행할 때 필요할 수 있는 설정을 제공할 수 있습니다. 자세한 내용은 [System Center Configuration Manager에서 앱 구성 정책을 사용하여 iOS 앱 구성](/sccm/apps/deploy-use/configure-ios-apps-with-app-configuration-policies)을 참조하세요.  

- **대량 구매한 iOS 앱 관리**

  버전 1602의 Configuration Manager(현재 분기)를 통해 앱 스토어에서 라이선스 정보를 가져오고 사용한 라이선스 수를 추적하여 Apple VPP(Volume-Purchase Program)에서 대량 구매한 앱을 배포하고 관리할 수 있습니다. 자세한 내용은 [System Center Configuration Manager를 사용하여 대량 구매한 iOS 앱 관리](/sccm/apps/deploy-use/manage-volume-purchased-ios-apps)를 참조하세요.  

- **Office 모바일 앱의 자동 만들기**

  Configuration Manager(현재 분기) 버전 1602부터, 버전 1511에서 업그레이드할 때 다음과 같은 Android 및 iOS용 Microsoft Office 모바일 앱이 생성됩니다.  

  -   Microsoft Word  
  -   Microsoft Excel  
  -   Microsoft PowerPoint  
  -   Microsoft OneDrive  
  -   Microsoft OneNote(iOS만 해당)  
  -   Microsoft Outlook  

  이러한 앱은 Configuration Manager 콘솔의 응용 프로그램 노드에 있습니다. 응용 프로그램을 배포하는 방법에 대한 자세한 내용은 [System Center Configuration Manager에서 응용 프로그램을 배포하는 방법](../../apps/deploy-use/deploy-applications.md)을 참조하세요.  

- **Android 삼성 KNOX 장치에 대한 키오스크 모드 설정**

  키오스크 모드에서는 장치를 잠가 특정 기능만 작동하도록 허용할 수 있습니다.  Configuration Manager(현재 분기) 버전 1602부터, 이제 삼성 KNOX 장치에 대한 키오스크 모드 설정을 지정할 수 있습니다. 자세한 내용은 [System Center Configuration Manager 클라이언트 없이 관리되는 Android 및 Samsung KNOX 장치에 대한 구성 항목을 만드는 방법](/sccm/compliance/deploy-use/create-configuration-items-for-android-and-samsung-knox-devices-managed-without-the-client)을 참조하세요.  

- **iOS 활성화 잠금**

  Configuration Manager(현재 분기) 버전 1602부터, iOS 7.1 이상 장치용 나의 iPhone 찾기(Find My iPhone) 앱의 기능인 iOS 활성화 잠금을 관리할 수 있습니다. 활성화 잠금은 장치에서 나의 iPhone 찾기 앱을 사용할 때 자동으로 사용하도록 설정됩니다.  자세한 내용은 [System Center Configuration Manager에 대한 iOS 활성화 잠금 무시 관리](/sccm/mdm/deploy-use/manage-ios-activation-lock#bypass-activation-lock)를 참조하세요.  



<!--HONumber=Nov16_HO1-->

