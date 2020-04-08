---
title: 2020.3.0 版發行說明
seo-title: AEM Cloud Manager 2020.3.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.3.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.3.0版的相關資訊
translation-type: tm+mt
source-git-commit: e7da473a22bec1d3d9b3d39bf654af0c596fe86d

---

# 2020.3.0 版發行說明 {#release-notes-for}

下節概述2020.3.0版的一 [!UICONTROL Cloud Manager] 般發行說明。

## Release Date {#release-date}

2020.3.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年3月05日。

## 新功能 {#whats-new}

* 現在建置步驟執行時，建置步驟記錄可供同時使用。
* 管道執行詳細資訊頁面上的部分訊息經過編輯，以更明確說明。

## 錯誤修正 {#bug-fixes}

* 如果部署失敗，某些部署配置可能會導致部署步驟的日誌不可用。
* 托管服務程式的部署步驟中的特定失敗可能導致後續執行無法啟動。
* 在設定的逾時期限內，建置步驟中使用的短暫 SonarQube 例項偶爾會無法啟動。
* 特定專案中，*ResourceResolver 物件應一律關閉*，這會產生 Null 指標異常，但不會影響管道執行。