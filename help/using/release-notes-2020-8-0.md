---
title: 2020.8.0 版發行說明
seo-title: AEM Cloud Manager 2020.8.0版發行說明
description: 請詳閱本頁，了解Cloud Manager 2020.8.0版的相關資訊
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2020.8.0版的相關資訊
feature: 發行資訊
exl-id: 94163e28-5c29-4a00-9a2b-e45bf6f71098
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 7%

---

# 2020.8.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2020.8.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2020.8.0版的發行日期為2020年8月6日。

## 新功能 {#whats-new}

現在支援與驗證綁定的專用Maven儲存庫。

## 錯誤修正 {#bug-fixes}

* 在程式碼品質掃描中，會執行一些不必要的SonarQube外掛程式。

* 在管道執行頁面上，分支名稱的格式不正確。

* 使用單一發佈、單一Dispatcher和冷備作者部署至拓撲時，Dispatcher會錯誤地從負載平衡器中移除。

* 在某些情況下，完成的管道執行未被成功記錄為已完成，從而防止了管道的新執行。

* 由於內部通訊問題，管道執行偶爾會出現&#x200B;*卡住*。

* 程式卡上的工具提示不一致。

* **概述**&#x200B;頁面的顏色不匹配。

* 網站效能測試現在支援使用驗證功能。

* 透過Cloud Manager部署Dispatcher設定時，會自動清除製作例項的Dispatcher快取。
