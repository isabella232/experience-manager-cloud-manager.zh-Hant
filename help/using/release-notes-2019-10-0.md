---
title: 2019.10.0 版發行說明
seo-title: AEM Cloud Manager2019.10.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.10.0版的資訊。
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2019.10.0版的資訊。
feature: 發行資訊
exl-id: b58f7a1b-2063-4ac8-b676-bb74200d7ac9
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '248'
ht-degree: 5%

---

# 2019.10.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2019.10.0版的一般發行說明，並新增部署步驟的更新及Maven專案版本處理。
如需詳細資訊，請參閱以下各節。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.10.0版的發行日期為2019年10月10日。

## 新功能 {#whats-new}

* 部署步驟的很大一部分已提高效能。
* 如適用，組建Maven專案版本現在會將專案版本整合至Git。
* 在建置時，可使用新的環境變數。
* 可從&#x200B;**概述**&#x200B;頁面和API上的卡片中刪除非生產管道。
* 在階段部署步驟之後，緊接著在安全性測試步驟之前，會有一個新的可選批准步驟。
* 在設定CI/CD管道時，可針對開發和預備環境，略過從負載平衡器分離和附加Dispatcher例項。
如需詳細資訊，請參閱**[部署程式](deploying-code.md#deployment-process)** 。
* Cloud Manager CLI已增強，可支援存取執行步驟記錄。
* Cloud Manager API現在支援編輯管道的已設定分支。
* 效能測試期間執行的請求現在會在使用者代理中加入特定Token ***CloudManagerTest***。

## 錯誤修正 {#bug-fixes}

* **概述**&#x200B;頁面上的某些卡片未正確垂直對齊。
* 某些失敗條件不會正確標籤管道執行，並防止後續執行。
