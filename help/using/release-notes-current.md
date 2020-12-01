---
title: 2020.11.0 版發行說明
seo-title: AEM Cloud Manager 2020.11.0版本注意事項
description: 請依照本頁取得Cloud Manager版本2020.11.0的資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.11.0版的相關資訊
translation-type: tm+mt
source-git-commit: 30d782f5a095b1b07ec4f2039def9ba30a559325
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 7%

---

# 2020.11.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2020.11.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2020.11.0版的發行日期為2020年11月12日。

## 新功能 {#whats-new}

* Cloud Manager中的&#x200B;**Learn**&#x200B;標籤會以UI中的新影像重新整理。

## 錯誤修正 {#bug-fixes}

* 某些客戶導致的部署錯誤現在會明確地出現在部署記錄中。

* 在建立執行前載入的相依性需要下載Maven外掛程式。

* 從Cloud Manager頁尾選取語言的連結現在會導覽至正確的位置。

* 有時在程式碼掃描期間，SonarQube程式不會啟動。 現在會自動偵測到此問題，並嘗試重新啟動。

* 在效能測試中使用的網站編目程式中，會自動重試前三個深度遍歷層級中逾時的請求。