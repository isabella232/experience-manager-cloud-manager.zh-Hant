---
title: CI/CD管線
seo-title: CI/CD管線
description: 'null'
seo-description: 請依照本節來瞭解在Cloud Manager中處理部署的CI/CD管線。
uuid: 763ddb24-05cd-463f-8d72-a2 e69 be6 b7 e
topic-tags: 簡介
discoiquuid: cdb76eb-1a91-4689-85799-0fa9fcc0592
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# CI/CD管線 {#ci-cd-pipeline}

## 管道概述 {#pipeline-overview}

[!UICONTROL Cloud Manager] 包括持續整合(CI)和持續傳送(CD)架構，可讓實施團隊快速測試並提供新的或更新的程式碼。例如，實施團隊可以設定、設定並開始自動化CI/CD管線，運用Adobe編碼最佳實務的最佳實務，以執行完整的程式碼掃描並確保程式碼品質。

CI/CD管線也會自動化單元和效能測試程序，以提高部署效率，並主動識別部署後昂貴的修正重要問題。實施團隊可存取完整的程式碼效能報告，以瞭解在程式碼部署至生產環境時，KPI和重大安全性驗證的潛在影響。

## 管線程序 {#pipeline-process}

下圖說明在開啓版本後會發生 [!UICONTROL Cloud Manager]甚麼事。下表說明工作流程中的每個步驟。

![](assets/screen_shot_2018-05-30at82457pm.png)

下表詳細說明過程中的每個步驟：

| 管線程序步驟 | 發生甚麼事？ |
|---|---|
| 1. 開始發行 | 部署管理員會透過Git認可或根據循環排程，手動觸發發行。 |
| 2. 建立版本標籤 | [!UICONTROL Cloud Manager] 建立Git標記，以使用自動產生的版本號碼來標示版本。例如：2018.531.245527.2001222 |
| 3. 以自動產生版本建立版本 | [!UICONTROL Cloud Manager] 以新指派的版本號碼建立應用程式。 |
| 4. 評估程式碼品質 | [!UICONTROL Cloud Manager] 掃描原始碼並提供摘要，然後再將程式碼部署至舞台環境 |
| 5. Versioned Artifacts(已儲存) | 會儲存發行路徑，以便在部署步驟中使用。 |
| 6. 自動部署Artifacts至AMS AEM舞台 | 版本實作會部署至舞台環境。 |
| 7. 觸發自動化測試 | [!UICONTROL Cloud Manager] 執行「效能與保全測試」。 |
| 8. 生產觸發部署 | 完成自動測試後，將部署 [!UICONTROL Cloud Manager] 開始至生產環境。 |
| 9. [!UICONTROL Cloud Manager] 取得要部署的項目 | [!UICONTROL Cloud Manager] 提取儲存的發行個體。 |
| 10. 對生產進行剪裁 | 發行項目會部署至生產環境。 |

### 如何設定CI/CD管線 {#how-to-setup-a-ci-cd-pipeline}

若要進一步瞭解管道組態，請參閱 [設定管道](configuring-pipeline.md)。

## Quality Gates {#quality-gates}

CI/CD管道提供品質關卡或接受標準，您必須先符合標準，才能將程式碼從舞台環境移至部署環境。管線中有三個閘門：

* 程式碼品質
* 效能測試
* 安全性測試

對於上述每個門，發現三個層級的問題：

* **重要** -關卡識別的問題，造成管線立即失敗。
* **重要** -關卡識別的問題，會導致管線進入暫停狀態。部署管理員、專案經理或業務擁有者可以覆寫問題，在此情況下，管線會發展，或者他們可以接受問題，此時管線會停止發生。
* **資訊** -依關卡識別的問題，僅供資訊目的使用，且不影響管線執行。

以下是程式碼掃描的範例，其中包含程式碼的相關問題：

![](assets/quality-gate-failed.png)

### 如何設定閘門 {#how-to-setup-gates}

如需設定程式碼、品質和效能閘門的詳細資訊，請參閱 **[設定蓋茨](configuring-pipeline.md)** 。
