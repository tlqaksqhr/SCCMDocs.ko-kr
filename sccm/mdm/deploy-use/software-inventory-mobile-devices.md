---
title: Microsoft Intune에서 등록한 모바일 장치를 위한 소프트웨어 인벤토리
titleSuffix: Configuration Manager
description: Microsoft Intune에서 등록한 모바일 장치를 위한 소프트웨어 인벤토리
ms.date: 03/05/2017
ms.prod: configuration-manager
ms.technology: configmgr-hybrid
ms.topic: conceptual
ms.assetid: a0eae17a-60a8-4132-91af-0b10ad338c92
author: aczechowski
ms.author: aaroncz
manager: dougeby
ms.openlocfilehash: a1aa0bb03b2e27aebbbf1c080b32445bc7c58c47
ms.sourcegitcommit: 0b0c2735c4ed822731ae069b4cc1380e89e78933
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="software-inventory-for-mobile-devices-enrolled-with-microsoft-intune"></a>Microsoft Intune에서 등록한 모바일 장치를 위한 소프트웨어 인벤토리

*적용 대상: System Center Configuration Manager(현재 분기)*

 모바일 장치에 설치되는 앱에 대한 인벤토리를 수집할 수 있습니다. 인벤토리에 추가되는 앱은 장치가 회사 소유인지 또는 개인 소유인지에 따라 달라집니다. 개인 장치의 경우 Microsoft Intune에서 관리되는 앱만 인벤토리에 추가됩니다.  

> [!NOTE]  
>  모바일 장치에 설치된 앱의 인벤토리는 [하드웨어 인벤토리](mobile-device-hardware-inventory-hybrid.md) 프로세스의 일부로 수집됩니다.  

 다음은 개인 소유 또는 회사 소유의 장치에 대해 인벤토리에 포함되는 앱입니다.  

|플랫폼|개인 소유 장치|회사 소유 장치|  
|--------------|---------------------------------|--------------------------------|  
|Windows 10(Configuration Manager 클라이언트 없음)|관리되는 앱만|관리되는 앱만|
|Windows 8.1(Configuration Manager 클라이언트 없음)|관리되는 앱만|관리되는 앱만|  
|Windows Phone 8|관리되는 앱만|관리되는 앱만|  
|Windows RT|관리되는 앱만|관리되는 앱만|  
|iOS|관리되는 앱만|장치에 설치되는 모든 앱|  
|Android|관리되는 앱만|장치에 설치되는 모든 앱|  

소프트웨어 인벤토리를 사용 클라이언트 장치에서 파일 정보를 수집하는 방법에 대한 자세한 내용은 [소프트웨어 인벤토리 소개](../../core/clients/manage/inventory/introduction-to-software-inventory.md) 및 [소프트웨어 인벤토리를 구성하는 방법](../../core/clients/manage/inventory/configure-software-inventory.md)을 참조하세요.
