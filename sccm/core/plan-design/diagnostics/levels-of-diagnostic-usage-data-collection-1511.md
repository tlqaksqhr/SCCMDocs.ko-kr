---
title: "1511에 대한 진단 데이터 | System Center Configuration Manager"
description: "System Center Configuration Manager 버전 1511에서 수집하는 진단 및 사용 현황 데이터에 대해 알아봅니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-other
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 9e614ae1-47d2-4a93-ba0a-89dc50d1e266
caps.latest.revision: 4
author: Brenduns
ms.author: brenduns
manager: angrobe
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- hu-hu
- it-it
- ja-jp
- ko-kr
- nl-nl
- pl-pl
- pt-br
- pt-pt
- ru-ru
- sv-se
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 3488efcd6638b538f05fae52dfd8918423a32b58

---
# <a name="levels-of-diagnostic-usage-data-collection-for-version-1511-of-system-center-configuration-manager"></a>System Center Configuration Manager 버전 1511에 대한 진단 사용 현황 데이터 수집의 수준

*적용 대상: System Center Configuration Manager(현재 분기)*

System Center Configuration Manager 버전 1511에서는 **기본**, **고급**, **전체** 등 세 가지 수준의 진단 및 사용 현황 데이터를 수집합니다. 기본적으로 이 기능은 고급 수준으로 설정되어 있습니다. 다음 섹션은 각 수준에서 수집되는 데이터에 대한 추가 세부 정보를 제공합니다.  

> [!IMPORTANT]  
>  Configuration Manager에서는 기본 또는 고급 수준에서 사이트 코드 또는 사이트 이름, IP 주소, 사용자 또는 컴퓨터 이름, 실제 주소 또는 메일 주소를 수집하지 않습니다. 전체 수준에서 이 정보가 수집되는 경우가 있어도 이는 특별한 목적이 있는 것은 아니며(잠재적으로 로그 파일 또는 메모리 스냅숏과 같은 고급 진단 정보에 포함됨) Microsoft에서는 이러한 정보를 사용자 식별, 연락 또는 광고 목적으로 사용하지 않습니다.  

##  <a name="a-namebkmkchangea-how-to-change-the-level"></a><a name="bkmk_change"></a> 수준을 변경하는 방법  
 **사이트** 개체 클래스에 대한 **수정** 권한이 포함된 역할 기반 관리 범위를 가진 관리자는 Configuration Manager 콘솔의 진단 및 사용 현황 데이터 설정에서 수집된 데이터의 수준을 변경할 수 있습니다.  

##  <a name="a-namebkmklevel1a-level-1---basic"></a><a name="bkmk_level1"></a> 수준 1 - 기본  
 기본 수준에는 계층 구조에 대한 데이터가 포함되어 있으며, 설치 환경이나 업그레이드 환경을 개선하고 계층 구조에 적용할 수 있는 Configuration Manager 업데이트를 확인하는 데 필요합니다.  

 System Center Configuration Manager 버전 1511부터 이 수준에는 다음이 포함됩니다.  


-   설치 정보(빌드, 설치 유형, 언어 팩, 사용하도록 설정한 기능, 업데이트 팩 배포 상태 및 오류)  

-   데이터베이스 성능 메트릭(복제 처리 정보, 디스크 사용 현황 및 프로세서에 따른 상위 SQL Server 저장 프로시저)  

-   기본 데이터베이스 구성(프로세서, 클러스터 구성, 분산 보기 구성)  

-   Configuration Manager 데이터베이스 스키마(모든 개체 정의의 해시)  

-   Configuration Manager 클라이언트 버전 및 운영 체제 버전 개수  

-   관리되는 장치의 운영 체제 및 Exchange Connector에서 설정한 정책 개수  

-   로캘 및 클라이언트 언어 개수  

-   분기 및 빌드별 Windows 10 장치 개수  

-   기본 Configuration Manager 사이트 계층 구조 데이터(사이트 목록, 유형, 버전, 상태, 클라이언트 수 및 표준 시간대)  

-   기본 사이트 시스템 서버 정보(사용되는 사이트 시스템 역할, 인터넷 및 SSL 상태, 운영 체제, 프로세서, 실제 또는 가상 컴퓨터)  

-   기본 사용자 검색 통계(사용자 검색 횟수, 최소/최대/평균 그룹 크기)  

-   기본 Endpoint Protection 정보(맬웨어 방지 클라이언트 버전)  

-   기본 응용 프로그램 및 배포 유형 수(총 앱, 여러 배포 유형을 사용하는 총 앱, 종속성을 가진 총 앱, 총 교체된 앱, 사용 중인 배포 기술 개수)  

-   기본 OSD 수(이미지)  

