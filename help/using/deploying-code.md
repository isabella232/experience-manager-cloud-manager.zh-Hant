---
title: 部署程式碼
seo-title: 部署程式碼
description: 提供Cloud Manager中部署程式的概觀
seo-description: 了解如何在設定管道（存放庫、環境和測試環境）後部署程式碼
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
feature: 程式碼部署
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: df2f598f91201d362f54b17e4092ff6bd6a72cec
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 1%

---

# 部署程式碼 {#deploy-your-code}

## 使用Cloud Manager {#deploying-code-with-cloud-manager}部署程式碼

>[!NOTE]
>若要了解如何在AEM as aCloud Service中部署Cloud Manager的程式碼，請參閱[此處](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)。

一旦配置了生產管道（儲存庫、環境和測試環境），您就可以部署代碼。

1. 按一下Cloud Manager中的&#x200B;**Deploy**&#x200B;以啟動部署過程。

   ![](assets/Deploy1.png)

1. 將顯示&#x200B;**Pipeline Execution**&#x200B;螢幕。

   按一下&#x200B;**Build**&#x200B;以啟動進程。

   ![](assets/Deploy2.png)

1. 完成的建置程式會部署您的程式碼。

   建置程式涉及下列階段：

   1. 階段部署
   1. 階段測試
   1. 生產部署

   >[!NOTE]
   >
   >此外，您也可以檢視記錄或檢閱測試條件的結果，以檢閱各種部署程式的步驟。

   「 **舞台部署**」涉及以下步驟：

   * 驗證：此步驟可確保管道配置為使用當前可用資源，例如，配置的分支存在，環境可用。
   * 構建和單元測試：此步驟會執行容器化的建置程式。 如需有關建置環境的詳細資訊，請參閱[了解建置環境](/help/using/build-environment-details.md)。
   * 代碼掃描：此步驟會評估應用程式程式碼的品質。 如需測試程式的詳細資訊，請參閱[了解測試結果](understand-your-test-results.md)。
   * 部署至預備

   ![](assets/Stage_Deployment1.png)

   **階段測試**&#x200B;涉及以下步驟：

   * 安全測試：此步驟會評估應用程式程式碼對AEM環境的安全性影響。 如需測試程式的詳細資訊，請參閱[了解測試結果](understand-your-test-results.md)。
   * 效能測試：此步驟會評估應用程式程式碼的效能。 如需測試程式的詳細資訊，請參閱[了解測試結果](understand-your-test-results.md)。

   ![](assets/Stage_Testing1.png)

   **生產部署**&#x200B;涉及以下步驟：

   * **申請核准** （如果已啟用）
   * **排程生產部署** （如果已啟用）
   * **CSE支援** （如果已啟用）
   * **部署至生產環境**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >在設定管道時，會啟用&#x200B;**排程生產部署**。
   >
   >
   >使用此選項，可以計畫生產部署，或按一下&#x200B;**Now**&#x200B;立即執行生產部署。
   >
   >
   >排程的日期和時間會根據使用者的時區指定。
   >
   >
   >按一下&#x200B;**確認**&#x200B;以驗證您的設定。

   ![](assets/Production_Deployment1.png)

   確認部署排程後，程式碼部署即告完成。

   從上述步驟中選取&#x200B;**Now**&#x200B;選項時，會顯示下列畫面。

   ![](assets/Production_Deployment2.png)

## 逾時 {#timeouts}

如果讓您等候使用者意見回饋，下列步驟會逾時：

| 步驟 | 逾時 |
|--- |--- |
| 程式碼品質測試 | 7天 |
| 安全性測試 | 7天 |
| 效能測試 | 7天 |
| 申請批准 | 7天 |
| 排程生產部署 | 7天 |
| CSE支援 | 7天 |

## 部署過程{#deployment-process}

以下章節說明如何在階段階段和生產階段部署AEM和Dispatcher套件。

Cloud Manager會將建置程式產生的所有target/*.zip檔案上傳至儲存位置。  在管道的部署階段，會從此位置檢索這些對象。

當Cloud Manager部署至非生產拓撲時，目標是盡快完成部署，因此成品會同時部署至所有節點，如下所示：

1. Cloud Manager會判斷每個工件是AEM或Dispatcher套件。
1. Cloud Manager會從負載平衡器中移除所有調度程式，以在部署期間隔離環境。

   除非另有配置，否則您可以跳過開發和階段部署中的負載平衡器更改，即分離和附加非生產管道中的步驟，用於開發環境，以及生產管道，用於預備環境。

   ![](assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能預計主要供1-1-1名客戶使用。

1. 每個AEM工件都會透過套件管理器API部署至每個AEM執行個體，且套件相依性會決定部署順序。

   要進一步了解如何使用包來安裝新功能、在實例之間轉移內容以及備份儲存庫內容，請參閱如何使用包。

   >[!NOTE]
   >
   >所有AEM成品都部署至作者和發佈者。 需要節點特定設定時，應運用執行模式。 若要進一步了解執行模式可如何讓您針對特定用途調整AEM執行個體，請參閱執行模式。

1. Dispatcher工件會依下列方式部署至每個Dispatcher:

   1. 當前配置被備份並複製到臨時位置
   1. 除不可變的檔案外，所有配置都將被刪除。 如需詳細資訊，請參閱管理Dispatcher設定。 這會清除目錄，以確保不會留下任何孤立的檔案。
   1. 將對象提取到`httpd`目錄。  不可覆寫的檔案。 在部署時，您對Git存放庫中不可變的檔案所做的任何變更都會被忽略。  這些檔案是AMS Dispatcher架構的核心，無法變更。
   1. Apache會執行設定測試。 若未找到錯誤，則會重新載入服務。 如果發生錯誤，則會從備份還原設定、重新載入服務，並將錯誤回報至Cloud Manager。
   1. 管道設定中指定的每個路徑都會失效或從Dispatcher快取中清除。

   >[!NOTE]
   >Cloud Manager預期Dispatcher工件會包含完整的檔案集。  所有Dispatcher設定檔都必須存在於Git存放庫中。 缺少檔案或資料夾將導致部署失敗。

1. 成功將所有AEM和Dispatcher套件部署至所有節點後，Dispatcher會新增回負載平衡器，且部署完成。

   >[!NOTE]
   >您可以跳過開發和預備部署中的負載平衡器更改，即在非生產管道、開發人員環境和生產管道中（用於預備環境）分離和附加步驟。

### 部署到生產階段{#deployment-production-phase}

部署至生產拓撲的程式稍有不同，以將對AEM網站訪客的影響降至最低。

生產部署通常會依照上述步驟進行，但以滾動方式進行：

1. 部署AEM套件以製作。
1. 從負載平衡器分離dispatcher1。
1. 將AEM套件部署至publish1，並將Dispatcher套件並行部署至Dispatcher1，排清Dispatcher快取。
1. 將dispatcher1放回負載平衡器。
1. 當dispatcher1重新服務後，請從負載平衡器分離dispatcher2。
1. 將AEM套件部署至publish2，並將Dispatcher套件並行部署至Dispatcher2，排清Dispatcher快取。
1. 將dispatcher2放回負載平衡器。
此過程將繼續，直到部署已到達拓撲中的所有發佈商和調度程式。
