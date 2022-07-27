---
title: AMS雲管理器簡介
description: 從此處開始瞭解Adobe Managed Services(AMS)的雲管理器，以及它如何使組織能夠在雲中自我管理Adobe Experience Manager。
exl-id: 58344d8a-b869-4177-a9cf-6a8b7dfe9588
source-git-commit: 22d40a1f07f56ee7a7dddb4897e4079f1e346674
workflow-type: tm+mt
source-wordcount: '1292'
ht-degree: 10%

---


# 簡介 [!UICONTROL Cloud Manager] AMS {#introduction-to-cloud-manager}

從此處開始瞭解Cloud Manager forAdobe管理服務(AMS)，以及它如何使組織能夠在雲中自我管理Adobe Experience Manager。

>[!CONTEXTUALHELP]
>id="aemcloud_cloudmanager_introduction"
>title="AMS雲管理器簡介"
>abstract="使組織能夠在雲中自我管理Adobe Experience Manager。 其內容包含持續整合與持續傳送 (CI/CD) 架構，可讓 IT 團隊與實作合作夥伴加快提供自訂或更新的傳送速度，而不會影響效能或安全性。"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/programs.html?lang=en#cloud-manager" text="建立程式"
>additional-url="https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/cloud-manager/environments.html?lang=en#cloud-manager" text="建立環境"

## 簡介 {#introduction}

[!UICONTROL Cloud Manager] 對於Adobe Experience Manager公司，開發人員能夠通過簡化的工作流建立具有影響力的客戶體驗，這些工作流基於Adobe Experience Manager的最佳做法。 為Adobe Experience Manager優化的CI/CD管道允許您通過簡單地簽入代碼來輕鬆合併開發工作流，然後代碼可以一直移動到生產就緒狀態。 在構建階段，您的自定義代碼更新將根據最佳做法進行徹底測試，以便為客戶提供可靠的應用程式。 Cloud Manager使用開放API方法，使您能夠與系統整合而不中斷現有流程和工具。

>[!NOTE]
>
>本文檔專門介紹Cloud Manager for Adobe Managed Services(AMS)的功能和特性。
>
>在中可找AEM到as a Cloud Service的等效文檔 [AEMas a Cloud Service文檔。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/home.html)

使用Cloud Manager，您的開發團隊可從以下功能中獲益：

* 持續整合/連續交付代碼(CI/CD)，將上市時間從數月/周縮短到數天/小時

* 基於最佳實踐的代碼檢查、效能測試和安全驗證，然後再推向生產，以最大限度地減少生產中斷

* 用於補充現有DevOps進程的API連接

* 自動擴展功能可智慧地檢測對增加容量的需要，並自動將額外的Dispatcher/發佈段帶到線上

此圖顯示了在中使用的CI/CD處理流 [!UICONTROL Cloud Manager]:

![CI/CD流](/help/assets/screen_shot_2018-05-12at73843pm.png)

## [!UICONTROL Cloud Manager] 中的重要功能  {#key-features-in-cloud-manager}

下面是對Cloud Manager的選定關鍵功能的更深入的瞭解。

### 自助服務介面 {#self-service-interface}

用於 [!UICONTROL Cloud Manager] 使您能夠輕鬆訪問和管理雲環境和CI/CD管道，以便您的Adobe Experience Manager應用程式使用。

您可以定義特定於應用程式的關鍵績效指標(KPI)（如每分鐘的峰值頁面視圖和頁面負載的預期響應時間），這些指標構成了衡量成功部署的基礎。 您可以輕鬆定義不同團隊成員的角色和權限。自助服務介面將控制權交到您手中，但它還提供指向最佳做法資源的連結，並可以訪問Adobe內可根據需要提供必要指導的專家。

瀏覽並開始使用 [!UICONTROL Cloud Manager]的UI，請參閱文檔 [首次登錄。](/help/getting-started/first-time-login.md)

### CI/CD 管道 {#ci-cd-pipeline}

[!UICONTROL Cloud Manager] 的一項重要功能是可運用最佳化的 CI/CD 管道，以加速自訂程式碼或更新的傳送，例如在網站上新增元件。

通過 [!UICONTROL Cloud Manager] UI，您可以配置和啟動CI/CD管道。 作為此流水線的一部分，執行徹底的代碼掃描以確保只有高質量的應用程式才能通過生產環境。

瞭解有關從配置管道的詳細資訊 [!UICONTROL Cloud Manager]的UI，請參閱文檔 [配置生產管線](/help/using/production-pipelines.md) 和 [配置非生產管道。](/help/using/non-production-pipelines.md)

