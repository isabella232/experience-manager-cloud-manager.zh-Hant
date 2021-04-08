---
title: 2021.4.0 版發行說明
description: 請依照本頁取得Cloud Manager 2021.4.0版的相關資訊
feature: 發行資訊
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
translation-type: tm+mt
source-git-commit: 1f7f87a4b944d1fadc708958a96a1bda7d41da5d
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 7%

---

# 2021.4.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2021.4.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager]版本2021.4.0的發行日期為2021年4月08日。
下一版預計於2021年5月06日推出。

## 新功能 {#whats-new}

* 效能測試虛擬使用者的請求逾時已從20秒增加至60秒。

* 即使未配置管線，「管理Git」按鈕也會顯示在「管線」卡上。

* 在「管線」執行頁的部署步驟期間，除了&#x200B;*進行中*&#x200B;狀態的UI中的當前步驟外，用戶還可以查看已完成和未來的部署步驟。

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 刪除環境時啟動管線時的錯誤消息已被澄清。

* Eclipse專案提供的OSGi組合現在已排除在規則`CQBP-84--dependencies`之外。

## 錯誤修正 {#bug-fixes}

* 在生產管線中，在&#x200B;*Assets Test*&#x200B;步驟中可能發生的罕見的暫時錯誤。

* 生產管線「載入測試」中的尾隨斜線導致404失敗。

* `Runmode`檢查對非資料夾節點產生誤報。