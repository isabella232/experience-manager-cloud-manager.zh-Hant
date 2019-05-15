---
title: 2019.4.0版發行說明
seo-title: 2019.4.0的AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2019.4.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2019.4.0的資訊。
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2019.4.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.4.0版本不包含重大功能變更。請遵循下列章節以瞭解詳細資訊。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.4.0版的發行日期為2019年月18日。

## 新功能 {#whats-new}

* Cloud Manager UI現在提供英文、法文、德文和日文版本。
* 部署步驟現在包含目前執行的程序，亦即，當備份執行時，會安裝封裝，並重新設定負載平衡器

## 錯誤修正 {#bug-fixes}

* Dispatcher變更所使用的部署方式已改善，以處理其他使用案例。
* 有些實體大小類型無法正確顯示在「環境」頁面上。
* 程式碼品質規則CQBP-84-Dependencies為內嵌Adobe程式庫(例如WCM核心元件和資產分享逗號)產生了錯誤的置信度。
* 無法使用程式碼掃描步驟的詳細資訊按鈕。
* 指定每分鐘KPI頁面檢視值無效的錯誤訊息的界限錯誤。
* 非生產管道上的部署類別不正確。
* 當git存放庫未正確設定時 **，「概述」** 頁面上的動作卡片呼叫有不正確的文字。

## 已知問題 {#known-issues}

* SLA值可能不正確。
