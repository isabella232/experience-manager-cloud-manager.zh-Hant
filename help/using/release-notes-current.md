---
title: 2021.5.0 版發行說明
description: 請依照本頁取得Cloud Manager 2021.5.0版的相關資訊
feature: 發行資訊
translation-type: tm+mt
source-git-commit: 3d6f9a760a1e5bafdae6ece5627358524467a0d2
workflow-type: tm+mt
source-wordcount: '202'
ht-degree: 6%

---

# 2021.5.0 版發行說明 {#release-notes-for}

下節概述[!UICONTROL Cloud Manager] 2021.5.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2021.5.0版的發行日期為2021年5月6日。
下一版預計於2021年6月03日推出。

## 新功能 {#whats-new}

* PackageOverlaps品質規則現在會偵測在相同部署的套件集中，同一套件已部署多次（即在多個內嵌位置）的情況。

* Public API中的儲存庫端點現在包含Git URL。

* 在「編輯方案」工作流程中，使用者只能設定非小數的KPI值。

* 現在已解決將程式碼推送至AdobeGit時間不斷發生的故障。

* 編輯程式體驗已重新整理。

## 錯誤修正 {#bug-fixes}

* 有時，即使未部署該配置，用戶在「IP允許清單」旁邊也會看到綠色&#x200B;*active*&#x200B;狀態。

* 管線變數API不會移除&#39;deleted&#39;變數，而只會以&#39;DELETED&#39;狀態標籤它們。

* 某些「程式碼氣味」類型的品質問題錯誤地影響「可靠性評等」。

* 當管道執行在午夜到凌晨1點之間啟動時，Cloud Manager生成的對象版本不保證大於前一天建立的版本。
