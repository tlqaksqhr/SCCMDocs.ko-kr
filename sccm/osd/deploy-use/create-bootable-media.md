---
title: "부팅 가능한 미디어 만들기 | Configuration Manager"
description: "Configuration Manager에서 부팅 가능한 미디어를 사용하면 쉽게 새 버전의 Windows를 설치하거나 컴퓨터 및 전송 설정을 바꿀 수 있습니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: ead79e64-1b63-4d0d-8bd5-addff8919820
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 6a3b72ecdee38f6955b601248300e49c1ffdee5d


---
# <a name="create-bootable-media-with-system-center-configuration-manager"></a>System Center Configuration Manager에서 부팅 가능 미디어 만들기

*적용 대상: System Center Configuration Manager(현재 분기)*

Configuration Manager의 부팅 가능한 미디어에는 부팅 이미지, 선택적 시작 전 명령 및 관련 파일, Configuration Manager 파일이 포함되어 있습니다. 다음 운영 체제 배포 시나리오에 대해 사전 준비된 미디어를 사용합니다.  

-   [새 컴퓨터에 새 버전의 Windows 설치(완전 복구)](install-new-windows-version-new-computer-bare-metal.md)  

-   [기존 컴퓨터 바꾸기 및 설정 전송](replace-an-existing-computer-and-transfer-settings.md)  

##  <a name="a-namebkmkcreatebootablemediaa-create-bootable-media"></a><a name="BKMK_CreateBootableMedia"></a> 부팅 가능한 미디어 만들기  
 부팅 가능한 미디어로 부팅하면 대상 컴퓨터가 시작되고 네트워크에 연결한 다음 네트워크에서 지정된 작업 순서, 운영 체제 이미지 및 기타 필수 콘텐츠를 검색합니다. 작업 순서는 이 미디어에 포함되어 있지 않으므로 미디어를 다시 만들지 않고도 작업 순서나 콘텐츠를 변경할 수 있습니다. 부팅 가능한 미디어에서 패키지는 암호화되지 않습니다. 미디어에 암호를 추가하는 방법과 같은 적합한 보안 방법을 활용하여 권한 없는 사용자로부터 패키지 콘텐츠를 보호해야 합니다.  

 작업 순서 미디어 만들기 마법사를 사용하여 부팅 가능한 미디어를 만들기 전에 다음 조건을 모두 충족해야 합니다.  

|작업|설명|  
|----------|-----------------|  
|부팅 이미지|운영 체제를 배포하는 작업 순서에서 사용할 부팅 이미지에 대한 다음 사항을 고려하세요.<br /><br /> -   부팅 이미지의 아키텍처는 대상 컴퓨터의 아키텍처에 적합해야 합니다. 예를 들어 x64 대상 컴퓨터는 x86 또는 x64 부팅 이미지를 부팅하고 실행할 수 있습니다. 그러나 x86 대상 컴퓨터는 x86 부팅 이미지만 부팅하고 실행할 수 있습니다.<br />-   부팅 이미지에 대상 컴퓨터를 프로비전하는 데 필요한 네트워크 드라이버와 대용량 저장소 드라이버가 포함되어 있어야 합니다.|  
|운영 체제를 배포하는 작업 순서 만들기|부팅 가능한 미디어의 일부로 운영 체제를 배포하는 작업 순서를 지정해야 합니다. 새 작업 순서를 만드는 단계를 보려면 [운영 체제를 설치하는 작업 순서 만들기](../deploy-use/create-a-task-sequence-to-install-an-operating-system.md)를 참조하세요.|  
|작업 순서와 관련된 모든 콘텐츠 배포|작업 순서에 필요한 모든 콘텐츠를 하나 이상의 배포 지점에 배포해야 합니다. 여기에는 부팅 이미지 및 관련된 기타 시작 전 파일이 포함됩니다. 마법사는 부팅 가능한 미디어를 만들 때 배포 지점에서 정보를 수집합니다. 해당 배포 지점의 콘텐츠 라이브러리에 대한 **읽기** 권한이 있어야 합니다.  자세한 내용은 [콘텐츠 라이브러리 정보](../../core/plan-design/hierarchy/the-content-library.md)를 참조하세요.|  
|이동식 USB 드라이브 준비|이동식 USB 드라이브:<br /><br /> 이동식 USB 드라이브를 사용하려는 경우 마법사가 실행되는 컴퓨터에 USB 장치를 연결해야 하며, Windows에서 USB 장치를 이동식 장치로 검색할 수 있어야 합니다. 마법사는 USB 드라이브에 직접 기록하여 미디어를 만듭니다. 독립 실행형 미디어는 FAT32 파일 시스템을 사용합니다. 크기가 4GB 이상인 파일을 포함하는 USB 플래시 드라이브에 독립 실행형 미디어를 만들 수 없습니다.|  
|출력 폴더 만들기|CD/DVD 세트:<br /><br /> 작업 순서 미디어 만들기 마법사를 실행하여 CD 또는 DVD 세트에 미디어를 만들려면 먼저 마법사에서 생성할 출력 파일의 폴더를 만들어야 합니다. CD 또는 DVD 세트용 미디어를 만드는 경우 해당 폴더에 .iso 파일로 직접 기록됩니다.|  

 부팅 가능한 미디어를 만들려면 다음 절차를 따르세요.  

