---
title: Surface 장치 대시보드
titleSuffix: Configuraton Manager
description: 대시보드를 사용하여 Surface 장치에 대한 정보를 검토합니다.
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.date: 03/22/2018
ms.topic: conceptual
ms.prod: configuration-manager
ms.technology: configmgr-client
ms.assetid: 7397fc17-3ae8-4525-8386-aea8a9cffa06
ms.openlocfilehash: db5df73db6a973ca689def785ee99a40425303fa
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="surface-device-dashboard-in-system-center-configuration-manager"></a>System Center Configuration Manager의 Surface 장치 대시보드

*적용 대상: System Center Configuration Manager(현재 분기)*

1802 버전부터 Surface 장치 대시보드는 사용자 환경에서 Surface 장치에 대한 정보를 한거번에 제공합니다. <!--1355788-->

## <a name="open-the-surface-device-dashboard"></a>Surface 장치 대시보드 열기

Surface 장치 대시보드를 열려면 다음 단계를 사용합니다. 

1. Configuration Manager 콘솔을 엽니다. 
2. **모니터링** 노드를 클릭합니다. 
3. 대시보드를 로드하려면 **Surface 장치**를 클릭합니다.

**Surface 장치 대시보드**
![Surface 장치 대시보드](media\Surface-device-dashboard.PNG)



## <a name="reviewing-information-in-the-surface-device-dashboard"></a>Surface 장치 대시보드의 정보 검토

Surface 장치 대시보드는 사용자 환경에 대한 세 개의 그래프를 보여줍니다. 

- **Surface 장치 백분율** - 환경 전체에서 Surface 장치의 백분율을 제공합니다.

    ![Surface 장치 백분율 그래프](media\Percent-Surface-Devices.PNG)
- **Surface 모델** - Surface 모델당 장치 수를 표시합니다. 
    - 그래프 섹션을 마우스로 가리키면 선택한 모델인 Surface 장치의 백분율을 제공합니다. 

         ![Surface 모델 그래프](media\Surface-Models-Hover.PNG)
    - 그래프 섹션을 클릭하면 모델에 대한 장치 목록으로 이동합니다. 
        ![Surface 모델 장치 목록](media\Surface-Model-Device-List.PNG)

- **상위 5개 펌웨어 버전** - 환경에서 상위 5개 펌웨어 모델을 포함한 차트를 표시합니다. 
    - 그래프 섹션을 마우스로 가리키면 선택한 펌웨어 버전인 Surface 장치 수를 제공합니다. 
       ![Surface 모델 장치 목록](media\Surface-Firmware-Hover.PNG)


## <a name="more-information"></a>추가 정보

Surface 장치에 대한 자세한 내용은 다음을 참조하세요.
 - [Surface]( https://go.microsoft.com/fwlink/?linkid=861998) 웹 사이트
    
Configuration Manager에서 Surface 펌웨어 업데이트를 배포하는 방법에 대한 자세한 내용은
 - [Configuration Manager에서 Surface 드라이버 업데이트를 관리하는 방법]( https://support.microsoft.com/help/4098906)을 참조하세요.




