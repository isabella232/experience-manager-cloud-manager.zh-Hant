---
title: Journey用戶
description: 此文檔列出了不同的登陸方案，並說明了您使用Cloud Manager的入門過程。
exl-id: deb3429c-dfcf-4e52-9aba-d9368aa240e6
source-git-commit: b0dbb602253939464ff034941ffbad84b7df77df
workflow-type: tm+mt
source-wordcount: '504'
ht-degree: 0%

---


# Journey用戶 {#user-journey}

作為Adobe Experience Manager用戶，您可以：

* 新來AEM。
* 當前使AEM用6.x。
* 需要升級到AEM6.5版才能使用 [!UICONTROL Cloud Manager]。

本文檔列出了這些方案，並說明了您的入門過程 [!UICONTROL Cloud Manager]。

>[!NOTE]
>
>[!UICONTROL Cloud Manager] 僅對使用6.4或更高版本的Adobe Managed Services(AMS)AEM客戶可用。

## 入門 {#onboarding}

登機過程因您是AMS的新客戶或現有AMS客戶而異。

### Adobe托管服務的新增功能 {#new-to-ams}

作為新客戶，您將 [!UICONTROL Cloud Manager] 作為Adobe Managed Services登錄過程的一部分。

作為登機過程的一部分，您將收到一封歡迎電子郵件，其中包括：

* 要訪問的URL [!UICONTROL Cloud Manager]
* 登錄說明 [!UICONTROL Experience Cloud]
* 使用Admin Console管理用戶及其相應權限以便他們可以訪問的說明 [!UICONTROL Cloud Manager] 的子菜單。

### 現有Adobe托管服務客戶 {#existing-customer}

作為現有AMS客戶，您首先需要將現有的生產和非生產環境升級AEM到6.4或更高版本。

執行升級時，您將被連接到Cloud Manager，並提供訪問該URL [!UICONTROL Cloud Manager]。 此外，對於需要訪問 [!UICONTROL Cloud Manager]，您需要開始使用Admin Console管理它們和它們各自的權限。

您的現AEM有項目還需要遵循建議的最佳實踐，因為您將開始使用 [!UICONTROL Cloud Manager] 將新代碼更改部署到您的AEM環境。

要獲取有關升級到6.5的益處AEM的更多資訊，請參閱文檔 [升級到AEM6.5。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/upgrading/upgrade.html)

## 訪問 [!UICONTROL Cloud Manager] {#accessing-cloud-manager}

您將可以訪問 [!UICONTROL Cloud Manager] 和您的AEM環境，只需登錄 [!UICONTROL Experience Cloud] 使用您的AdobeIdentity Management憑據並從解決方AEM案切換器介面中進行選擇。

登錄後 [!UICONTROL Cloud Manager] 您將首次能夠直接從AEMWindows [!UICONTROL Cloud Manager] UI。 此時，您已準備好探索 [!UICONTROL Cloud Manager] 並準備將您的第一個代碼分支部署到您的階段和生產環境中。

開始 [!UICONTROL Cloud Manager]，請參閱文檔 [首次登錄](/help/getting-started/first-time-login.md)。

有關的其他信AEM息，請參閱文檔 [部署和維護。](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html)

## 入門 [!UICONTROL Cloud Manager] {#getting-started-with-cloud-manager}

登錄後 [!UICONTROL Cloud Manager] 您可以通過以下方式開始AEM項目：

1. 設定代碼儲存庫環境。
1. 設定您的團隊和角色。
   * 通過將用戶添加到 [!UICONTROL Cloud Manager] 使用Admin Console配置檔案。
1. 在Git儲存庫中設定原始碼分支。
1. 根據負載和效能KPI定義目標。
1. 定義test方案，以便在所有質量檢查成功通過後將代碼成功部署到您的階段和生產環境。

## 端到端旅程 {#end-to-end-journey}

此圖說明了使用 [!UICONTROL Cloud Manager] CI/CD管道，用於將代碼更改部署到過渡和生產環境。

![端到端行程](/help/assets/screen_shot_2018-05-15at124004pm.png)
