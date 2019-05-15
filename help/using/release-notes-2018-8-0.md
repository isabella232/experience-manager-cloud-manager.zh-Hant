---
title: 2018.8.0版發行說明
seo-title: 2018.8.0AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2018.8.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager版本2018.8.0的資訊。
uuid: e8aa32-89b4-4bc5-b295-09b755252612
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 版本注意事項
discoiquuid: 9222ac3b-525e-47c1-b481-ac9 d22 e3 d559
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2018.8.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.8.0版本新增了對觸發CI/CD管線的支援，可在Git標記時自動觸發，以及新的精靈以根據AEM專案類型建立應用程式專案。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2018.8.0版的發行日期為2018年10月04日。

## 新功能 {#what-s-new}

* **方案設定** -新精靈可使用AEM專案類別類型建立應用程式專案，請參閱 [建立AEM應用程式專案](create-an-application-project.md) 以瞭解詳細資訊。

* **CI/CD管道** -已將下列變更新增至CI/CD管線。請參閱 [設定您的CI/CD管線](configuring-pipeline.md) 以瞭解更多資訊。

   * 在Git變更觸發器中，每當有逗號新增至配置的git分支時，就會啓動CI/CD管線。
   * 首頁畫面上的資訊卡現在會連結至管道執行頁面的特定區段。
   * 「活動」頁面現在會列出每個執行所使用的特定分支。
   * 活動頁面現在會在小時和分鐘內指出時段。
   * 管道執行頁面現在會顯示為執行建立的版本/標記名稱。
   * Apache Maven版本更新為3.5.3。

* **導覽** -將會新增下列變更至 [!UICONTROL Cloud Manager]。

   * 全域導覽中的資源連結將導覽至SharePoint中的「Runbook」。
   * 「說明」功能表已重新整理，包含更多 [!UICONTROL Cloud Manager]特定內容。

## 錯誤修正 {#bug-fixes}

* Firefox中無法顯示效能測試對話方塊中的某些詳細資料。
* 內部系統之間的逾時偶爾會造成部署失敗。
* 部分成功的管道執行中，「活動」頁面上的圖示顏色不正確。
* 在某些情況下，「效能測試」對話方塊會多次列出相同的量度。
* 如果在CI/CD管線啓動後新增新執行個體，則不會在新建立的例項上執行部署。

## 已知問題 {#known-issues}

* 使用「應用程式專案精靈」建立的分支不能包含虛線。
* [!UICONTROL Experience Cloud] 通知資訊看板無法一致地載入通知。但是，通知會顯示在其中， [!UICONTROL Experience Cloud] 如果設定，仍會透過電子郵件傳送。

