---
title: 重要概念
description: 與所有功能強大的工具一樣，Cloud Manager包含許多概念和術語。 本文檔總結了開始使用雲管理器時對您最重要的一些內容。
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 73e322cf93dc7709b7581860974079c8d94034ba
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 4%

---


# 重要概念 {#key-concepts}

與所有功能強大的工具一樣，Cloud Manager包含許多概念和術語。 本文檔總結了開始使用雲管理器時對您最重要的一些內容。

## 應用程式 {#application}

而應用程式是客戶為調整底層而建立的一組定制和配置 [解決方案](#solution) (如AEM Sites或AEM Assets)。 應用程式是可由多個元件組成的邏輯單元 [對象。](#artifact)

一個示例應用是虛構 [WKND生活方式應用。](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=zh-Hant)

## 成品 {#artifact}

偽影是可展開單元，是將原始碼轉換為單個單元的某個生成過程的結果。 例如，包含原始碼的.zip檔案。

## 項目儲存庫 {#artifact-repository}

項目儲存庫是特定於客戶的儲存位置 [偽](#artifact) 被保存和保護。

## 環境 {#environment}

環境是一個 [的子菜單。](#program) 例如AEM，這由創作實例（可選地附加冷備用創作實例）、零個或多個發佈實例、一個或多個調度程式實例和負載平衡器組成。

## Git儲存庫 {#git-repository}

Git儲存庫是儲存特定於客戶的原始碼並可訪問的位置 [用git](https://git-scm.com)

## 例項 {#instance}

實例是運行以下命令的特定虛擬服AEM務器 [解決方案。](#solution) 實例從部署角度表示單個邏輯單元。

## 組織 {#organization}

組織是代表企業客戶的Adobe結構。 一家公司可能擁有多個組織，具體取決於在AdobeIdentity Management系統(IMS)中配置這些組織的方式。

## 管線 {#pipeline}

流水線是按順序執行的一組部署步驟。

## 產品 {#product}

產品是產品中的一組特定功能 [解決方案](#solution) 由組織授權。 不同 [方案](#program) 組織內部可以擁有不同的產品，例如AEM Sites、AEM Assets或AEM Forms。

## 計畫 {#program}

計畫是一組支援客戶計畫的邏輯分組的環境，通常對應於購買的服務級別協定(SLA)。 每個程式都只有一個生產環境，並且可能有許多非生產環境。

## 解決方案 {#solution}

解決方案是Adobe [!UICONTROL Experience Cloud] 解決方案。 例如，Adobe Experience Manager、Adobe Target或Adobe Analytics。

## 步驟 {#step}

步驟是配置的指令集，其將某些工作單元作為 [管線。](#pipeline)
