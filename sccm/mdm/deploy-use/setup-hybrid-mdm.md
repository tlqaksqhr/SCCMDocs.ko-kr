---
title: 하이브리드 MDM 설정
titleSuffix: Configuration Manager
description: Configuration Manager 및 Intune을 사용하여 하이브리드 장치 등록을 설정합니다.
ms.date: 03/08/2018
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: bb95154b-f63e-4491-896e-41d732c802f8
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: fbc5b9abf63d95185795716cfcb9ebfaf3e2ec3d
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="setup-hybrid-mobile-device-management-mdm-with-system-center-configuration-manager-and-microsoft-intune"></a>System Center Configuration Manager 및 Microsoft Intune을 사용하여 하이브리드 MDM(모바일 장치 관리) 설정

*적용 대상: System Center Configuration Manager(현재 분기)*


Configuration Manager를 사용하여 iOS, Windows 및 Android 장치를 관리하려면 먼저 Intune에 등록해야 합니다. Configuration Manager 및 Intune을 사용하여 하이브리드 장치 등록을 설정하려면 다음 단계를 따르세요. 다음 단계를 완료하면 사용자에 대해 BYOD("Bring Your Own Device") 등록을 사용하도록 설정됩니다. 이 단계는 [BYOD 장치 등록](enroll-hybrid-ios-mac.md) 및 [회사 소유 장치 등록](enroll-company-owned-devices.md)의 필수 조건이기도 합니다.

 |단계|세부 정보|  
 |-----------|-------------|  
 |**1단계:** [MDM 컬렉션 만들기](create-mdm-collection.md)|해당 장치를 등록할 수 있는 사용자를 포함하는 Configuration Manager 사용자 컬렉션을 만듭니다.|  
 |**2단계:** [도메인 이름 요구 사항](confirm-dns.md)|조직의 DNS(도메인 이름 서비스) 및 Active Directory 사용자 관리가 MDM 요구 사항을 충족하는지 확인합니다.|
 |**3단계:** [Intune 구독 구성](configure-intune-subscription.md)|Intune 서비스를 사용하면 인터넷을 통해 장치를 관리할 수 있습니다.|  
 |**4단계:** [계약조건 추가](terms-and-conditions.md)| 회사 포털 앱을 사용하기 전에 사용자가 동의해야 하는 계약조건을 만듭니다.|
 |**5단계:** [서비스 연결 지점 만들기](create-service-connection-point.md)|서비스 연결 지점은 설정과 소프트웨어 배포 정보를 Configuration Manager에 전송하고 모바일 장치에서 상태 및 인벤토리 메시지를 검색합니다. |  
 |**6단계:** [플랫폼 등록 사용](enable-platform-enrollment.md)|iOS 및 Windows 장치에 대한 MDM 등록에는 서비스와 장치 간의 통신을 위한 추가 단계가 필요합니다. Android에는 추가 구성이 필요하지 않습니다.|  
 |**7단계:** [추가 관리 설정](set-up-additional-management.md)|(선택 사항) 등록된 장치에 대한 구성 항목 및 조건부 액세스를 설정합니다.|
 |**8단계:** [MDM 구성 확인](verify-mdm-configuration.md)|로그 파일을 보고 서비스 연결 지점이 성공적으로 만들어졌는지, 그리고 사용자 계정이 동기화되고 있는지 확인합니다.|

Configuration Manager 없이 Intune을 사용하고 싶으세요?
> [!div class="button"]
[Intune 문서 보기 >](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune)


## <a name="enroll-devices"></a>장치 등록
하이브리드 설치가 완료된 후 Configuration Manager에서 다음과 같은 다양한 방법으로 장치를 등록할 수 있습니다.
- **회사 소유(COD) 장치:** [회사 소유 장치 등록](enroll-company-owned-devices.md)에서는 회사 소유 장치를 등록하는 다양한 플랫폼별 방법에 대한 지침을 제공합니다.
- **사용자 소유(BYOD) 장치:** [사용자 소유(BYOD) 장치 등록](enroll-hybrid-ios-mac.md)에서는 사용자 소유 장치를 등록하는 방법에 대한 지침을 제공합니다.
