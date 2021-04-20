---
title: 2020.3.0 版發行說明
seo-title: Cloud Manager AEM 2020.3.0版本說明
description: 請依照本頁取得Cloud Manager 2020.3.0版的相關資訊
seo-description: 請依照本頁取得AEMCloud Manager 2020.3.0版的資訊
feature: Release Information
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 51%

---

# 2020.3.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2020.3.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager]版本2020.3.0的發行日期為2020年3月05日。

## 新功能 {#whats-new}

* 現在建置步驟執行時，建置步驟記錄可供同時使用。
* 管道執行詳細資訊頁面上的部分訊息經過編輯，以更明確說明。

## 錯誤修正 {#bug-fixes}

* 如果部署失敗，某些部署配置可能會導致部署步驟的日誌不可用。
* Managed Services程式部署步驟中的特定失敗可能導致後續的執行無法啟動。
* 在設定的逾時期限內，建置步驟中使用的短暫 SonarQube 例項偶爾會無法啟動。
* 特定專案中，*ResourceResolver 物件應一律關閉*，這會產生 Null 指標異常，但不會影響管道執行。