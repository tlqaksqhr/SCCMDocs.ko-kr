---
title: "미디어 캡처 만들기 | Configuration Manager"
description: "작업 순서 미디어 만들기 마법사를 사용하여 Configuration Manager에서 미디어 캡처를 만들면 참조 컴퓨터에서 운영 체제 이미지를 캡처할 수 있습니다."
ms.custom: na
ms.date: 10/06/2016
ms.prod: configuration-manager
ms.reviewer: na
ms.suite: na
ms.technology:
- configmgr-osd
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 10eb8958-3848-49d7-95c0-16119b624580
caps.latest.revision: 11
caps.handback.revision: 0
author: Dougeby
ms.author: dougeby
manager: angrobe
translationtype: Human Translation
ms.sourcegitcommit: 1134bb2f04152288e72d40b1b1083f415cb4e900
ms.openlocfilehash: 604844d073ca3caedbbfc77d76cb3368965980af


---
# <a name="create-capture-media-with-system-center-configuration-manager"></a>System Center Configuration Manager에서 미디어 캡처 만들기

*적용 대상: System Center Configuration Manager(현재 분기)*

Configuration Manager의 미디어 캡처를 사용하면 참조 컴퓨터에서 운영 체제 이미지를 캡처할 수 있습니다. 다음 시나리오에서는 미디어 캡처를 사용합니다.  

-   [운영 체제를 캡처하는 작업 순서 만들기](create-a-task-sequence-to-capture-an-operating-system.md)  

##  <a name="a-namebkmkcreatecapturemediaa-how-to-create-capture-media"></a><a name="BKMK_CreateCaptureMedia"></a> 미디어 캡처를 만드는 방법  
 미디어 캡처를 사용하여 참조 컴퓨터에서 운영 체제 이미지를 캡처할 수 있습니다. 미디어 캡처에는 참조 컴퓨터를 시작하는 부팅 이미지와, 운영 체제 이미지를 캡처하는 작업 순서가 포함되어 있습니다.

미디어 캡처는 작업 순서 미디어 만들기 마법사를 사용하여 만듭니다. 마법사를 실행하기 전에 다음 모든 조건이 충족되어야 합니다.  

|작업|설명|  
|----------|-----------------|  
|부팅 이미지|운영 체제를 캡처하는 작업 순서에서 사용할 부팅 이미지에 대한 다음 사항을 고려하세요.<br /><br /> -   부팅 이미지의 아키텍처는 대상 컴퓨터의 아키텍처에 적합해야 합니다. 예를 들어 x64 대상 컴퓨터는 x86 또는 x64 부팅 이미지를 부팅하고 실행할 수 있습니다. 그러나 x86 대상 컴퓨터는 x86 부팅 이미지만 부팅하고 실행할 수 있습니다.<br />-   부팅 이미지에 대상 컴퓨터를 프로비전하는 데 필요한 네트워크 드라이버와 대용량 저장소 드라이버가 포함되어 있어야 합니다.|  
|작업 순서와 관련된 모든 콘텐츠 배포|작업 순서에 필요한 모든 콘텐츠를 하나 이상의 배포 지점에 배포해야 합니다. 여기에는 부팅 이미지, 운영 체제 이미지 및 관련된 기타 파일이 포함됩니다. 마법사가 독립 실행형 미디어를 만들 때 배포 지점에서 정보를 수집합니다. 해당 배포 지점의 콘텐츠 라이브러리에 대한 **읽기** 권한이 있어야 합니다.  자세한 내용은 [콘텐츠 배포](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_distribute)를 참조하세요.|  
|이동식 USB 드라이브 준비|이동식 USB 드라이브:<br /><br /> 이동식 USB 드라이브를 사용하려는 경우 마법사가 실행되는 컴퓨터에 USB 장치를 연결해야 하며, Windows에서 USB 장치를 이동식 장치로 검색할 수 있어야 합니다. 마법사는 USB 드라이브에 직접 기록하여 미디어를 만듭니다.|  
|출력 폴더 만들기|CD/DVD 세트:<br /><br /> 작업 순서 미디어 만들기 마법사를 실행하여 CD 또는 DVD 세트에 미디어를 만들려면 먼저 마법사에서 생성할 출력 파일의 폴더를 만들어야 합니다. CD 또는 DVD 세트용 미디어를 만드는 경우 해당 폴더에 .iso 파일로 직접 기록됩니다.|  

 미디어 캡처를 만들려면 다음 절차를 따르세요.  

