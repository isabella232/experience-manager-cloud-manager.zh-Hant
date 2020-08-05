---
title: 2020.8.0 版發行說明
seo-title: AEM Cloud Manager 2020.8.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.8.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.8.0版的相關資訊
translation-type: tm+mt
source-git-commit: 3be958aa21d5423ddf371c286825d01afd554c4b
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 20%

---

# 2020.8.0 版發行說明 {#release-notes-for}

下節概述2020.8.0版 [!UICONTROL Cloud Manager] 的一般發行說明。

## 發行日期 {#release-date}

2020.8.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年8月06日。

## 新功能 {#whats-new}

* Sites Performance Testing現在支援選擇性使用驗證。

   有關詳細資訊，請參閱。

* 現在支援驗證綁定的專用Maven儲存庫。

## 錯誤修正 {#bug-fixes}

* 在程式碼品質掃描中，會執行一些不必要和不需要的SonarQube外掛程式。

* 在管線執行頁面上，分支名稱格式不正確。

* 當使用單個發佈、單個調度程式和冷備用作者部署到拓撲時，調度程式錯誤地從負載平衡器中刪除。

* 在某些情況下，未完成的管線執行未成功記錄為已完成，從而防止了管線的新執行。

* 管道執行偶爾會因 *內部* 通訊問題而卡住。

* 程式卡上的工具提示不一致正確。

* 概述頁面上的顏色不符。

## 已知問題 {#known-issues}

* 當AMS環境包含備用實例時，記錄的消息會指出該實例處於關閉狀態，而非處於備用模式。

* 由於程式碼涵蓋範圍的計算方式有所變更，Jacoco 外掛程式的&#x200B;_最低_&#x200B;版本現在是 0.7.5.201505241946 (2015 年 5 月發佈)。若客戶明確參考較舊版本，會在程式碼品質處理程序中收到錯誤訊息。
