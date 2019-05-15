---
title: 2019.2.0版發行說明
seo-title: 2019.2.0AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2019.2.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2019.2.0的資訊。
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2019.2.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.2.0版本新增了新的系統監控功能。這可讓客戶在系統層級檢視其Adobe Managed Services環境的狀態。


## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.2.0版的發行日期為2019年月21日。

## 新功能 {#whats-new}

* 新的系統監控功能。請參閱 [監控您的環境](monitor-your-environments.md) 以瞭解更多資訊。
* 精靈產生專案中的dispatcher模組現在包含README檔案。
* 程式碼掃描問題的排序順序已改善，以符合問題優先順序。
* 即使在部署失敗時，現在也會將階段例項還原為負載平衡器。
* Admin Console中提供新的API開發人員角色，可讓特定使用者獲得在Adobe I/主控台中建立整合的權限。請參閱 [管理開發人員](https://www.adobe.com/go/aac_api_prod_learn) 以瞭解更多資訊。
* Maven Archetype的版本已更新至16版。
* Maven的版本已更新至3.6.0版。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，在Azure托管目標環境時，管線不會執行。
* 環境的訂購不一致。
* 當發現頁面路徑包含逗號字元時，效能測試可能會失敗。
* 從Web UI啓動管線執行時，瀏覽器上一頁按鈕無法正常運作。
* 「概述」頁面上的「詳細資訊」連結未開啓新標籤。
* 上傳程式縮圖時，可能無法立即顯示。
* 在某些情況下，程式碼掃描失敗，因為專案特定設定。
* 「瞭解非生產管道」卡片上的更多連結前往錯誤的位置。
* 當品質關卡被覆寫時，狀態顯示不一致。
* 使用冷備拓撲的客戶會收到不正確的安全性測試結果。
* 使用精靈建立新專案時，無法建立包含破折號字元的分支。

## 已知問題 {#known-issues}

* 當監控資料時，任何隱藏的系列都會解除隱藏。
* 想要檢視現有SLA報告的客戶必須手動瀏覽，直到下一個版本發行為止。

   若要建立此URL，請遵循模式(`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`)，例如，如果Experience Cloud的URL為(`https://weretailprod.experiencecloud.adobe.com`)，則您的SLA報表URL為(`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`)。

   預計下一版將會解決此問題，並提供內部SLA報告 [!UICONTROL Cloud Manager]。