#### <a name="to-create-capture-media"></a>미디어 캡처를 만들려면  

1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리**를 클릭합니다.  

2.  **소프트웨어 라이브러리** 작업 영역에서 **운영 체제**를 확장하고 **작업 순서**를 클릭합니다.  

3.  **홈** 탭의 **만들기** 그룹에서 **작업 순서 미디어 만들기** 를 클릭하여 작업 순서 미디어 만들기 마법사를 시작합니다.  

4.  **미디어 유형 선택** 페이지에서 **미디어 캡처**를 선택한 후에 **다음**을 클릭합니다.  

5.  **미디어 유형** 페이지에서 미디어가 플래시 드라이브 또는 CD/DVD 세트인지를 지정하고 다음을 구성합니다.  

    -   **USB 플래시 드라이브**를 선택하는 경우 콘텐츠를 저장할 드라이브를 지정합니다.  

    -   **CD/DVD 세트**를 선택하는 경우 미디어 용량 및 출력 파일의 이름과 경로를 지정해야 합니다. 마법사에서 출력 파일을 이 위치에 기록합니다. 예: **\\\servername\folder\outputfile.iso**  

         미디어 용량이 부족하여 전체 콘텐츠를 저장하지 못하는 경우 파일이 여러 개 생성되며, 여러 CD 또는 DVD에 콘텐츠를 저장해야 합니다. 여러 미디어가 필요한 경우 Configuration Manager는 생성된 각 출력 파일의 이름에 일련 번호를 추가합니다. 또한 응용 프로그램과 함께 운영 체제를 배포하는 경우 응용 프로그램이 단일 미디어에 맞지 않는 경우 Configuration Manager는 여러 미디어를 사용하여 응용 프로그램을 저장합니다. 독립 실행형 미디어가 실행되는 경우 Configuration Manager는 응용 프로그램이 저장된 그다음 미디어를 삽입하라는 메시지를 표시합니다.  

        > [!IMPORTANT]  
        >  기존 .iso 이미지를 선택하는 경우 작업 순서 미디어 만들기 마법사는 다음 페이지로 진행된 후 바로 드라이브나 공유에서 해당 이미지를 삭제합니다. 기존 이미지는 이후에 마법사를 취소하는 경우라도 삭제됩니다.  

     **다음**을 클릭합니다.  

6.  **부팅 이미지** 페이지에서 다음 정보를 지정한 후에 **다음**을 클릭합니다.  

    > [!IMPORTANT]  
    >  지정하는 부팅 이미지의 아키텍처는 참조 컴퓨터의 아키텍처에 적합해야 합니다. 예를 들어 x64 참조 컴퓨터는 x86 또는 x64 부팅 이미지를 부팅하고 실행할 수 있습니다. 그러나 x86 참조 컴퓨터는 x86 부팅 이미지만 부팅하고 실행할 수 있습니다.  

    -   **부팅 이미지** 상자에서 참조 컴퓨터를 시작할 부팅 이미지를 지정합니다.  

    -   **배포 지점** 상자에서 부팅 이미지가 있는 배포 지점을 지정합니다. 마법사는 배포 지점에서 부팅 이미지를 검색하여 미디어에 기록합니다.  

        > [!NOTE]  
        >  배포 지점의 콘텐츠 라이브러리에 대한 읽기 액세스 권한이 있어야 합니다.  

7.  마법사를 완료합니다.  



<!--HONumber=Nov16_HO1-->

