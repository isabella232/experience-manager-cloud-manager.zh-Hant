---
title: CI/CD管道
description: 瞭解CI/CD管道，以及它們如何在Cloud Manager中處理到暫存和生產環境的部署。
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 6572c16aea2c5d2d1032ca5b0f5d75ade65c3a19
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---


# CI/CD管道 {#ci-cd-pipeline}

瞭解CI/CD管道，以及它們如何在Cloud Manager中處理到暫存和生產環境的部署。

## 概觀 {#overview}

[!UICONTROL Cloud Manager] 包括連續整合/連續交付(CI/CD)框架，該框架允許實施團隊快速test和提供新的或更新的代碼。 例如，實施團隊可以設定、配置和啟動自動化的CI/CD管道，該管道利用Adobe編碼最佳做法執行徹底的代碼掃描並確保最高的代碼質量。

CI/CD流水線還自動化了單元和效能測試過程，以提高部署效率並主動發現部署後修復成本高昂的關鍵問題。 實施團隊可以訪問一個全面的代碼效能報告，以便瞭解在將代碼部署到生產環境時對KPI和關鍵安全驗證的潛在影響。

## 管道進程 {#pipeline-process}

此圖說明了在中觸發版本後發生的情況 [!UICONTROL Cloud Manager] 使用管線。

![管線進程](/help/assets/screen_shot_2018-05-30at82457pm.png)

| 管線步驟 | 說明 |
|---|---|
| 1。啟動發行 | 部署管理器可以手動、通過Git提交或基於循環計畫來觸發發行。 |
| 2.建立發行標籤 | [!UICONTROL Cloud Manager] 建立git標籤以使用自動生成的版本號來標籤釋放，例如 `2018.531.245527.0000001222`。 |
| 3.以自動生成的版本構建為版本 | [!UICONTROL Cloud Manager] 使用新分配的版本號生成應用程式。 |
| 4.評估代碼質量 | [!UICONTROL Cloud Manager] 掃描原始碼並提供摘要，然後代碼才能部署到暫存環境。 |
| 5.已儲存的版本化項目 | 釋放對象被儲存，以供以後在部署步驟中使用。 |
| 6。自動將項目部署到AMS暫AEM存 | 釋放對象被部署到轉移環境。 |
| 7。觸發自動test | [!UICONTROL Cloud Manager] 對項目運行效能和安全test。 |
| 8.生產觸發器部署 | 自動test完成後， [!UICONTROL Cloud Manager] 開始向生產部署。 |
| 9。 [!UICONTROL Cloud Manager] 獲取要部署的對象 | [!UICONTROL Cloud Manager] 提取儲存的釋放對象。 |
| 10.將對象部署到生產 | 將發行對象部署到生產環境。 |

### 如何設定CI/CD管線 {#how-to-setup-a-ci-cd-pipeline}

要瞭解有關管道配置的詳細資訊，請參閱文檔 [配置生產管線](/help/using/production-pipelines.md) 和 [配置非生產管道。](/help/using/non-production-pipelines.md)

## 質量門 {#quality-gates}

CI/CD管道提供質量門或接受標準，在將代碼從暫存環境移動到部署環境之前必須滿足這些標準。 有三道門正在鋪設中：

* 代碼質量
* 效能測試
* 安全測試

對於每一個門，可以確定三個問題級別：

* **關鍵**  — 閘門發現的關鍵問題導致管道立即失效。
* **重要**  — 由門確定的重要問題導致管道進入暫停狀態。 部署經理、項目經理或業務所有者可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道將因失敗而停止。
* **資訊**  — 該門所查明的資訊問題純粹是為了提供資訊，對管道執行沒有影響。

這是一個代碼掃描的示例，其中發現了問題。

![代碼掃描示例](/help/assets/quality-gate-failed.png)

### 如何設定門 {#how-to-setup-gates}

查看文檔 [配置生產管線](/help/using/production-pipelines.md) 有關設定代碼、質量和效能門的詳細資訊。
