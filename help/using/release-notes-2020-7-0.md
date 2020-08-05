---
title: 2020.7.0 版發行說明
seo-title: AEM Cloud Manager 2020.7.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.7.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.7.0版的相關資訊
translation-type: tm+mt
source-git-commit: 3be958aa21d5423ddf371c286825d01afd554c4b
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 51%

---

# 2020.7.0 版發行說明 {#release-notes-for}

下節概述2020.7.0版 [!UICONTROL Cloud Manager] 的一般發行說明。

## 發行日期 {#release-date}

The Release Date for [!UICONTROL Cloud Manager] Version 2020.7.0 is July 09, 2020.

## 新功能 {#whats-new}

* 在生產部署期間從負載平衡器分離和連接調度器實例現在可以以更一致的方式工作。

* Cloud Manager 建置容器現可支援 Java 8 和 Java 11。

* Cloud Manager 管道現在支援客戶設定變數和機密。如需詳細資訊，請參閱[管道變數](/help/using/create-an-application-project.md#pipeline-variables)。

## 錯誤修正 {#bug-fixes}

* The **Cancel** and **Save** options on the Non-Production Pipeline Edit page were not always visible.

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

## 已知問題 {#known-issues}

* 當AMS環境包含備用實例時，記錄的消息會指出該實例處於關閉狀態，而非處於備用模式。

* 由於程式碼涵蓋範圍的計算方式有所變更，Jacoco 外掛程式的&#x200B;_最低_&#x200B;版本現在是 0.7.5.201505241946 (2015 年 5 月發佈)。若客戶明確參考較舊版本，會在程式碼品質處理程序中收到錯誤訊息。
