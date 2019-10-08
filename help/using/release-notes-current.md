---
title: 2019.10.0發行說明
seo-title: AEM Cloud manager 2019.10.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.10.0版的資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.10.0版的相關資訊。
translation-type: tm+mt
source-git-commit: de9d2834ffa6c235e580227bd020fb8a0b94d22c

---

# 2019.10.0發行說明 {#release-notes-for}

2019. [!UICONTROL Cloud Manager] 10.0版本會更新安全性測試標準、新增可下載的監控圖表，並修正客戶報告的可用性問題。

## 發行日期 {#release-date}

2019.10.0版 [!UICONTROL Cloud Manager] 的發行日期為2019年10月12日。

## 新功能 {#whats-new}

* 部署步驟中的大部分已提升效能。
* 如果適用，組建Maven專案的版本現在將以git的形式整合專案版本。
* 在構建時，有新的環境變數可用。
* 非生產管道可從「概述」頁面和API的卡片中刪除。
* 在階段部署步驟之後，但在安全性測試步驟之前，會立即有新的選擇性核准步驟。
* 在配置CI/CD流水線時，可以跳過從負載平衡器分離和附加調度器實例，以用於開發和階段環境。
* Cloud Manager CLI已擴充，可支援存取執行步驟記錄檔。
* Cloud Manager API現在支援編輯管道的已設定分支。
* 效能測試期間執行的要求現在包含使用者代理中的特定Token(「CloudManagerTest」)。

## 錯誤修正 {#bug-fixes}

* 「概述」頁面上的某些卡片未正確垂直對齊。
* 某些故障條件不會導致管線執行被正確標籤，並且阻止後續執行。
