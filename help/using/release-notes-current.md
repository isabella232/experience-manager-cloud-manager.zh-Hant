---
title: 2020.4.0 版發行說明
seo-title: AEM Cloud Manager 2020.4.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.4.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.4.0版的相關資訊
translation-type: tm+mt
source-git-commit: e7da473a22bec1d3d9b3d39bf654af0c596fe86d

---

# 2020.4.0 版發行說明 {#release-notes-for}

下節概述2020.4.0版的一 [!UICONTROL Cloud Manager] 般發行說明。

## Release Date {#release-date}

2020.4.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年4月09日。

## 新功能 {#whats-new}

* 對導航CM概述頁面的更改，允許用戶從CM概述頁面編輯或切換程式。
* 允許用戶從CM登錄頁上的程式卡編輯程式的更改。
* 新管線狀態「管線運行」(Pipeline Running)對其關聯的環境顯示。
* 管道執行頁面的增強功能。 這包括「管線名稱」（僅限非生產管線）和「類型」(Type)的顯示，以及指示管線狀態為「正在進行／已取消／失敗」的標章。
* 用來產生Git密碼的程式對底層服務層中的問題具有更強的適應能力。

## 錯誤修正 {#bug-fixes}

* 監控資料有時可能會以不正確的方式顯示，或根據技術值的微小差異完全無法顯示。
* 已更新建置容器中使用的Maven組態，以避免在下載對象中繼資料時造成死鎖。
* Assets效能測試程式偶爾無法解密AEM密碼，導致測試失敗。
* 某些具有備用實例的拓撲在安全性測試中可能具有假負值。
* 如果舞台環境包含已停止的實例，則安全性測試步驟有時會失敗。
* 未一致收到Experience Cloud通知。

