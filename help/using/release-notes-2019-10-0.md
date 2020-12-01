---
title: 2019.10.0 版發行說明
seo-title: AEM Cloud Manager 2019.10.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.10.0版的資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.10.0版的相關資訊。
translation-type: tm+mt
source-git-commit: 52c54568d8ab7b5091c25b3b65b4baa126bf61f5
workflow-type: tm+mt
source-wordcount: '246'
ht-degree: 4%

---

# 2019.10.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2019.10.0版的一般發行說明，並新增部署步驟的更新，並管理專案版本處理。
請依照下列章節瞭解詳細資訊。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.10.0版的發行日期為2019年10月10日。

## 新功能 {#whats-new}

* 部署步驟中的大部分已提升效能。
* 如果適用，組建Maven專案的版本現在將以git的形式整合專案版本。
* 在構建時，有新的環境變數可用。
* 非生產管線可從&#x200B;**概述**&#x200B;頁面和API上的卡片中刪除。
* 在階段部署步驟之後，但在安全性測試步驟之前，會立即有新的選擇性核准步驟。
* 在配置CI/CD流水線時，可以跳過從負載平衡器分離和附加調度器實例，以用於開發和階段環境。
有關詳細資訊，請參閱**[部署進程](deploying-code.md#deployment-process)**。
* Cloud Manager CLI已擴充，可支援存取執行步驟記錄檔。
* Cloud Manager API現在支援編輯管道的已設定分支。
* 效能測試期間執行的要求現在包含使用者代理中的特定Token ***CloudManagerTest***。

## 錯誤修正 {#bug-fixes}

* **概述**&#x200B;頁面上的某些卡片未正確垂直對齊。
* 某些故障條件不會導致管線執行被正確標籤，並阻止後續執行。
