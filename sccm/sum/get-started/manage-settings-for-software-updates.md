---

title: "소프트웨어 업데이트에 대한 설정 관리 | Configuration Manager"
description: "소프트웨어 업데이트 지점을 설치한 후 사이트에서 소프트웨어 업데이트에 적합한 클라이언트 설정을 알아봅니다."
keywords: 
author: dougeby
ms.author: dougeby
manager: angrobe
ms.date: 10/06/2016
ms.topic: article
ms.prod: configuration-manager
ms.service: 
ms.technology:
- configmgr-sum
ms.assetid: 0d484c1a-e903-4bff-9e9b-e452c62e38a8
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 4d7ffc12a3626f35a4481a3dcaed40abc0bbdac0


---

#  <a name="a-namebkmkmanagesusettingsa-manage-settings-for-software-updates"></a><a name="BKMK_ManageSUSettings"></a> 소프트웨어 업데이트 설정 관리  

*적용 대상: System Center Configuration Manager(현재 분기)*

Configuration Manager에서 소프트웨어 업데이트를 동기화한 후 다음 섹션에서 설정을 구성 및 확인합니다.

##  <a name="a-namebkmkclientsettingsa-client-settings-for-software-updates"></a><a name="BKMK_ClientSettings"></a> 소프트웨어 업데이트를 위한 클라이언트 설정  
소프트웨어 업데이트 지점을 설치하면 클라이언트에서 기본적으로 소프트웨어 업데이트를 사용할 수 있게 되고 클라이언트 설정의 **소프트웨어 업데이트** 페이지에 나오는 설정에는 기본값이 지정됩니다. 클라이언트 설정은 사이트 전체에 사용되며 소프트웨어 업데이트에서 준수를 검색할 시기 및 클라이언트 컴퓨터에 소프트웨어 업데이트를 설치하는 방법과 시기에 영향을 줍니다. 소프트웨어 업데이트를 배포하기 전에 클라이언트 설정이 사이트의 소프트웨어 업데이트에 적절한지 확인합니다.  

> [!IMPORTANT]  
>  **클라이언트에서 소프트웨어 업데이트 사용** 설정은 기본적으로 사용하도록 설정됩니다. 이 설정을 선택하지 않으면 Configuration Manager가 클라이언트에서 기존 배포 정책을 제거합니다.  

클라이언트 설정을 구성하는 방법에 대한 자세한 내용은 [클라이언트 설정을 구성하는 방법](../../core/clients/deploy/configure-client-settings.md)을 참조하세요.  

클라이언트 설정에 대한 자세한 내용은 [클라이언트 설정 정보](../../core/clients/deploy/about-client-settings.md)를 참조하세요.  

##  <a name="a-namebkmkgrouppolicya-group-policy-settings-for-software-updates"></a><a name="BKMK_GroupPolicy"></a> 소프트웨어 업데이트를 위한 그룹 정책 설정  
소프트웨어 업데이트 지점에서 실행되는 WSUS에 연결하기 위해 클라이언트 컴퓨터의 WUA(Windows Update 에이전트)에서 사용하는 특정 그룹 정책 설정이 있습니다. 이러한 그룹 정책 설정은 소프트웨어 업데이트 준수를 성공적으로 검사하고 소프트웨어 업데이트 및 WUA를 자동으로 업데이트하는 데에도 사용됩니다.

### <a name="specify-intranet-microsoft-update-service-location-local-policy"></a>인트라넷 Microsoft 업데이트 서비스 위치 지정 로컬 정책  
사이트에 소프트웨어 업데이트 지점을 만들면 클라이언트가 소프트웨어 업데이트 지점 서버 이름을 제공하는 컴퓨터 정책을 받고 컴퓨터에서 **인트라넷 Microsoft 업데이트 서비스 위치 지정** 로컬 정책을 구성합니다. WUA는 **인트라넷 업데이트 서비스에서 업데이트를 검색하도록 설정** 설정에 지정된 서버 이름을 검색한 다음 소프트웨어 업데이트 호환성을 검사할 때 이 서버에 연결합니다. **인트라넷 Microsoft 업데이트 서비스 위치 지정** 설정에 대한 도메인 정책이 만들어지면 이 도메인 정책이 로컬 정책을 덮어쓰고 WUA가 소프트웨어 업데이트 지점이 아닌 서버에 연결할 수 있습니다. 이렇게 될 경우 클라이언트가 여러 제품, 분류 및 언어에 따라 소프트웨어 업데이트 호환성을 검사할 수 있습니다. 그러므로 클라이언트 컴퓨터에 대한 Active Directory 정책을 구성하면 안 됩니다.  

