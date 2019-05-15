---
title: 部署您的程式碼
seo-title: 部署您的程式碼
description: 'null'
seo-description: 設定您的管道(儲存庫、環境和測試環境)後，即可部署您的程式碼。請依照本頁瞭解更多資訊。
uuid: 4e3807e1-437e-4922-ba48-0badf293 a99
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 使用
discoiquuid: 832a4647-9b83-4a9d-b373-30Fe16092 b15
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 部署您的程式碼 {#deploy-your-code}

## 使用Cloud Manager部署程式碼 {#deploying-code-with-cloud-manager}

設定 **您的管道** (儲存庫、環境和測試環境)後，即可部署您的程式碼。

1. 按一下 **Cloud Manager中** 的部署，以開始部署程序。

   ![](assets/Deploy1.png)

1. 隨即顯示 **「管道執行** 」畫面。

   按一下 **「建立** 」以開始處理程序。

   ![](assets/Deploy2.png)

1. 完整的建置程序會部署您的程式碼。

   建立程序涉及下列階段：

   1. 階段部署
   1. 測試階段測試
   1. 生產部署
   >[!NOTE]
   >
   >此外，您可以檢視各種部署程序的步驟，檢視記錄檔或檢視結果，以瞭解測試准則。

   **「舞台部署**」包含下列步驟：

   * 建置與單元測試
   * 程式碼掃描
   * 部署至舞台
   ![](assets/Stage_Testing.png)

   **Stage Testing**(舞台測試)包含下列步驟：

   * 安全性測試
   * 效能測試
   ![](assets/Stage_Deployment.png)

   **生產部署**包含下列步驟：

   * **Application for Approval** (if enabled)
   * **排程生產部署** (如果已啓用)
   * **CSE支援** (如果已啓用)
   * **部署至生產環境**
   >[!NOTE]
   >
   >設定管線時，啓用 **「排程生產部署** 」。
   >
   >
   >使用此選項，您可以排程生產刪除，或按一下 **「現在」** 以立即執行生產部署。
   >
   >
   >排程日期和時間會按照使用者的時區指定。
   >
   >
   >按一下 **「確認** 」以確認您的設定。

   ![](assets/Production_Deployment1.png)

   在您確認部署計劃後，程式碼部署就會完成。

   會顯示下列畫面，並從上方步驟選取 **「現在」** 選項。

   ![](assets/Production_Deployment2.png)

## 部署程序 {#deployment-process}

下節說明AEM和Dispatcher套件如何在階段階段和生產階段中部署。

Cloud Manager會將建置程序產生的所有目標/.zip檔案上傳至儲存位置。這些項目是在管線部署階段期間從此位置擷取。

當Cloud Manager部署到非生產環境時，其目標是盡快完成部署，因此會同時部署這些項目至所有節點：

1. Cloud Manager會決定每個工作流程是AEM或dispatcher套件。
1. Cloud Manager會移除「載入平衡器」中的所有發送器，以在部署期間隔離環境。
1. 每個AEM實例都是透過Package Manager API部署到每個AEM實例，而封裝管理員則會決定部署順序。

   若要進一步瞭解如何使用套件來安裝新功能、在例項之間傳輸內容，以及備份存放庫內容，請參閱如何使用套件。

   >[!NOTE]
   >
   >所有AEM影像都會部署給作者和發行者。當需要特定節點組態時，應運用執行模式。若要進一步瞭解執行模式如何讓您根據特定用途調整AEM實例，請參閱執行模式。

1. dispatcher atiactual會部署至每個發送器，如下所示：

   1. 目前的設定會備份並複製至暫存位置
   1. 除了無法執行的檔案外，所有設定都會被刪除。如需詳細資訊，請參閱管理您的Dispatcher組態。如此會清除目錄，以確保不會留下孤立的檔案。
   1. 此主題會擷取至httpd目錄。不會覆寫無法管理的檔案。在部署時，您對git存放庫所做的任何變更都會被忽略。這些檔案是AMS Dispatcher架構的核心，無法變更。
   1. Apache會執行config測試。如果找不到任何錯誤，則會重新載入服務。如果發生錯誤，則會從備份還原設定，重新載入服務，並回報錯誤回Cloud Manager。
   1. 管線組態中指定的每個路徑都會失效或從dispatcher快取中清除。
   >[!NOTE]
   >
   >Cloud Manager預期dispatcher Artifact會包含完整的檔案集。所有dispatcher組態檔都必須存在於git存放庫中。遺失檔案或資料夾將導致部署失敗。

1. 所有AEM和Dispatcher套件成功部署至所有節點後，系統會將調度器新增回負載平衡器，並完成部署。

### 部署至生產階段 {#deployment-production-phase}

部署至生產環境的程序稍有差異，以降低對AEM網站訪客的影響。

生產部署通常遵循上述步驟，但以滾動方式執行：

1. 將AEM套件部署至作者。
1. 來自負載平衡器的detch dispatcher1。
1. 部署AEM封裝以發佈1和dispatcher封裝至dispatcher1、purchum dispatcher快取。
1. 將dispatcher放回負載平衡器中。
1. 在dispatcher返回服務後，從負載平衡器取消鎖定dispatcher2。
1. 部署AEM套件以發佈和傳送chatcher封裝至dispatcher2、purchum dispatcher快取。
1. 將dispatcher放回負載平衡器中。
此程序會繼續進行，直到部署已送達拓撲中的所有發佈商和調度員。


