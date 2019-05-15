---
title: 2018.9.0版發行說明
seo-title: 2018.9.0的AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2018.9.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2018.9.0的資訊。
uuid: af5808f-828f-4846-bee4-1e62194 b48 ad
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 版本注意事項
discoiquuid: 85a1dcf-3ef-4ba8-b4 d1-09e4 a88 c7 bd0
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.9.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本新增支援以Adobe I/為基礎的API，包括Events，以便將 [!UICONTROL Cloud Manager]的CI/CD管線與其他系統整合。它也會開始在回應中重新編寫UI圖層。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.9.0版的發行日期為2018年11月01日。

## 新功能 {#whats-new}

* **CI/CD管道** -新API和事件系統，用於將 [!UICONTROL Cloud Manager]CI/CD管線與其他系統整合。請參閱 [!UICONTROL Cloud Manager] API文件(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)，以瞭解更多資訊。

* **UI** -推出更具互動性和協調性的全新UI圖層。

## 錯誤修正 {#bug-fixes}

* 在 [!UICONTROL Cloud Manager] 2018.8.0中，活動頁面期間在幾分鐘和數小時內列出，但該資訊未反映在表格標題中。
* 客戶偶爾無法啓動新的應用程式專案精靈。
* 新應用程式專案精靈對話方塊中的按鈕標籤產生誤導。
* 在某些情況下，按一下「活動」頁面中的「詳細資料」按鈕會重新導向至「概述」頁面。
* 某些罕見而意外的狀況造成「概述」頁面上遺失資訊卡。
* 「資產」圖示會顯示在所有客戶的「方案清單」頁面上。
* 當後端失敗時，有時候管線執行會出現在 *「驗證* 步驟」中。
* 在某些情況下，程式描述的長度計算錯誤。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含虛線。
* Adobe [!UICONTROL Experience Cloud] 通知資訊看板無法一致地載入通知。但是，通知會出現在Adobe [!UICONTROL Experience Cloud] ，如果設定，仍會透過電子郵件傳送。

