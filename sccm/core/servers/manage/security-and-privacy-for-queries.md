---
title: 쿼리에 대한 보안 및 개인 정보
titleSuffix: Configuration Manager
description: 사이트 데이터베이스에서 정보를 쿼리할 때 보안 및 개인 정보에 대한 모범 사례를 이해합니다.
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.technology: configmgr-other
ms.topic: conceptual
ms.assetid: 30080620-20d3-4c38-b8dd-db5516e1acae
author: aczechowski
manager: dougeby
ms.author: aaroncz
ms.openlocfilehash: 2d84385782df17d4019d6de65bcc7006aeab8b24
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="security-and-privacy-for-queries-in-system-center-configuration-manager"></a>System Center Configuration Manager에서 쿼리에 대한 보안 및 개인 정보

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager의 쿼리를 사용하여 지정하는 기준에 따라 사이트 데이터베이스에서 정보를 검색할 수 있습니다. Configuration Manager에서 표준 작업 중에 사이트 데이터베이스 정보를 수집합니다. 예를들어, 검색 또는 인벤토리에서 수집 된 정보를 사용 하 여 지정 된 조건을 충족 하는 장치를 식별 하는 쿼리를 구성할 수 있습니다.  

 쿼리에 대한 자세한 내용은 [System Center Configuration Manager의 쿼리 소개](../../../core/servers/manage/introduction-to-queries.md)를 참조하세요. 쿼리를 사용하여 검색할 수 있는 정보를 수집하는 Configuration Manager 작업에 대해 보안 모범 사례 및 개인 정보에 대한 자세한 내용은 [System Center Configuration Manager의 보안 및 개인 정보](../../../core/plan-design/security/security-and-privacy.md)를 참조하세요.  

## <a name="security-best-practices-for-queries"></a>쿼리에 대 한 보안 모범 사례  
 쿼리의 경우 다음 보안 모범 사례를 따르세요.  

|보안 모범 사례|추가 정보|  
|----------------------------|----------------------|  
|네트워크 위치에 저장된 쿼리를 가져오거나 내보내는 경우 해당 위치와 네트워크 채널을 보호합니다.|네트워크 폴더에 액세스할 수 있는 사용자를 제한합니다.<br /><br /> 쿼리 데이터를 가져오기 전에 공격자가 변조하지 못하도록 네트워크 위치와 사이트 서버 간에 SMB(서버 메시지 블록) 서명 또는 IPsec(인터넷 프로토콜 보안)을 사용합니다.|  

## <a name="see-also"></a>참고 항목  
 [System Center Configuration Manager에 대한 쿼리 기술 참조](../../../core/servers/manage/queries-technical-reference.md)
