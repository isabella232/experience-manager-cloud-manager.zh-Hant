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
source-git-commit: 1e3dc17d28ab69dcd6b2337280bb38ba07352beb
workflow-type: tm+mt
source-wordcount: '1834'
ht-degree: 1%

---

# 設定 CI/CD 管道 {#configure-your-ci-cd-pipeline}

>[!NOTE]
>若要了解如何在AEMas a Cloud Service中為Cloud Manager設定CI/CD管道，請參閱[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)。

以下頁面說明如何配置&#x200B;**管道**。 若要查看管道運作方式的更多概念資訊，請參閱[CI/CD管道概述](ci-cd-pipeline.md)。

## 教學課程影片 {#video-tutorial-one}

### 在Cloud Manager中設定管道 {#config-pipeline-video}

CI/CD生產管道設定會定義將啟動管道的觸發器、控制生產部署的參數以及效能測試參數。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## 了解流量 {#understanding-the-flow}

您可以從 **** UI [!UICONTROL Cloud Manager]的「Pipeline Settings 」 (管道設定) 圖格來設定管道。

部署管理員負責設定管道。 這麼做時，您會先從&#x200B;**Git存放庫**&#x200B;中選取分支。 管道設定包含：

* 定義將啟動管道的觸發器。
* 定義控制生產部署的參數。
* 配置效能測試參數。

## 設定管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git存放庫至少有一個分支且[程式設定](setting-up-program.md)完成前，無法設定管道。

開始部署代碼之前，必須從[!UICONTROL Cloud Manager]配置管道設定。

>[!NOTE]
>
>可在初始設定後更改管道設定。

## 從管道卡添加新的生產管道 {#adding-production-pipeline}

設定程式並使用[!UICONTROL Cloud Manager] UI至少有一個環境後，即可新增生產管道。

請依照下列步驟，設定生產管道的行為和偏好設定：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**+Add**&#x200B;並選擇&#x200B;**添加生產管道**。

   ![](/help/using/assets/configure-pipelines/add-prod1.png)

1. **新增生產** 管道對話方塊隨即顯示。

   1. 輸入&#x200B;**管道名稱**。 您可以選擇&#x200B;**Repository**&#x200B;和&#x200B;**Git分支**。

      ![](/help/using/assets/configure-pipelines/add-prod2.png)

   1. 您可以從&#x200B;**部署選項**&#x200B;設定&#x200B;**部署觸發器**&#x200B;和&#x200B;**重要度量失敗行為**。

      ![](/help/using/assets/configure-pipelines/add-prod3.png)


      您可以指派下列部署觸發器以啟動管道：

      * **手動**  — 使用UI手動啟動管道。
      * **On Git Changes**  — 每當有提交項新增至設定的Git分支時，就會啟動CI/CD管道。即使選取此選項，也始終可以手動啟動管道。

      在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。

      這對希望實現更自動化流程的客戶非常有用。 可用選項包括：

      * **每次詢問**  — 此為預設設定，需要手動干預任何「重要」失敗。
      * **立即失敗**  — 如果選中此選項，則每當出現「重要」故障時，管道都將被取消。這實質上是模擬用戶手動拒絕每個故障。
      * **立即繼續**  — 如果選中此選項，則每當出現「重要」(Important)故障時，管道將自動繼續。這實際上是在模擬使用者手動核准每個失敗。
   1. 選擇&#x200B;**部署選項**。

      ![](/help/using/assets/configure-pipelines/add-prod4.png)

      * **在階段部署** 後批准的功能與在生產部署前批准的功能類似，但會在階段部署步驟後立即進行，即在完成任何測試之前，與在完成所有測試後完成的生產部署之前的批准進行比較。

      * **跳過負載平衡器** 更改將更改。
   1. 為Stage選取&#x200B;**Dispatcher設定**。 輸入路徑，從&#x200B;**Type**&#x200B;中選擇操作，然後按一下&#x200B;**Add Path**。 您可以為每個環境指定最多100個路徑。

      ![](/help/using/assets/configure-pipelines/dispatcher-stage.png)

   1. 為生產選擇&#x200B;**部署選項**。 現在您可以定義控制生產部署的參數。

      ![](/help/using/assets/configure-pipelines/prod-deploymentoptions.png)

      三種可用選項如下：

      * **使用上線批准**  — 部署必須由業務擁有者、專案經理或部署經理透過UI手動 [!UICONTROL Cloud Manager] 核准。

      * **已排程**  — 此選項可讓使用者啟用已排程的生產部署。

         >[!NOTE]
         >如果選取了&#x200B;**已排程**&#x200B;選項，您可以在預備部署(和&#x200B;**使用GoLive核准**，如果已啟用)之後，將生產部署排程到管道&#x200B;**。**&#x200B;使用者也可以選擇立即執行生產部署。
         >
         >請參閱[部署代碼](deploying-code.md)，以設定部署計畫或立即執行生產。

         * **使用CSE監督**  — 參與CSE以實際開始部署。在管道設定或啟用CSE監督時編輯期間，部署管理器可以選擇：

            * **任何CSE**:是指任何可用的CSE
            * **我的CSE**:是指如果客戶不在辦公室，則分配給客戶或其備份的特定CSE
   1. 為「生產」設定&#x200B;**Dispatcher設定**。 輸入路徑，從&#x200B;**Type**&#x200B;中選擇操作，然後按一下&#x200B;**Add Path**。 您可以為每個環境指定最多100個路徑。

      ![](/help/using/assets/configure-pipelines/dispatcher-prod.png)

      作為部署管理員，您可以設定一組內容路徑，這些路徑會在設定或編輯管道時，從AEM Dispatcher快取中取消&#x200B;****&#x200B;或&#x200B;**已清除**。

      您可以為「預備」和「生產」部署設定個別的路徑集。 如果已配置，則這些快取操作將作為部署管道步驟的一部分執行，即在部署任何內容包後執行。 這些設定使用標準的AEM Dispatcher行為 — 無效執行快取失效，類似於從製作啟動內容以進行發佈時；刷新執行快取刪除。

      一般而言，最好使用無效動作，但可能會有需要排清的情況，尤其是使用AEMHTML用戶端程式庫時。

      >[!NOTE]
      >
      >請參閱[Dispatcher綜覽](dispatcher-configurations.md)以取得有關Dispatcher快取的詳細資訊。





