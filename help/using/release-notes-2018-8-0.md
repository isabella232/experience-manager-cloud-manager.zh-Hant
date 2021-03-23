---
title: 2018.8.0 版發行說明
seo-title: Cloud Manager AEM 2018.8.0發行說明
description: 請依照本頁取得Cloud Manager 2018.8.0版的相關資訊。
seo-description: 請依照本頁取得AEMCloud Manager 2018.8.0版的資訊。
uuid: e8aaba32-89b4-4bc5-b295-09b753252612
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 9222ac3b-525e-47c1-b481-ac9d22e3d559
feature: 發行資訊
translation-type: tm+mt
source-git-commit: fb10d775c930b5bb475b497aac2fd59b053a9a00
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 4%

---


# 2018.8.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0版新增支援在Git提交時自動觸發CI/CD管道，以及新精靈，以Project Archetype為基礎，在Git中建立應用程式專AEM案。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.8.0版的發行日期為2018年10月04日。

## 新功能 {#what-s-new}

* **程式設定** -使用「項目原型」在Git中建立應用程式項目的新AEM嚮導

* **CI/CD管線** - CI/CD管線中添加了以下更改。請參閱[配置CI/CD Pipeline](configuring-pipeline.md)以瞭解更多資訊。

   * On Git Changes trigger, this trigger when when the commits added to the configured git branch.
   * 首頁畫面上的卡片現在深入連結至管道執行頁面的特定區段。
   * 「活動」頁面現在會列出用於每個執行的特定分支。
   * 「活動」頁面現在會以小時和分鐘來指出持續時間。
   * 管線執行頁面現在會顯示為執行所建立的版本／標籤名稱。
   * Apache Maven版本已更新至3.5.3。

* **導覽** -下列變更會新增至 [!UICONTROL Cloud Manager]。

   * 全域導覽中的資源連結將導覽至Sharepoint中的「操作手冊」。
   * 說明功能表已重新整理，以包含更多[!UICONTROL Cloud Manager]特定內容。

## 錯誤修正 {#bug-fixes}

* 在Firefox中看不到「效能測試」對話方塊中的某些詳細資訊。
* 內部系統之間的逾時偶爾會報告部署失敗。
* 對於某些成功的管線執行，「活動」(Activity)頁面上的表徵圖顏色不正確。
* 在某些情況下，「效能測試」對話方塊會多次列出相同的度量。
* 如果在CI/CD管道啟動後新增了新實例，則不會在新建立的實例上執行部署。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含虛線。
* [!UICONTROL Experience Cloud]通知邊欄可能無法一致地載入通知。 但是，通知會顯示在[!UICONTROL Experience Cloud]中，若已設定，仍會透過電子郵件傳送。

