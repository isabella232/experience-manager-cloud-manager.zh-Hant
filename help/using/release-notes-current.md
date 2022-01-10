---
title: 2021.12.0 版發行說明
description: 以下是Cloud Manager 2021.12.0版的發行說明。
feature: Release Information
exl-id: 2d38abb1-cfc7-44a9-b303-b555e2827eea
source-git-commit: 61f2d1e0882b752d1a1d5e62f9c028aa71941efe
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 3%

---

# Cloud Manager發行說明2021.12.0版 {#release-notes}

以下章節概述的一般發行說明 [!UICONTROL Cloud Manager] 2021.12.0版。

>[!NOTE]
>
>如需AEM as a Cloud Service中Cloud Manager的最新發行說明，請參閱 [AEM as a Cloud Service最新發行說明中的Cloud Manager](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/release-notes-cloud-manager/release-notes-cm-current.html)

## 發行日期 {#release-date}

的發行日期 [!UICONTROL Cloud Manager] 2021.12.0版是2021年12月16日。 下一版預計於2022年1月推出。

## 新增功能 {#whats-new}

* UI中已顯示提交雜湊，現在也會在API中提供。
* 「活動」頁面現在包含用於執行管道的快顯視窗，可提供管道詳細資訊的摘要，一覽無遺。
* 已新增更新，加入「活動」頁面中顯示的其他詳細資料。
* Cloud Manager中的「學習」標籤現在提供API指南和相關資源的快速存取。
* 具有部署管理員角色的用戶現在可以為資料庫啟動項目/分支建立嚮導，該資料庫沒有「資料庫」頁面上的「操作」菜單中的分支。
* 現在，如果所選儲存庫沒有分支，將通知處於添加或編輯管道工作流的部署管理員如何建立分支或項目。
* 在「編輯生產管道」視窗中，如果有多個生產階段環境，則可使用供環境選取的下拉式清單。
* Cloud Manager使用的AEM專案原型版本已更新為32版。

## 錯誤修正 {#bug-fixes}

* 即使使用者在名稱欄位中輸入不同名稱，完整堆疊生產管道仍會保留名為「生產管道」。
