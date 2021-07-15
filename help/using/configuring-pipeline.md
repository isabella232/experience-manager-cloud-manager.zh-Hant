---
title: 設定 CI/CD 管道
seo-title: 設定 CI/CD 管道
description: 請依照本頁所述，從Cloud Manager配置管道設定。
seo-description: '開始部署程式碼之前，您必須先從AEM Cloud Manager配置管道設定。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
feature: CI-CD管道
exl-id: d489fa3c-df1e-480b-82d0-ac8cce78a710
source-git-commit: 1c103b1c43a1e5fe7a6fa27110fc692bba6fb8b2
workflow-type: tm+mt
source-wordcount: '1308'
ht-degree: 2%

---

# 設定 CI/CD 管道 {#configure-your-ci-cd-pipeline}

>[!NOTE]
>若要了解如何在AEM as aCloud Service中為Cloud Manager設定CI/CD管道，請參閱[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/configure-pipeline.html?lang=en#using-cloud-manager)。

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

### 從[!UICONTROL Cloud Manager]配置管道設定 {#configuring-the-pipeline-settings-from-cloud-manager}

使用[!UICONTROL Cloud Manager] UI設定程式後，即可設定管道。

請依照下列步驟來設定管道的行為和偏好設定：

1. 按一下&#x200B;**設定管道**&#x200B;以設定和設定管道。

   ![](assets/Setup-Pipeline.png)

1. **設定管道**&#x200B;畫面隨即顯示。

   三步嚮導允許您設定&#x200B;**Branch**、**Environments**&#x200B;和&#x200B;**Testing**環境。
選取您的Git分支，然後按一下**Next**。

   >[!NOTE]
   >
   >在Git存放庫中找到的分支會連結至您的計畫。


1. 訪問&#x200B;**Environments**&#x200B;頁簽以選擇&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;選項。

   您可以定義觸發器以啟動管道：

   * **On Git Changes**  — 每當有提交項新增至設定的Git分支時，就會啟動CI/CD管道。即使選取此選項，也始終可以手動啟動管道。
   * **手動**  — 使用UI手動啟動管道。

   在管道設定或編輯期間，部署管理器可以選擇在任何質量門（如代碼質量、安全測試和效能測試）中遇到重要故障時定義管道的行為。

   這對希望實現更自動化流程的客戶非常有用。 可用選項包括：

* **每次詢問**  — 此為預設設定，需要手動干預任何「重要」失敗。
* **立即取消**  — 如果選中此選項，則每當出現「重要」故障時，管道都將被取消。這實質上是模擬用戶手動拒絕每個故障。
* **立即批准**  — 如果選取此選項，每當出現「重要」故障時，管道就會自動繼續。這實際上是在模擬使用者手動核准每個失敗。

   現在您可以定義控制生產部署的參數。 三種可用選項如下：

* **使用上線批准**  — 部署必須由業務擁有者、專案經理或部署經理透過UI手動 [!UICONTROL Cloud Manager] 核准。
* **使用CSE監督**  — 參與CSE以實際開始部署。在管道設定或啟用CSE監督時編輯期間，部署管理器可以選擇：

   * **任何CSE**:是指任何可用的CSE
   * **我的CSE**:是指如果客戶不在辦公室，則分配給客戶或其備份的特定CSE

* **已排程**  — 此選項可讓使用者啟用已排程的生產部署。

>[!NOTE]
>如果選取了&#x200B;**已排程**&#x200B;選項，您可以在預備部署(和&#x200B;**使用GoLive核准**，如果已啟用)之後，將生產部署排程到管道&#x200B;**。**&#x200B;使用者也可以選擇立即執行生產部署。
>
>請參閱&#x200B;[**部署代碼**](deploying-code.md)，以設定部署計畫或立即執行生產。

![](assets/configure-pipeline-new.png)

>[!NOTE]
>
>「**使用CSE監督**」選項不適用於所有客戶。

**在階段部署後批准**

在預備部署後，有可在生產管道中設定的選用步驟&#x200B;**核准**。
在**管道編輯**&#x200B;畫面上的新選項中啟用：

![](assets/post_deployment1.png)

接著，在管道執行期間，這會顯示為個別步驟：

![](assets/post_deployment2.png)

>[!NOTE]
>
>**在階段部署** 後批准的功能與在生產部署前批准的功能類似，但會在階段部署步驟後立即進行，即在完成任何測試之前，與在完成所有測試後完成的生產部署之前的批准進行比較。

**Dispatcher失效**

作為部署管理員，您可以設定一組內容路徑，這些路徑會在設定或編輯管道時，從AEM Dispatcher快取中取消&#x200B;****&#x200B;或&#x200B;**已清除**。

您可以為「預備」和「生產」部署設定個別的路徑集。 如果已配置，則這些快取操作將作為部署管道步驟的一部分執行，即在部署任何內容包後執行。 這些設定使用標準的AEM Dispatcher行為 — 無效執行快取失效，類似於從製作啟動內容以進行發佈時；刷新執行快取刪除。

一般而言，最好使用無效動作，但可能會有需要排清的情況，尤其是使用AEM HTML用戶端程式庫時。

>[!NOTE]
>
>請參閱[Dispatcher綜覽](dispatcher-configurations.md)以取得有關Dispatcher快取的詳細資訊。

請依照下列步驟來設定Dispatcher無效判定：

1. 按一下「Dispatcher設定」標題下的「**設定**」

   ![](assets/image2018-8-7_14-53-24.png)

1. 輸入路徑，從&#x200B;**Type**&#x200B;中選擇操作，然後按一下&#x200B;**Add**。 您可以為每個環境指定最多100個路徑。 新增路徑後，按一下「**套用**」。

   ![](assets/image2018-8-7_14-58-11.png)

1. 回到&#x200B;**管道設定**&#x200B;頁面後，您會看到選取項目的更新摘要。

   按一下&#x200B;**Save**&#x200B;以保存此配置。

   ![](assets/image2018-8-7_15-4-30.png)

1. 訪問&#x200B;**Testing**&#x200B;頁簽，以定義程式的測試標準。 您現在可以設定效能測試參數。

   您可以根據您已授權的產品，設定&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;效能測試。 如需詳細資訊，請參閱[效能測試](understand-your-test-results.md#performance-testing) 。

1. 按一下&#x200B;**Save**&#x200B;以完成管道進程的設定。

   >[!NOTE]
   >此外，設定管道後，您仍可以使用[!UICONTROL Cloud Manager] UI的&#x200B;**生產管道設定**&#x200B;圖磚，編輯相同項目的設定。

   ![](assets/Production-Pipeline.png)


## 僅限非生產和代碼品質的管道

除了部署到預備和生產的主管道外，客戶還可以設定其他管道，稱為&#x200B;**非生產管道**。 這些管道一律會執行建置和程式碼品質步驟。 他們也可以選擇部署至Adobe Managed Services環境。

## 教學課程影片 {#video-tutorial-two}

### 僅限Cloud Manager非生產與程式碼品質管道 {#non-prod-video}

CI/CD非生產管道分為兩類：程式碼品質管道和部署管道。 程式碼品質會管道來自Git分支的所有程式碼，以根據Cloud Manager的程式碼品質掃描來建置和評估。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

在主螢幕上，這些管道會列在新卡中：

1. 從Cloud Manager主畫面存取&#x200B;**非生產管道**&#x200B;方塊。

   ![](/help/using/assets/non-prod-add.png)

1. 按一下&#x200B;**Add**&#x200B;按鈕，以指定管道名稱、管道類型和Git分支。

   此外，您也可以從管道選項設定部署觸發程式和重要失敗行為。

   ![](assets/non-prod-pipe.png)

1. 按一下「**儲存**」，主畫面的卡片上會顯示管道，其中包含五個動作：

   * **編輯**  — 允許編輯管道設定
   * **詳細資訊**  — 顯示上次管道執行（如果有的話）
   * **建置**  — 導覽至執行頁面，可從該頁面執行管道
   * **存取存放庫資訊**  — 可讓使用者取得存取Cloud Manager Git存放庫所需的資訊
   * **了解更多**  — 導覽至了解CI/CD管道檔案資源。

      ![](assets/prod-one.png)
   >[!NOTE]
   >
   >管道執行期間，會顯示目前步驟，且只有&#x200B;**Details**&#x200B;動作可用。

## 後續步驟 {#the-next-steps}

設定管道後，您需要部署程式碼。

如需詳細資訊，請參閱[部署程式碼](deploying-code.md) 。
