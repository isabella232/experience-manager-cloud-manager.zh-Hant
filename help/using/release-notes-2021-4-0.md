---
title: 2021.4.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.4.0版的資訊
feature: 發行資訊
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 5f81fdb86b1dfa6c748bb7784ef00dc062c9f8ef
workflow-type: tm+mt
source-wordcount: '185'
ht-degree: 7%

---

# 2021.4.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2021.4.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.4.0版的發行日期為2021年4月8日。

## 新功能 {#whats-new}

* 效能測試虛擬使用者的請求逾時已從20秒增加為60秒。

* 即使未設定管道，「管理Git」按鈕仍會顯示在管道卡上。

* 在「管道」執行頁面的部署步驟期間，除了&#x200B;*進行中*&#x200B;狀態的UI中的目前步驟外，使用者還可以查看已完成和未來的部署步驟。

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 已釐清刪除環境時啟動管道時的錯誤訊息。

* Eclipse專案提供的OSGi套件組合現已從規則`CQBP-84--dependencies`中排除。

## 錯誤修正 {#bug-fixes}

* 在生產管道的&#x200B;*資產測試*&#x200B;步驟中可能發生的罕見暫時性錯誤。

* 生產管道負載測試中的尾端斜線導致404失敗。

* `Runmode`檢查對非資料夾節點產生誤判。