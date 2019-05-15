---
title: 設定您的CI/CD管線
seo-title: 設定您的CI/CD管線
description: 請遵循此頁面，從Cloud Manager設定您的管道設定。
seo-description: '在開始部署程式碼之前，您必須從AEM Cloud Manager設定您的管線設定。 '
uuid: 35fd56ac-dc9 c-4aca-6ad6-36c29 c4 ec497
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 使用
content-type: 引用
discoiquuid: ba6c763a-b78 a-439e-8c40-367203a719 b3
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 設定您的CI/CD管線 {#configure-your-ci-cd-pipeline}

以下頁面說明如何設定 **管道**。若要檢視更多有關管道運作方式的概念性資訊，請參閱 [CI/CD管線概觀](ci-cd-pipeline.md)。

## 瞭解流程 {#understanding-the-flow}

您可以從UI **的「管道設定** 」方塊設定渠道 [!UICONTROL Cloud Manager] 。

部署管理員負責設定管道。這樣做時，您先從 **Git存放庫中選取分支**。管道組態包含：

* 定義將啓動管線的觸發器。
* 定義控制生產部署的參數。
* 設定效能測試參數。

## 設定管道 {#setting-up-the-pipeline}

>[!CAUTION]
>
>無法設定管線，直到Git存放庫至少有一個分支和 [程式設定](setting-up-program.md) 完成為止。

在開始部署程式碼之前，您必須先設定您的管道設定 [!UICONTROL Cloud Manager]。

>[!NOTE]
>
>您可以在初次設定後變更管線設定。

### 設定管道設定，從 [!UICONTROL Cloud Manager]{#configuring-the-pipeline-settings-from-cloud-manager}

使用 [!UICONTROL Cloud Manager] UI設定程式後，您就可以設定您的管道。

請遵循下列步驟來設定管線的行為和偏好設定：

1. 按一下 **「設定管道** 」以設定及設定您的管道。

   ![](assets/Configure_ci-cd-1.png)

1. 隨即顯示 **「設定管道** 」畫面。

   三步驟精靈可讓您設定您的 **分支**、 **環境**和 **測試** 環境。
選取「Git」分支，然後按「 **Next**」(下一步)。

   >[!NOTE]
   >
   >在Git存放庫中找到的分支會連結至您的程式。

   ![](assets/Configure_ci-cd-2.png)


1. 存取 **「環境** 」索引標籤，選取 **「舞台(Stage)」** 和 **「生產(Production)」** 選項。

   您可以定義觸發器來啓動管線：

   * **在「Git變更** 」(Git變更)中，每當已將逗號新增至配置的壁虎分支時，就會啓動CI/CD管線。即使您選取此選項，也可以手動啓動管線。
   * **手動** -使用UI手動啓動管線。
   * **已排程** -此選項即將於即將發行的版本中推出。
   在管道設定或編輯期間，部署管理員可選擇在任何品質關卡(例如程式碼品質、安全性測試和效能測試)中遇到重要故障時，定義管線行為。

   這對於想要更自動化程序的客戶而言，是很有用的。可用的選項包括：

* **每次詢問** -這是預設設定，而且需要手動執行任何重大失敗。
* **立即失敗** -如果已選取，當發生重大故障時，管線將會被取消。這基本上是模擬使用者手動拒絕每個失敗。
* **立即繼續** -如果選取了，當發生重大失敗時，管線會自動繼續。這基本上是模擬使用者手動核准每個失敗。

   現在您定義控制生產部署的參數。下列可用選項如下：

* **使用上線核准** -必須由企業擁有者、專案經理或部署管理員手動核准部署 [!UICONTROL Cloud Manager] 。
* **使用CSE監督** -參與實際啓動部署。在啓用CSE監督時進行管線設定或編輯時，部署管理員可選擇選取：

   * **任何CSE**：是指任何可用的CSE
   * **我的CSE**：是指指派給客戶或其備份的特定CSE，如果CSE不在辦公室中

* **已排程** -此選項可讓使用者啓用排程的生產部署。

>[!NOTE]
>
>如果選取 **「已排程** 」選項，您可以在舞台部署 **後** 排程生產部署至管線(並 **使用GoLive核准**(如果已啓用)，等待設定排程。使用者也可以選擇立即執行生產部署。
>
>請參閱 [**部署您的程式碼**](deploying-code.md)，以設定部署計劃或立即執行生產。

![](assets/Configure_ci-cd-3.png)

>[!NOTE]
>
>「 **使用CSE監督** 」選項不適用於所有客戶。

**Dispatcher失效**

身為部署管理員，您有機會設定一組路徑，在設定或編輯管線時，此路徑將會 **在AEM Dispatcher快取中失效** 或 **重新整理** 。

您可以設定「舞台(Stage)」和「生產(Production)」部署的個別路徑集。如果設定，這些快取動作會在部署任何內容封裝後執行，做為部署管線步驟的一部分。這些設定使用標準AEM Dispatcher行為-失效會執行快取失效，類似於從作者啓動內容時的內容；push會執行快取刪除。

一般來說，使用無效動作是最好的方式，但有時可能需要刷新，尤其是在使用AEM HTML Client Libraries時。

>[!NOTE]
>
>請參閱 [Dispatcher概述](dispatcher-configurations.md) 取得有關Dispatcher快取的更多資訊。

請遵循下列步驟來設定Dispatcher失效：

1. 按一下 **「Dispatcher Configuration」標題** 下的「Configure」(設定)

   ![](assets/image2018-8-7_14-53-24.png)

1. 輸入路徑，從 **「類型**」選取動作，然後按一下 **「新增**」。每個環境最多可指定100個路徑。新增路徑後，按一下 **「套用」**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 返回 **「管道設定** 」頁面後，您將看到選取範圍的更新摘要。

   按一下 **「儲存** 」以保存此設定。

   ![](assets/image2018-8-7_15-4-30.png)

1. 存取「 **測試** 」標籤，定義您的程式的測試准則。

   現在，您可以設定效能測試參數。

   您可以根據您已授權的產品，設定 *AEM Sites* 和 *AEM Assets* 效能測試。

   **AEM Sites:**

   Cloud Manager會在測試階段伺服器上請求頁面(為未驗證的使用者)，以執行AEM Sites程式的效能測試，並測量每個頁面的回應時間以及各頁面的回應時間。頁面由三個 **頁面集合選取**；您可以從一個到全部三個集進行選擇。流量的分配是根據所選的設定數目，也就是說，如果所有三個項目都已選取，則每個集合會放置33%的頁面檢視總數；如果選取兩個，則50%移至每個集合；如果選取了一個，則100%流量都會移至該設定。

   例如，假設「熱門即時頁面」和「新頁面」設定之間有50%/50%的分割(在此範例中，「其他即時頁面」未使用)和「新頁面」集包含3000頁。每分鐘KPI的頁面檢視設為200。30分鐘測試期間：

   * 「熱門即時頁面」設定中的每個25頁都會點擊240次-((200*0.5)/25)*30=120

   * 「新頁面」設定中的每個頁面都將點擊一次-((200*0.5)/3000)*30=1
   ![](assets/Configuring_Pipeline_AEM-Sites.png)

   **AEM Assets:**

   Cloud Manager會在30分鐘測試期間內重復上傳資產，並測量每個資產的處理時間以及各種系統層級量度，執行AEM Assets程式的效能測試。此功能可同時上傳影像和PDF文件。在「管線設定」或「編輯」畫面中，會設定每分鐘上傳每個類型資產的資產數。

   例如，如果使用70/30分割，請參閱下圖。每分鐘上傳10個資產，每分鐘上傳個影像和份文件。

   ![](assets/Configuring_Pipeline_AEM-Assets.png)

   >[!NOTE]
   >
   >有預設影像和PDF文件，但是大部分的情況下，客戶會想要上傳自己的資產。這可從「管道設定」或「編輯」畫面完成。Photoshop、Illustrator和PostScript檔案支援常見的影像格式，例如JPEG、PNG、GIF和BMP。

1. 按一下 **「儲存** 」以完成管線程序的設定。

   >[!NOTE]
   >
   >此外，當您設定管線後，您仍可從UI使用 **「管道設定** 」方塊編輯 [!UICONTROL Cloud Manager] 相同的設定。

   ![](assets/Configuring_Pipeline-Settings.png)

## 僅限非生產與程式碼品質管線

除了部署至佈置和生產的主要管線外，客戶也可以設定其他管道，稱為 **非生產管線**。這些管道一律會執行建置和程式碼品質步驟。他們也可以選擇部署至Adobe Managed Services環境。

在主畫面上，這些管道會列在新的卡片中：

1. 從Cloud Manager首頁畫面存取 **「非生產管道** 」方塊。

   ![](assets/Configuring_Pipeline_Add-Production.png)

1. 按一下「新增」按鈕，指定「管線名稱」、「管線類型」和「Git分支」。

   此外，您也可以從「管道選項」設定部署觸發器和重要失敗行為。

   ![](assets/Configuring_Pipeline_Add-Production2.png)

1. 按一下 **「儲存」** ，並以三個動作顯示在首頁上的資訊卡上：

   * **編輯** -允許編輯管線設定
   * **詳細資料** -顯示上次管線執行(如果有的話)
   * **構建** -導覽至執行頁面，從中執行管線
   ![](assets/Configuring_Pipeline_Add-Production3.png)

   >[!NOTE]
   >
   >當管線執行時，會顯示目前的步驟，只會有 **「詳細資料** 」動作可供使用。

## 後續步驟 {#the-next-steps}

設定渠道後，您需要部署程式碼。

如需詳細資訊，請參閱 [部署您的程式碼](deploying-code.md) 。
