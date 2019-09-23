---
title: 2018.9.0發行說明
seo-title: AEM Cloud manager 2018.9.0版本注意事項
description: 請依照本頁取得Cloud Manager 2018.9.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2018.9.0版的相關資訊。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: 發行說明
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: 949d3cf0239a02875ba4ad1888e081f104dec2e2

---


# 2018.9.0發行說明 {#release-notes-for}

2018.9.0 [!UICONTROL Cloud Manager] 版本新增了對Adobe I/O型API（包括Events）的支援，以整合其 [!UICONTROL Cloud Manager]他系統的CI/CD管道。 它也會開始在React中重寫UI層。

## 發行日期 {#release-date}

2018.9.0版 [!UICONTROL Cloud Manager] 的發行日期為2018年11月1日。

## 新功能 {#whats-new}

* **CI/CD管道** -用於將CI/CD管道與其他系統 [!UICONTROL Cloud Manager]整合的新API和事件系統。 如需詳細資 [!UICONTROL Cloud Manager] 訊，請參閱API檔案(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)。

* **UI** —— 新UI層的簡介，回應速度更快，效能更強。

## 錯誤修正 {#bug-fixes}

* 在 [!UICONTROL Cloud Manager] 2018.8.0中，「活動」頁面的持續時間以分鐘和小時為單位列出，但該資訊並未反映在表格標題中。
* 在少數情況下，客戶無法啟動新的應用程式專案精靈。
* 「新建應用程式項目嚮導」對話框中的按鈕標籤具有誤導性。
* 在某些情況下，按一下「活動」頁面的「詳細資料」按鈕會重新導向至「概述」頁面。
* 某些罕見且意外的情況導致「概述」頁面上遺失資訊卡。
* 「資產」圖示會顯示在所有客戶的「方案清單」頁面上。
* 當出現後端故障時，有時管線執行會顯示在「驗證」( *Validate* )步驟中。
* 在某些情況下，程式說明的長度計算錯誤。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含虛線。
* Adobe通知 [!UICONTROL Experience Cloud] 側欄可能無法一致地載入通知。 不過，通知會顯示在Adobe中， [!UICONTROL Experience Cloud] 若已設定，仍會透過電子郵件傳送。

