---
title: 2019.2.0 版發行說明
seo-title: AEM Cloud Manager 2019.2.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.2.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.2.0版的相關資訊。
translation-type: tm+mt
source-git-commit: 98395c4413b1b6bfbb3a565388ffa32dc3880dff
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 3%

---


# 2019.2.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.2.0版新增了系統監控功能。 這可讓客戶在系統層級檢視其Adobe Managed Services環境的狀態。


## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.2.0版的發行日期為2019年2月21日。

## 新功能 {#whats-new}

* 新的系統監控功能。 請參閱[監控您的環境](monitor-your-environments.md)以瞭解更多資訊。
* 嚮導生成的項目中的調度器模組現在包含README檔案。
* 「程式碼掃描」問題的排序順序已改良，以符合問題優先順序。
* 現在，即使在部署失敗時，也始終將階段實例還原到負載平衡器。
* Admin Console中提供新的API開發人員角色，可讓特定使用者獲得在Adobe I/O主控台中建立整合的權限。 請參閱[管理開發人員](https://www.adobe.com/go/aac_api_prod_learn)以瞭解詳細資訊。
* Maven Archetype的版本已更新為16版。
* Maven的版本已更新至3.6.0版。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，當目標環境裝載在Azure中時，管道將不會執行。
* 環境順序不一致。
* 當發現的頁面路徑包含逗號字元時，效能測試可能會失敗。
* 從Web UI啟動管線執行時，瀏覽器上一步按鈕無法正常運作。
* 「概述」頁面上的「瞭解更多」連結未開啟新的標籤。
* 上傳程式縮圖時，可能尚未立即顯示。
* 在某些情況下，由於專案特定的設定，程式碼掃描失敗。
* 「非生產管道」卡上的「瞭解更多」(Learn More)連結到了錯誤的位置。
* 當品質選項被覆寫時，狀態顯示不一致。
* 使用冷備用拓撲的客戶在安全測試中收到錯誤結果。
* 使用嚮導建立新項目時，無法建立包含破折號字元的分支。

## 已知問題 {#known-issues}

* 重新整理監控資料時，任何隱藏的系列都會取消隱藏。
* 希望查看其現有SLA報告的客戶需要手動導航到下一版。

   若要建立此URL，請遵循模式(`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`)，例如，如果Experience Cloud的URL是(`https://weretailprod.experiencecloud.adobe.com`)，則您的SLA報表URL是(`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`)。

   在下一版中，當[!UICONTROL Cloud Manager]內部提供SLA報告時，此問題預計會得到解決。
