---
title: 2020.7.0 版發行說明
seo-title: AEM Cloud Manager 2020.7.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.7.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.7.0版的相關資訊
translation-type: tm+mt
source-git-commit: a4ea83c0b64515915871956c1cd3e53606f1c26b
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 7%

---

# 2020.7.0 版發行說明 {#release-notes-for}

下節概述2020.7.0版 [!UICONTROL Cloud Manager] 的一般發行說明。

## 發行日期 {#release-date}

2020.7.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年7月09日。

## 新功能 {#whats-new}

* 在生產部署期間從負載平衡器分離和連接調度器實例現在可以以更一致的方式工作。

* Cloud Manager組建容器現在支援Java 8和Java 11。

## 錯誤修正 {#bug-fixes}

* 「非 **生產管線編** 輯」(Non-Production Pipeline Edit)頁面上的「取消」(Cancel)和「保存」(Save **** )選項並不總是可見。

* 程式碼品質處理中的某些失敗可能會導致記錄檔無法正確產生。

* 有些大型管線步驟記錄無法一貫地透過使用者介面下載。

## 已知問題 {#known-issues}

* 當AMS環境包含備用實例時，記錄的消息會指出該實例處於關閉狀態，而非處於備用模式。

* 由於程式碼涵蓋範圍的計算方式有所變 _更_ ,Jacoco外掛程式的最低版本現在為0.7.5.201505241946（2015年5月發行）。 明確參照舊版的客戶會在程式碼品質程式中收到錯誤訊息。
