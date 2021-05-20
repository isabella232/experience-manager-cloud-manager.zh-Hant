---
title: 2018.8.0 版發行說明
seo-title: AEM Cloud Manager 2018.8.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2018.8.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2018.8.0版的資訊。
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
feature: 發行資訊
exl-id: 20f87048-30f7-4869-aad0-13ca383a404b
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 4%

---

# 2018.8.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0版新增了在Git提交項目時自動觸發CI/CD管道的支援，以及根據AEM專案原型在Git中建立應用程式專案的新精靈。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.8.0版的發行日期為2018年10月4日。

## 新功能 {#what-s-new}

* **方案設定**  — 使用AEM專案原型在Git中建立應用程式專案的新精靈

* **CI/CD管道**  - CI/CD管道新增下列變更。請參閱[設定CI/CD管道](configuring-pipeline.md)以深入了解。

   * On Git Changes（Git變更）觸發器，每當有提交項新增至設定的Git分支時，就會啟動CI/CD管道。
   * 主畫面上的卡片現在可深入連結至管道執行頁面的特定區段。
   * 活動頁面現在會列出用於每次執行的特定分支。
   * 活動頁面現在會指出持續時間（以小時和分鐘為單位）。
   * 管道執行頁面現在會顯示為執行建立的版本/標籤名稱。
   * Apache Maven版本已更新至3.5.3。

* **導覽**  — 會將下列變更新增至 [!UICONTROL Cloud Manager]。

   * 全局導航中的資源連結將導航到Sharepoint中的Runbook。
   * 已重新整理說明功能表，加入更多[!UICONTROL Cloud Manager]專屬內容。

## 錯誤修正 {#bug-fixes}

* Firefox中未顯示「效能測試」對話方塊中的某些詳細資訊。
* 內部系統之間的逾時偶爾會導致報告部署失敗。
* 對於某些成功的管道執行，「活動」頁面上的圖示顏色不正確。
* 在某些情況下，效能測試對話方塊會多次列出相同的量度。
* 如果在CI/CD管道啟動後新增了新執行個體，則不會在新建立的執行個體上執行部署。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含破折號。
* [!UICONTROL Experience Cloud]通知側欄可能無法一致地載入通知。 不過，通知會顯示在[!UICONTROL Experience Cloud]中，如果已設定，仍會透過電子郵件傳送。
