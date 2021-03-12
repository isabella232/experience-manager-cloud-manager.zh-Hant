---
title: 2021.3.0 版發行說明
seo-title: Cloud Manager AEM 2021.3.0版本說明
description: 請依照本頁取得Cloud Manager 2021.3.0版的相關資訊
seo-description: 請依照本頁取得AEMCloud Manager 2021.3.0版的資訊
translation-type: tm+mt
source-git-commit: b0c29ed6712abd556458aea6d49f6382f183cdae
workflow-type: tm+mt
source-wordcount: '279'
ht-degree: 4%

---

# 2021.3.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2021.3.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.3.0版的發行日期為2021年3月11日。

## 新功能 {#whats-new}

* 擁有必要權限的使用者現在可以編輯程式，讓他們以自助方式執行下列作業：

   *將Sites解決方案加入包含資產的現有計畫（反之亦然）。
   * 將網站（或資產）從現有的計畫中移除，同時包含網站和資產。
   * 新增（上一步）解決方案可以對現有方案或作為新方案執行。

* 為驗證客戶調度器配置(Dispatcher Optimization Tool)，引入了新的代碼質量工具。

* 現在，在導覽至Unified Shell的「用戶配置檔案」表徵圖（右上角）後，用戶可以選擇「查看雲管理員角色」****&#x200B;選項，以查看其Cloud Manager角色。

* **申請批准**&#x200B;標籤已重新標籤至&#x200B;**生產批准**，以更清楚明瞭。

* **版本**&#x200B;標籤已重新標籤至「生產管線」執行畫面中的&#x200B;**Git Tag**。

* 當重要量度不符合定義的臨界值時，定義行為的標籤已重新標籤，以反映其真實行為- *取消立即*&#x200B;和批准立即&#x200B;*。*

* 類別和方法取代清單已根據Cloud ServiceSDK的`2021.3.4997.20210303T022849Z-210225`版AEM本更新。

## 錯誤修正 {#bug-fixes}

* 在將包嵌入其他包時，未正確發現某些質量問題。

* 有時，如果用戶在啟動管線後立即導航離開管線執行頁面，則會顯示一條錯誤消息，指出操作失敗，儘管實際上執行開始。