-   배포 지점, 관리 지점 유형 및 기본 구성 정보(보호됨, 미리 구성됨, PXE, 멀티캐스트, SSL 상태, 풀/피어 배포 지점, MDM 사용, SSL 사용 등)  

-   원격 분석 통계(실행, 런타임, 오류 시)  

##  <a name="a-namebkmklevel2a-level-2---enhanced"></a><a name="bkmk_level2"></a> 수준 2 - 고급  
고급 수준에는 기본적으로 다음과 같은 설정이 있습니다. 이 수준은 기본 수준에서 수집한 데이터 외에 기능별 데이터(사용 빈도 및 기간), Configuration Manager 클라이언트 설정(구성 요소 이름, 상태 및 폴링 간격과 같은 특정 설정) 및 소프트웨어 업데이트에 대한 기본 정보를 포함합니다.  

이 수준에 포함된 정보는 Microsoft에서 향후 개선된 제품 및 서비스를 제공하기 위해 필요한 최소한의 데이터로 유용하게 사용할 수 있기 때문에 이 수준을 사용하는 것이 권장됩니다. 이 수준에서는 개체 이름(사이트, 사용자, 컴퓨터 또는 개체), 보안 관련 개체의 세부 정보 또는 소프트웨어 업데이트가 필요한 시스템 개수와 같은 취약성은 수집하지 않습니다.  

System Center Configuration Manager 버전 1511부터 이 수준에는 다음이 포함됩니다.  

-   **응용 프로그램 관리:**  

    -   기본 사용 현황/조직 내에서 사용되는 배포 유형에 대한 대상 정보(대상이 되는 사용자 대 장치, 필요 대 가능)  

    -   응용 프로그램 배포 정보(설치/제거, 승인 필요, 사용자 조작 사용/사용 안 함)  

    -   사용 가능한 응용 프로그램 요청 통계  

    -   유형별 패키지 개수  

    -   운영 체제별 응용 프로그램 적용 가능성 개수  

    -   패키지/프로그램 배포 개수  

    -   App-V 환경 및 배포 속성 개수  

    -   Windows 10 사용이 허가된 응용 프로그램 라이선스 개수  

    -   사용자/장치별 응용 프로그램 배포의 최소/최대/평균 수  

    -   유지 관리 기간 유형 및 지속 시간  

-   **클라이언트:**  

    -   사용하도록 설정된 클라이언트 에이전트 목록/개수  

    -   각 원본 위치 유형의 클라이언트 설치 개수  

    -   클라이언트 설치 오류 개수  

-   **준수 설정:**  

    -   유형별 구성 항목 개수  

    -   기본 구성 기준 정보(개수, 배포 수 및 참조 수)  

    -   기본 제공 설정을 참조하는 배포 개수(설정 값은 캡처되지 않음)  

    -   사용자 지정 설정에 대해 만들어진 규칙 및 배포 개수  

    -   배포된 단순 인증서 등록 프로토콜 템플릿 개수  

-   **콘텐츠:**  

    -   유형별 경계 개수  

    -   경계 그룹 정보(각 경계 그룹에 할당된 경계 및 사이트 시스템 개수)  

    -   배포 지점 그룹 정보(각 배포 지점 그룹에 할당된 패키지 및 배포 지점 개수)  

    -   배포 지점 구성 정보(분기 캐시 사용, 배포 지점 모니터링)  

    -   배포 관리자 구성 정보(스레드, 다시 시도 지연, 다시 시도 횟수, 풀 배포 지점 설정)  

-   **Endpoint Protection:**  

    -   Endpoint Protection 맬웨어 방지 및 Windows 방화벽 정책 사용 현황(그룹에 할당된 고유 정책 수, 정책에 포함된 설정 정보는 포함되지 않음)  

    -   Endpoint Protection 배포 오류(Endpoint protection 정책 배포 오류 코드 개수)  

    -   Endpoint Protection 대시보드에 표시하기 위해 선택한 컬렉션 개수  

    -   Endpoint Protection 기능에 대해 구성된 경고 개수  

-   **MAM(모바일 응용 프로그램 관리):**  

    -   운영 체제별 MAM 사용 Office 및 LOB(기간 업무) 응용 프로그램과 정책 개수  

    -   MAM 응용 프로그램/정책 배포 개수  

    -   MAM 설정당 만들어진 규칙 개수  

-   **MDM(모바일 장치 관리):**  

    -   실행된 모바일 장치 작업(잠금, 핀 다시 설정, 초기화, 사용 중지) 명령 개수  

    -   Configuration Manager 및 Microsoft Intune에서 관리되는 모바일 장치 개수 및 등록 방법(대량, 사용자 기반)  

    -   모바일 장치 폴링 일정 및 통계 모바일 장치 체크 인 기간  

    -   모바일 장치 정책 개수  

    -   등록된 여러 모바일 장치를 사용하는 사용자 개수  

