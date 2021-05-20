---
title: CI/CD 管道
seo-title: CI/CD 管道
description: CI/CD管道概觀，可在Cloud Manager中處理預備和生產的部署
seo-description: 請依照本節所述了解CI/CD管道，該管道可處理Cloud Manager中預備和生產的部署
uuid: 763ddb24-05cd-463f-8d72-a2e69bbe6b7e
topic-tags: introduction
discoiquuid: 1cdb76eb-1a91-4689-8579-0fa9fccc0592
feature: CI-CD管道
exl-id: 7130e5b7-6986-48c8-900c-90f3e4187f91
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 1%

---

# CI/CD 管道 {#ci-cd-pipeline}

## 管道概述{#pipeline-overview}

[!UICONTROL Cloud Manager] 包含Continuous Integration(CI)和Continuous Delivery(CD)架構，可讓實作團隊快速測試並傳送新的或更新的程式碼。例如，實作團隊可以設定、設定和啟動自動化CI/CD管道，利用Adobe編碼最佳實務來執行徹底的程式碼掃描，並確保最高的程式碼品質。

CI/CD管道還自動執行單元和效能測試流程，以提高部署效率，並主動確定部署後需要修復的重要問題。 實作團隊可存取完整的程式碼效能報表，以掌握將程式碼部署至生產環境時，對KPI和重要安全性驗證的潛在影響。

## 管道進程{#pipeline-process}

下圖說明在[!UICONTROL Cloud Manager]中觸發發行後會發生什麼事。 隨附的表格說明工作流程中的每個步驟。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表詳細說明在程式的每個步驟中進行的動作：

| 管道處理步驟 | 怎麼回事？ |
|---|---|
| 1.開始發行 | 部署管理員會手動、透過Git提交或根據循環排程觸發發行。 |
| 2.建立發行標籤 | [!UICONTROL Cloud Manager] 會建立Git標籤，使用自動產生的版本號碼來標示發行。例如：2018.531.245527.0000001222 |
| 3.建置為版本，並自動產生版本 | [!UICONTROL Cloud Manager] 使用新指派的版本號來建立應用程式。 |
| 4.評估程式碼品質 | [!UICONTROL Cloud Manager] 掃描原始碼並提供摘要，然後才能將代碼部署到預備環境 |
| 5.儲存的版本控制對象 | 將儲存發行對象，以供稍後在部署步驟中使用。 |
| 6.將工件自動部署到AMS AEM Stage | 將發行對象部署到預備環境。 |
| 7.觸發自動測試 | [!UICONTROL Cloud Manager] 運行對象的效能和安全測試。 |
| 8.生產觸發程式部署 | 完成自動化測試後[!UICONTROL Cloud Manager]開始部署到生產環境。 |
| 9.[!UICONTROL Cloud Manager]獲取要部署的對象 | [!UICONTROL Cloud Manager] 提取儲存的發行成品。 |
| 10.將成品退出生產 | 發行成品會部署至生產環境。 |

### 如何設定CI/CD管道{#how-to-setup-a-ci-cd-pipeline}

若要進一步了解管道設定，請參閱[設定管道](configuring-pipeline.md)。

## 質量門{#quality-gates}

CI/CD管道提供品質入口或接受標準，必須先符合這些條件，才能將程式碼從預備環境移至部署環境。 有三扇門正在鋪設：

* 程式碼品質
* 效能測試
* 安全性測試

針對每個門，已識別三個層級的問題：

* **關鍵**  — 閘道所識別，造成管道立即失敗的問題。
* **重要**  — 閘道所識別的問題，導致管道進入暫停狀態。部署經理、項目經理或業務負責人可以覆蓋問題，在這種情況下，管道將繼續，或者他們可以接受問題，在這種情況下，管道會因故障而停止。
* **資訊**  — 閘道所識別的問題，純粹供參考，對管道執行沒有影響。

以下是程式碼掃描的範例，其中包含針對程式碼所識別的問題：

![](assets/quality-gate-failed.png)

### 如何設定門{#how-to-setup-gates}

有關設定代碼、質量和效能門的詳細資訊，請參閱&#x200B;**[配置門](configuring-pipeline.md)**。
