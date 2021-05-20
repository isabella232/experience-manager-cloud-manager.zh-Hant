---
title: 2020.4.0 版發行說明
seo-title: AEM Cloud Manager 2020.4.0版發行說明
description: 請詳閱本頁，了解Cloud Manager 2020.4.0版的相關資訊
seo-description: 請詳閱本頁以取得AEM Cloud Manager 2020.4.0版的相關資訊
feature: 發行資訊
exl-id: bb21b7ea-6bae-4755-becb-37cef0d49412
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '241'
ht-degree: 38%

---

# 2020.4.0 版發行說明 {#release-notes-for}

以下章節概述[!UICONTROL Cloud Manager] 2020.4.0版的一般發行說明。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2020.4.0版的發行日期為2020年4月9日。

## 新功能 {#whats-new}

* 導覽Cloud Manager概述頁面的變更，可讓使用者編輯或切換程式。
* 變更項目可讓使用者在 Cloud Manager 登陸頁面上的程式資訊卡編輯程式。
* 新管道狀態&#x200B;**管道正在執行**&#x200B;會針對關聯環境而顯示。
* 改良管道執行頁面的可理解性。這包括管道名稱（僅限非生產管道）和類型的顯示，以及指出管道狀態為「進行中/已取消/失敗」的徽章。
* 用於產生 git 密碼的程式對於基礎服務層的問題更具彈性。

## 錯誤修正 {#bug-fixes}

* 監控資料有時可能會因技術值的微小差異而以不正確的方式顯示，或完全不顯示。
* 已建置容器中使用的 Maven 設定經過更新，可避免在下載成品中繼資料時發生鎖死。
* AEM效能測試程式偶爾無法解密密碼，導致測試失敗。
* 具有備用實例的某些拓撲在安全測試中可能具有偽負值。
* 如果預備環境包含已停止的例項，則安全性測試步驟有時會失敗。
* 無法一致地收到 Experience Cloud 通知。
