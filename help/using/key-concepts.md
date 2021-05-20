---
title: 重要概念
seo-title: 重要概念
description: 本頁列出與Cloud Manager相關的主要術語。
seo-description: 請詳閱本頁，了解與Cloud Manager相關的重要術語。
uuid: 2a37810b-98f8-4f01-90de-1e52c754ad16
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: introduction
discoiquuid: b702dfc0-3534-4d90-af19-8559d8baf6a6
feature: 快速入門
level: Beginner
exl-id: 86dfc976-f3da-479a-9faa-08f40ca909e0
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '347'
ht-degree: 2%

---

# 重要概念 {#key-concepts}

本頁說明Cloud Manager中使用的一些基本術語。 強烈建議您先閱讀本頁面，再檢閱其餘的Cloud Manager檔案。

**** 應用程式由客戶建立的自訂和設定集，以根據其特定使用案例和需求調整基礎解決方案。應用程式是一個邏輯單元，可由多個偽像組成。

例如， *We.Retail*。

**** ArtifactA可部署單元。將原始碼轉換為單一單元的某些構建過程的結果。 例如包含原始碼的Zip檔案。

**對象** 儲存庫儲存和保護客戶特定對象的儲存位置。

**** 環境：程式內的單個虛擬機群集。對於AEM，這是由製作例項（可選擇搭配其他冷備用製作例項）、零個或多個發佈例項、一或多個Dispatcher例項，以及負載平衡器所組成。

**Git存** 放庫儲存客戶專屬原始碼的位置，可使用Git通訊協定存取。

**** 執行個體執行AEM解決方案的特定虛擬伺服器。實例從部署角度表示單個邏輯單元。

**** 組織Adobe建構代表企業客戶。根據Adobe的Identity Management系統中最初布建的組織方式，一家公司可能有多個組織。

**** 管道(Pipeline)依序執行的一組部署步驟。

**** 產品在由組織授權的解決方案內的特定功能集。組織內的不同方案可能有權獲得不同的產品集。 例如Sites、Forms的Assets。

**** 方案支援客戶活動邏輯分組的一組環境，通常對應於購買的服務級別協定(SLA)。每個程式都只有一個生產環境，並且可能有許多非生產環境。

**** 解決方案Adobe解決 [!UICONTROL Experience Cloud] 方案之一。例如Adobe Experience Manager、Adobe Target或Adobe Analytics。

**** Step（步驟）配置的指令集，用於完成管道的某些工作單元、構建塊。