1. 選擇所有選項後，按一下&#x200B;**繼續**。

1. 從&#x200B;**階段測試**&#x200B;步驟中選取選項。 您可以根據您已授權的產品，設定&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;效能測試。 如需詳細資訊，請參閱[效能測試](understand-your-test-results.md#performance-testing) 。

   1. 從&#x200B;**網站內容傳送/分佈式載入權數**&#x200B;中選取選項。 如需詳細資訊，請參閱效能測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-sites)中的[AEM Sites 。

      ![](/help/using/assets/configure-pipelines/add-prod5.png)

   1. 從&#x200B;**Assets效能測試分發**&#x200B;中選擇選項。 如需詳細資訊，請參閱效能測試](https://experienceleague.adobe.com/docs/experience-manager-cloud-manager/using/how-to-use/understand-your-test-results.html?lang=en#aem-assets)中的[AEM Assets 。

      ![](/help/using/assets/configure-pipelines/add-prod6.png)

1. 按一下&#x200B;**Save**&#x200B;以完成添加生產管線。

### 編輯生產管道 {#editing-prod-pipeline}

您可以從&#x200B;**程式概述**&#x200B;頁面編輯管道設定。

請依照下列步驟編輯已設定的管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...**&#x200B;管道&#x200B;**卡上的**，按一下&#x200B;**編輯**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/edit-prod1.png)

1. 隨即顯示&#x200B;**編輯生產管道**&#x200B;對話方塊。

   1. **Configuration**&#x200B;標籤可讓您更新&#x200B;**Pipeline Name**、**Repository**、**Git分支**、**Deployment Trigger**、**Important Metrics Failure Behavion**、**DeploymentOptions**&#x200B;和&lt;a14/&lt;A5/>Dispatcher配置。****

      >[!NOTE]
      >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) ，了解如何在Cloud Manager中新增和管理存放庫。


   1. **階段測試**&#x200B;索引標籤提供從&#x200B;**網站內容傳送/分佈式負載權重**&#x200B;和&#x200B;**資產效能測試分佈**&#x200B;重新選取選項的選項。

1. 編輯管道後，按一下&#x200B;**更新**。

### 其他生產管道動作 {#additional-prod-actions}

#### 執行生產管道 {#run-prod}

可以從「管道」卡運行生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...**&#x200B;管道&#x200B;**卡上的**，按一下&#x200B;**運行**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/prod-run.png)

#### 刪除生產管道 {#delete-prod}

您可以從「管道」卡中刪除生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...從**&#x200B;管道&#x200B;**卡中按一下**&#x200B;刪除&#x200B;**，如下圖所示。**

   ![](/help/using/assets/configure-pipelines/prod-delete.png)

   >[!NOTE]
   >部署管理員角色中的使用者現在可以透過管道卡中的&#x200B;**Delete**&#x200B;選項，以自助方式刪除生產管道。

## 僅限非生產和代碼品質的管道

