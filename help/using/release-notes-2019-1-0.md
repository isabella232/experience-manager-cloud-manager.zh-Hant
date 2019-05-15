---
title: 2019.1.0版發行說明
seo-title: 2019.1.0AEM Cloud Manager發行說明
description: 請依照此頁面取得Cloud Manager發行2019.1.0的資訊。
seo-description: 請依照此頁面取得AEM Cloud Manager發行2019.1.0的資訊。
uuid: af5808f-828f-4846-bee4-1e62194 b48 ad
contentOwner: jsyal
products: SG_ PERIENCENCENAGER/CLUDManager
topic-tags: 版本注意事項
discoiquuid: 85a1dcf-3ef-4ba8-b4 d1-09e4 a88 c7 bd0
translation-type: tm+mt
source-git-commit: 1dfb065c09569f811e5a006d3d74825d3bd7cc8d

---


# 2019.1.0版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本新增支援AEM Assets程式以及其他執行建置和程式碼品質步驟的管道類型，可選擇部署至非生產環境。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.1.0版的發行日期是2019年月17日。

## 新功能 {#whats-new}

* 新增AEM Assets效能測試的支援。如需詳細資訊，請參閱設定您 [的CI/CD Pipelinea](configuring-pipeline.md)。
* 新增支援僅執行建置和編碼品質步驟和管線至非生產環境的管線。如需詳細資訊，請參閱設定您的CI/CD管道中的 **「非生產與程式碼品質僅限管線**[](configuring-pipeline.md) 」區段。
* 新增建置環境中自訂環境變數的支援。如需詳細資訊，請參閱 [建立AEM應用程式專案](create-an-application-project.md) 。
* 對於具有多重舞台或生產環境的客戶，請在 [「設定CI/CD管線」](configuring-pipeline.md) 頁面中選擇要部署為生產管道一部分的環境。
* 已新增httxt2dfm來建立容器。
* 所有說明功能表項目都會開啓新標籤。

## 錯誤修正 {#bug-fixes}

* 編輯程式時，可以取消選取所有頁面集。
* 核准步驟的標題不正確。
* 在某些情況下，程式標誌不正確。
* 如果只建立了發送器組態套件，部署步驟將會失敗。
* 包含冷備例項的環境無法正確處理。
* 程式切換程式會顯示某些已終止的程式。
* 如果在編輯管線時新增分支至Git存放庫，可能無法立即選取。
* 在某些螢幕上，「說明」功能表中的「Developer Connection」(開發人員連線)圖示不會顯示。
* 在dispatcher快顯組態對話方塊中，無法正確處理標籤索引鍵。

## 已知問題 {#known-issues}

* 開啓具有「網站」而非「資產」、「KPI」的程式時，所有使用者都會看到使用 **「設定程式** 」按鈕對動作卡進行的呼叫。不過，只有「商務擁有者」角色中的使用者可以按一下 **「設定程式** 」按鈕。