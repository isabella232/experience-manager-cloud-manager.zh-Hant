---
title: 2020.7.0 版發行說明
seo-title: AEM Cloud Manager 2020.7.0版發行說明
description: 請詳閱本頁，了解Cloud Manager 2020.7.0版的相關資訊
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2020.7.0版的資訊
feature: 發行資訊
exl-id: c0272d9d-0a6d-4abd-add1-f82280b7ecec
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '212'
ht-degree: 52%

---

# 2020.7.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2020.9.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2020.7.0版的發行日期為2020年7月9日。

## 新功能 {#whats-new}

* 現在起，在生產部署期間，從負載平衡器分離和附加Dispatcher例項，可以以更一致的方式運作。

* Cloud Manager 建置容器現可支援 Java 8 和 Java 11。

* Cloud Manager 管道現在支援客戶設定變數和機密。如需詳細資訊，請參閱[管道變數](/help/using/build-environment-details.md#pipeline-variables)。

## 錯誤修正 {#bug-fixes}

* 非生產管道編輯頁面上的&#x200B;**取消**&#x200B;和&#x200B;**儲存**&#x200B;選項不一定會顯示。

* 程式碼品質處理程序的某些失敗作業可能導致系統無法正確產生記錄檔。

* 部分大型管道步驟記錄檔無法透過使用者介面穩定下載。

## 已知問題 {#known-issues}

* 當AMS環境包含備用執行個體時，記錄的訊息會指出執行個體關閉，而非處於備用模式。

* 由於程式碼涵蓋範圍的計算方式有所變更，Jacoco 外掛程式的&#x200B;_最低_&#x200B;版本現在是 0.7.5.201505241946 (2015 年 5 月發佈)。若客戶明確參考較舊版本，會在程式碼品質處理程序中收到錯誤訊息。
