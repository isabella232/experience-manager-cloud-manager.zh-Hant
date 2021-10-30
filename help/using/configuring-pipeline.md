---
title: 設定 CI/CD 管道
seo-title: Configure your CI/CD Pipeline
description: 請依照本頁所述，從Cloud Manager配置管道設定。
seo-description: Before you start to deploy your code, you must configure your pipeline settings from the AEM Cloud Manager.
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD Pipeline
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 2be8f290b58fff2991f876c37dd1b499bc6c5352
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 1%

---

# 設定 CI/CD 管道 {#configure-your-ci-cd-pipeline}

>[!NOTE]
>若要了解如何在AEMas a Cloud Service中為Cloud Manager設定CI/CD管道，請參閱 [此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager).

以下頁面說明如何設定 **管道**. 若要檢閱管道運作方式的詳細概念資訊，請參閱 [CI/CD管道概觀](ci-cd-pipeline.md).


## 了解流量 {#understanding-the-flow}

您可以從 **** UI [!UICONTROL Cloud Manager]的「Pipeline Settings 」 (管道設定) 圖格來設定管道。

部署管理員負責設定管道。 執行此操作時，您會先從 **Git存放庫**. 管道設定包含：

* 定義將啟動管道的觸發器。
* 定義控制生產部署的參數。
* 配置效能測試參數。

## 教學課程影片 {#video-tutorial-one}

### 在Cloud Manager中設定管道 {#config-pipeline-video}

CI/CD生產管道設定會定義將啟動管道的觸發器、控制生產部署的參數以及效能測試參數。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)

## 設定管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存放庫至少有一個分支和 [程式設定](setting-up-program.md) 完成。

開始部署程式碼之前，您必須先從 [!UICONTROL Cloud Manager].

>[!NOTE]
>
>可在初始設定後更改管道設定。

### 從管道卡添加新的生產管道 {#adding-production-pipeline}

在您設定程式後，並且至少有一個環境使用 [!UICONTROL Cloud Manager] UI，您已準備好新增生產管道。