#### <a name="to-create-bootable-media"></a>부팅 가능한 미디어를 만들려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **홈** 탭의 **만들기** 그룹에서 **작업 순서 미디어 만들기** 를 클릭하여 작업 순서 미디어 만들기 마법사를 시작합니다.  

4.  **미디어 유형 선택** 페이지에서 다음 옵션을 지정한 후에 **다음**을 클릭합니다.  

    -   **부팅 가능한 미디어**를 선택합니다.  

    -   선택적으로, 사용자가 입력할 필요 없이 운영 체제를 배포만 하도록 허용하려면 **운영 체제 자동 배포 허용**을 선택합니다.  

        > [!IMPORTANT]  
        >  이 옵션을 선택하는 경우 사용자에게 네트워크 구성 정보나 선택적 작업 순서에 대해 묻지 않습니다. 단, 미디어에 암호 보호를 구성한 경우 사용자가 암호를 입력해야 합니다.  

5.  **미디어 관리** 페이지에서 다음 옵션 중 하나를 지정한 후에 **다음**을 클릭합니다.  

    -   사이트 경계의 클라이언트 위치에 따라 관리 지점에서 미디어를 다른 관리 지점으로 리디렉션할 수 있도록 하려면 **동적 미디어** 를 선택합니다.  

    -   미디어를 지정된 관리 지점에만 연결하려면 **사이트 기반 미디어** 를 선택합니다.  

6.  **미디어 유형** 페이지에서 미디어가 플래시 드라이브 또는 CD/DVD 세트인지를 지정하고 다음을 구성합니다.  

    > [!IMPORTANT]  
    >  독립 실행형 미디어는 FAT32 파일 시스템을 사용합니다. 크기가 4GB 이상인 파일을 포함하는 USB 플래시 드라이브에 독립 실행형 미디어를 만들 수 없습니다.  

    -   **USB 플래시 드라이브**를 선택하는 경우 콘텐츠를 저장할 드라이브를 지정합니다.  

    -   **CD/DVD 세트**를 선택하는 경우 미디어 용량 및 출력 파일의 이름과 경로를 지정해야 합니다. 마법사에서 출력 파일을 이 위치에 기록합니다. 예: **\\\servername\folder\outputfile.iso**  

         미디어 용량이 부족하여 전체 콘텐츠를 저장하지 못하는 경우 파일이 여러 개 생성되며, 여러 CD 또는 DVD에 콘텐츠를 저장해야 합니다. 여러 미디어가 필요한 경우 Configuration Manager는 생성된 각 출력 파일의 이름에 일련 번호를 추가합니다. 또한 응용 프로그램과 함께 운영 체제를 배포하는 경우 응용 프로그램이 단일 미디어에 맞지 않는 경우 Configuration Manager는 여러 미디어를 사용하여 응용 프로그램을 저장합니다. 독립 실행형 미디어가 실행되는 경우 Configuration Manager는 응용 프로그램이 저장된 그다음 미디어를 삽입하라는 메시지를 표시합니다.  

        > [!IMPORTANT]  
        >  기존 .iso 이미지를 선택하는 경우 작업 순서 미디어 만들기 마법사는 다음 페이지로 진행된 후 바로 드라이브나 공유에서 해당 이미지를 삭제합니다. 기존 이미지는 이후에 마법사를 취소하는 경우라도 삭제됩니다.  

     **다음**을 클릭합니다.  

