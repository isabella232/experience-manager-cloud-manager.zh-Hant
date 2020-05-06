---
title: 2020.4.0 版發行說明
seo-title: AEM Cloud Manager 2020.4.0版本注意事項
description: 請依照本頁取得Cloud Manager 2020.4.0版的相關資訊
seo-description: 請依照本頁取得AEM Cloud Manager 2020.4.0版的相關資訊
translation-type: tm+mt
source-git-commit: 278858465592482449080fedc3c0165805db223d
workflow-type: tm+mt
source-wordcount: '239'
ht-degree: 37%

---

# 2020.4.0 版發行說明 {#release-notes-for}

下節概述2020.4.0版的一 [!UICONTROL Cloud Manager] 般發行說明。

## 發行日期 {#release-date}

2020.4.0版 [!UICONTROL Cloud Manager] 的發行日期為2020年4月09日。

## 新功能 {#whats-new}

* 對導覽Cloud Manager概述頁面所做的變更，可讓使用者編輯或切換程式。
* 變更項目可讓使用者在 Cloud Manager 登陸頁面上的程式資訊卡編輯程式。
* 新管道狀態&#x200B;**管道正在執行**&#x200B;會針對關聯環境而顯示。
* 改良管道執行頁面的可理解性。這包括「管線名稱」（僅限非生產管線）和「類型」(Type)的顯示，以及指示管線狀態為「正在進行／已取消／失敗」的標章。
* 用於產生 git 密碼的程式對於基礎服務層的問題更具彈性。

## 錯誤修正 {#bug-fixes}

* 監控資料有時可能會以不正確的方式顯示，或根據技術值的微小差異完全無法顯示。
* 已建置容器中使用的 Maven 設定經過更新，可避免在下載成品中繼資料時發生鎖死。
* Assets效能測試程式偶爾無法解密AEM密碼，導致測試失敗。
* 某些具有備用實例的拓撲在安全性測試中可能具有假負值。
* 如果舞台環境包含已停止的實例，則安全性測試步驟有時會失敗。
* 無法一致地收到 Experience Cloud 通知。

