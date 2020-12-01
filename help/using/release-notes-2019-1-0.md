---
title: 2019.1.0 版發行說明
seo-title: AEM Cloud Manager 2019.1.0版本注意事項
description: 請依照本頁取得Cloud Manager 2019.1.0版的相關資訊。
seo-description: 請依照本頁取得AEM Cloud Manager 2019.1.0版的相關資訊。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
translation-type: tm+mt
source-git-commit: c35398110e9d8311bf58f217efdd082cf0cfd90a
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 4%

---


# 2019.1.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版本新增支援測試AEM Assets程式，以及執行建立和程式碼品質步驟的其他管道類型，可選擇部署至非生產環境。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.1.0版的發行日期為2019年1月17日。

## 新功能 {#whats-new}

* 新增對AEM Assets效能測試的支援。 有關詳細資訊，請參閱配置[CI/CD Pipeline](configuring-pipeline.md)。
* 新增支援僅執行建置和程式碼品質步驟的管道，以及部署至非生產環境的管道。 如需詳細資訊，請參閱[設定您的CI/CD管道](configuring-pipeline.md)中的&#x200B;**非生產與程式碼品質專用管道**&#x200B;一節。
* 新增對建置環境中自訂環境變數的支援。
* 對於具有多階段或生產環境的客戶，在[配置CI/CD Pipeline](configuring-pipeline.md)頁面中可選擇將部署到哪個環境作為生產管線的一部分。
* httpxt2dbm已新增至建立容器。
* 所有幫助菜單項都會開啟一個新頁籤。

## 錯誤修正 {#bug-fixes}

* 編輯程式時，可以取消選擇所有頁面集。
* 核准步驟的標題不正確。
* 在某些情況下，程式標誌不正確匹配。
* 如果只生成了調度程式配置包，則部署步驟將失敗。
* 包含冷備用實例的環境無法正確處理。
* 節目切換器上出現了一些終止的節目。
* 如果在編輯管線時新增分支至git儲存庫，則可能無法立即選取。
* 在某些畫面上，「說明」選單中的「Developer Connection」圖示不會顯示。
* Tab鍵未在調度程式刷新配置對話框中正確處理。

## 已知問題 {#known-issues}

* 當開啟已設定「網站」但未設定「資產」、「KPI」的程式時，所有使用者都會看到使用&#x200B;**設定程式**&#x200B;按鈕的動作卡。 但是，只有「業務所有者」角色的用戶可以實際按一下&#x200B;**設定程式**&#x200B;按鈕。