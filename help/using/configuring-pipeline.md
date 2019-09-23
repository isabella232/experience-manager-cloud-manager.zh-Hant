---
title: 配置CI/CD管線
seo-title: 配置CI/CD管線
description: 請依照本頁，從Cloud manager設定您的管道設定。
seo-description: '開始部署程式碼之前，您必須從AEM Cloud Manager設定您的管道設定。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 使用
content-type: 引用
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
translation-type: tm+mt
source-git-commit: 862501f28f5104d0829a6d2d2ad5f5ce9f8ba341

---


# 配置CI/CD管線 {#configure-your-ci-cd-pipeline}

下頁說明了如何配置管 **線**。 若要檢視管道運作方式的更多概念性資訊，請參閱 [CI/CD管道概觀](ci-cd-pipeline.md)。

## 瞭解流程 {#understanding-the-flow}

您可以從UI的「管線設 **定」圖格** ，設定管 [!UICONTROL Cloud Manager] 線。

部署管理器負責設定管道。 執行此操作時，首先從 **Git Repository中選擇一個分支**。 管線配置包括：

* 定義將啟動管線的觸發器。
* 定義控制生產部署的參數。
* 配置效能測試參數。

## 設定管線 {#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git儲存庫至少有一個分支且程式設定完成之前，無法 [設定管道](setting-up-program.md) 。

開始部署代碼之前，必須從中配置管線設定 [!UICONTROL Cloud Manager]。

>[!NOTE]
>
>可在初始設定後更改管線設定。

### 從配置管線設定 [!UICONTROL Cloud Manager]{#configuring-the-pipeline-settings-from-cloud-manager}

使用 [!UICONTROL Cloud Manager] UI設定程式後，您就可以設定管道。

請依照下列步驟來設定管道的行為和偏好設定：

1. 按一下「 **設定管線** 」(Setup Pipeline)以設定和配置管線。

   ![](assets/Configure_ci-cd-1.png)

1. 將顯 **示「設定管線** 」螢幕。

   三步嚮導允許您設定 **Branch**、 **Environments**&#x200B;和 **Testing** 環境。
選取您的Git分支，然後按一 **下Next**。

   >[!NOTE]
   >
   >在Git儲存庫中找到的分支會連結至您的程式。

   ![](assets/Configure_ci-cd-2.png)


1. 存取「 **環境** 」標籤以選 **擇「舞台** 」 **和「生產** 」選項。

   可定義觸發器以啟動管線：

   * **On Git Changes** —— 每當有提交添加到配置的git分支時，啟動CI/CD管線。 即使選取此選項，也始終可以手動啟動管線。
   * **手動** -使用UI手動啟動管線。
   * **已排程** -這個選項即將在即將發行的版本中推出。
   在管道設定或編輯期間，當在任何質量門（如代碼質量、安全性測試和效能測試）中遇到重要故障時，部署管理器可以選擇定義管道的行為。

   這對希望實現更自動化流程的客戶非常有用。 可用的選項包括：

* **每次詢問** -這是預設設定，需要手動干預任何重要故障。
* **立即失敗** -如果選中此選項，當出現「重要」(Impertient)故障時，管線將被取消。 這實際上是模擬使用者手動拒絕每個失敗。
* **立即繼續** -如果選中此選項，則每當出現「重要」(Impertient)故障時，管線將自動繼續。 這實際上是在模擬用戶手動批准每個故障。

   現在，您可以定義控制生產部署的參數。 三種可用選項如下：

* **使用上線核准** -部署必須由業務擁有者、專案經理或部署經理透過 [!UICONTROL Cloud Manager] UI手動核准。
* **使用CSE監督** -參與CSE以實際開始部署。 在管線設定或啟用CSE監督時編輯期間，部署管理員可以選擇：

   * **任何CSE**:是指任何可用的CSE
   * **我的CSE**:是指指派給客戶的特定CSE或其備份（如果CSE不在辦公室）

* **已排程** -此選項可讓使用者啟用已排程的生產部署。

>[!NOTE]
>
>如果選 **取** 「已排程」選項，您可以在階段部署後將生產部署排程至管道(若已啟用，則 **使用GoLive Approval******)，以等待排程設定。 使用者也可以選擇立即執行生產部署。
>
>請參閱「 [**部署程式碼**](deploying-code.md)」，以設定部署排程或立即執行生產。

![](assets/Configure_ci-cd-3.png)

>[!NOTE]
>
>「使 **用CSE監督** 」選項不適用於所有客戶。

**Dispatcher Invalidation**

身為部署管理員，您有機會設定一組路徑，在設定或編輯管線時，這些路徑會 **使****AEM Dispatcher快取無效或被清除** 。

您可以為「舞台(Stage)」和「生產(Production)」部署設定個別的路徑集。 如果已配置，則這些快取動作將作為部署管線步驟的一部分執行，就在部署任何內容封裝後執行。 這些設定使用標準的AEM Dispatcher行為——無效執行快取失效，類似於從作者啟動內容以進行發佈；flush會執行快取刪除。