除了部署到預備和生產的主管道外，客戶還可以設定其他管道，稱為&#x200B;**非生產管道**。 這些管道一律會執行建置和程式碼品質步驟。 他們也可以選擇部署至Adobe Managed Services環境。

## 教學課程影片 {#video-tutorial-two}

### 僅限Cloud Manager非生產與程式碼品質管道 {#non-prod-video}

CI/CD非生產管道分為兩類：程式碼品質管道和部署管道。 程式碼品質會管道來自Git分支的所有程式碼，以根據Cloud Manager的程式碼品質掃描來建置和評估。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

### 新增非生產管道 {#add-non-production-pipeline}

在主螢幕上，這些管道會列在新卡中：

1. 從Cloud Manager主畫面存取&#x200B;**管道**&#x200B;卡片。 按一下&#x200B;**+Add**&#x200B;並選擇&#x200B;**添加非生產管道**。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add1.png)

1. **添加非生產管道**  對話框隨即顯示。選取您要建立的管道類型，可以是&#x200B;**代碼品質管道**&#x200B;或&#x200B;**部署管道**。

   此外，您也可以從&#x200B;**部署選項**&#x200B;設定&#x200B;**部署觸發器**&#x200B;和&#x200B;**重要度量失敗行為**。 按一下&#x200B;**繼續**。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add2.png)


1. 新建立的非生產管道現在顯示在&#x200B;**管道**&#x200B;卡中。

   ![](/help/using/assets/configure-pipelines/nonprod-pipeline-add4.png)


   管道會顯示在主畫面的卡片上，包含三個動作，如下所示：

   * **新增**  — 允許新增管道。
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊。
   * **了解更多**  — 導覽至了解CI/CD管道檔案資源。

### 編輯非生產管道 {#editing-nonprod-pipeline}

您可以從&#x200B;**程式概述**&#x200B;頁面的&#x200B;**管道卡**&#x200B;編輯管道配置。

請依照下列步驟編輯已設定的非生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 選擇非生產管道，然後按一下&#x200B;**...**。 按一下&#x200B;**Edit**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit1.png)

1. 隨即顯示「編輯生產管道&#x200B;**」對話框，該對話框允許您更新**&#x200B;管道名稱&#x200B;**、**&#x200B;儲存庫&#x200B;**、** Git分支&#x200B;**、**&#x200B;部署觸發器&#x200B;**和**&#x200B;重要度量失敗行為&#x200B;**。**

   ![](/help/using/assets/configure-pipelines/non-prod-pipeline-edit2.png)

   >[!NOTE]
   >請參閱[新增和管理存放庫](/help/implementing/cloud-manager/managing-code/cloud-manager-repositories.md) ，了解如何在Cloud Manager中新增和管理存放庫。

   您可以指派下列部署觸發器以啟動管道：

   * **手動**  — 使用UI手動啟動管道。
   * **On Git Changes**  — 每當有提交項新增至設定的Git分支時，就會啟動CI/CD管道。即使選取此選項，也始終可以手動啟動管道。

   在管道設定或編輯期間，部署管理器可以選擇在任何質量門中遇到重要故障時定義管道的行為。 這對希望實現更自動化流程的客戶非常有用。 可用選項包括：

   * **每次詢問**  — 此為預設設定，需要手動干預任何「重要」失敗。
   * **立即失敗**  — 如果選中此選項，則每當出現「重要」故障時，管道都將被取消。這實質上是模擬用戶手動拒絕每個故障。
   * **立即繼續**  — 如果選中此選項，則每當出現「重要」(Important)故障時，管道將自動繼續。這實際上是在模擬使用者手動核准每個失敗。


1. 編輯完非生產管道後，按一下「**更新**」。

### 其他非生產管道動作 {#additional-nonprod-actions}

#### 執行非生產管道 {#run-nonprod}

可以從「管道」卡運行生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...**&#x200B;管道&#x200B;**卡上的**，按一下&#x200B;**運行**，如下圖所示。

   ![](/help/using/assets/configure-pipelines/nonprod-run1.png)

#### 刪除非生產管道 {#delete-nonprod}

您可以從「管道」卡中刪除生產管道：

1. 從&#x200B;**程式概述**&#x200B;頁面導覽至&#x200B;**管道**&#x200B;卡片。

1. 按一下&#x200B;**...從**&#x200B;管道&#x200B;**卡中按一下**&#x200B;刪除&#x200B;**，如下圖所示。**

   ![](/help/using/assets/configure-pipelines/nonprod-delete.png)


## 後續步驟 {#the-next-steps}

設定管道後，您需要部署程式碼。

如需詳細資訊，請參閱[部署程式碼](deploying-code.md) 。
