---
title: CI/CD 管道
seo-title: CI/CD 管道
description: 'null'
seo-description: 請依照本節內容瞭解CI/CD管道，該管道可在Cloud manager中處理部署和生產。
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
translation-type: tm+mt
source-git-commit: 2d7b18ea55e2bd5879cf8bd896cafed4d46c0011

---

SHANKARI_TEST_CHANGE
# CI/CD 管道 {#ci-cd-pipeline}

## 管線概述 {#pipeline-overview}

[!UICONTROL Cloud Manager] 包含連續整合(CI)和連續傳送(CD)架構，可讓實施團隊快速測試並傳送新的或更新的程式碼。 例如，實作團隊可以設定、設定和啟動自動化CI/CD管道，運用Adobe編碼最佳實務來執行完整的程式碼掃描，並確保最高的程式碼品質。

CI/CD管道還自動化了單元和效能測試流程，以提高部署效率，並主動發現部署後需要修復的重要問題。 實作團隊可存取完整的程式碼效能報告，以便在將程式碼部署至生產環境時，洞悉KPI和重要安全性驗證的潛在影響。

## 管線處理 {#pipeline-process}

下圖說明在中觸發發行後會發生什麼 [!UICONTROL Cloud Manager]。 隨附的表格說明工作流程中的每個步驟。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表詳細說明了流程每個步驟中的情況：

| 管線處理步驟 | 怎麼回事？ |
|---|---|
| 1.開始發行 | 部署管理員會以手動方式、透過Git提交或根據循環排程來觸發發行。 |
| 2.建立發行標籤 | [!UICONTROL Cloud Manager] 建立Git標籤，以使用自動產生的版本號碼來標籤發行。 例如：2018.531.245527.000001222 |
| 3.使用自動產生的版本建立為發行 | [!UICONTROL Cloud Manager] 使用新指派的版本號碼建立應用程式。 |
| 4.評估程式碼品質 | [!UICONTROL Cloud Manager] 掃描原始碼並提供摘要，然後代碼才能部署到階段環境 |
| 5.已儲存的版本化對象 | 發行對象會儲存起來，以便日後在部署步驟中使用。 |
| 6.自動將對象部署到AMS AEM Stage | 釋放對象部署到舞台環境。 |
| 7.觸發自動測試 | [!UICONTROL Cloud Manager] 運行對象的效能和安全性測試。 |
| 8.生產觸發器部署 | 完成自動測試後， [!UICONTROL Cloud Manager] 開始將部署至生產環境。 |
| 9.獲 [!UICONTROL Cloud Manager] 取要部署的對象 | [!UICONTROL Cloud Manager] 提取儲存的釋放對象。 |
| 10.將對象放入生產環境 | 發行對象將部署到生產環境。 |

### 如何設定CI/CD管線 {#how-to-setup-a-ci-cd-pipeline}

要瞭解有關管線配置的更多資訊，請參 [閱配置管線](configuring-pipeline.md)。

## 質量門 {#quality-gates}

CI/CD管線提供了質量門或驗收標準，在將代碼從階段環境移動到部署環境之前必須滿足這些標準。 目前有三扇門正在醖釀之中：

* 程式碼品質
* 效能測試
* 安全性測試

對於每個門，都有三個層次的問題：

* **Critical** —— 澆口發現的導致管道立即故障的問題。
* **重要** -閘道所識別導致管線進入暫停狀態的問題。 部署經理、專案經理或業務負責人可以覆寫問題（在這種情況下，管道會繼續），或者接受問題（在這種情況下，管道會因故障而停止）。
* **資訊** -網關所發現的問題，這些問題僅供參考，對管線執行沒有影響。

以下是代碼掃描的示例，其中列出了代碼的問題：

![](assets/quality-gate-failed.png)

### 如何設定門 {#how-to-setup-gates}

如需 **[設定程式碼](configuring-pipeline.md)**、品質和效能閘道的詳細資訊，請參閱設定閘道。
