---
title: 部署程式碼
seo-title: Deploy your Code
description: 提供Cloud Manager中部署過程的概述
seo-description: Learn how to deploy your code once you have configured your pipeline (repository, environment, and testing environment)
uuid: 4e3807e1-437e-4922-ba48-0bcadf293a99
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: using
discoiquuid: 832a4647-9b83-4a9d-b373-30fe16092b15
feature: Code Deployment
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 9a9d7067a1369e80ccf9b2925369a466b3da2901
workflow-type: tm+mt
source-wordcount: '1615'
ht-degree: 1%

---

# 部署程式碼 {#deploy-your-code}

## 使用雲管理器部署代碼 {#deploying-code-with-cloud-manager}

>[!NOTE]
>要瞭解有關在as a Cloud Service中部署Cloud Manager的代AEM碼，請參閱 [這裡](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/implementing/using-cloud-manager/deploy-code.html?lang=en#using-cloud-manager)。

配置了生產管道（儲存庫、環境和測試環境）後，您就可以部署代碼了。

1. 按一下 **部署** 啟動部署過程。

   ![](assets/Deploy1.png)

1. 的 **管道執行** 螢幕。

   按一下 **生成** 以啟動進程。

   ![](assets/Deploy2.png)

1. 完整的生成過程將部署您的代碼。

   構建過程涉及以下階段：

   1. 階段部署
   1. 階段測試
   1. 生產部署

   >[!NOTE]
   >
   >此外，您還可以通過查看日誌或查看結果來查看各種部署流程中的步驟，以瞭解測試標準。

   「 **舞台部署**」涉及以下步驟：

   * 驗證：此步驟確保將管道配置為使用當前可用資源，例如，配置的分支存在，環境可用。
   * 構建和單元測試：此步驟將運行集裝箱化生成進程。 請參閱 [瞭解構建環境](/help/using/build-environment-details.md) 的子菜單。
   * 代碼掃描：此步驟將評估應用程式碼的質量。 請參閱 [瞭解您的Test結果](understand-your-test-results.md) 的子菜單。
   * 部署到階段

   ![](assets/Stage_Deployment1.png)

   的 **階段測試**，涉及以下步驟：

   * 安全測試：此步驟評估應用程式碼對環境的安全AEM影響。 請參閱 [瞭解您的Test結果](understand-your-test-results.md) 的子菜單。
   * 效能測試：此步驟評估應用程式碼的效能。 請參閱 [瞭解您的Test結果](understand-your-test-results.md) 的子菜單。

   ![](assets/Stage_Testing1.png)

   的 **生產部署**，涉及以下步驟：

   * **申請審批** （如果已啟用）
   * **計畫生產部署** （如果已啟用）
   * **CSE支援** （如果已啟用）
   * **部署到生產**

   ![](assets/Prod_Deployment1.png)

   >[!NOTE]
   >
   >的 **計畫生產部署** 在配置管道時啟用。
   >
   >
   >使用此選項，您可以計畫生產部署，或按一下 **現在** 立即執行生產部署。
   >
   >
   >計畫的日期和時間根據用戶的時區指定。
   >
   >
   >按一下 **確認** 來驗證您的設定。

   ![](assets/Production_Deployment1.png)

   確認部署計畫後，代碼部署即完成。

   顯示以下螢幕，時間 **現在** 的雙曲餘切值。

   ![](assets/Production_Deployment2.png)

## 超時 {#timeouts}

如果留在等待用戶反饋，以下步驟將超時：

| 步驟 | 逾時 |
|--- |--- |
| 代碼質量測試 | 14天 |
| 安全測試 | 14天 |
| 效能測試 | 14天 |
| 申請審批 | 14天 |
| 計畫生產部署 | 14天 |
| CSE支援 | 14天 |

## 部署過程 {#deployment-process}

以下部分介紹在AEM階段階段和生產階段如何部署和調度程式包。

Cloud Manager將生成過程生成的所有目標/*.zip檔案上載到儲存位置。  在管線的部署階段，將從此位置檢索這些對象。

當Cloud Manager部署到非生產拓撲時，目標是盡快完成部署，因此將對象同時部署到所有節點，如下所示：

1. Cloud Manager確定每個對象是AEM包還是分派程式包。
1. Cloud Manager從負載平衡器中刪除所有調度程式，以在部署期間隔離環境。

   除非另有配置，否則您可以跳過開發和階段部署中的負載平衡器更改，即在非生產管道、開發環境和生產管道中分離和附加階段環境的步驟。

   ![](assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能預計主要由1-1-1客戶使用。

1. 每個AEM項目都通過包管AEM理器API部署到每個實例，並且包依賴關係決定部署順序。

   有關如何使用軟體包來安裝新功能、在實例之間傳輸內容以及備份儲存庫內容的詳細資訊，請參閱如何使用軟體包。

   >[!NOTE]
   >
   >所有AEM對象都部署到作者和發佈者。 當需要特定於節點的配置時，應利用運行模式。 要瞭解有關運行模式如何允許您針對特定目AEM的調整實例的詳細資訊，請參閱運行模式。

1. 調度程式項目按如下方式部署到每個調度程式：

   1. 將當前配置備份並複製到臨時位置
   1. 除不可變檔案外，所有配置都將被刪除。 有關詳細資訊，請參閱管理Dispatcher配置。 這將清除目錄，以確保不會留下孤立檔案。
   1. 將偽影提取到 `httpd` 的子菜單。  不可改寫的檔案。 在部署時，您對Git儲存庫中不可變檔案所做的任何更改都將被忽略。  這些檔案是AMS分派程式框架的核心，無法更改。
   1. Apache執行配置test。 如果找不到錯誤，則重新載入服務。 如果發生錯誤，則從備份中恢復配置，重新載入服務，並將錯誤報告回雲管理器。
   1. 在流水線配置中指定的每個路徑被無效或從調度程式快取中刷新。

   >[!NOTE]
   >Cloud Manager希望調度程式項目包含完整檔案集。  所有調度程式配置檔案必須存在於Git儲存庫中。 缺少檔案或資料夾將導致部署失敗。

1. 成功將所有包和AEM調度程式包部署到所有節點後，調度程式將重新添加到負載平衡器，部署完成。

   >[!NOTE]
   >您可以跳過開發和階段部署中的負載平衡器更改，即在非生產管道、開發人員環境和生產管道中對階段環境分離和附加步驟。

### 部署到生產階段 {#deployment-production-phase}

部署到生產拓撲的過程略有不同，以最大限度地減少對站點訪AEM問者的影響。

生產部署通常遵循與上述步驟相同的步驟，但是以滾動方式：

1. 部署AEM要創作的包。
1. 從負載平衡器中分離Dispatcher1。
1. 將包部AEM署到publish1 ，將調度程式包部署到並行刷新的調度程式快取中的dispatcher1。
1. 將dispatcher1放回負載平衡器。
1. 一旦dispatcher1恢復服務，將dispatcher2與負載平衡器分離。
1. 將包部AEM署到publish2，將調度程式包部署到並行刷新的調度程式快取中的dispatcher2。
1. 將dispatcher2放回負載平衡器中。
此過程一直持續到部署到達拓撲中的所有發佈者和調度程式為止。

## 緊急管道執行模式 {#emergency-pipeline}

在關鍵情況下，Adobe Managed Services客戶可能需要將代碼更改部署到其階段和生產環境，而無需等待Cloud Managertest週期的完整執行。

要解決這些情況，Cloud Manager生產管道可以在 *緊急* 的子菜單。 使用此模式時，不執行安全和效能test步驟；所有其他步驟（包括任何已配置的批准步驟）都按照正常管道執行模式執行。

>[!NOTE]
>緊急管道執行模式功能由客戶成功工程師根據程式激活。

### 使用緊急管道執行模式 {#using-emergency-pipeline}

啟動生產管道執行時，如果已激活此功能，則可以從對話框以正常或緊急模式啟動執行，如下圖所示。

![](assets/execution-emergency1.png)

此外，查看以緊急模式運行的執行的管道執行詳細資訊頁面時，螢幕頂部的breadcrumbs會顯示用於此特定執行的緊急模式的指示器。

![](assets/execution-emergency2.png)

也可以通過Cloud Manager API或CLI在此緊急模式下建立管道執行。 要在緊急模式下啟動執行，請使用查詢參數將PUT請求提交到管道的執行終結點 `?pipelineExecutionMode=EMERGENCY` 或，在使用CLI時：

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

>[!IMPORTANT]
>使用 `--emergency` 標誌可能需要更新到最新 `aio-cli-plugin-cloudmanager` 。

## 重新執行生產部署 {#Reexecute-Deployment}

對於生產部署步驟已完成的執行，支援重新執行生產部署步驟。 完成類型不重要 — 部署可能成功（僅適用於AMS程式）、取消或失敗。 話雖如此，預計主要使用案例將是生產部署步驟因暫時原因而失敗的案例。 重新執行使用同一管道建立新執行。 此新執行包括三個步驟：

1. 驗證步驟 — 這實質上與正常管道執行期間發生的驗證相同。
1. 生成步驟 — 在重新執行的上下文中，生成步驟是複製對象，而不是實際執行新的生成進程。
1. 生產部署步驟 — 與正常管道執行中的生產部署步驟使用相同的配置和選項。

生成步驟在UI中的標籤可能稍有不同，以反映它正在複製對象，而不是重新生成。

![](assets/Re-deploy.png)

限制:

* 重新執行生產部署步驟將僅在上次執行時可用。
* 無法重新執行回滾執行。
* 如果上次執行是回滾執行，則不可能重新執行。
* 如果上次執行是推式更新執行，則不可能重新執行。
* 如果上次執行在生產部署步驟之前的任何時間點失敗，則無法重新執行。

### 重新執行API {#Reexecute-API}

### 標識重新執行

為了確定執行是否是重新執行，可檢查觸發欄位。 它的價值是 *執行(_E)*。

### 觸發新執行

要觸發重新執行，需要向HAL連結&lt;(PUT請求)<http://ns.adobe.com/adobecloud/rel/pipeline/reExecute>)>。 如果存在此連結，則可以從該步驟重新啟動執行。 如果缺少，則無法從該步驟重新啟動執行。 在初始版本中，此連結將只出現在生產部署步驟中，但將來的版本可能支援從其他步驟啟動管道。 範例:

```Javascript
 {
  "_links": {
    "http://ns.adobe.com/adobecloud/rel/pipeline/logs": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/logs",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/reExecute": {
      "href": "/api/program/4/pipeline/1/execution?stepId=2983530",
      "templated": false
    },
    "http://ns.adobe.com/adobecloud/rel/pipeline/metrics": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530/metrics",
      "templated": false
    },
    "self": {
      "href": "/api/program/4/pipeline/1/execution/953671/phase/1575676/step/2983530",
      "templated": false
    }
  },
  "id": "6187842",
  "stepId": "2983530",
  "phaseId": "1575676",
  "action": "deploy",
  "environment": "weretail-global-b75-prod",
  "environmentType": "prod",
  "environmentId": "59254",
  "startedAt": "2022-01-20T14:47:41.247+0000",
  "finishedAt": "2022-01-20T15:06:19.885+0000",
  "updatedAt": "2022-01-20T15:06:20.803+0000",
  "details": {
  },
  "status": "FINISHED"
```


HAL連結的語法 *href*  以上值不打算用作參考點。 實際值應始終從HAL連結中讀取而不是生成。

提交 *PUT* 對此終結點的請求將導致 *201* 如果成功，則響應主體將表示新執行。 這類似於通過API啟動常規執行。
