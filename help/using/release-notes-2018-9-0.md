---
title: 2018.9.0 版發行說明
seo-title: Cloud Manager AEM 2018.9.0發行說明
description: 請依照本頁取得Cloud Manager 2018.9.0版的相關資訊。
seo-description: 請依照本頁取得AEMCloud Manager 2018.9.0版的資訊。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: 發行資訊
translation-type: tm+mt
source-git-commit: c5d32d49782c899d013fcc60b9c4d2b67e9350ae
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 9%

---


# 2018.9.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版新增了對Adobe I/O型API（包括事件）的支援，以整合[!UICONTROL Cloud Manager]的CI/CD管道與其他系統。 同時也開始在 React 中重寫 UI 層。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.9.0版的發行日期為2018年11月1日。

## 新功能 {#whats-new}

* **CI/CD管道** -用於將CI/CD管道與其他系統 [!UICONTROL Cloud Manager]整合的新API和事件系統。如需詳細資訊，請參閱[!UICONTROL Cloud Manager] API檔案(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)。

* **UI**  —— 新UI層的簡介，回應速度更快。

## 錯誤修正 {#bug-fixes}

* 在[!UICONTROL Cloud Manager] 2018.8.0中，「活動」頁面持續時間以分鐘和小時為單位列出，但該資訊並未反映在表格標題中。
* 在少數情況下，客戶無法啟動新的應用程式專案精靈。
* 「新建應用程式項目嚮導」對話框中的按鈕標籤具有誤導性。
* 在某些情況下，按一下「活動」頁面的「詳細資料」按鈕會重新導向至「概述」頁面。
* 某些罕見且意外的情況導致「概述」頁面上遺失資訊卡。
* 「資產」圖示會顯示在所有客戶的「方案清單」頁面上。
* 當出現後端故障時，有時管線執行仍會顯示在&#x200B;*Validate*&#x200B;步驟中。
* 在某些情況下，程式說明的長度計算錯誤。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含虛線。
* Adobe[!UICONTROL Experience Cloud]通知邊欄可能無法一致地載入通知。 不過，通知會顯示在Adobe[!UICONTROL Experience Cloud]中，如果已設定，仍會透過電子郵件傳送。

