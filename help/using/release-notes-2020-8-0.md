---
title: 2020.8.0 版發行說明
seo-title: AEM Cloud Manager 2020.8.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.8.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.8.0版的相關資訊
translation-type: tm+mt
source-git-commit: c1d07c95088a279376ef495001a5165c7e459642
workflow-type: tm+mt
source-wordcount: '192'
ht-degree: 6%

---

# 2020.8.0 版發行說明 {#release-notes-for}

下節概述2020.8.0版 [!UICONTROL Cloud Manager] 的一般發行說明。

## 發行日期 {#release-date}

2020.8.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年8月06日。

## 新功能 {#whats-new}

現在支援驗證綁定的專用Maven儲存庫。

## 錯誤修正 {#bug-fixes}

* 在程式碼品質掃描中，會執行一些不必要和不需要的SonarQube外掛程式。

* 在管線執行頁面上，分支名稱格式不正確。

* 當使用單個發佈、單個調度程式和冷備用作者部署到拓撲時，調度程式錯誤地從負載平衡器中刪除。

* 在某些情況下，未完成的管線執行未成功記錄為已完成，從而防止了管線的新執行。

* 管道執行偶爾會因 *內部* 通訊問題而卡住。

* 程式卡上的工具提示不一致正確。

* 「概述」頁面上的顏色不 **符** 。

* Sites Performance Testing現在支援選擇性使用驗證。

* 當透過Cloud Manager部署分派程式設定時，作者例項的分派程式快取會自動清除。

