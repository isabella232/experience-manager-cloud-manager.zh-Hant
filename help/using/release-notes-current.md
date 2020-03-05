---
title: 2020.3.0 的發行說明
seo-title: AEM Cloud Manager 2020.3.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.3.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.3.0版的相關資訊
translation-type: tm+mt
source-git-commit: 44671d89edad0ccb6ded998b62beb5fa012678e9

---

# 2020.3.0 的發行說明 {#release-notes-for}

下節概述2020.3.0版的一 [!UICONTROL Cloud Manager] 般發行說明。

## Release Date {#release-date}

2020.3.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年3月05日。

## 新功能 {#whats-new}

* 現在，在運行生成步驟時，生成步驟的日誌可用。
* 已編輯管線執行詳細資訊頁面上的部分消息以明確說明。

## 錯誤修正 {#bug-fixes}

* 如果部署失敗，某些部署配置可能會導致部署步驟的日誌不可用。
* 托管服務程式的部署步驟中的特定失敗可能導致後續執行無法啟動。
* 建置步驟中使用的短暫SonarQube實例偶爾在配置的超時內無法啟動。
* 在特定項目中， *ResourceResolver對象應始終關閉* ，將產生Null指針異常；但是，這不會影響管線執行。