請依照下列步驟，設定生產管道的行為和偏好設定：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **+添加** 選取 **新增生產管道**.

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **新增生產管道** 對話框。

   1. 輸入 **管道名稱**. 您可以選擇 **存放庫** 和 **Git分支**.

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. 您可以設定 **部署觸發程式** 和 **重要量度失敗行為** 從 **部署選項**.

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      您可以指派下列部署觸發器以啟動管道：

      * **手動**  — 使用UI手動啟動管道。
      * **Git變更時**  — 每當有提交項新增至設定的git分支時，就會啟動CI/CD管道。 即使選取此選項，也始終可以手動啟動管道。

      在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。

      這對希望實現更自動化流程的客戶非常有用。 可用選項包括：

      * **每次都問**  — 這是預設設定，需要手動干預任何「重要」故障。
      * **立即失敗**  — 如果選中，則每當出現「重要」(Important)故障時，管道將被取消。 這實質上是模擬用戶手動拒絕每個故障。
      * **立即繼續**  — 如果選中此選項，則每當出現「重要」故障時，管道將自動繼續。 這實際上是在模擬使用者手動核准每個失敗。
   1. 選取 **部署選項**.

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **在階段部署後批准** 功能與生產部署前的核准類似，但會在階段部署步驟後立即發生，亦即，在完成任何測試之前，與生產部署前的核准（所有測試完成後）相比。

      * **跳過負載平衡器更改** 略過變更。
   1. 選取 **Dispatcher設定** 為舞台。 輸入路徑，從中選取動作 **類型**，然後按一下 **新增路徑**. 您可以為每個環境指定最多100個路徑。

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. 選取 **部署選項** 生產。 現在您可以定義控制生產部署的參數。

      ![](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

      三種可用選項如下：

      * **使用上線批准**  — 部署必須由業務所有者、項目經理或部署經理通過 [!UICONTROL Cloud Manager] UI。

      * **已排程**  — 此選項可讓使用者啟用排程的生產部署。

         >[!NOTE]
         >若 **已排程** 選項，您可以將生產部署排程到管道 **after** 預備部署(和 **使用GoLive核准**，則會等待排程設定完成。 使用者也可以選擇立即執行生產部署。
         >
         >請參閱 [部署程式碼](deploying-code.md)，以設定部署排程或立即執行生產。

         * **使用CSE監督** - CSE參與，以實際開始部署。 在管道設定或啟用CSE監督時編輯期間，部署管理器可以選擇：

            * **任何CSE**:是指任何可用的CSE
            * **我的CSE**:是指如果客戶不在辦公室，則分配給客戶或其備份的特定CSE
   1. 設定 **Dispatcher設定** 生產。 輸入路徑，從中選取動作 **類型**，然後按一下 **新增路徑**. 您可以為每個環境指定最多100個路徑。

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      作為部署管理員，您有機會配置一組內容路徑，這些路徑可以 **失效** 或 **已清除** 設定或編輯管道時從AEM Dispatcher快取中取得的發佈例項。

      您可以為「預備」和「生產」部署設定個別的路徑集。 如果已配置，則這些快取操作將作為部署管道步驟的一部分執行，即在部署任何內容包後執行。 這些設定使用標準的AEM Dispatcher行為 — 無效執行快取失效，類似於從製作啟動內容以進行發佈時；刷新執行快取刪除。

      一般而言，最好使用無效動作，但可能會有需要排清的情況，尤其是使用AEMHTML用戶端程式庫時。

      >[!NOTE]
      >
      >請參閱 [Dispatcher綜覽](dispatcher-configurations.md) 取得Dispatcher快取的詳細資訊。





1. 按一下 **繼續** 選取所有選項後。

1. 從 **階段測試** 步驟。 您可以設定 *AEM Sites* 和 *AEM Assets* 效能測試，具體取決於您已授權的產品。 請參閱 [效能測試](understand-your-test-results.md#performance-testing) 以取得更多詳細資訊。

   1. 從 **網站內容傳送/分散的載入量**. 請參閱 [AEM Sites效能測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites) 以取得更多詳細資訊。

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. 從 **資產效能測試分發**. 請參閱 [AEM Assets效能測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets) 以取得更多詳細資訊。

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

1. 按一下 **儲存** 完成新增生產管道。

### 編輯生產管道 {#editing-prod-pipeline}

可以從 **計畫概述** 頁面。

請依照下列步驟編輯已設定的管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **編輯**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/edit-prod1.png)

1. 此 **編輯生產管道** 對話框。

   1. 此 **設定** 索引標籤可讓您更新 **管道名稱**, **存放庫**, **Git分支**, **部署觸發程式**, **重要量度失敗行為**, **部署選項** 和 **Dispatcher設定**.

      >[!NOTE]
      >請參閱 [添加和管理儲存庫](/help/using/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。


   1. 此 **階段測試** 索引標籤提供選項，可從 **網站內容傳送/分散的載入量** 和 **資產效能測試分發**.

1. 按一下 **更新** 編輯管道後。

### 其他生產管道動作 {#additional-prod-actions}

#### 執行生產管道 {#run-prod}

可以從「管道」卡運行生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **執行**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/prod-run.png)

#### 刪除生產管道 {#delete-prod}

您可以從「管道」卡中刪除生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **刪除**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/prod-delete.png)

   >[!NOTE]
   >部署管理員角色中的使用者現在可以透過 **刪除** 選項。

## 僅限非生產和代碼品質的管道

除了部署至預備和生產的主要管道外，客戶還能設定其他管道，如 **非生產管道**. 這些管道一律會執行建置和程式碼品質步驟。 他們也可以選擇部署至Adobe Managed Services環境。

## 教學課程影片 {#video-tutorial-two}

### 僅限Cloud Manager非生產與程式碼品質管道 {#non-prod-video}

CI/CD非生產管道分為兩類：程式碼品質管道和部署管道。 程式碼品質會管道來自Git分支的所有程式碼，以根據Cloud Manager的程式碼品質掃描來建置和評估。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### 新增非生產管道 {#add-non-production-pipeline}

在主螢幕上，這些管道會列在新卡中：

1. 存取 **管道** Cloud Manager主畫面中的資訊卡。 按一下 **+添加** 選取 **新增非生產管道**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **新增非生產管道**  對話框。 選取要建立的管線類型 **程式碼品質管道** 或 **部署管道**.

   此外，您也可以設定 **部署觸發程式** 和 **重要量度失敗行為** 從 **部署選項**. 按一下 **繼續**.

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. 新建立的非生產管道現在會顯示在 **管道** 卡片。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   管道會顯示在主畫面的卡片上，包含三個動作，如下所示：

   * **新增**  — 允許添加新管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **更多詳情**  — 導覽至了解CI/CD管道檔案資源。

### 編輯非生產管道 {#editing-nonprod-pipeline}

可以從 **管道卡** 從 **計畫概述** 頁面。

請依照下列步驟編輯已設定的非生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 選取非生產管道，然後按一下 **...**. 按一下 **編輯**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. 此 **編輯生產管道** 對話框顯示，允許您更新 **管道名稱**, **存放庫**, **Git分支**, **部署觸發程式**，和 **重要量度失敗行為**.

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >請參閱 [添加和管理儲存庫](/help/using/cloud-manager-repositories.md) 了解如何在Cloud Manager中新增和管理存放庫。

   您可以指派下列部署觸發器以啟動管道：

   * **手動**  — 使用UI手動啟動管道。
   * **Git變更時**  — 每當有提交項新增至設定的git分支時，就會啟動CI/CD管道。 即使選取此選項，也始終可以手動啟動管道。

   在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。 這對希望實現更自動化流程的客戶非常有用。 可用選項包括：

   * **每次都問**  — 這是預設設定，需要手動干預任何「重要」故障。
   * **立即失敗**  — 如果選中，則每當出現「重要」(Important)故障時，管道將被取消。 這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當出現「重要」故障時，管道將自動繼續。 這實際上是在模擬使用者手動核准每個失敗。


1. 按一下 **更新** 編輯完非生產管道後。

### 其他非生產管道動作 {#additional-nonprod-actions}

#### 執行非生產管道 {#run-nonprod}

可以從「管道」卡運行生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **執行**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/nonprod-run1.png)

#### 刪除非生產管道 {#delete-nonprod}

您可以從「管道」卡中刪除生產管道：

1. 導覽至 **管道** 卡片 **計畫概述** 頁面。

1. 按一下 **...** 從 **管道** 卡片並按一下 **刪除**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/nonprod-delete.png)


## 後續步驟 {#the-next-steps}

設定管道後，您需要部署程式碼。

請參閱 [部署程式碼](deploying-code.md) 以取得更多詳細資訊。
