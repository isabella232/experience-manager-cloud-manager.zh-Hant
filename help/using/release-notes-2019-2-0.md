---
title: 2019.2.0 版發行說明
seo-title: AEM Cloud Manager 2019.2.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.2.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2019.2.0版的資訊。
feature: 發行資訊
exl-id: e7198efa-4a73-42e5-bb17-8dea255e056e
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 4%

---

# 2019.2.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2019.2.0版新增了新的「系統監控」功能。 這可讓客戶在系統層級檢視其Adobe Managed Services環境的狀態。


## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.2.0版的發行日期為2019年2月21日。

## 新功能 {#whats-new}

* 新的系統監視功能。 請參閱[監視環境](monitor-your-environments.md)以了解詳細資訊。
* 精靈產生專案中的Dispatcher模組現在包含README檔案。
* 已改善程式碼掃描問題的排序順序，以符合問題優先順序。
* 現在，即使在部署失敗時，階段例項也一律會還原至負載平衡器。
* Admin Console中提供新的API開發人員角色，可讓特定使用者有權在Adobe I/O主控台中建立整合。 請參閱[管理開發人員](https://www.adobe.com/go/aac_api_prod_learn)以深入了解。
* Maven原型的版本已更新為16版。
* Maven的版本已更新至3.6.0版。

## 錯誤修正 {#bug-fixes}

* 在某些情況下，當目標環境托管於Azure時，管道不會執行。
* 環境順序不一致。
* 發現的頁面路徑包含逗號字元時，效能測試可能會失敗。
* 從Web UI啟動管道執行時，瀏覽器上一步按鈕無法正常運作。
* 概述頁面上的了解更多連結未開啟新標籤。
* 上傳程式縮圖時，可能尚未立即顯示。
* 在某些情況下，由於專案專屬的設定，程式碼掃描失敗。
* 非生產管道卡上的「了解更多」連結出現錯誤。
* 當質量門被覆蓋時，狀態顯示不一致。
* 使用冷備用拓撲的客戶收到了錯誤的安全測試結果。
* 使用精靈建立新專案時，無法建立包含破折號字元的分支。

## 已知問題 {#known-issues}

* 重新整理監控資料時，會取消隱藏任何隱藏的系列。
* 希望查看其現有SLA報告的客戶需要手動導航到下一個版本。

   要制定此URL，請按照模式(`https://<Experience Cloud URL>/content/mac/<Experience Cloud Tenant>/managedservices/sla.html`)，例如，如果Experience Cloud的URL是(`https://weretailprod.experiencecloud.adobe.com`)，則您的SLA報告URL是(`https://weretailprod.experiencecloud.adobe.com/content/mac/weretailprod/managedservices/sla/html`)。

   在[!UICONTROL Cloud Manager]內提供SLA報告時，預計在下一版中會解決此問題。
