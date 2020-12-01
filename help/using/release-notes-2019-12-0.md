---
title: 2019.12.0 版發行說明
seo-title: AEM Cloud Manager 2019.12.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.12.0版的資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.12.0版的相關資訊。
translation-type: tm+mt
source-git-commit: 0fa1fedccb013e82c8df5838a612ce26a1efb7e8
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 5%

---


# 2019.12.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager]版本2019.12.0的一般發行說明，並新增管線執行的更新以及程式碼品質掃描的增強功能。
請依照下列章節瞭解詳細資訊。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager]版本2019.12.0的發行日期為2019年12月12日。

## 新功能 {#whats-new}

* 流水線執行中的步驟現在會顯示每個步驟的完成時間戳記。
* 程式碼品質掃描不含Java程式碼的專案，現在報告的程式碼涵蓋率為100%。
* CQ Dispatcher Configuration Health檢查已刪除。

## 錯誤修正 {#bug-fixes}

* 某些瀏覽器無法正確顯示日期。
* 在少數情況下，當效能測試仍在執行時，生產管道會移至核准步驟。
* 在某些狀態下，概述頁面頂部區域上的按鈕未正確對齊。
* 在某些情況下，未經授權的用戶看到一個按鈕來啟動管道，儘管按鈕本身無法按一下。
* 非生產管線的操作按鈕有時會顯示在錯誤的位置。
* 具有granite：無法掃描「排名」節點類型的封裝，以發現某些品質規則違規。
* 程式碼品質程式中的某些失敗錯誤會錯誤計算為錯誤。
* 無法為某些拓撲載入監視資料。