7.  **보안** 페이지에서 다음 옵션을 지정한 후 **다음**을 클릭합니다.  

    -   미디어에서 Configuration Manager로 관리되지 않는 컴퓨터에 운영 체제를 배포할 수 있도록 하려면 **알 수 없는 컴퓨터 지원 사용** 확인란을 선택합니다. Configuration Manager 데이터베이스에 이러한 컴퓨터의 레코드가 없습니다.  

         알 수 없는 컴퓨터는 다음과 같습니다.  

        -   Configuration Manager 클라이언트가 설치되지 않은 컴퓨터  

        -   Configuration Manager로 가져오지 않은 컴퓨터  

        -   Configuration Manager에서 검색되지 않은 컴퓨터  

    -   미디어의 무단 액세스를 방지하도록 **암호로 미디어 보호** 확인란을 선택하고 강력한 암호를 입력합니다. 암호를 지정하면 사용자가 부팅 가능한 미디어를 사용하기 위해 암호를 입력해야 합니다.  

        > [!IMPORTANT]  
        >  부팅 가능한 미디어를 보호하기 위해 항상 암호를 지정하는 것이 좋습니다.  

    -   HTTP 통신의 경우 **자체 서명 미디어 인증서 만들기**를 선택한 다음 인증서의 시작 날짜와 만료 날짜를 지정합니다.  

    -   HTTPS 통신의 경우 **PKI 인증서 가져오기**를 선택한 다음 가져올 인증서와 해당 암호를 지정합니다.  

         부팅 이미지에 사용되는 이 클라이언트 인증서에 대한 자세한 내용은 [PKI 인증서 요구 사항](../../core/plan-design/network/pki-certificate-requirements.md)을 참조하세요.  

    -   **사용자 장치 선호도**: Configuration Manager에서 사용자 중심 관리를 지원하려면 미디어에서 사용자를 대상 컴퓨터와 연결하는 방식을 지정합니다. 운영 체제 배포에서 사용자 장치 선호도를 지원하는 방식에 대한 자세한 내용은 [사용자를 대상 컴퓨터에 연결](../get-started/associate-users-with-a-destination-computer.md)을 참조하세요.  

        -   미디어에서 사용자를 대상 컴퓨터와 자동으로 연결하도록 하려면 **자동 승인을 받는 사용자 장치 선호도 허용** 을 지정합니다. 이 기능은 운영 체제를 배포하는 작업 순서의 작업을 기반으로 합니다. 이 시나리오에서 작업 순서는 운영 체제를 대상 컴퓨터에 배포할 때 지정된 사용자와 대상 컴퓨터 사이의 관계를 만듭니다.  

        -   승인이 부여된 후에 미디어에서 사용자를 대상 컴퓨터와 자동으로 연결하도록 하려면 **관리자 승인을 보류 중인 사용자 장치 선호도 허용** 을 지정합니다. 이 기능은 운영 체제를 배포하는 작업 순서의 범위를 기반으로 합니다.  이 시나리오에서 작업 순서는 지정된 사용자와 대상 컴퓨터 사이의 관계를 만들지만 관리자의 승인을 기다렸다가 운영 체제를 배포합니다.  

        -   미디어에서 사용자를 대상 컴퓨터와 연결하지 않도록 하려면 **사용자 장치 선호도 허용 안 함** 을 지정합니다. 이 시나리오에서 작업 순서는 운영 체제를 배포할 때 사용자를 대상 컴퓨터와 연결하지 않습니다.  

8.  **부팅 이미지** 페이지에서 다음 옵션을 지정한 후 **다음**을 클릭합니다.  

    > [!IMPORTANT]  
    >  배포되는 부팅 이미지의 아키텍처는 대상 컴퓨터의 아키텍처에 적합해야 합니다. 예를 들어 x64 대상 컴퓨터는 x86 또는 x64 부팅 이미지를 부팅하고 실행할 수 있습니다. 그러나 x86 대상 컴퓨터는 x86 부팅 이미지만 부팅하고 실행할 수 있습니다.  

    -   **부팅 이미지** 상자에서 대상 컴퓨터를 시작할 부팅 이미지를 지정합니다.  

    -   **배포 지점** 상자에서 부팅 이미지가 있는 배포 지점을 지정합니다. 마법사는 배포 지점에서 부팅 이미지를 검색하여 미디어에 기록합니다.  

        > [!NOTE]  
        >  배포 지점의 콘텐츠 라이브러리에 대한 **읽기** 권한이 있어야 합니다.  

    -   마법사의 **미디어 관리** 페이지에서 사이트 기반 부팅 가능한 미디어를 만드는 경우 **관리 지점** 상자에서 기본 사이트의 관리 지점을 지정합니다.  

    -   마법사의 **미디어 관리** 페이지에서 동적 부팅 가능한 미디어를 만드는 경우 **관련된 관리 지점**상자에서 사용할 기본 사이트 관리 지점과 초기 통신의 우선 순위를 지정합니다.  

9. **사용자 지정** 페이지에서 다음 옵션을 지정한 후 **다음**을 클릭합니다.  

    -   작업 순서에서 운영 체제를 배포하는 데 사용하는 변수를 지정합니다.  

    -   작업 순서를 실행하기 전에 실행할 시작 전 명령을 지정합니다. 시작 전 명령은 작업 순서를 실행하여 운영 체제를 설치하기 전에 Windows PE의 사용자와 상호 작용할 수 있는 스크립트나 실행 파일입니다. 자세한 내용은 [작업 순서 미디어에 대한 시작 전 명령](../understand/prestart-commands-for-task-sequence-media.md)을 참조하세요.  

        > [!TIP]  
        >  작업 순서 미디어를 만드는 동안 작업 순서는 Configuration Manager 콘솔을 실행하는 컴퓨터의 CreateTSMedia.log 로그 파일에, 모든 작업 순서 변수의 값을 비롯하여 패키지 ID 및 시작 전 명령줄을 기록합니다. 이 로그 파일을 검토하여 작업 순서 변수의 값을 확인할 수 있습니다.  

         선택적으로, **시작 전 명령을 위한 파일 포함** 확인란을 선택하여 시작 전 명령의 필수 파일을 포함합니다.  

10. 마법사를 완료합니다.  

## <a name="next-steps"></a>다음 단계  
[부팅 가능한 미디어를 사용하여 네트워크를 통해 Windows 배포](use-bootable-media-to-deploy-windows-over-the-network.md)  



<!--HONumber=Nov16_HO1-->

