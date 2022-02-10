---
title: CI/CD 管道
seo-title: CI/CD Pipeline
description: CI/CD管道概述，該管道處理在Cloud Manager中存放和生產的部署
seo-description: Follow this section to learn about the CI/CD pipeline, which handles deployments to stage and production in Cloud Manager
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
feature: CI-CD Pipeline
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 4f0e1d163001fd18cfa838256c813152d65c3b4c
workflow-type: tm+mt
source-wordcount: '533'
ht-degree: 1%

---

# CI/CD 管道 {#ci-cd-pipeline}

## 管道概述 {#pipeline-overview}

[!UICONTROL Cloud Manager] 包括連續整合(CI)和連續交付(CD)框架，使實施團隊能夠快速test並交付新的或更新的代碼。 例如，實施團隊可以設定、配置和啟動自動化的CI/CD管道，該管道利用Adobe編碼最佳做法執行徹底的代碼掃描並確保最高的代碼質量。

CI/CD流水線還自動化了單元和效能測試流程，以提高部署效率並主動確定部署後需要花費大量資金才能解決的關鍵問題。 實施團隊可以訪問一個全面的代碼效能報告，以便瞭解在將代碼部署到生產環境時對KPI和關鍵安全驗證的潛在影響。

## 管道進程 {#pipeline-process}

下圖說明在中觸發發行後發生的情況 [!UICONTROL Cloud Manager]。 隨附的表說明了工作流中的每個步驟。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表詳細說明了在流程的每個步驟中發生的情況：

| 管線處理步驟 | 怎麼回事？ |
|---|---|
| 1。啟動發行 | 部署管理器可以手動、通過Git提交或基於循環計畫來觸發發行。 |
| 2.建立發行標籤 | [!UICONTROL Cloud Manager] 建立Git標籤，以使用自動生成的版本號標籤釋放。 例如：2018.531.245527.0000001222 |
| 3.以自動生成的版本作為版本構建 | [!UICONTROL Cloud Manager] 使用新分配的版本號生成應用程式。 |
| 4.評估代碼質量 | [!UICONTROL Cloud Manager] 掃描原始碼並提供摘要，然後代碼才能部署到階段環境 |
| 5.已儲存版本控制的項目 | 將儲存釋放對象，以便以後在部署步驟中使用。 |
| 6。自動將對象部署到AMS階AEM段 | 釋放對象被部署到階段環境。 |
| 7。觸發自動Test | [!UICONTROL Cloud Manager] 運行對象的效能和安全test。 |
| 8.生產觸發器部署 | 自動test完成後 [!UICONTROL Cloud Manager] 開始向生產部署。 |
| 9。 [!UICONTROL Cloud Manager] 獲取要部署的對象 | [!UICONTROL Cloud Manager] 提取儲存的釋放對象。 |
| 10.將工件卸載到生產 | 版本對象將部署到生產環境。 |

### 如何設定CI/CD管道 {#how-to-setup-a-ci-cd-pipeline}

要瞭解有關管道配置的詳細資訊，請參閱文檔 [配置生產管線](configuring-production-pipelines.md) 和 [配置非生產管道。](configuring-non-production-pipelines.md)

## 質量門 {#quality-gates}

CI/CD管道提供質量門或接受標準，在將代碼從階段環境移動到部署環境之前必須滿足這些標準。 有三道門正在鋪設中：

* 代碼質量
* 效能測試
* 安全測試

對於每一個門，都有三個層次的問題：

* **關鍵**  — 閘門所發現的導致管道立即失效的問題。
* **重要**  — 由入口標識的導致管道進入暫停狀態的問題。 部署經理、項目經理或業務所有者可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道將因失敗而停止。
* **資訊**  — 閘門所發現的問題，這些問題純粹是為了提供資訊而提供的，對管線執行沒有影響。

以下是代碼掃描的示例，其中為代碼標識了問題：

![](assets/quality-gate-failed.png)

### 如何設定門 {#how-to-setup-gates}

查看文檔 [配置生產管線](configuring-production-pipelines.md) 有關設定代碼、質量和效能門的詳細資訊。
