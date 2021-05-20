---
title: 2019.1.0 版發行說明
seo-title: AEM Cloud Manager 2019.1.0版發行說明
description: 請詳閱本頁以取得Cloud Manager 2019.1.0版的資訊。
seo-description: 請詳閱本頁，以取得AEM Cloud Manager 2019.1.0版的資訊。
uuid: 3af5808f-828f-4846-bee4-1e62194b48ad
contentOwner: jsyal
products: SG_EXPERIENCEMANAGER/CLOUDMANAGER
topic-tags: release-notes
discoiquuid: 85a1dcf3-2eef-4ba8-b4d1-09e4a88c7bd0
feature: 發行資訊
exl-id: 383ca5a0-4b0b-48e9-aa48-1d1388875329
source-git-commit: 43bb3c477ef9c1ce178509b8180479d7616edc66
workflow-type: tm+mt
source-wordcount: '337'
ht-degree: 4%

---

# 2019.1.0 版發行說明 {#release-notes-for}

[!UICONTROL Cloud Manager] 2018.9.0版新增了對AEM Assets程式的支援測試，以及執行組建和程式碼品質步驟的其他管道類型，可選擇部署至非生產環境。

## 發行日期 {#release-date}

[!UICONTROL Cloud Manager] 2019.1.0版的發行日期為2019年1月17日。

## 新功能 {#whats-new}

* 新增對AEM Assets效能測試的支援。 如需詳細資訊，請參閱設定[CI/CD管道](configuring-pipeline.md) 。
* 新增對僅執行組建和程式碼品質步驟的管道以及部署至非生產環境的管道的支援。 如需詳細資訊，請參閱[設定CI/CD管道](configuring-pipeline.md)中的&#x200B;**僅限非生產與程式碼品質管道**&#x200B;區段。
* 新增對建置環境中自訂環境變數的支援。
* 若為具有多階段或生產環境的客戶，可在[設定CI/CD管道](configuring-pipeline.md)頁面中選取要部署為生產管道一部分的環境。
* 已將httxt2dbm新增至建置容器。
* 所有幫助菜單項都開啟一個新頁簽。

## 錯誤修正 {#bug-fixes}

* 編輯程式時，可以取消選取所有頁面集。
* 核准步驟的標題不正確。
* 在某些情況下，計畫徽標的匹配不正確。
* 如果僅建置Dispatcher設定套件，部署步驟將會失敗。
* 未正確處理包含冷備用實例的環境。
* 節目切換器上出現了一些終止的節目。
* 如果在編輯管道時將新分支新增至Git存放庫，可能尚未立即選取。
* 在某些畫面上，「說明」功能表中的「Developer Connection」圖示未顯示。
* 在Dispatcher排清設定對話方塊中，未正確處理索引標籤金鑰。

## 已知問題 {#known-issues}

* 開啟具有Sites但未設定Assets、KPI的程式時，所有使用者都會看到帶有&#x200B;**設定程式**&#x200B;按鈕的動作卡呼叫。 但是，只有業務所有者角色中的用戶才能實際按一下&#x200B;**設定程式**&#x200B;按鈕。