### 有彈性的部署模式 {#flexible-deployment-modes}

[!UICONTROL Cloud Manager] 提供靈活且可配置的部署模式，因此您可以根據不斷變化的業務需求提供體驗。

使用自動觸發模式，代碼基於諸如代碼提交之類的特定事件自動部署到環境。 您也可以在指定的時間範圍內，甚至在工作時間以外，排程程式碼部署。

與部署觸發器無關，每次觸發部署時，質量檢查始終作為CI/CD管道執行的一部分執行。 質量檢查包括代碼檢查、安全性測試和效能測試，所有這些都是開箱即用的，無需您或您的合作夥伴的任何努力。

要瞭解有關部署代碼和質量檢查的詳細資訊，請參閱文檔 [部署代碼。](/help/using/code-deployment.md)

## 雲管理器中的可選功能 {#optional-features-in-cloud-manager}

Cloud Manager提供附加的高級功能，這些功能可能會根據您特定環境的設定和需求對您的項目有所幫助。 如果您對這些功能感興趣，請聯繫您的客戶成功工程師(CSE)或Adobe代表以進一步討論。

### 自動縮放 {#autoscaling}

當生產環境承受異常高的負荷時， [!UICONTROL Cloud Manager] 檢測對附加容量的需求，並使用其自動縮放功能自動將附加容量聯機。

在這樣的情況下， [!UICONTROL Cloud Manager] 自動觸發自動縮放設定過程，發送自動縮放事件的通知，並在幾分鐘內將附加容量聯機。 在生產環境中，在相同的區域中配置額外容量，並且與運行中的Dispatcher/publishing節點匹配相同的系統規格。

自動縮放功能僅適用於調度器/發佈層，並且使用水準縮放方法執行，調度器/發佈對的至少一個附加段最多為十個段。 佈建的額外容量會在十個工作天的期間內以手動縮放，實際時間長短由 CSE (客戶成功工程師) 決定。

>[!NOTE]
>
>如果您想瞭解自動縮放是否適合您的應用程式，請與CSE或Adobe代表聯繫。

### 藍綠部署 {#blue-green}

藍色/綠色部署是一種技術，它通過運行兩種稱為藍色和綠色的相同生產環境來減少停機時間和風險。

在任何時候，只有一個環境是可用的，而即時環境則為所有生產流量提供服務。 通常，藍色是當前的活動環境，綠色是空閒的。

* 藍色/綠色部署是Cloud Manager CI/CD管道的附加元件，在該管道中，將建立第二組發佈和Dispatcher實例（綠色）並用於部署。 綠色實例隨後連接到生產負載平衡器，舊實例（藍色）被刪除並終止。
* 藍色/綠色的這種實現方式將實例視為瞬態，藍色/綠色管道的每個迭代都將建立一組新的發佈和Dispatcher伺服器。
* 將建立綠色負載平衡器作為安裝的一部分。 此負載平衡器將永不更改，並且您應將綠色或「test」URL指向。
* 在藍色/綠色部署期間，將建立現有發佈/調度程式層的精確副本（從TDL讀取）。

#### 藍/綠部署流 {#flow}

啟用藍色/綠色部署時，部署流與標準Cloud Service部署流不同。

| 步驟 | 藍色/綠色部署 | 標準部署 |
|---|---|---|
| 1 | 部署到作者 | 部署到作者 |
| 2 | 暫停測試 | - |
| 3 | 建立了綠色基礎架構 | - |
| 4 | 部署到綠色發佈/調度程式層 | 部署到發佈伺服器 |
| 5 | 暫停測試（最多24小時） | - |
| 6 | 綠色基礎架構已添加到生產負載平衡器 | - |
| 7 | 從生產負載平衡器中刪除藍色基礎結構 —  |
| 8 | 藍色基礎架構自動終止 | - |

#### 實施藍色/綠色 {#implementing}

所有使用Cloud Manager進行生產部署的AMS用戶均有資格使用藍色/綠色部署。 但是，使用藍綠部署需要通過AdobeCSE對您的環境和設定進行額外的驗證。

如果您對藍色/綠色部署感興趣，請考慮以下要求和限制，並與CSE聯繫。

#### 要求和限制 {#limitations}

* 藍色/綠色僅可用於發佈/調度程式對。
* 預覽調度程式/發佈對不屬於藍色/綠色部署。
* 每個Dispatcher/publish對與其他Dispatcher/publish對完全相同。
* 藍色/綠色僅在生產環境中可用。
* 藍色/綠色在AWS和Azure都可用。
* 藍色/綠色不僅適用於資產客戶。
