1.  Configuration Manager 콘솔에서 **소프트웨어 라이브러리** > **소프트웨어 업데이트**로 이동합니다.  

2.  다음 방법 중 하나를 사용하여 다운로드할 소프트웨어 업데이트를 선택합니다.  

    -   **소프트웨어 업데이트 그룹**에서 하나 이상의 소프트웨어 업데이트를 선택한 후에 **홈** 탭의 **업데이트 그룹** 그룹에서 **다운로드**를 클릭합니다.  

    -   **모든 소프트웨어 업데이트**에서 하나 이상의 소프트웨어 업데이트를 선택한 후에 **홈** 탭의 **업데이트** 그룹에서 **다운로드**를 클릭합니다.  

        > [!NOTE]  
        >  **모든 소프트웨어 업데이트** 노드에서 Configuration Manager는 지난 30일 이내에 배포되고 **위험** 및 **보안**으로 분류된 소프트웨어 업데이트만 표시합니다.  

        > [!TIP]  
        >  **조건 추가** 를 클릭하여 **모든 소프트웨어 업데이트** 노드에 표시되는 소프트웨어 업데이트를 필터링하고 자주 사용하는 검색 조건을 저장한 후에 **검색** 탭에서 저장된 검색을 관리합니다.  

         **소프트웨어 업데이트 다운로드 마법사** 가 열립니다.  

3.  **배포 패키지** 페이지에서 다음 설정을 구성합니다.  

    1.  **배포 패키지 선택**: 배포에 있는 소프트웨어 업데이트에 대한 기존 배포 패키지를 선택하려면 이 설정을 선택합니다.  

        > [!NOTE]  
        >  선택한 배포 패키지에 이미 다운로드된 소프트웨어 업데이트는 다시 다운로드되지 않습니다.  

    2.  **새 배포 패키지 만들기**: 배포에 있는 소프트웨어 업데이트에 대한 새 배포 패키지를 만들려면 이 설정을 선택합니다. 다음 설정을 구성합니다.  

        -   **이름**: 배포 패키지의 이름을 지정합니다. 패키지의 이름은 패키지 콘텐츠를 간략하게 설명하는 고유한 이름이어야 합니다.  길이는 50자로 제한됩니다.  

        -   **설명**: 배포 패키지에 대한 설명을 지정합니다. 패키지 설명은 패키지 콘텐츠에 대한 정보를 제공하고 길이는 127자로 제한됩니다.  

        -   **패키지 원본**: 소프트웨어 업데이트 원본 파일의 위치를 지정합니다. 원본 위치의 네트워크 경로(예: **\\\server\sharename\path**)를 입력하거나 **찾아보기** 를 클릭하여 네트워크 위치를 검색합니다. 다음 페이지를 진행하기 전에 배포 패키지 원본 파일에 대한 공유 폴더를 만들어야 합니다.  

            > [!NOTE]  
            >  지정되는 배포 패키지 원본 위치는 다른 소프트웨어 배포 패키지에서 사용할 수 없습니다.  

            > [!IMPORTANT]  
            >  SMS 공급자 컴퓨터 계정 및 소프트웨어 업데이트 다운로드를 위해 마법사를 실행하는 사용자는 모두 다운로드 위치에 대해 **쓰기** NTFS 권한을 보유해야 합니다. 공격자가 소프트웨어 업데이트 원본 파일을 변조하는 위험을 줄이기 위해 다운로드 위치에 대한 액세스 권한은 신중하게 제한해야 합니다.  

            > [!IMPORTANT]  
            >  Configuration Manager에서 배포 패키지를 만든 후 배포 패키지 속성에서 패키지 원본 위치를 변경할 수 있습니다. 그러나 이렇게 하려면 먼저 콘텐츠를 원래 패키지 원본에서 새 패키지 원본 위치로 복사해야 합니다.  

     **다음**을 클릭합니다.  

