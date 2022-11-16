---
title: 重要概念
description: 像所有強大的工具一樣，Cloud Manager 包含了許多概念和術語。本文件會概述您開始使用 Cloud Manager 時最重要的一些內容。
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 73e322cf93dc7709b7581860974079c8d94034ba
workflow-type: ht
source-wordcount: '419'
ht-degree: 100%

---


# 重要概念 {#key-concepts}

像所有強大的工具一樣，Cloud Manager 包含了許多概念和術語。本文件會概述您開始使用 Cloud Manager 時最重要的一些內容。

## 應用程式 {#application}

應用程式是客戶建立的自訂項目和設定組，以便根據他們的特定使用案例和需求來調整基礎的[解決方案](#solution) (例如 AEM Sites 或 AEM Assets)。應用程式是一種邏輯單位，可能包含多個[成品。](#artifact)

一個應用程式範例是虛構的 [WKND 生活方式應用程式。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html)

## 成品 {#artifact}

成品是可部署的單位，而且是將原始程式碼轉換為單一單位的某些建置流程的結果。例如，.zip 檔就包含了原始程式碼。

## 成品存放庫 {#artifact-repository}

成品存放庫是儲存和保護客戶特定[成品](#artifact)的儲存位置。

## 環境 {#environment}

環境指[方案中的單一叢集虛擬機器。](#program) 對於 AEM，這會由一個製作執行個體 (可選擇外加一個額外的冷待命製作執行個體)、零個或多個發佈執行個體、一個或多個 Dispatcher 執行個體和一個負載平衡器組成。

## Git 存放庫 {#git-repository}

Git 存放庫是儲存客戶特定原始程式碼的位置，並可[使用 Git 存取。](https://git-scm.com)

## 執行個體 {#instance}

執行個體是一種特定的虛擬伺服器，會執行 AEM [解決方案。](#solution) 從部署的角度來看，執行個體代表單一邏輯單位。

## 組織 {#organization}

組織指代表企業客戶的 Adobe&#x200B; 建構。一家公司可能有多個組織，會依據在 Adob&#x200B;&#x200B;e 的 Identity Management System (IMS) 中對其進行佈建方式而定。

## 管道 {#pipeline}

管道指一組按順序執行的部署步驟。

## 產品 {#product}

產品指獲組織授權的[解決方案](#solution)中的一組特定功能。組織內的不同[方案](#program)可能有權使用不同的產品集，例如 AEM Sites、AEM Assets 或 AEM Forms。

## 計劃 {#program}

方案指一組支援客戶倡議邏輯分組的環境，通常會對應購買的服務等級協議 (SLA)。每個方案只會有一個生產環境，並可能有許多非生產環境。

## 解決方案 {#solution}

解決方案指 Adobe [!UICONTROL Experience Cloud] 解決方案的其中一種。 例如，Adobe Experience Manager、Adobe Target 或 Adobe Analytics。

## 步驟 {#step}

步驟指已設定的指令集，會完成某些工作單位，是[管道的建置組塊。](#pipeline)
