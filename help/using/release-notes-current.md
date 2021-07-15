---
title: 2021.7.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.7.0版的資訊
feature: 發行資訊
source-git-commit: 1da4ceef0d89223580800d9018c46aaec51f8927
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 6%

---

# 2021.7.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.7.0版的一般發行說明。

>[!NOTE]
>請參閱[最新發行說明](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/onboarding/getting-access/release-notes-cloud-manager/release-notes-cm-current.html?lang=en#getting-access) ，查看AEM as aCloud Service中Cloud Manager的最新發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.7.0版的發行日期為2021年7月15日。
下一版預計於2021年8月12日發行。

## 新增功能 {#whats-new}

* 客戶現在可以將Azul 8和11 JDK用於其Cloud Manager構建進程，並且可以選擇將其中一個JDK用於與工具鏈相容的Maven插件&#x200B;*或*&#x200B;整個Maven進程執行。

* 傳出輸出IP現在將記錄在建置步驟記錄檔中。

* **管理Git**&#x200B;按鈕已取消&#x200B;**存取Git資訊**，對話方塊也已視覺化重新整理。

* Cloud Manager使用的AEM專案原型版本已更新為28版。

* 某些意外的拓撲重新配置可能導致從管道執行詳細資訊頁面中不再提供詳細測試報告。

## 錯誤修正 {#bug-fixes}

* 手動導覽至非現有執行的執行詳細資訊頁面時未顯示錯誤，只是無休止的載入畫面。

* 在某些情況下，Sites效能中使用的失敗容器的自動重試在2小時內不會生效，導致測試失敗。

## 已知問題 {#known-issues}

切換使用Azul JDK的客戶應注意，並非所有現有應用程式都會在Azul JDK上編譯，且不會出現錯誤。 強烈建議您在切換前先在本機測試。