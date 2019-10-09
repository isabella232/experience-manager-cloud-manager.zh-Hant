---
title: 2019.10.0發行說明
seo-title: AEM Cloud manager 2019.10.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.10.0版的資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.10.0版的相關資訊。
translation-type: tm+mt
source-git-commit: 1e927076e6bc84e8e1761e33a86cff61a3be0d2f

---

# 2019.10.0發行說明 {#release-notes-for}

下節概述2018.10.0版的一般發行說明，並新增部署步驟的更新，並管理專案版本處理。 [!UICONTROL Cloud Manager] 
請依照下列頁面瞭解詳細資訊。

## 發行日期 {#release-date}

2019.10.0版 [!UICONTROL Cloud Manager] 的發行日期為2019年10月12日。

## 新功能 {#whats-new}

* 部署步驟中的大部分已提升效能。
* 如果適用，組建Maven專案的版本現在將以git的形式整合專案版本。
* 在構建時，有新的環境變數可用。
* 非生產管道可從「概述」頁面和API的卡片中刪除。
* 在階段部署步驟之後，但在安全性測試步驟之前，會立即有新的選擇性核准步驟。
* 在配置CI/CD流水線時，可以跳過從負載平衡器分離和附加調度器實例，以用於開發和階段環境。
請參閱部 **[署程式](deploying-code.md#deployment-process)** ，以取得詳細資訊。
* Cloud Manager CLI已擴充，可支援存取執行步驟記錄檔。
* Cloud Manager API現在支援編輯管道的已設定分支。
* 效能測試期間執行的要求現在會在使用者代理 ***中包含特定的Token cloudManagerTest*** 。

## 錯誤修正 {#bug-fixes}

* 「概述」頁面上的某些卡 **片未** 正確垂直對齊。
* 某些故障條件不會導致管線執行被正確標籤，並且阻止後續執行。
