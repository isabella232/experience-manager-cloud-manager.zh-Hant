---
title: 使用者旅程圖
description: 本文件會展示不同的上線案例，並說明您的 Cloud Manager 快速入門旅程。
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '546'
ht-degree: 100%

---


# 使用者旅程圖 {#user-journey}

身為 Adobe Experience Manager 使用者，您可能：

* 是 AEM 的新手。
* 目前正在用 AEM 6.x。
* 為了使用[!UICONTROL Cloud Manager]，需要升級到 AEM 6.5 版。

本文件會展示上述案例，並說明您的 [!UICONTROL Cloud Manager] 使用者入門旅程。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 僅供使用 AEM 6.4 或以上版本的 Adobe Managed Services (AMS) 客戶使用。

## 上線 {#onboarding}

此上線流程會依據您是 AMS 新手或是現有的 AMS 客戶而不同。

### Adobe Managed Services 的新手 {#new-to-ams}

如果您是新客戶，您將加入 [!UICONTROL Cloud Manager]，這屬於 Adobe Managed Services 上線流程的一部分。

在上線流程中，您將收到一封歡迎電子郵件，內容包括：

* 存取 [!UICONTROL  的 URLCloud Manager]
* 登入至 [!UICONTROL Experience Cloud] 的說明
* 使用 Admin Console 來管理您的使用者和他們個別權限的說明，讓他們在需要時能夠存取 [!UICONTROL Cloud Manager]。

### 現有的 Adobe Managed Services 客戶 {#existing-customer}

由於您是現有的 AMS 客戶，您首先需要將現有的生產和非生產環境升級到 AEM 6.4 或更高版本。

完成升級後，系統會將您加入 Cloud Manager 並提供您存取 [!UICONTROL Cloud Manager] 的 URL。此外，若使用者需要存取 [!UICONTROL Cloud Manager]，您將需要開始使用 Admin Console 來管理他們以及他們的個別權限。

您現有的 AEM 專案也將必須符合建議的最佳做法，因為您將開始使用 [!UICONTROL Cloud Manager] 對 AEM 環境部署新程式碼變更。

若要取得更多有關升級至 AEM 6.5 的優勢的資訊，請參閱文件：[升級至 AEM 6.5。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html)

## 存取 [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

您將能存取 [!UICONTROL Cloud Manager] 以及您的 AEM 環境，僅需使用您的 Adobe Identity Management 憑證登入至 [!UICONTROL Experience Cloud] 登陸頁面，並從解決方案切換器介面選取 AEM 即可。

第一次登入 [!UICONTROL Cloud Manager] 後，您將可直接從 [!UICONTROL Cloud Manager] UI 存取您的 AEM 環境。 此時，您已準備就緒，可探索 [!UICONTROL Cloud Manager] 的所有可能性，並為您將部署至中繼和生產環境的第一個程式碼預做準備。

若要開始使用 [!UICONTROL Cloud Manager]，請參閱文件：[第一次登入](/help/getting-started/first-time-login.md)。

如需更多有關 AEM 的資訊，請參閱文件：[部署和維護。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)

## [!UICONTROL  快速入門Cloud Manager] {#getting-started-with-cloud-manager}

登入至 [!UICONTROL Cloud Manager] 後，您就可以透過以下步驟開始使用 AEM 專案：

1. 設定您的程式碼存放庫環境。
1. 設定您的團隊和角色。
   * 透過使用 Admin Console 將使用者新增到 [!UICONTROL Cloud Manager] 設定檔來指派角色會籍。
1. 在 Git 存放庫中設定您的原始程式碼分支。
1. 根據載入和效能 KPI 定義您的目標。
1. 一旦所有的品質檢查都成功通過後，定義測試情境以將程式碼成功部署到中繼和生產環境。

## 端對端旅程圖 {#end-to-end-journey}

此圖表會說明使用用於將程式碼變更部署到中繼和生產環境的 [!UICONTROL Cloud Manager] CI/CD 管道時高層級的客戶歷程。

![端對端旅程圖](/help/assets/screen_shot_2018-05-15at124004pm.png)
