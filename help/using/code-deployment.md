---
title: 代碼部署
description: 瞭解如何部署代碼以及在部署代碼時在Cloud Manager中將發生什麼。
exl-id: 3d6610e5-24c2-4431-ad54-903d37f4cdb6
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '1609'
ht-degree: 0%

---


# 代碼部署 {#code-deployment}

瞭解如何部署代碼以及在部署代碼時在Cloud Manager中將發生什麼。

## 使用雲管理器部署代碼 {#deploying-code-with-cloud-manager}

一旦配置了生產管道（包括必要的儲存庫和環境），您就可以部署代碼。

1. 按一下 **部署** 啟動部署過程。

   ![「部署」按鈕](/help/assets/Deploy1.png)

1. 的 **管道執行** 螢幕。 按一下 **生成** 以啟動進程。

   ![「生成」按鈕](/help/assets/Deploy2.png)

生成過程啟動代碼部署過程，包括以下步驟：

* 階段部署
* 階段測試
* 生產部署

您可以查看日誌或查看結果以查看測試標準中各個部署流程的步驟。

## 部署步驟 {#deployment-steps}

在部署的每個步驟中都會發生許多操作，本節將介紹這些操作。 請參閱一節 [部署流程詳細資訊](#deployment-process) 有關如何在幕後部署代碼本身的技術詳細資訊。

### 階段部署步驟 {#stage-deployment}

的 **階段部署** 步驟包括以下操作：

* **驗證**:此步驟確保管道配置為使用當前可用資源，例如，已配置的分支存在且環境可用。
* **構建和單元測試**:此步驟將運行集裝箱化生成進程。 查看文檔 [構建環境](/help/getting-started/build-environment.md) 的雙曲餘切值。
* **代碼掃描**:此步驟將評估應用程式碼的質量。 查看文檔 [瞭解Test結果](/help/using/code-quality-testing.md) 的子菜單。
* **部署到階段**

![階段部署](/help/assets/Stage_Deployment1.png)

### 階段測試步驟 {#stage-testing}

的 **階段測試** 步驟包括以下操作：

* **安全測試**:此步驟評估代碼對環境的安全AEM影響。 查看文檔 [瞭解Test結果](/help/using/code-quality-testing.md) 的子菜單。
   * **效能測試**:此步驟評估代碼的效能。 請參閱 [瞭解Test結果](/help/using/code-quality-testing.md) 的子菜單。

   ![階段測試](/help/assets/Stage_Testing1.png)

### 生產部署步驟 {#production-deployment}

的 **生產部署** 步驟，包括以下操作：

* **申請審批**
   * 配置管道時啟用此選項。
   * 使用此選項，您可以計畫生產部署，或按一下 **現在** 立即執行生產部署。
* **計畫生產部署**
   * 配置管道時啟用此選項。
   * 計畫的日期和時間根據用戶的時區指定。
      ![計畫部署](/help/assets/Production_Deployment1.png)
* **CSE支援** （如果已啟用）
* **部署到生產**

![生產部署](/help/assets/Prod_Deployment1.png)

部署完成後，您的代碼將位於其目標環境中，您可以查看日誌。

![部署完成](/help/assets/Production_Deployment2.png)

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

## 部署流程詳細資訊 {#deployment-process}

Cloud Manager將生成過程生成的所有目標/*.zip檔案上載到儲存位置。 在管線的部署階段，將從此位置檢索這些對象。

當Cloud Manager部署到非生產拓撲時，目標是盡快完成部署，因此將對象同時部署到所有節點，如下所示：

1. Cloud Manager確定每個對象是AEM包還是分派程式包。
1. Cloud Manager從負載平衡器中刪除所有調度程式，以在部署期間隔離環境。

   * 除非另有配置，否則您可以跳過開發和轉移部署中的負載平衡器更改，例如，對於開發環境，在非生產管道中分離和附加步驟，以及對於生產管道的轉移環境。

   ![跳過負載平衡器](/help/assets/load_balancer.png)

   >[!NOTE]
   >
   >此功能預計主要由1-1-1客戶使用。

1. 每個AEM項目都通過包管AEM理器API部署到每個實例，並且包依賴關係決定部署順序。

   * 有關如何使用軟體包安裝新功能、在實例之間傳輸內容以及備份儲存庫內容的詳細資訊，請參閱文檔 [包管理器。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/developer-tools/package-manager.html)
   >[!NOTE]
   >
   >所有AEM對象都部署到作者和發佈者。 當需要特定於節點的配置時，應利用運行模式。 要瞭解有關運行模式如何允許您針對特定目AEM的調整實例的詳細資訊，請參閱 [將文檔部署到AEMas a Cloud Service的「運行模式」部分。](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/deploying/overview.html#runmodes)

1. 調度程式項目按如下方式部署到每個調度程式：

   1. 當前配置將被備份並複製到臨時位置。
   1. 除不可變檔案外，所有配置都將被刪除。 請參閱文檔 [Dispatcher配置](/help/getting-started/dispatcher-configurations.md) 的子菜單。 這將清除目錄，以確保不會留下孤立檔案。
   1. 將偽影提取到 `httpd` 的子菜單。 不可改寫的檔案。 在部署時，您對Git儲存庫中不可變檔案所做的任何更改都將被忽略。 這些檔案是AMS分派程式框架的核心，無法更改。
   1. Apache執行配置test。 如果找不到錯誤，則重新載入服務。 如果發生錯誤，則從備份中恢復配置，重新載入服務，並將錯誤報告回雲管理器。
   1. 在流水線配置中指定的每個路徑被無效或從調度程式快取中刷新。

   >[!NOTE]
   >
   >Cloud Manager希望調度程式項目包含完整檔案集。 所有調度程式配置檔案必須存在於Git儲存庫中。 缺少檔案或資料夾將導致部署失敗。

1. 成功將所有包和AEM調度程式包部署到所有節點後，調度程式將重新添加到負載平衡器，部署完成。

   >[!NOTE]
   >
   >您可以跳過開發和暫存部署中的負載平衡器更改，例如，對於開發環境，在非生產管道中分離和附加步驟，以及對於生產管道的暫存環境。

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

為瞭解決這些情況，Cloud Manager生產管道可以在緊急模式下執行。 使用此模式時，不執行安全和效能test步驟。 所有其他步驟（包括任何已配置的批准步驟）都按照正常管道執行模式執行。

>[!NOTE]
>
>緊急管道執行模式功能由客戶成功工程師按程式激活。

### 使用緊急管道執行模式 {#using-emergency-pipeline}

啟動生產管道執行時，如果已為程式激活緊急管道執行模式功能，則可以從對話框以正常或緊急模式啟動執行。

![運行管線選項](/help/assets/execution-emergency1.png)

查看以緊急模式運行的執行的管道執行詳細資訊頁面時，螢幕頂部的麵包屑會顯示管道正在以緊急模式執行的指示器。

![緊急模式麵包屑](/help/assets/execution-emergency2.png)

也可以通過Cloud Manager API或CLI在緊急模式下執行管道。 要在緊急模式下啟動執行，請提交 `PUT` 使用查詢參數向管道的執行終結點請求 `?pipelineExecutionMode=EMERGENCY` 或，在使用CLI時：

```
$ aio cloudmanager:pipeline:create-execution PIPELINE_ID --emergency
```

## 重新執行生產部署 {#re-execute-deployment}

生產部署步驟的重新執行可用於生產部署步驟已完成的執行。 完成的類型不重要。 部署可能成功（僅適用於AMS程式）、取消或失敗。 主要使用情形是生產部署步驟因暫時原因失敗。 重新執行使用同一管道建立新執行。 此新執行包括三個步驟：

1. **驗證步驟**  — 這基本上與正常管道執行期間的驗證相同。
1. **生成步驟**  — 在重新執行的上下文中，生成步驟會複製對象，而實際上不會執行新的生成進程。
1. **生產部署步驟**  — 這與正常管道執行中的生產部署步驟使用相同的配置和選項。

生成步驟可以在UI中以不同方式標籤，以反映它正在複製對象，而不是重新生成。

![重新執行](/help/assets/Re-deploy.png)

### 限制 {#limitations}

* 重新執行生產部署步驟僅可用於上次執行。
* 無法重新執行回滾執行或推送更新執行。
* 如果上次執行在生產部署步驟之前的任何時間點失敗，則無法重新執行。

### 標識重新執行 {#identifying}

要確定執行是否為重新執行， `trigger` 可以檢查欄位。 它的價值是 `RE_EXECUTE`。

### 觸發重新執行 {#triggering}

要觸發重新執行， `PUT` 需要向HAL連結提出請求 `http://ns.adobe.com/adobecloud/rel/pipeline/reExecute` 生產部署步驟狀態。 如果存在此連結，則可以從該步驟重新啟動執行。 如果缺少，則無法從該步驟重新啟動執行。 此連結將只出現在生產部署步驟中

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

HAL連結的語法 `href` 值不打算用作參考點。 實際值應始終從HAL連結中讀取而不是生成。

提交 `PUT` 對此終結點的請求將導致 `201` 如果成功，則響應主體將表示新執行。 這類似於通過API啟動常規執行。