4.  **배포 지점** 페이지에서 소프트웨어 업데이트 파일을 호스트할 배포 지점 또는 배포 지점 그룹을 지정한 후에 **다음**을 클릭합니다. 배포 지점에 대한 자세한 내용은 [Distribution point configurations](../../core/servers/deploy/configure/install-and-configure-distribution-points.md#bkmk_configs)섹션을 참조하세요.  

    > [!NOTE]  
    >  배포 지점 페이지는 새 소프트웨어 업데이트 배포 패키지를 만드는 경우에만 사용할 수 있습니다.  

6.  **배포 설정** 페이지에서 다음 설정을 지정합니다.  

    -   **배포 우선 순위**: 배포 패키지에 대한 배포 우선 순위를 지정하려면 이 설정을 사용합니다. 배포 우선 순위는 배포 패키지를 자식 사이트의 배포 지점으로 전송할 때 적용됩니다. 배포 패키지는 **높음**, **중간**또는 **낮음**의 우선 순위에 따라 보내집니다. 우선 순위가 서로 같은 패키지들은 만들어진 순서에 따라 보내집니다. 백로그가 없는 경우 패키지는 우선 순위에 관계없이 즉시 처리됩니다. 기본적으로 패키지는 **중간** 우선 순위를 사용하여 전송됩니다.  

    -   **기본 배포 지점으로 이 패키지의 콘텐츠 배포**: 주문형 콘텐츠 배포를 기본 배포 지점에 사용하도록 설정하려면 이 설정을 사용합니다. 이 설정을 활성화하면, 클라이언트가 패키지에 대한 콘텐츠를 요청했으나 모든 기본 배포 지점에서 해당 콘텐츠를 사용할 수 없을 경우 관리 지점에서 배포 관리자에 대해 트리거를 만들어 모든 기본 배포 지점으로 콘텐츠를 배포하도록 조치합니다. 기본 배포 지점 및 주문형 콘텐츠에 대한 자세한 내용은 [Content source location scenarios](../../core/plan-design/hierarchy/content-source-location-scenarios.md)를 참조하세요.  

    -   **사전 준비된 배포 지점 설정**: 사전 준비된 배포 지점으로 콘텐츠를 배포하는 방법을 지정하려면 이 설정을 사용합니다. 다음 옵션 중 하나를 선택합니다.  

        -   **배포 지점에 패키지가 할당될 때 자동으로 콘텐츠 다운로드**: 사전 준비된 설정을 무시하고 배포 지점에 콘텐츠를 배포하려면 이 설정을 사용합니다.  

        -   **배포 지점에 콘텐츠 변경 내용만 다운로드**: 배포 지점에 초기 콘텐츠를 사전 준비한 후 콘텐츠 변경 내용을 배포하려면 이 설정을 사용합니다.  

        -   **배포 지점에 이 패키지의 콘텐츠 수동으로 복사**: 배포 지점에 항상 콘텐츠를 사전 준비하려면 이 설정을 사용합니다. 이것이 기본 설정입니다.  

         배포 지점의 콘텐츠를 사전 준비하는 방법에 대한 자세한 내용은 [사전 준비된 콘텐츠 사용](../../core/servers/deploy/configure/deploy-and-manage-content.md#bkmk_prestage) 섹션을 참조하세요.  

     **다음**을 클릭합니다.  

6.  **다운로드 위치** 페이지에서 Configuration Manager가 소프트웨어 업데이트 원본 파일을 다운로드하는 데 사용할 위치를 지정합니다. 필요에 따라 다음 옵션을 사용합니다.  

    -   **인터넷에서 소프트웨어 업데이트 다운로드**: 인터넷 위치에서 소프트웨어 업데이트를 다운로드하려면 이 설정을 선택합니다. 이것이 기본 설정입니다.  

    -   **로컬 네트워크 위치에서 소프트웨어 업데이트 다운로드**: 로컬 폴더 또는 공유 네트워크 폴더에서 소프트웨어 업데이트를 다운로드하려면 이 설정을 선택합니다. 마법사를 실행하는 컴퓨터에서 인터넷에 접속할 수 없을 때 이 설정을 사용합니다.  

        > [!NOTE]  
        >  이 설정을 사용하는 경우 인터넷에 접속할 수 있는 아무 컴퓨터에서나 소프트웨어 업데이트를 다운로드한 후에 마법사를 실행하는 컴퓨터에서 액세스할 수 있는 로컬 네트워크 위치에 소프트웨어 업데이트를 복사합니다.  

     **다음**을 클릭합니다.  

7.  **언어 선택** 페이지에서 선택한 소프트웨어 업데이트를 다운로드할 언어를 지정하고 **다음**을 클릭합니다. Configuration Manager에서는 선택한 언어로 사용 가능한 소프트웨어 업데이트만 다운로드합니다. 특정 언어에 한정되지 않는 소프트웨어 업데이트는 항상 다운로드됩니다.  

8. **요약 페이지**에서, 마법사에서 선택한 설정을 확인한 후 **다음**을 클릭하여 소프트웨어 업데이트를 다운로드합니다.  

9. **완료** 페이지에서 소프트웨어 업데이트가 성공적으로 다운로드되었는지 확인한 후 **닫기**를 클릭합니다.  


<!--HONumber=Nov16_HO1-->

