---
title: 2018.9.0 版發行說明
seo-title: AEM Cloud Manager 2018.9.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2018.9.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2018.9.0版的資訊。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: 發行資訊
exl-id: bf611743-ded2-4503-97c8-12b12454c7b7
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '277'
ht-degree: 9%

---

# 2018.9.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版新增了對Adobe I/O型API（包括Events）的支援，以整合[!UICONTROL Cloud Manager]的CI/CD管道與其他系統。 同時也開始在 React 中重寫 UI 層。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.9.0版的發行日期為2018年11月1日。

## 新功能 {#whats-new}

* **CI/CD管道**  — 整合CI/CD管道與其 [!UICONTROL Cloud Manager]他系統的全新API和事件系統。如需詳細資訊，請參閱[!UICONTROL Cloud Manager] API檔案(https://www.adobe.io/apis/experiencecloud/cloud-manager/docs.html)。

* **UI**  — 導入回應更快的新UI層。

## 錯誤修正 {#bug-fixes}

* 在[!UICONTROL Cloud Manager] 2018.8.0中，活動頁面持續時間以分鐘和小時為單位列出，但表格標題中未反映該資訊。
* 在少數情況下，客戶無法啟動新的應用程式項目嚮導。
* 「新建應用程式項目嚮導」對話框中的按鈕標籤具有誤導性。
* 在某些情況下，按一下「活動」頁面中的「詳細資料」按鈕會重新導向至「概觀」頁面。
* 某些罕見且非預期的情況會導致「概述」頁面上遺失資訊卡。
* 「資產」圖示會顯示在「方案清單」頁面上，供所有客戶使用。
* 當有後端失敗時，有時管道執行會顯示保留在&#x200B;*驗證*&#x200B;步驟中。
* 在某些情況下，錯誤計算了程式描述的長度。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含破折號。
* Adobe[!UICONTROL Experience Cloud]通知側欄可能無法一致地載入通知。 不過，Adobe[!UICONTROL Experience Cloud]中會顯示通知，如果已設定，仍會透過電子郵件傳送。