-   **Microsoft Intune 문제 해결:**  

    -   상태(state), 상태(status), 인벤토리, RDR, DDR, UDX, 테넌트 상태, POL, LOG, Cert, CRP, Resync, CFD, RDO, BEX, ISM 개수와 크기 및 Microsoft Intune에서 다운로드된 준수 메시지  

    -   장치 작업(초기화, 사용 중지, 잠금) 개수와 크기, 원격 분석 및 Microsoft Intune에 복제된 데이터 메시지  

    -   Microsoft Intune에 대한 전체 및 델타 사용자 동기화 통계  

-   **온-프레미스 MDM(모바일 장치 관리):**  

    -   온-프레미스 MDM 응용 프로그램 배포에 대한 배포 성공/실패 통계  

    -   Windows 10 대량 등록 패키지 및 프로필 개수  

-   **운영 체제 배포:**  

    -   부팅 이미지, 드라이버, 드라이버 패키지, 멀티캐스트 사용 배포 지점, PXE 사용 배포 지점 및 작업 순서 개수  

-   **소프트웨어 업데이트:**  

    -   소프트웨어 업데이트를 배포한 컬렉션의 총/평균 수 및 배포된 업데이트의 최대/평균 수  

    -   동기화에 연결된 자동 배포 규칙 수  

    -   업데이트를 새로 만들거나 기존 그룹에 추가하는 자동 배포 규칙 수  

    -   자동 배포 규칙에 사용된 사용 가능한 델타 및 최종 기한 델타  

    -   업데이트당 할당의 평균 및 최대 수  

    -   System Center Update Publisher로 만들고 배포한 업데이트 개수  

    -   업데이트 그룹 및 할당 개수  

    -   업데이트 패키지 개수 및 패키지를 사용하여 대상으로 지정된 배포 지점의 최대/최소/평균 수  

    -   업데이트 그룹 수 및 그룹당 업데이트의 최소/최대/평균 수  

    -   배포, 만료, 교체, 다운로드 및 EULA 포함 업데이트 수 및 백분율  

    -   업데이트 검사 오류 코드 및 컴퓨터 수  

    -   클라이언트 업데이트 평가 및 검사 일정  

    -   소프트웨어 업데이트 지점 동기화 일정  

    -   여러 배포에서 자동 배포 규칙 수  

    -   활성 Windows 10 서비스 계획에 사용되는 구성  

    -   Windows 10 대시보드 콘텐츠 버전  

    -   비즈니스용 Windows 업데이트를 사용하는 Windows 10 클라이언트 개수  

    -   클러스터 패치 통계  

    -   배포된 Office 365 업데이트 개수  

-   **SQL/성능 데이터:**  

    -   가장 큰 데이터베이스 테이블 개수  

    -   SQL Always-On 복제본 정보  

    -   유형별 컬렉션 개수  

##  <a name="a-namebkmklevel3a-level-3---full"></a><a name="bkmk_level3"></a> 수준 3 - 전체  
전체 수준은 기본 및 고급 수준의 모든 데이터를 포함합니다. 또한 Endpoint Protection, 업데이트 준수 비율 및 소프트웨어 업데이트 정보에 대한 추가 정보를 포함합니다.  또한 이 수준은 캡처 시점의 메모리 또는 로그 파일에 있던 개인 정보를 포함할 수도 있는 시스템 파일 및 메모리 스냅숏과 같은 고급 진단 정보를 포함할 수 있습니다.  

System Center Configuration Manager 버전 1511부터 이 수준에는 다음이 포함됩니다.  

-   컬렉션 평가 및 새로 고침 통계  

-   Endpoint Protection 상태 요약(보호된 클라이언트, 위험한 클라이언트, 알 수 없는 클라이언트, 지원되지 않는 클라이언트 개수 포함)  

-   Endpoint Protection 정책 구성  

-   소프트웨어 업데이트 배포 정보(클라이언트에서 대상으로 지정된 배포의 비율 대 UTC 시간, 필수 대 선택 사항 대 자동, 다시 부팅 제거)  

-   소프트웨어 업데이트 배포의 전반적인 준수  

-   자동 배포 규칙 평가 일정 정보  

-   네트워크 액세스 보호 정책을 사용하는 클라이언트 수  

-   소프트웨어 업데이트 배포 오류 코드 및 개수  

-   소프트웨어 업데이트 배포 컬렉션에서 비활성 클라이언트의 최소/최대/평균 수  

-   소프트웨어 업데이트가 만료된 그룹 개수  

-   패키지당 소프트웨어 업데이트의 최소/최대/평균 수  

-   소프트웨어 업데이트 검사 성공 비율  

-   마지막 소프트웨어 업데이트 검사 이후 최소/최대/평균 시간 수  



<!--HONumber=Nov16_HO1-->

