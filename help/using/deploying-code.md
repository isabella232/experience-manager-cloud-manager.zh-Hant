---
title: 部署程式碼
seo-title: 部署程式碼
description: 提供Cloud Manager中部署程式的概述
seo-description: 瞭解在配置了管道（儲存庫、環境和測試環境）後，如何部署代碼
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
feature: Code Deployment
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 1%

---


# 部署程式碼 {#deploy-your-code}

## 使用Cloud Manager部署代碼{#deploying-code-with-cloud-manager}

一旦配置了生產管線（儲存庫、環境和測試環境），您就可以部署代碼。

1. 從Cloud Manager按一下「**部署**」以開始部署程式。

   ![](assets/Deploy1.png)

1. 將顯示&#x200B;**管線執行**&#x200B;螢幕。

   按一下&#x200B;**Build**&#x200B;啟動進程。

   ![](assets/Deploy2.png)

1. 完整的建立程式會部署您的程式碼。

   構建過程涉及以下階段：

   1. 階段部署
   1. 階段測試
   1. 生產部署

   >[!NOTE]
   >
   >此外，您也可以檢視記錄檔或檢視結果，以檢視各種部署程式中的步驟，以取得測試標準。

   「 **舞台部署**」涉及以下步驟：

   * 驗證：此步驟確保將管線配置為使用當前可用資源，例如，已配置的分支存在，環境可用。
   * 構建和單元測試：此步驟會執行容器化的建立程式。 有關構建環境的詳細資訊，請參閱[瞭解構建環境](/help/using/build-environment-details.md)。
   * 代碼掃描：此步驟會評估您的應用程式碼的品質。 如需測試程式的詳細資訊，請參閱[瞭解測試結果](understand-your-test-results.md)。
   * 部署至舞台

   ![](assets/Stage_Deployment1.png)

   **階段測試**&#x200B;包含下列步驟：

   * 安全性測試：此步驟會評估應用程式碼對環境的安全AEM影響。 如需測試程式的詳細資訊，請參閱[瞭解測試結果](understand-your-test-results.md)。
   * 效能測試：此步驟會評估應用程式碼的效能。 如需測試程式的詳細資訊，請參閱[瞭解測試結果](understand-your-test-results.md)。

   ![](assets/Stage_Testing1.png)

   **生產部署**&#x200B;涉及以下步驟：

   * **申請核准** （如果已啟用）
   * **排程生產部署** （如果已啟用）
   * **CSE支援** （如果已啟用）
   * **部署至生產環境**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >在配置管線時，**計畫生產部署**&#x200B;已啟用。
   >
   >
   >使用此選項，您可以計畫生產部署，或按一下&#x200B;**Now**&#x200B;立即執行生產部署。
   >
   >
   >排程的日期和時間會根據使用者的時區指定。
   >
   >
   >按一下&#x200B;**確認**&#x200B;以驗證設定。

   ![](assets/Production_Deployment1.png)

   在確認部署排程後，您的程式碼部署就會完成。

   從上述步驟中選擇&#x200B;**Now**&#x200B;選項時，將顯示以下螢幕。

   ![](assets/Production_Deployment2.png)

## 部署過程{#deployment-process}

以下部分介紹在階AEM段階段和生產階段中如何部署和調度程式包。

Cloud Manager會將建立程式產生的所有目標/*.zip檔案上傳至儲存位置。  在管線的部署階段，會從此位置檢索這些對象。

當Cloud Manager部署到非生產拓撲時，其目標是盡快完成部署，因此對象將同時部署到所有節點，如下所示：

1. Cloud Manager會決定每個對象是AEM一個還是調度程式包。
1. Cloud Manager會從負載平衡器中刪除所有調度程式，以在部署期間隔離環境。

   除非另行配置，否則您可以跳過開發和階段部署中的負載平衡器更改，即分離和附加非生產管線中的步驟，以用於開發環境，以及生產管線中的步驟，用於階段環境。

   ![](assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能預期主要由1-1-1客戶使用。

1. 每個對AEM像都通過包管AEM理器API部署到每個實例，並且包依賴性決定部署順序。

   有關如何使用軟體包來安裝新功能、在實例之間傳輸內容以及備份儲存庫內容的詳細資訊，請參閱如何使用軟體包。

   >[!NOTE]
   >
   >所有AEM物件都會部署至作者和發佈者。 當需要特定節點的配置時，應使用運行模式。 若要進一步瞭解執行模式如何讓您針對特定目AEM的調整執行個體，請參閱執行模式。

1. 調度器對象按如下方式部署到每個調度器：

   1. 當前配置將備份並複製到臨時位置
   1. 除不可變檔案外，所有配置都將被刪除。 有關詳細資訊，請參閱管理Dispatcher配置。 這會清除目錄，以確保不會留下孤立的檔案。
   1. 該對象被提取到`httpd`目錄。  不會覆寫不可變的檔案。 在部署時，您對git儲存庫中不可變檔案所做的任何更改都將被忽略。  這些檔案是AMS調度器框架的核心檔案，不能更改。
   1. Apache會執行組態測試。 如果未找到錯誤，則重新載入服務。 如果發生錯誤，則從備份中恢復配置，重新載入服務，並將錯誤報告回Cloud Manager。
   1. 在流水線配置中指定的每個路徑都無效或從調度器快取中刷新。

   >[!NOTE]
   >Cloud Manager希望調度器對象包含完整檔案集。  所有調度程式配置檔案都必須存在於git儲存庫中。 缺少檔案或資料夾將導致部署失敗。

1. 成功將所有和分AEM發程式包部署到所有節點後，調度程式將添加回負載平衡器並完成部署。

   >[!NOTE]
   >您可以跳過開發和階段部署中的負載平衡器更改，即在非生產流水線、開發人員環境和生產流水線中分離和附加步驟，以用於階段環境。

### 部署到生產階段{#deployment-production-phase}

部署至生產拓撲的程式略有不同，以盡量降低對網站訪AEM客的影響。

生產部署通常遵循與上述步驟相同的步驟，但是以滾動方式：

1. 部署AEM要編寫的套件。
1. 從負載平衡器分離dispatcher1。
1. 將包部AEM署到publish1 ，並將調度程式包部署到pispatcher1 ，以並行方式刷新調度程式快取。
1. 將dispatcher1放回負載平衡器。
1. 在dispatcher1恢復服務後，請從負載平衡器分離dispatcher2。
1. 將包部AEM署到publish2 ，將調度程式包部署到pispatcher2並行刷新調度程式快取。
1. 將dispatcher2放回負載平衡器。
此過程將繼續，直到部署到拓撲中所有發佈者和調度程式為止。