一般而言，使用無效動作較為可取，但有時可能需要刷新，尤其是在使用AEM HTML Client Libraries時。

>[!NOTE]
>
>請參閱 [Dispatcher概述](dispatcher-configurations.md) ，以取得有關Dispatcher快取的詳細資訊。

按照以下步驟配置Dispatcher Invalidations:

1. 按一下 **Dispatcher Configuration標題下的** Configure（配置）

   ![](assets/image2018-8-7_14-53-24.png)

1. 輸入路徑，從「類型」( **Type**)中選擇操作 **，然後按一下「**&#x200B;添加」(Add)。 每個環境最多可以指定100個路徑。 新增路徑後，按一下「套 **用」**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 返回「管線設 **置」頁** ，您將看到選擇的更新摘要。

   按一 **下「儲存** 」以保存此設定。

   ![](assets/image2018-8-7_15-4-30.png)

1. 存取「 **測試** 」標籤，以定義您方案的測試准則。

   現在，您可以設定效能測試參數。

   您可以設 *定AEM Sites* 和 *AEM Assets* Performance Testing，視您擁有的授權產品而定。

   **AEM Sites:**

   Cloud manager會在階段發佈伺服器上請求頁面（身為未驗證的使用者）達30分鐘的測試期間，並測量每個頁面的回應時間以及各種系統層級度量，以執行AEM Sites程式的效能測試。頁面由三個頁面集 **選取**;您可以選擇從一組到三組的任意位置。 流量的分配是根據選擇的集數，即如果全部三個都被選中，則33%的頁面檢視會放入每個集；如果選取2個，則每組50%;如果選取其中一個，則100%的流量會移至該集合。

   例如，假設「熱門即時頁面」和「新頁面」集（在此範例中，未使用其他即時頁面）之間有50%/50%的分割，而「新頁面」集包含3000個頁面。 每分鐘頁面檢視次數KPI設定為200。 在30分鐘的測試期間：

   * 「熱門即時頁面」集中的25個頁面，每個頁面將被點擊240次-((200 * 0.5)/ 25)* 30 = 120

   * 「新頁面」集中的3000個頁面中，每個頁面都會點擊一次-((200 * 0.5)/ 3000)* 30 = 1
   ![](assets/Configuring_Pipeline_AEM-Sites.png)

   **AEM Assets:**

   Cloud Manager會重複上傳資產30分鐘的測試期間，並測量每個資產的處理時間以及各種系統層級的度量，以執行AEM Assets程式的效能測試。 此功能可上傳影像和PDF檔案。 每分鐘上載的每種類型的資產數量分佈在「管線設定」或「編輯」螢幕中設定。

   例如，如果使用70/30分割，如下圖所示。 每分鐘上傳10個資產，每分鐘上傳7個影像和3個檔案。

   ![](assets/Configuring_Pipeline_AEM-Assets.png)

   >[!NOTE]
   >
   >有預設影像和PDF檔案，但在大多數情況下，客戶會想要上傳自己的資產。 這可從「管線設定」(Pipeline Setup)或「編輯」(Edit)螢幕中完成。 Photoshop、Illustrator和Postscript檔案支援常見的影像格式，例如JPEG、PNG、GIF和BMP。

1. 按一下 **「保存** 」(Save)以完成管線流程的設定。

   >[!NOTE]
   >
   >此外，在設定管線後，您仍可使用 **UI中的「生產管線設定」圖格來編輯相同的設**[!UICONTROL Cloud Manager] 定。

   ![](assets/Prod-Pipeline-Settings-Dialog.png)

## 非生產和代碼純質量管道

除了部署到生產階段的主管道外，客戶還可以設定額外的管道，即非生 **產管道**。 這些管線始終執行構建和代碼質量步驟。 他們也可以選擇性地部署至Adobe Managed Services環境。

在主螢幕上，新卡中列出了以下管線：

1. 從Cloud manager **主畫面存取「非生產管道** 」圖格。

   ![](assets/Configuring_Pipeline_Add-Production.png)

1. 按一下「添加」(Add)按鈕，指定「管線名稱」(Pipeline Name)、「管線類型」(Pipeline Type)和「Git分支」(Git Branch)。

   此外，還可以從Pipeline Options中設定部署觸發器和重要故障行為。

   ![](assets/Configuring_Pipeline_Add-Production2.png)

1. 按一 **下「儲存** 」(Save)，主畫面上的資訊卡上會顯示管線，並執行下列三個動作：

   * **編輯** -允許編輯管線設定
   * **Detail** —— 顯示上次管線執行（如果有）
   * **Build** —— 導航到執行頁，可從中執行管線
   ![](assets/Configuring_Pipeline_Add-Production3.png)

   >[!NOTE]
   >
   >在管線運行時，將顯示當前步驟，並且只有「詳細 **資訊** 」(Details)操作可用。

## 後續步驟 {#the-next-steps}

在設定管道後，您需要部署程式碼。

如需詳細 [資訊，請參閱](deploying-code.md) 「部署程式碼」。
