---
title: 設定 CI/CD 管道
seo-title: 設定 CI/CD 管道
description: 請依照本頁，從Cloud Manager設定您的管道設定。
seo-description: '在開始部署程式碼之前，您必須從Cloud Manager設定您的管AEM線設定。 '
uuid: 35fd56ac-dc9c-4aca-8ad6-36c29c4ec497
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
content-type: reference
discoiquuid: ba6c763a-b78a-439e-8c40-367203a719b3
translation-type: tm+mt
source-git-commit: 5542942da33efc2926e62cce00ea39e3c65b3e16
workflow-type: tm+mt
source-wordcount: '1776'
ht-degree: 1%

---


# 設定 CI/CD 管道 {#configure-your-ci-cd-pipeline}

下頁說明如何配置&#x200B;**Pipeline**。 要查看有關管線工作方式的更多概念資訊，請參閱[CI/CD管線概述](ci-cd-pipeline.md)。

## 教學影片{#video-tutorial-one}

### 在Cloud Manager中配置管線{#config-pipeline-video}

CI/CD Production Pipeline配置定義將啟動管線的觸發器、控制生產部署和效能測試參數的參數。

>[!VIDEO](https://video.tv.adobe.com/v/26314/)


## 瞭解流{#understanding-the-flow}

您可以從 **** UI [!UICONTROL Cloud Manager]的「Pipeline Settings 」 (管道設定) 圖格來設定管道。

部署管理器負責設定管道。 執行此操作時，首先從&#x200B;**Git Repository**&#x200B;中選擇一個分支。 管線配置包括：

* 定義將啟動管線的觸發器。
* 定義控制生產部署的參數。
* 配置效能測試參數。

## 設定管線{#setting-up-the-pipeline}

>[!CAUTION]
>
>在Git儲存庫至少有一個分支且[程式設定](setting-up-program.md)完成之前，無法設定管線。

開始部署代碼之前，必須從[!UICONTROL Cloud Manager]配置管線設定。

>[!NOTE]
>
>可在初始設定後更改管線設定。

### 從[!UICONTROL Cloud Manager] {#configuring-the-pipeline-settings-from-cloud-manager}配置管線設定

使用[!UICONTROL Cloud Manager] UI設定程式後，您就可以設定管線。

請依照下列步驟來設定管道的行為和偏好設定：

1. 按一下「設定管線」(Setup Pipeline)「**」(**)以設定和配置管線。

   ![](assets/Setup-Pipeline.png)

1. 將顯示&#x200B;**設定管線**&#x200B;螢幕。

   三步嚮導允許您設定&#x200B;**Branch**、**Environments**&#x200B;和&#x200B;**Testing**環境。
選擇Git分支，然後按一下**Next**。

   >[!NOTE]
   >
   >在Git儲存庫中找到的分支會連結至您的程式。


1. 訪問&#x200B;**環境**&#x200B;頁籤以選擇&#x200B;**Stage**&#x200B;和&#x200B;**Production**&#x200B;選項。

   可定義觸發器以啟動管線：

   * **On Git Changes** -每當有提交添加到配置的git分支時，啟動CI/CD管線。即使選取此選項，也始終可以手動啟動管線。
   * **手動** -使用UI手動啟動管線。

   在管道設定或編輯期間，當在任何質量門（如代碼質量、安全性測試和效能測試）中遇到重要故障時，部署管理器可以選擇定義管道的行為。

   這對希望實現更自動化流程的客戶非常有用。 可用的選項包括：

* **每次詢問** -這是預設設定，需要手動干預任何重要故障。
* **立即取消** -如果選中此選項，則每當出現「重要」(Impertient)故障時，管線將被取消。這實際上是模擬使用者手動拒絕每個失敗。
* **立即批准** -如果選中此選項，當出現「重要」故障時，管線將自動繼續。這實際上是在模擬用戶手動批准每個故障。

   現在，您可以定義控制生產部署的參數。 三種可用選項如下：

* **使用上線核准** -部署必須由業務擁有者、專案經理或部署經理透過 [!UICONTROL Cloud Manager] UI手動核准。
* **使用CSE監督** -參與CSE以實際開始部署。在管線設定或啟用CSE監督時編輯期間，部署管理員可以選擇：

   * **任何CSE**:是指任何可用的CSE
   * **我的CSE**:是指指派給客戶的特定CSE或其備份（如果CSE不在辦公室）

* **已排程** -此選項可讓使用者啟用已排程的生產部署。

>[!NOTE]
>
>如果選擇了「已調度」**「已調度」**&#x200B;選項，則可以在階段部署&#x200B;**(和**&#x200B;使用GoLive批准&#x200B;**，如果已啟用)之後將生產部署計畫安排到流水線。**&#x200B;使用者也可以選擇立即執行生產部署。
>
>請參閱&#x200B;[**部署您的程式碼**](deploying-code.md)，以設定部署排程或立即執行生產。

![](assets/configure-pipeline-new.png)

>[!NOTE]
>
>**使用CSE監督**&#x200B;選項不適用於所有客戶。

**在階段部署後核准**

可在生產管線中配置一個可選步驟&#x200B;**在階段部署後批准**。
在**管線編輯**&#x200B;螢幕上的新選項中啟用此選項：

![](assets/post_deployment1.png)

然後，在管線執行期間，它會顯示為個別步驟：

![](assets/post_deployment2.png)

>[!NOTE]
>
>**在階段部署後** 進行核准的功能與在生產部署前進行核准類似，但是會在階段部署步驟（即在測試完成之前）後立即執行，而在生產部署完成之後，則會先進行核准。

**Dispatcher Invalidation**

作為部署管理員，您有機會在設定或編輯管線時配置一組內容路徑，這些路徑將從AEMDispatcher快取中為發佈實例清除&#x200B;**無效**&#x200B;或&#x200B;**。**

您可以為「舞台(Stage)」和「生產(Production)」部署設定個別的路徑集。 如果已配置，則這些快取動作將作為部署管線步驟的一部分執行，就在部署任何內容封裝後執行。 這些設定使用標準AEM的Dispatcher行為——使快取失效，類似於從作者激活內容以發佈時；flush會執行快取刪除。

通常，最好使用無效動作，但有時可能需要刷新，尤其是使用AEMHTML客戶端庫時。

>[!NOTE]
>
>請參閱[Dispatcher Overview](dispatcher-configurations.md)以獲取有關Dispatcher快取的詳細資訊。

按照以下步驟配置Dispatcher Invalidations:

1. 按一下「Dispatcher Configuration」標題下的&#x200B;**Configure**

   ![](assets/image2018-8-7_14-53-24.png)

1. 輸入路徑，從&#x200B;**Type**&#x200B;中選擇操作，然後按一下&#x200B;**Add**。 每個環境最多可以指定100個路徑。 添加路徑後，按一下&#x200B;**應用**。

   ![](assets/image2018-8-7_14-58-11.png)

1. 回到&#x200B;**管線設定**&#x200B;頁面後，您將會看到選項的更新摘要。

   按一下&#x200B;**保存**&#x200B;以保存此配置。

   ![](assets/image2018-8-7_15-4-30.png)


1. 訪問&#x200B;**Testing**&#x200B;頁籤，以定義程式的測試標準。

   現在，您可以設定效能測試參數。

   您可以根據您擁有的授權產品，設定&#x200B;*AEM Sites*&#x200B;和&#x200B;*AEM Assets*&#x200B;效能測試。

   **AEM Sites:**

   Cloud Manager會在舞台發佈伺服器上要求頁面（依預設為未驗證的使用者）30分鐘的測試時段，並測量每個頁面的回應時間以及各種系統層級度量，以執行AEM Sites程式的效能測試。 這些請求是從一組已知的專用地址發出的。 您可向客戶成功工程師或Adobe代表取得地址範圍。

   在30分鐘測試期開始之前，Cloud Manager將使用客戶成功工程師配置的一組或多個&#x200B;*seed* URL來編目Stage環境。 從這些URL開始，會檢查每個頁面的HTML，並以寬度優先的方式瀏覽連結。 此編目程式最多限制為5000頁。 來自Crawler的請求有10秒的固定逾時。

   頁面由三個&#x200B;**頁面集**&#x200B;選擇；您可以選擇從一組到三組的任意位置。 流量的分配是根據選擇的集數，即如果全部三個都被選中，則33%的頁面檢視會放入每個集；如果選取2個，則每組50%;如果選取其中一個，則100%的流量會移至該集合。

   例如，假設「熱門即時頁面」和「新頁面」集（在此範例中，未使用其他即時頁面）之間有50%/50%的分割，而「新頁面」集包含3000個頁面。 每分鐘頁面檢視次數KPI設定為200。 在30分鐘的測試期間：

   * 「熱門即時頁面」集中的25個頁面，每個頁面將被點擊120次-((200 * 0.5)/ 25)* 30 = 120

   * 「新頁面」集中的3000個頁面中，每個頁面都會點擊一次-((200 * 0.5)/ 3000)* 30 = 1

   ![](assets/Configuring_Pipeline_AEM-Sites.png)

   如需詳細資訊，請參閱[已驗證的效能測試](#authenticated-performance-testing)。

   **AEM Assets:**

   Cloud Manager會在30分鐘的測試期間內重複上傳資產，並測量每個資產的處理時間以及各種系統層級的度量，以執行AEM Assets程式的效能測試。 此功能可上傳影像和PDF檔案。 每分鐘上載的每種類型的資產數量分佈在「管線設定」或「編輯」螢幕中設定。

   例如，如果使用70/30分割，如下圖所示。 每分鐘上傳10個資產，每分鐘上傳7個影像和3個檔案。

   ![](assets/Configuring_Pipeline_AEM-Assets.png)

   >[!NOTE]
   >
   >有預設影像和PDF檔案，但在大多數情況下，客戶會想要上傳自己的資產。 這可從「管線設定」(Pipeline Setup)或「編輯」(Edit)螢幕中完成。 JPEG、PNG、GIF和BMP等常用影像格式以及Photoshop、Illustrator和Postscript檔案都受支援。

1. 按一下&#x200B;**保存**&#x200B;以完成管線進程的設定。

   >[!NOTE]
   >
   >此外，在設定管線後，您仍可使用[!UICONTROL Cloud Manager] UI的&#x200B;**「生產管線設定」(Production Pipeline Settings)**&#x200B;圖格來編輯相同的設定。

   ![](assets/Production-Pipeline.png)

### 已驗證的效能測試{#authenticated-performance-testing}

具有已驗證網站的AMS客戶可以指定Cloud Manager在Sites效能測試期間用來存取網站的使用者名稱和密碼。

用戶名和口令被指定為[管線變數](/help/using/build-environment-details.md#pipeline-variables)，名稱為`CM_PERF_TEST_BASIC_USERNAME`和`CM_PERF_TEST_BASIC_PASSWORD`。

雖然並非嚴格要求，但建議使用字串變數類型做為username，並建議使用secretString變數類型作為密碼。 如果同時指定了這兩者，則效能測試Crawler和測試虛擬用戶的每個請求都將包含這些憑據作為HTTP Basic身份驗證。

要使用[Cloud Manager CLI](https://github.com/adobe/aio-cli-plugin-cloudmanager)設定這些變數，請運行：

`$ aio cloudmanager:set-pipeline-variables <pipeline id> --variable CM_PERF_TEST_BASIC_USERNAME <username> --secret CM_PERF_TEST_BASIC_PASSWORD <password>`

## 非生產和代碼純質量管道

除了部署到生產階段的主管道外，客戶還可以設定額外的管道，稱為&#x200B;**非生產管道**。 這些管線始終執行構建和代碼質量步驟。 他們也可以選擇性地部署至Adobe Managed Services環境。

## 教學影片{#video-tutorial-two}

### Cloud Manager非生產和僅代碼質量管道{#non-prod-video}

CI/CD非生產管道分為代碼質量管道和部署管道兩類。 程式碼品質會從Git分支輸入所有程式碼，以根據Cloud Manager的程式碼品質掃描來建立和評估。

>[!VIDEO](https://video.tv.adobe.com/v/26316/)

在主螢幕上，新卡中列出了以下管線：

1. 從Cloud Manager主螢幕訪問&#x200B;**非生產管線**&#x200B;表徵圖。

   ![](assets/Non-Production-Pipeline.png)

1. 按一下「添加」(Add)按鈕，指定「管線名稱」(Pipeline Name)、「管線類型」(Pipeline Type)和「Git分支」(Git Branch)。

   此外，還可以從Pipeline Options中設定部署觸發器和重要故障行為。

   ![](assets/non-prod-pipe.png)

1. 按一下&#x200B;**Save** ，主螢幕上的卡上將顯示管線，並執行以下三個操作：

   * **編輯** -允許編輯管線設定
   * **Detail**  —— 顯示上次管線執行（如果有）
   * **Build**  —— 導航到執行頁，可從中執行管線

   ![](assets/Non-prod-2.png)

   >[!NOTE]
   >
   >在管線運行時，將顯示當前步驟，並且僅提供&#x200B;**Details**&#x200B;操作。

## 後續步驟{#the-next-steps}

在設定管道後，您需要部署程式碼。

如需詳細資訊，請參閱[部署您的程式碼](deploying-code.md)。
