---
title: 2021.4.0 版發行說明
description: 請詳閱本頁以取得Cloud Manager 2021.4.0版的資訊
feature: Release Information
source-git-commit: 09dd8fe608d95cd9dbc95129cf86b9693c2839b5
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 6%

---

# 2021.4.0 版發行說明 {#release-notes-for}

以下章節概述的一般發行說明 [!UICONTROL Cloud Manager] 版本2021.4.0。

## 發行日期 {#release-date}

的發行日期 [!UICONTROL Cloud Manager] 2021.4.0版是2021年4月8日。

## 新增功能 {#whats-new}

* 效能測試虛擬使用者的請求逾時已從20秒增加為60秒。

* 即使未設定管道，「管理Git」按鈕仍會顯示在管道卡上。

* 在管道執行頁面的部署步驟期間，除了適用於的UI中的目前步驟外，使用者還可以檢視已完成和未來的部署步驟 *進行中* 狀態。

* Cloud Manager使用的AEM專案原型版本已更新為27版。

* 已釐清刪除環境時啟動管道時的錯誤訊息。

* Eclipse專案提供的OSGi套件組合現已從規則中排除 `CQBP-84--dependencies`.

## 錯誤修正 {#bug-fixes}

* 罕見、暫時性錯誤，可能發生在 *資產測試* 在生產管道中執行步驟。

* 生產管道負載測試中的尾端斜線導致404失敗。

* 此 `Runmode` 檢查對非資料夾節點產生誤判。