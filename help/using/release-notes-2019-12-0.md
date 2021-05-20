---
title: 2019.12.0 版發行說明
seo-title: AEM Cloud Manager2019.12.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.12.0版的資訊。
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2019.12.0版的資訊。
feature: 發行資訊
exl-id: e173962f-587d-439e-a499-81ea98c52cc9
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '231'
ht-degree: 6%

---

# 2019.12.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2019.12.0版的一般發行說明，並新增管道執行的更新和程式碼品質掃描的增強功能。
如需詳細資訊，請參閱以下各節。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.12.0版的發行日期為2019年12月12日。

## 新功能 {#whats-new}

* 管道執行中的步驟現在會顯示每個步驟的完成時間戳記。
* 如果專案中不含Java程式碼，程式碼品質掃描現在會回報程式碼涵蓋率為100%。
* 已移除CQ Dispatcher設定健全狀態檢查。

## 錯誤修正 {#bug-fixes}

* 某些瀏覽器中無法正確顯示日期。
* 在少數情況下，當效能測試仍在執行時，生產管道會移至核准步驟。
* 在某些狀態下，概覽頁面頂部區域的按鈕未正確對齊。
* 在某些情況下，雖然無法點按按鈕本身，但未授權的使用者仍看到啟動管道的按鈕。
* 非生產管道的動作按鈕有時會顯示在錯誤的位置。
* 無法掃描具有granite：排名節點類型的套件，以了解是否有某些品質規則違規。
* 程式碼品質處理程式中的某些失敗錯誤計為錯誤。
* 無法為某些拓撲載入監視資料。