### <a name="allow-signed-content-from-intranet-microsoft-update-service-location-group-policy"></a>인트라넷 Microsoft 업데이트 서비스 위치 그룹 정책에서 서명된 콘텐츠 허용  
컴퓨터의 WUA가 System Center Updates Publisher를 사용하여 만들고 게시한 소프트웨어 업데이트를 검사하기 전에 **인트라넷 Microsoft 업데이트 서비스 위치에서 서명된 콘텐츠 허용** 그룹 정책 설정을 사용하도록 설정해야 합니다. 이 정책 설정을 사용하도록 설정하면 소프트웨어 업데이트가 로컬 컴퓨터의 **신뢰할 수 있는 게시자** 인증서 저장소에서 서명된 경우 WUA가 인트라넷 위치를 통해 받은 소프트웨어 업데이트를 허용합니다. Updates Publisher에 필요한 그룹 정책 설정에 대한 자세한 내용은 [Updates Publisher 2011 Documentation Library(Updates Publisher 2011 문서 라이브러리)](http://go.microsoft.com/fwlink/p/?LinkId=232476)를 참조하세요.  

### <a name="automatic-updates-configuration"></a>자동 업데이트 구성  
자동 업데이트를 사용하면 클라이언트 컴퓨터에서 보안 업데이트 및 다른 중요한 다운로드를 받을 수 있습니다. 자동 업데이트는 **자동 업데이트 구성** 그룹 정책 설정이나 로컬 컴퓨터의 제어판을 통해 구성됩니다. 자동 업데이트를 사용하도록 설정하면 클라이언트 컴퓨터에서 업데이트 알림을 받고 구성된 설정에 따라 필수 업데이트를 다운로드하고 설치합니다. 자동 업데이트를 소프트웨어 업데이트와 함께 사용하면 각 클라이언트 컴퓨터에서 동일한 업데이트에 대해 알림 아이콘 및 팝업 표시를 나타낼 수 있습니다. 그리고, 다시 시작해야 하는 경우 각 클라이언트 컴퓨터에서 동일한 업데이트에 대해 다시 시작 대화 상자도 표시할 수 있습니다.  

### <a name="self-update"></a>자동 업데이트  
클라이언트 컴퓨터에서 자동 업데이트를 사용하도록 설정하면 최신 버전을 사용할 수 있는 경우나 WUA 구성 요소에 문제가 있는 경우에 WUA가 자동으로 자동 업데이트를 수행합니다. 자동 업데이트를 구성하지 않았거나 사용하지 않도록 설정한 경우 클라이언트 컴퓨터에 이전 버전의 WUA가 있으면 클라이언트 컴퓨터에서 WUA 설치 파일을 실행해야 합니다.  

## <a name="software-updates-properties"></a>소프트웨어 업데이트 속성
소프트웨어 업데이트 속성은 소프트웨어 업데이트 및 관련 콘텐츠에 대한 정보를 제공합니다. 또한 이러한 속성을 사용하여 소프트웨어 업데이트에 대한 설정을 구성할 수도 있습니다. 여러 소프트웨어 업데이트에 대한 속성을 열면 **최대 실행 시간** 과 **사용자 지정 심각도** 탭만 표시됩니다.   

소프트웨어 업데이트 속성을 열려면 다음 절차를 따르세요.  

#### <a name="to-open-software-update-properties"></a>소프트웨어 업데이트 속성을 열려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  
2.  소프트웨어 라이브러리 작업 영역에서 **소프트웨어 업데이트**를 확장하고 **모든 소프트웨어 업데이트**를 클릭합니다.  
3.  하나 이상의 소프트웨어 업데이트를 선택한 후에 **홈** 탭의 **속성** 그룹에서 **속성** 을 클릭합니다.  

   > [!NOTE]  
   >  **모든 소프트웨어 업데이트** 노드에서 Configuration Manager는 지난 30일 이내에 배포되고 **위험** 및 **보안**으로 분류된 소프트웨어 업데이트만 표시합니다.  

###  <a name="a-namebkmksoftwareupdatesinformationa-review-software-updates-information"></a><a name="BKMK_SoftwareUpdatesInformation"></a> 소프트웨어 업데이트 정보 검토  
소프트웨어 업데이트 속성에서는 소프트웨어 업데이트에 대한 자세한 정보를 검토할 수 있습니다. 둘 이상의 소프트웨어 업데이트를 선택할 경우 자세한 정보가 표시되지 않습니다. 다음 섹션에서는 선택한 소프트웨어 업데이트에 대해 사용할 수 있는 정보를 설명합니다.  

####  <a name="a-namebkmksoftwareupdatedetailsa-software-update-details"></a><a name="BKMK_SoftwareUpdateDetails"></a> 소프트웨어 업데이트 정보  
**업데이트 세부 정보** 탭에서 선택한 소프트웨어 업데이트에 대한 다음 요약 정보를 볼 수 있습니다.  

- **공지 ID**: 보안 소프트웨어 업데이트와 연결된 공지 ID를 지정합니다. [Microsoft Security Bulletin Search(Microsoft 보안 공지 검색)](http://go.microsoft.com/fwlink/p/?LinkId=58313) 웹 페이지에서 공지 ID를 검색하여 보안 공지 세부 정보를 찾을 수 있습니다.  

- **문서 ID**: 소프트웨어 업데이트에 대한 문서 ID를 지정합니다. 참조된 문서에서는 소프트웨어 업데이트 및 소프트웨어 업데이트로 수정되거나 개선된 문제에 대해 좀더 자세한 정보를 제공합니다.  

- **수정 날짜**: 소프트웨어 업데이트를 마지막으로 수정한 날짜를 지정합니다.  

- **최대 심각도 등급**: 소프트웨어 업데이트에 대해 공급업체 정의 심각도 등급을 지정합니다.  

- **설명**: 소프트웨어 업데이트로 수정되고 개선되는 조건에 대해 간략히 설명합니다.  

- **사용 가능한 언어**: 소프트웨어 업데이트가 적용되는 언어를 나열합니다.  

- **영향 받는 제품**: 소프트웨어 업데이트가 적용되는 제품을 나열합니다.  

####  <a name="a-namebkmkcontentinformationa-content-information"></a><a name="BKMK_ContentInformation"></a> 콘텐츠 정보  
**콘텐츠 정보** 탭에서 선택한 소프트웨어 업데이트와 연결된 콘텐츠에 대해 다음 정보를 검토합니다.  

-   **콘텐츠 ID**: 소프트웨어 업데이트에 대한 콘텐츠 ID를 지정합니다.  

-   **다운로드됨**: Configuration Manager에서 소프트웨어 업데이트 파일을 다운로드했는지 여부를 나타냅니다.  

-   **언어**: 소프트웨어 업데이트에 대한 언어를 지정합니다.  

-   **원본 경로**: 소프트웨어 업데이트 원본 파일에 대한 경로를 지정합니다.  

-   **크기(MB)**: 소프트웨어 업데이트 원본 파일의 크기를 지정합니다.  

####  <a name="a-namebkmkcustombundleinformationa-custom-bundle-information"></a><a name="BKMK_CustomBundleInformation"></a> 사용자 지정 번들 정보  
**사용자 지정 번들 정보** 탭에서 소프트웨어 업데이트에 대한 사용자 지정 번들 정보를 검토합니다. 선택한 소프트웨어 업데이트가 소프트웨어 업데이트 파일에 포함된 번들 소프트웨어 업데이트를 포함하는 경우 이 번들 소프트웨어 업데이트는 **번들 정보** 섹션에 표시됩니다. 이 탭에는 여러 언어에 대한 업데이트 파일과 같이 **콘텐츠 정보** 탭에 표시되는 번들 소프트웨어 업데이트는 나타나지 않습니다.  

####  <a name="a-namebkmksupersedenceinformationa-supersedence-information"></a><a name="BKMK_SupersedenceInformation"></a> 대체 정보  
**교체 정보** 탭에서 소프트웨어 업데이트의 교체에 대한 다음 정보를 확인할 수 있습니다.  

- **이 업데이트는 다음 업데이트로 교체됨**: 이 업데이트를 교체하는 소프트웨어 업데이트를 지정합니다. 즉 나열된 업데이트가 더 최신 버전입니다. 대부분의 경우 소프트웨어 업데이트를 교체하는 소프트웨어 업데이트 중 하나를 배포합니다. 목록에 표시되는 소프트웨어 업데이트에는 소프트웨어 업데이트에 대해 더 자세한 정보를 보여 주는 웹 페이지의 하이퍼링크가 포함되어 있습니다. 이 업데이트가 교체되지 않으면 **없음** 이 표시됩니다.  

- **이 업데이트는 다음 업데이트를 교체함**: 이 소프트웨어 업데이트로 교체되는 소프트웨어 업데이트를 지정합니다. 즉 이 소프트웨어 업데이트가 더 최신 버전입니다. 대부분의 경우 교체되는 소프트웨어 업데이트를 바꾸기 위해 이 소프트웨어 업데이트를 배포합니다. 목록에 표시되는 소프트웨어 업데이트에는 소프트웨어 업데이트에 대해 더 자세한 정보를 보여 주는 웹 페이지의 하이퍼링크가 포함되어 있습니다. 이 업데이트로 다른 어느 업데이트도 교체되지 않으면 **없음** 이 표시됩니다.  

###  <a name="a-namebkmksoftwareupdatessettingsa-configure-software-updates-settings"></a><a name="BKMK_SoftwareUpdatesSettings"></a> 소프트웨어 업데이트 설정 구성  
속성에서 하나 이상의 소프트웨어 업데이트에 대한 소프트웨어 업데이트 설정을 구성할 수 있습니다. 대부분의 소프트웨어 업데이트 설정은 중앙 관리 사이트 또는 독립 실행형 기본 사이트에서만 구성할 수 있습니다. 다음 섹션에서는 소프트웨어 업데이트에 대한 설정을 구성하는 방법에 대해 설명합니다.  

####  <a name="a-namebkmksetmaxruntimea-set-maximum-run-time"></a><a name="BKMK_SetMaxRunTime"></a> 최대 실행 시간 설정  
**최대 실행 시간** 탭에서 소프트웨어 업데이트가 클라이언트 컴퓨터에 할당되어 완료되는 최대 시간을 설정합니다. 업데이트가 최대 실행 시간 값보다 더 오래 걸리면 Configuration Manager에서는 상태 메시지를 만들고 소프트웨어 업데이트 설치를 위한 배포에 대해 모니터링을 중지합니다. 이 설정은 중앙 관리 사이트 또는 독립 실행형 기본 사이트에서만 구성할 수 있습니다.  

Configuration Manager에서는 이 설정을 사용하여, 구성된 유지 관리 기간 안에 소프트웨어 업데이트 설치를 시작할 것인지 여부를 결정합니다. 최대 실행 시간 값이 유지 관리 기간 중 남은 가용 기간보다 더 크면 소프트웨어 업데이트 설치는 다음 유지 관리 기간이 시작될 때까지 연기됩니다. 유지 관리 기간이 구성된 클라이언트 컴퓨터에 여러 소프트웨어 업데이트를 설치해야 할 경우 최대 실행 시간이 가장 적은 소프트웨어 업데이트가 먼저 설치되고 최대 실행 시간이 다음으로 적은 소프트웨어 업데이트가 그 후 차례로 설치됩니다. 클라이언트는 각 소프트웨어 업데이트를 설치하기 전에 가용 유지 관리 기간이 소프트웨어 업데이트를 설치하는 데 충분한지 확인합니다. 소프트웨어 업데이트는 설치가 시작되면 유지 관리 기간이 종료된 후에도 계속 설치가 진행됩니다. 유지 관리 기간에 대한 자세한 내용은 [System Center Configuration Manager에서 유지 관리 기간을 사용하는 방법](../../core/clients/manage/collections/use-maintenance-windows.md)을 참조하세요.  

**최대 실행 시간** 탭에서 다음 설정을 확인 및 구성할 수 있습니다.  

- **최대 실행 시간**: Configuration Manager에서 설치 모니터링을 중단하기 전에 소프트웨어 업데이트 설치를 완료할 수 있도록 할당되는 최대 시간(분)을 지정합니다. 이 설정은 유지 관리 기간이 종료되기 전에 업데이트를 설치할 수 있도록 가용 시간이 충분히 남아 있는지 확인하는 데도 사용됩니다. 기본 설정은 서비스 팩의 경우 60분이고 기타 모든 소프트웨어 업데이트 형식의 경우 5분입니다. 이 값의 범위는 5~9999분입니다.  

> [!IMPORTANT]  
>  최대 실행 시간 값은 구성된 유지 관리 기간 값보다 작게 설정해야 합니다. 그렇지 않으면 소프트웨어 업데이트 설치는 시작되지 않습니다.  

####  <a name="a-namebkmksetcustomseveritya-set-custom-severity"></a><a name="BKMK_SetCustomSeverity"></a> 사용자 지정 심각도 설정  
소프트웨어 업데이트에 대한 속성에서 **사용자 지정 심각도** 탭을 사용하면 소프트웨어 업데이트에 대한 사용자 지정 심각도 값을 구성할 수 있습니다. 미리 정의된 심각도 값이 특정 요구를 충족하지 못하면 이 작업이 필요할 수 있습니다. 사용자 지정 값은 Configuration Manager 콘솔의 **사용자 지정 심각도** 열에 나열됩니다. 소프트웨어 업데이트를 정의된 사용자 지정 심각도 값에 따라 정렬할 수 있고 이 값을 기준으로 필터링할 수 있는 쿼리 및 보고서를 만들 수도 있습니다. 이 설정은 중앙 관리 사이트 또는 독립 실행형 기본 사이트에서만 구성할 수 있습니다.  

**사용자 지정 심각도** 탭에서 다음 설정을 구성할 수 있습니다.  

- **사용자 지정 심각도**: 소프트웨어 업데이트에 대한 사용자 지정 심각도 값을 설정합니다. 목록에서 **위험**, **중요**, **보통**, **낮음** 등을 선택할 수 있습니다. 기본적으로 사용자 지정 심각도 값은 비어 있습니다.

## <a name="crl-checking-for-software-updates"></a>소프트웨어 업데이트에 대한 CRL 확인
기본적으로 System Center Configuration Manager 소프트웨어 업데이트의 서명을 확인할 때 CRL(인증서 해지 목록)은 확인되지 않습니다. 인증서가 사용될 때마다 CRL을 확인하면 해지된 인증서를 사용할 경우보다는 보안성이 향상되지만, 연결 지연이 발생할 수 있고 CRL 확인을 수행하는 컴퓨터에서 처리 부하가 증가합니다.  

CRL 확인이 사용되는 경우 소프트웨어 업데이트를 처리하는 Configuration Manager 콘솔에서 사용하도록 설정되어야 합니다.  

#### <a name="to-enable-crl-checking"></a>CRL 확인을 사용하려면  
CRL 확인을 수행하는 컴퓨터에서 제품 DVD를 사용하여 명령 프롬프트에서 **\SMSSETUP\BIN\X64\\**<*언어*>**\UpdDwnldCfg.exe /checkrevocation**을 실행합니다.  

예를 들어 영어(미국)의 경우 **\SMSSETUP\BIN\X64\00000409\UpdDwnldCfg.exe /checkrevocation**을 실행합니다.  



<!--HONumber=Nov16_HO1-->

